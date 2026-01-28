# Code Quality Standards

## Metadata

- **Versão:** 1.0.0
- **Status:** Template (Path-targeted)
- **Última atualização:** Template
- **Responsável:** {{RESPONSIBLE_NAME}}
- **Paths:** src/**/*, *.py

---

## Quando Aplicar Esta Regra

**SEMPRE** - Esta regra deve ser aplicada em:
- Todo novo código escrito
- Code reviews
- Refatorações
- Correções de bugs
- Antes de commits (via pre-commit hooks)

---

## Referências

- [Projeto.md](../../documents/core/Projeto.md) - Contexto e arquitetura
- [testing-requirements.md](testing-requirements.md) - Requisitos de testes
- [security-best-practices.md](security-best-practices.md) - Segurança
- [.claude/CLAUDE.md](../CLAUDE.md) - Regras gerais do projeto

---

## Padrões Obrigatórios

### 1. PEP 8 Compliance

**Regra de Ouro:** Todo código Python deve seguir PEP 8.

**Ferramentas Obrigatórias:**
```bash
# Formatação automática
black src/ tests/

# Organização de imports
isort src/ tests/

# Linting
pylint src/
```

**Configuração (pyproject.toml):**
```toml
[tool.black]
line-length = 100
target-version = ['py311']

[tool.isort]
profile = "black"
line_length = 100

[tool.pylint.messages_control]
max-line-length = 100
```

**Linha máxima:** 100 caracteres (balanceio entre legibilidade e uso de tela)

---

### 2. Type Hints Obrigatórios

**Regra de Ouro:** Toda função pública deve ter type hints.

#### Correto

```python
from typing import Optional

def calcular_metrica(
    valor_base: float,
    fator: float
) -> float:
    """
    Calcula métrica aplicando fator.

    Args:
        valor_base: Valor inicial
        fator: Fator multiplicador

    Returns:
        Resultado do cálculo

    Raises:
        ValueError: Se valor_base <= 0
    """
    if valor_base <= 0:
        raise ValueError("valor_base deve ser positivo")
    return valor_base * fator


def processar_dados(
    dados: dict,
    filtro: Optional[str] = None
) -> Optional[dict]:
    """
    Processa dados com filtro opcional.

    Args:
        dados: Dados de entrada
        filtro: Filtro opcional (None se não aplicável)

    Returns:
        Dados processados ou None se falhar
    """
    if filtro is None:
        return dados
    return {k: v for k, v in dados.items() if filtro in k}
```

#### Incorreto

```python
def calcular_metrica(valor_base, fator):
    # Sem type hints
    return valor_base * fator
```

**Validação:**
```bash
mypy src/
```

---

### 3. Docstrings Google Style

**Regra de Ouro:** Toda função, classe e módulo público deve ter docstring.

#### Estrutura Padrão

```python
def funcao_exemplo(
    param1: int,
    param2: str,
    param3: Optional[float] = None
) -> bool:
    """
    [Linha resumo de uma sentença terminada em ponto.]

    [Parágrafo de descrição detalhada opcional, explicando o "porquê"
    e contexto de negócio se relevante.]

    Args:
        param1: Descrição clara do parâmetro
        param2: Descrição com exemplo se útil (ex: "formato: 'YYYY-MM-DD'")
        param3: Opcional - Descrição incluindo default se relevante

    Returns:
        Descrição do valor de retorno e possíveis casos especiais

    Raises:
        ValueError: Quando e por que esta exceção é levantada
        TypeError: Quando e por que esta exceção é levantada

    Example:
        >>> funcao_exemplo(42, "teste", 3.14)
        True

    Note:
        Informação adicional importante, como:
        - Performance considerations
        - Side effects
        - Thread safety
    """
    # Implementação
    pass
```

---

### 4. Constants Nomeadas (Sem Magic Numbers)

**Regra de Ouro:** Valores literais devem ser constants nomeadas.

#### Correto

