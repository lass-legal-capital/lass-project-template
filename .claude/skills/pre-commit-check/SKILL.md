---
name: pre-commit-check
description: Checklist completo de qualidade e validações antes de git commit. Use SEMPRE antes de fazer commit, incluindo validações de code quality, testing, security, e git status. Este é um gate de qualidade obrigatório para garantir que apenas código bem estruturado e testado seja commitado.
---

# Pre-Commit Check

Checklist completo de qualidade antes de git commit.

## Quando Usar

- ✅ **SEMPRE** antes de git commit
- ✅ Automatizado via git hooks (futuro)

## O Que Valida

### 1. Code Quality

Validação completa de qualidade de código Python.

**Comandos:**

```bash
# Formatação (deve passar sem erros)
black --check src/ tests/

# Imports ordenados
isort --check src/ tests/

# Linting (meta: >8.0/10)
pylint src/

# Type checking (opcional, recomendado)
mypy src/
```

**Critérios de Aprovação:**

| Validação | Meta | Bloqueador |
|-----------|------|------------|
| black --check | 0 erros | ✅ Sim |
| isort --check | 0 erros | ✅ Sim |
| pylint | >8.0/10 | ✅ Sim |
| docstrings | 100% públicas | ⚠️ MVP: >80% |
| type hints | 100% públicas | ⚠️ MVP: >80% |
| secrets | 0 hardcoded | ✅ Sim (crítico) |

**Auto-fix disponível:**

```bash
black src/ tests/      # Formatar código
isort src/ tests/      # Ordenar imports
```

**Busca de secrets (CRÍTICO):**

```bash
# Patterns que NUNCA devem existir
grep -r "password\s*=\s*['\"]" src/
grep -r "api_key\s*=\s*['\"]" src/
grep -r "SECRET\s*=\s*['\"]" src/
```

### 2. Testing

Executa todos os testes e valida cobertura.

**Comandos:**

```bash
# Executar todos os testes
pytest

# Com cobertura
pytest --cov=src --cov-report=term-missing

# Verificar cobertura mínima
pytest --cov=src --cov-fail-under=80
```

**Critérios de Aprovação:**

| Validação | Meta | Bloqueador |
|-----------|------|------------|
| Testes passam | 100% | ✅ Sim |
| Coverage overall | >80% | ✅ Sim |
| Coverage business logic | >90% | ✅ Sim |

### 3. Security
Validações de segurança.

**Verifica:**
- .env não staged (git status)
- .env.example atualizado (se necessário)
- Nenhum credential em código (já validado em code-quality)
- requirements.txt atualizado

### 4. Git Status
Valida estado do repositório.

**Verifica:**
- Arquivos corretos staged
- Nenhum arquivo sensível staged (.env, credentials)
- Mensagem de commit planejada (conventional)

### 5. Opcional (Recomendado)
Validações adicionais conforme contexto.

**Se alterou regras:**
```bash
audit-rules quick
```

**Se alterou docs:**
```bash
validate-docs-links check
```

## Procedimento Completo

```bash
1. Validar Code Quality
   a. black --check src/ tests/
      - Se FAIL: black src/ tests/ (auto-fix)

   b. isort --check src/ tests/
      - Se FAIL: isort src/ tests/ (auto-fix)

   c. pylint src/
      - Se score <8.0: Corrigir issues críticos

   d. Buscar secrets hardcoded
      - Se encontrado: BLOQUEAR commit

2. Validar Testes
   a. pytest --cov=src --cov-fail-under=80
      - Se FAIL: Corrigir testes ou aumentar coverage

3. Validar segurança:
   a. git status | grep .env
      - Se .env staged: git reset .env

   b. Verificar .env.example atualizado
      - Se mudou variáveis: Atualizar .env.example

   c. Verificar requirements.txt
      - pip freeze > requirements.txt (se mudou deps)

4. Validar git status:
   a. git status
      - Revisar arquivos staged
      - Confirmar que são os corretos

   b. Planejar mensagem de commit
      - Formato: type(scope): subject
      - Referência: organize-commits

5. Validações opcionais:
   - Se alterou .claude/rules/: audit-rules quick
   - Se alterou documents/: validate-docs-links check

6. Gerar relatório final: ✅ READY ou ❌ NOT READY
```

## Exemplo de Output

