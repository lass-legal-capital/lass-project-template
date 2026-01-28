---
name: validate-testing
description: Validar cobertura de testes e estrutura de testes do projeto. Use após implementar feature, antes de commits, durante validação de DoD, ou após refactoring para garantir que os testes estão adequados e a cobertura atende aos padrões estabelecidos.
---

# Validate Testing

Valida cobertura de testes e estrutura de tests/ seguindo regras do projeto.

## Quando Usar

- Após implementar feature
- Antes de commit (parte do pre-commit)
- Durante DoD validation
- Após refactoring

## O Que Valida

### 1. Execução de Testes (pytest)
Executa todos os testes e verifica se passam.

```bash
pytest tests/ -v
```

**Meta:** 100% dos testes passando (zero failures)

### 2. Cobertura de Testes (coverage)
Valida cobertura de código por categoria.

```bash
pytest tests/ --cov=src/ --cov-report=html --cov-report=term
```

**Metas por Categoria:**

| Categoria | Meta | Justificativa |
|-----------|------|---------------|
| **Overall** | >80% | Cobertura geral adequada |
| **Business Logic** | >90% | Código crítico de negócio |
| **Integrações** | >80% | Pontos de integração |
| **Utils** | >70% | Utilitários (menos crítico) |

### 3. Estrutura de Testes
Verifica organização de tests/.

**Estrutura esperada:**
```
tests/
├── unit/              # Testes unitários
│   ├── test_*.py
├── integration/       # Testes de integração
│   ├── test_*.py
├── fixtures/          # Fixtures compartilhados
│   ├── conftest.py
│   ├── sample_data/
└── smoke/             # Smoke tests (se aplicável)
    └── test_basic_flow.py
```

### 4. Naming Convention
Valida nomenclatura dos testes.

**Padrão esperado:**
```python
def test_<function>_<scenario>_<expected>():
    """Test docstring."""
    pass
```

**Exemplos:**
- `test_login_valid_credentials_success()`
- `test_login_invalid_credentials_raises_error()`
- `test_parse_xml_malformed_returns_none()`

## Procedimento de Validação

```bash
1. Executar pytest com coverage:
   pytest tests/ --cov=src/ --cov-report=html --cov-report=term -v

2. Validar resultados de testes:
   a. Contar testes executados
   b. Verificar failures (meta: 0)
   c. Verificar skipped (investigar se necessário)

3. Validar cobertura mínima:
   a. Overall: >80%
   b. Business logic (src/processors/, src/collectors/): >90%
   c. Integrações (pontos de I/O): >80%
   d. Utils (src/utils/): >70%

4. Verificar estrutura tests/:
   a. unit/ existe e tem testes
   b. integration/ existe (se aplicável)
   c. fixtures/ existe com conftest.py

5. Validar naming convention:
   a. Todos arquivos começam com test_
   b. Todos testes começam com test_
   c. Formato: test_<function>_<scenario>_<expected>

6. Gerar relatório: ✅ PASS ou ❌ FAIL
```

## Exemplo de Output

```
✅ Testing Validation
=====================

## Execução de Testes

======================== test session starts =========================
collected 42 items

tests/unit/test_scraper.py ........... [ 26%]
tests/unit/test_parser.py ........... [ 50%]
tests/integration/test_pipeline.py ..... [ 61%]
tests/integration/test_end_to_end.py ........ [100%]

======================== 42 passed in 3.45s ==========================

✅ Todos os 42 testes passaram (0 failures)

---

## Cobertura de Testes

---------- coverage: platform darwin, python 3.11.5 -----------
Name                              Stmts   Miss  Cover
-----------------------------------------------------
src/collectors/scraper.py           120     18    85%
src/collectors/parser.py            95      8    92%
src/processors/normalizer.py       45      5    89%
src/processors/classifier.py       60      3    95%
src/utils/helpers.py               30      8    73%
-----------------------------------------------------
TOTAL                              350     42    88%

✅ Overall coverage: 88% (meta: >80%) ✅
✅ Business logic:
   - collectors/: 88% ✅
   - processors/: 92% ✅ (meta: >90%)
✅ Utils: 73% ✅ (meta: >70%)

Relatório HTML: htmlcov/index.html

---

## Estrutura de Testes

✅ tests/unit/ existe (20 arquivos)
✅ tests/integration/ existe (5 arquivos)
✅ tests/fixtures/ existe com conftest.py
✅ Estrutura OK

---

## Naming Convention

✅ 42/42 testes seguem padrão (100%)
   - test_<function>_<scenario>_<expected>

Exemplos:
✅ test_login_valid_credentials_success
✅ test_parse_xml_malformed_returns_none
✅ test_classify_asset_dc_returns_dc_category

---

## Resultado: ✅ PASS

Todos os critérios de testing atendidos!
```