```python
# constants.py
LIMITE_CRITICO = 70.0  # %
LIMITE_ATENCAO = 80.0  # %
TIMEOUT_SEGUNDOS = 30
MAX_RETRIES = 3

# uso
from constants import LIMITE_CRITICO

def detectar_alerta(percentual: float) -> str:
    """Detecta nível de alerta."""
    if percentual < LIMITE_CRITICO:
        return "CRÍTICO"
    elif percentual < LIMITE_ATENCAO:
        return "ATENÇÃO"
    else:
        return "OK"
```

#### Incorreto

```python
def detectar_alerta(percentual):
    if percentual < 70:  # Magic number - de onde veio 70?
        return "CRÍTICO"
    elif percentual < 80:  # Magic number
        return "ATENÇÃO"
    else:
        return "OK"
```

**Exceções Aceitáveis:**
- `0`, `1`, `-1` em contextos óbvios (índices, flags)
- `100` em conversões percentuais explícitas
- Valores em strings literais claras

---

### 5. Error Handling Padrão

**Regra de Ouro:** Sempre validar inputs e tratar erros esperados.

#### Correto

```python
from typing import Optional
import logging

logger = logging.getLogger(__name__)

def processar_item(
    item_id: str,
    data: date
) -> Optional[Dict[str, float]]:
    """
    Processa item para data específica.

    Args:
        item_id: ID do item (ex: "ITEM_001")
        data: Data do processamento

    Returns:
        Dict com resultados ou None se processamento falhar

    Raises:
        ValueError: Se item_id vazio ou data inválida
    """
    # Validação de inputs
    if not item_id or not item_id.strip():
        raise ValueError("item_id não pode ser vazio")

    if data > date.today():
        raise ValueError(f"Data {data} está no futuro")

    try:
        # Operação que pode falhar
        dados = buscar_dados(item_id, data)

        if not dados:
            logger.warning(
                f"Dados não disponíveis: item={item_id}, data={data}"
            )
            return None

        resultado = calcular(dados)
        return resultado

    except ConnectionError as e:
        logger.error(
            f"Erro de conexão ao processar item={item_id}: {e}",
            exc_info=True
        )
        return None

    except ValueError as e:
        logger.error(
            f"Dados inválidos para item={item_id}: {e}",
            exc_info=True
        )
        raise  # Re-raise se erro crítico
```

**Hierarquia de Exceptions:**
- Use exceptions específicas (`ValueError`, `TypeError`)
- Evite `except Exception` genérico (a menos que necessário)
- Sempre log antes de silenciar exceções

---

### 6. Logging Estruturado

**Regra de Ouro:** Use logging ao invés de print. Estruture logs para facilitar debugging.

#### Correto

```python
import logging
from typing import Dict, Any

logger = logging.getLogger(__name__)

def processar_lote(items: List[str]) -> None:
    """Processa lote de items."""
    logger.info(
        f"Iniciando processamento de {len(items)} items",
        extra={"item_count": len(items)}
    )

    for i, item_id in enumerate(items, 1):
        logger.info(f"Processando item {i}/{len(items)}: {item_id}")

        try:
            resultado = processar_item(item_id)
            logger.info(
                f"Item processado com sucesso: {item_id}",
                extra={"resultado": resultado}
            )
        except Exception as e:
            logger.error(
                f"Erro ao processar item {item_id}: {e}",
                exc_info=True,
                extra={"item_id": item_id}
            )
```

**Níveis de Log:**
- `DEBUG`: Informação detalhada para debugging
- `INFO`: Confirmações de fluxo normal
- `WARNING`: Algo inesperado mas não bloqueante
- `ERROR`: Erro que impede funcionalidade
- `CRITICAL`: Erro grave que pode parar o sistema

---

### 7. Secrets via pydantic-settings

**Regra de Ouro:** NUNCA hardcodear credentials. Use pydantic-settings + .env.

#### Correto