```
✔️  Pre-Commit Checklist
========================

## 1. Code Quality ✅
✅ black: PASSED
✅ isort: PASSED
✅ pylint: 9.2/10 ✅
✅ docstrings: 95% cobertura
✅ secrets: Nenhum hardcoded

## 2. Testing ✅
✅ pytest: 42 testes PASSED
✅ coverage: 88% (meta: >80%) ✅

## 3. Security ✅
✅ .env não staged
✅ .env.example atualizado
✅ Nenhum credential hardcoded
✅ requirements.txt atualizado

## 4. Git Status ✅
📁 Arquivos staged (5):
   M  src/collectors/scraper.py
   M  src/collectors/parser.py
   A  tests/unit/test_scraper.py
   A  tests/unit/test_parser.py
   M  requirements.txt

⚠️  Arquivos não staged (1):
   M  documents/core/TODO.md

Ação recomendada: git add documents/core/TODO.md

## 5. Mensagem de Commit 💡
Use conventional commit:
   feat(collector): implementa scraper básico

---

✅ READY TO COMMIT

Próximo passo:
git commit -m "type(scope): subject"

Ou organize commits complexos:
organize-commits
```

## Checklist Completo

### Code Quality
- [ ] black --check (formatação)
- [ ] isort --check (imports)
- [ ] pylint >8.0/10 (linting)
- [ ] docstrings Google style
- [ ] type hints
- [ ] Nenhum secret hardcoded

### Testing
- [ ] pytest (todos passam)
- [ ] coverage >80% (overall)
- [ ] coverage >90% (business logic)

### Security
- [ ] .env não commitado
- [ ] .env.example atualizado
- [ ] Nenhum credential em código
- [ ] requirements.txt atualizado

### Git
- [ ] Arquivos corretos staged
- [ ] Nenhum arquivo sensível staged
- [ ] Mensagem planejada (conventional)

### Opcional
- [ ] audit-rules quick (se alterou regras)
- [ ] validate-docs-links check (se alterou docs)

## Quando Bloquear Commit

**Bloqueadores (❌ NOT READY):**
- Code quality FAIL
- Testing FAIL (testes falhando ou coverage baixa)
- .env staged
- Secrets hardcoded encontrados

**Warnings (⚠️  Revisar):**
- Arquivos não staged (revisar se devem ser incluídos)
- .env.example desatualizado
- requirements.txt desatualizado

## Auto-Fix Disponível

```bash
# Formatar código
black src/
isort src/

# Atualizar requirements
pip freeze > requirements.txt

# Unstage .env
git reset .env
```

## Integração com Organize Commits

Se múltiplas mudanças pendentes:

```bash
organize-commits  # Primeiro organize
pre-commit-check  # Depois valide cada commit
```

## Integração Futura (Git Hooks)

### .git/hooks/pre-commit

```bash
#!/bin/bash
# Execute pre-commit check
pre-commit-check || exit 1
```

Benefícios:
- Validação automática
- Previne commits problemáticos
- Reduz carga cognitiva

## Exemplo de Uso

### Caso 1: Tudo OK

```bash
$ pre-commit-check

✔️  Pre-Commit Checklist
========================
✅ Code Quality: PASS
✅ Testing: PASS
✅ Security: PASS
✅ Git Status: OK

✅ READY TO COMMIT

$ git commit -m "feat(collector): implementa scraper"
[main abc123] feat(collector): implementa scraper
 5 files changed, 450 insertions(+), 20 deletions(-)
```

### Caso 2: Issues Encontrados

```bash
$ pre-commit-check

✔️  Pre-Commit Checklist
========================
❌ Code Quality: FAIL
   - pylint: 7.5/10 (meta: >8.0)
   - 3 erros encontrados em scraper.py

✅ Testing: PASS
❌ Security: FAIL
   - .env está staged!

❌ NOT READY TO COMMIT

Ações necessárias:
1. Corrigir erros de pylint
2. Unstage .env: git reset .env
3. Re-executar: pre-commit-check

$ # Corrigir issues
$ git reset .env
$ # Fix code
$ pre-commit-check
✅ READY TO COMMIT
```

## Referências

- `@rules/code-quality-standards.md` - Detalhes de padrões Python
- `@rules/testing-requirements.md` - Requisitos de testes
- `@rules/security-best-practices.md` - Práticas de segurança

## Skills Relacionadas

**Antes de commit:**
- `organize-commits` - Se múltiplas mudanças
- `pre-commit-check` - Validar (você está aqui)

**Validação adicional:**
- `audit-rules` - Se alterou regras
- `validate-docs-links` - Se alterou docs
- `audit-architecture` - Se alterou documentação estrutural