## Metas de Cobertura Detalhadas

### Overall Coverage (>80%)

**Inclui:**
- Todo código em src/
- Média ponderada de todos componentes

**Cálculo:**
```
Overall = (Total Stmts - Total Miss) / Total Stmts
```

### Business Logic (>90%)

**Componentes:**
- `src/collectors/` - Coleta de dados (scraping, parsing)
- `src/processors/` - Processamento (normalização, classificação)
- `src/alerting/` - Motor de regras de alertas

**Justificativa:**
- Código crítico de negócio
- Erros aqui impactam diretamente o produto
- Requerem maior confiança

### Integrações (>80%)

**Componentes:**
- Pontos de I/O (API calls, file I/O, database)
- Scraping (Selenium, requests)
- Email sending

**Justificativa:**
- Pontos de integração são frágeis
- Requerem testes de integração adequados

### Utils (>70%)

**Componentes:**
- `src/utils/` - Utilitários, helpers

**Justificativa:**
- Código de suporte
- Menos crítico
- Meta mais relaxada

## Tipos de Testes

### 1. Unit Tests (tests/unit/)

**O que testar:**
- Funções isoladas
- Lógica de negócio
- Edge cases
- Error handling

**Exemplo:**
```python
def test_parse_xml_valid_returns_dict():
    """Parse de XML válido retorna dict correto."""
    xml_str = "<root><item>value</item></root>"
    result = parse_xml(xml_str)
    assert isinstance(result, dict)
    assert result["item"] == "value"

def test_parse_xml_malformed_raises_error():
    """Parse de XML malformado levanta XMLError."""
    xml_str = "<root><item>unclosed"
    with pytest.raises(XMLError):
        parse_xml(xml_str)
```

### 2. Integration Tests (tests/integration/)

**O que testar:**
- Fluxo completo (end-to-end)
- Integração entre componentes
- I/O real (arquivos, mock de APIs)

**Exemplo:**
```python
def test_collector_pipeline_full_flow():
    """Pipeline completo: login → download → parse."""
    scraper = Scraper()
    scraper.login()
    raw_data = scraper.download_data()
    parsed = Parser().parse(raw_data)

    assert parsed is not None
    assert "items" in parsed
    assert len(parsed["items"]) > 0
```

### 3. Fixtures (tests/fixtures/)

**conftest.py:**
```python
import pytest

@pytest.fixture
def sample_xml():
    """XML de exemplo para testes."""
    return """
    <data>
        <item>value</item>
        <count>1000000.00</count>
    </data>
    """

@pytest.fixture
def mock_scraper():
    """Mock do scraper para testes de integração."""
    class MockScraper:
        def login(self):
            return True
        def download_data(self):
            return "<mock>data</mock>"
    return MockScraper()
```

## Quando Bloquear Commit

**Bloqueadores (❌ FAIL):**
- Algum teste falhando
- Cobertura overall <80%
- Cobertura business logic <90%
- Estrutura tests/ incorreta

**Warnings (⚠️  Revisar):**
- Cobertura utils <70% (não-bloqueante, mas revisar)
- Testes skipped (investigar motivo)
- Naming convention não seguida (<90%)

## Relatório de Coverage HTML

```bash
# Gerar relatório HTML
pytest tests/ --cov=src/ --cov-report=html

# Abrir no navegador
open htmlcov/index.html
```

**Relatório mostra:**
- Cobertura por arquivo
- Linhas não cobertas (em vermelho)
- Branch coverage (if/else não testados)

## Parâmetros

### Caminho (opcional)

```bash
# Validar testes de src/ (padrão)
validate-testing

# Validar testes de módulo específico
validate-testing src/collectors/

# Validar arquivo específico
validate-testing src/collectors/scraper.py
```

## Integração com DoD

Este check é parte do DoD de features:

**DoD Checklist:**
- [ ] Funcionalidade implementada
- [ ] `validate-testing` → ✅ PASS ← Você está aqui
  - [ ] Cobertura >80% (overall)
  - [ ] Cobertura >90% (business logic)
- [ ] Code review aprovado

## Dependências

### Ferramentas necessárias:

```bash
# requirements-dev.txt
pytest==7.4.4
pytest-cov==4.1.0
pytest-mock==3.12.0  # Para mocking
```

### Instalação:

```bash
pip install -r requirements-dev.txt
```

## Referências

- `.claude/rules/testing-requirements.md` - Regra base
- pytest: https://docs.pytest.org/
- pytest-cov: https://pytest-cov.readthedocs.io/

## Skills Relacionadas

- `pre-commit-check` - Checklist completo (inclui testing)
- `validate-dod [milestone]` - Validar DoD (inclui testing)
- `rules/code-quality-standards.md` - Padrões de qualidade de código
