# Skill: validate-dod

Validar Definition of Done de um milestone antes de marcá-lo como completo.

---
name: validate-dod
description: Validar Definition of Done de um milestone antes de marcá-lo como completo. Use OBRIGATORIAMENTE antes de marcar milestone como completo, durante desenvolvimento como checklist de progresso, ou antes de transição para próximo milestone. Este é um gate bloqueador - nenhum milestone pode ser marcado completo sem DoD 100% validado.
---

## Quando Usar

- **OBRIGATORIAMENTE** antes de marcar milestone como completo
- Durante desenvolvimento como checklist de progresso
- Antes de transição para próximo milestone
- Quando precisar evidências de conclusão

## Input Esperado

```
validate-dod [milestone-id]
```

Exemplos:
- `validate-dod M1.2`
- `validate-dod M2.1`
- `validate-dod` (auto-detecta milestone atual do TODO.md)

## Workflow

### 1. Identificar Milestone

```
Se milestone-id não fornecido:
  → Ler TODO.md
  → Identificar milestone ativo (seção "Em Progresso" ou último referenciado)
  → Confirmar com usuário se ambíguo
```

### 2. Extrair DoD do Roadmap

```
Ler Roadmap.md
Localizar seção do milestone
Extrair TODOS os critérios de DoD (checkbox items)
```

### 3. Validar Cada Critério

Para cada item do DoD:

```yaml
Critério: "[texto do critério]"
Status: PASS | FAIL | PARCIAL
Evidência:
  - [link para código/teste/doc]
  - [output de comando se aplicável]
Notas: [observações se necessário]
```

### 4. Executar Verify Steps (Se Aplicável)

Se TODO.md contém tarefas com formato `- verify: [comando]`:

```bash
# Executar cada verify step
pytest tests/unit/test_example.py  # exemplo
mypy src/                          # exemplo

# Registrar output
```

### 5. Gerar Verification Report

```markdown
# Verification Report: [MILESTONE-ID]

**Data:** [YYYY-MM-DD HH:MM]
**Status Geral:** ✅ APROVADO | ⚠️ PARCIAL | ❌ REPROVADO

## Sumário
- Total de Critérios: X
- Aprovados: Y (Z%)
- Reprovados: W

## Critérios Detalhados

### ✅ Critério 1: [descrição]
- **Evidência:** [link/output]

### ❌ Critério 2: [descrição]
- **Gap:** [o que falta]
- **Ação necessária:** [próximo passo]

## Verify Steps Executados

| Comando | Status | Output |
|---------|--------|--------|
| `pytest tests/` | ✅ PASS | 15 passed |
| `mypy src/` | ✅ PASS | Success |

## Decisão

[ ] DoD 100% atendido - Milestone pode ser marcado como COMPLETO
[ ] DoD parcialmente atendido - Ver gaps acima
[ ] DoD não atendido - Milestone NÃO pode ser marcado como completo
```

## Critérios Comuns de DoD

### Código
- [ ] Funcionalidade implementada conforme especificação
- [ ] Sem erros de lint (pylint/black/isort)
- [ ] Type hints em funções públicas
- [ ] Docstrings Google style

### Testes
- [ ] Testes unitários escritos
- [ ] Cobertura >80% (ou meta definida)
- [ ] Todos os testes passando
- [ ] Casos de borda testados

### Documentação
- [ ] Docstrings atualizadas
- [ ] README atualizado (se aplicável)
- [ ] Changelog atualizado

### Segurança
- [ ] Nenhum secret hardcoded
- [ ] Inputs validados
- [ ] Error handling adequado

### Integração
- [ ] Código revisado (se aplicável)
- [ ] Integrado com componentes existentes
- [ ] Sem regressões

## Regras

1. **DoD é OBRIGATÓRIO** - Não existe "quase done"
2. **Evidências são necessárias** - Não basta afirmar, precisa provar
3. **Verify steps devem passar** - Comandos programáticos validam critérios
4. **Parcial não é completo** - Se 1 critério falhar, milestone não está done

## Output

Gera relatório estruturado com:
- Status de cada critério
- Evidências coletadas
- Gaps identificados
- Decisão final (APROVADO/REPROVADO)

## Integração com Outros Skills

| Skill | Quando Usar |
|-------|-------------|
| `validate-dor` | Antes de iniciar milestone |
| `pre-commit-check` | Antes de commits |
| `validate-testing` | Para critérios de cobertura |
| `update-docs` | Após DoD aprovado |

## Exemplo de Uso

```
User: validate-dod M1.2

Claude:
# Verification Report: M1.2

**Data:** 2026-01-25 14:30
**Status Geral:** ✅ APROVADO

## Sumário
- Total de Critérios: 5
- Aprovados: 5 (100%)
- Reprovados: 0

## Critérios Detalhados

### ✅ Funcionalidade implementada
- **Evidência:** src/collectors/scraper.py:45-120

### ✅ Testes unitários (>80%)
- **Evidência:** `pytest --cov` → 85% coverage

### ✅ Documentação atualizada
- **Evidência:** docs/collectors.md atualizado

### ✅ Sem secrets hardcoded
- **Evidência:** `bandit -r src/` → No issues

### ✅ Code review aprovado
- **Evidência:** PR #12 merged

## Verify Steps Executados

| Comando | Status | Output |
|---------|--------|--------|
| `pytest tests/unit/` | ✅ PASS | 23 passed |
| `mypy src/` | ✅ PASS | Success |
| `bandit -r src/` | ✅ PASS | No issues |

## Decisão

[x] DoD 100% atendido - Milestone pode ser marcado como COMPLETO
```

---

**Versão:** 1.0.0
**Última atualização:** Template