```python
# settings.py
from pydantic_settings import BaseSettings, SettingsConfigDict
from typing import Optional

class Settings(BaseSettings):
    """Configurações do sistema via environment variables."""

    # Credenciais (SENSÍVEL)
    API_USERNAME: str
    API_PASSWORD: str
    API_URL: str = "https://api.exemplo.com"
    API_TIMEOUT_SECONDS: int = 30

    # E-mail
    EMAIL_HOST: str
    EMAIL_PORT: int
    EMAIL_USER: str
    EMAIL_PASSWORD: str

    # Paths
    DATA_PATH: str = "./data"
    LOGS_PATH: str = "./logs"

    # Configurações
    DEBUG: bool = False
    MAX_RETRIES: int = 3

    model_config = SettingsConfigDict(
        env_file=".env",
        env_file_encoding="utf-8",
        case_sensitive=True
    )


# Instância global (singleton)
settings = Settings()
```

#### Incorreto

```python
# NUNCA FAZER ISSO
API_PASSWORD = "minha_senha_123"  # Hardcoded!
```

---

## Estrutura de Arquivos Padrão

```python
# Ordem de imports (isort)
# 1. Standard library
import os
import sys
from datetime import date, datetime
from typing import Dict, List, Optional

# 2. Third-party
import pandas as pd
from pydantic import BaseModel

# 3. Local
from src.services.api import APIClient
from src.processors.calculator import calcular
from src.storage.repository import salvar

# Constants
LIMITE_CRITICO = 70.0
LIMITE_ATENCAO = 80.0

# Classes
class Item(BaseModel):
    """Model de dados de um item."""
    id: str
    nome: str
    valor: float

# Functions
def processar_item(item: Item) -> Dict[str, float]:
    """Processa dados de um item."""
    pass

# Main
if __name__ == "__main__":
    # Entry point
    pass
```

---

## Naming Conventions

### Variáveis e Funções
- `snake_case`
- Nomes descritivos
- Evitar abreviações obscuras

```python
# Correto
percentual_resultado = 75.5
tempo_execucao_segundos = 6.2
def calcular_percentual(valor: float, total: float) -> float: pass

# Incorreto
pr = 75.5  # O que é "pr"?
te = 6.2
def calc_perc(v, t): pass  # Abreviações obscuras
```

### Classes
- `PascalCase`
- Substantivos descritivos

```python
# Correto
class APIClient: pass
class ItemHistorico: pass
class EmailSender: pass

# Incorreto
class api_client: pass  # Não use snake_case
class Client: pass      # Muito genérico
```

### Constants
- `UPPER_SNAKE_CASE`

```python
# Correto
LIMITE_CRITICO = 70.0
MAX_RETRIES = 3
TIMEOUT_SECONDS = 30

# Incorreto
limite_critico = 70.0  # Não usar snake_case para constants
```

---

## Ferramentas de Qualidade

### Pre-commit Hooks (Recomendado)

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/psf/black
    rev: 23.3.0
    hooks:
      - id: black
        language_version: python3.11

  - repo: https://github.com/pycqa/isort
    rev: 5.12.0
    hooks:
      - id: isort

  - repo: https://github.com/pycqa/pylint
    rev: v3.0.0
    hooks:
      - id: pylint
        args: [--max-line-length=100]

  - repo: https://github.com/pre-commit/mirrors-mypy
    rev: v1.3.0
    hooks:
      - id: mypy
        additional_dependencies: [types-all]
```

**Instalação:**
```bash
pip install pre-commit
pre-commit install
```

---

## Checklist de Code Review

Antes de aprovar um PR, verificar:

- [ ] PEP 8 compliance (black + isort executados)
- [ ] Type hints em todas as funções públicas
- [ ] Docstrings Google style em funções públicas
- [ ] Constants nomeadas (sem magic numbers)
- [ ] Error handling adequado (validações + try/except)
- [ ] Logging ao invés de print
- [ ] Nenhum secret hardcoded
- [ ] Testes unitários com >80% coverage
- [ ] Nomes descritivos (variáveis, funções, classes)
- [ ] Imports organizados (isort)
- [ ] Sem código comentado ou debug prints
- [ ] Documentação inline onde necessário

---

## Quando Atualizar Esta Regra

Atualize esta regra quando:

- Novas ferramentas de qualidade são adotadas (ex: ruff, bandit)
- Padrões do projeto evoluem (ex: nova convenção de naming)
- Python é atualizado (ex: 3.11 → 3.12+)
- Feedback de code reviews identifica gap

---

**Última atualização:** Template
**Versão:** 1.0.0
