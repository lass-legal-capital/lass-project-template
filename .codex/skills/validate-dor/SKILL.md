# Skill: validate-dor

Validar Definition of Ready de um milestone antes de iniciar trabalho.

---
name: validate-dor
description: Validar Definition of Ready de um milestone antes de iniciar trabalho. Use OBRIGATORIAMENTE antes de iniciar qualquer milestone, quando planejar trabalho, ou ao completar milestone anterior para validar próximo. Este é um gate bloqueador - nenhum trabalho deve começar sem DoR 100% completo.
---

## Quando Usar

- **OBRIGATORIAMENTE** antes de iniciar qualquer milestone
- Quando planejar trabalho para próxima sprint
- Ao completar milestone anterior (validar próximo)
- Quando houver dúvida se pré-requisitos estão atendidos

## Input Esperado

```
validate-dor [milestone-id]
```

Exemplos:
- `validate-dor M1.2`
- `validate-dor M2.1`
- `validate-dor` (auto-detecta próximo milestone do Roadmap.md)

## Workflow

### 1. Identificar Milestone

```
Se milestone-id não fornecido:
  → Ler Roadmap.md
  → Identificar último milestone completo
  → Selecionar próximo milestone sequencial
  → Confirmar com usuário se ambíguo
```

### 2. Extrair DoR do Roadmap

```
Ler Roadmap.md
Localizar seção do milestone
Extrair TODOS os critérios de DoR (checkbox items)
```

### 3. Validar Cada Critério

Para cada item do DoR:

```yaml
Critério: "[texto do critério]"
Status: COMPLETO | PENDENTE | BLOQUEADO
Evidência:
  - [link para código/doc/decisão]
  - [output de verificação se aplicável]
Ação: [se pendente, o que fazer]
```

### 4. Verificar Dependências

```
Para cada milestone que este depende:
  → Verificar se está marcado como COMPLETO
  → Verificar se DoD foi validado
  → Listar se há gaps
```

### 5. Gerar Readiness Report

```markdown
# Readiness Report: [MILESTONE-ID]

**Data:** [YYYY-MM-DD HH:MM]
**Status Geral:** ✅ READY | ⚠️ PARCIAL | ❌ NOT READY

## Sumário
- Total de Critérios: X
- Completos: Y (Z%)
- Pendentes: W
- Bloqueados: V

## Dependências

| Milestone | Status | DoD Validado |
|-----------|--------|--------------|
| M1.1 | ✅ Completo | ✅ Sim |
| M1.2 | ⏳ Em progresso | - |

## Critérios Detalhados

### ✅ Critério 1: [descrição]
- **Evidência:** [link/referência]

### ⏳ Critério 2: [descrição]
- **Gap:** [o que falta]
- **Ação necessária:** [próximo passo]
- **Responsável:** [quem deve resolver]

### 🚫 Critério 3: [descrição]
- **Bloqueador:** [descrição do bloqueio]
- **Dependência:** [de quem/o quê depende]

## Decisão

[ ] DoR 100% completo - Milestone pode ser INICIADO
[ ] DoR parcialmente completo - Ver pendências acima
[ ] DoR não completo - Milestone NÃO pode ser iniciado
```

## Critérios Comuns de DoR

### Requisitos
- [ ] Requisitos documentados e claros
- [ ] Critérios de aceite definidos
- [ ] Escopo delimitado (o que está IN e OUT)

### Dependências
- [ ] Milestones anteriores completos
- [ ] Dependências técnicas resolvidas
- [ ] Acessos necessários disponíveis

### Recursos
- [ ] Ambiente de desenvolvimento pronto
- [ ] Ferramentas necessárias instaladas
- [ ] Documentação de referência acessível

### Conhecimento
- [ ] Arquitetura compreendida
- [ ] Decisões técnicas tomadas
- [ ] Dúvidas esclarecidas

## Regras

1. **DoR é PRÉ-REQUISITO** - Não inicie sem 100% completo
2. **Pendências devem ser resolvidas PRIMEIRO** - Antes de começar código
3. **Bloqueios escalam imediatamente** - Não espere resolver sozinho
4. **Documente gaps** - Para tracking e follow-up

## Output

Gera relatório estruturado com:
- Status de cada critério
- Dependências verificadas
- Gaps identificados
- Ações necessárias
- Decisão final (READY/NOT READY)

## Integração com Outros Skills

| Skill | Quando Usar |
|-------|-------------|
| `validate-dod` | Ao completar milestone |
| `fresh-context` | Se contexto anterior perdido |
| `update-docs` | Após resolver pendências |

## Exemplo de Uso

```
User: validate-dor M1.3

Claude:
# Readiness Report: M1.3

**Data:** 2026-01-25 10:00
**Status Geral:** ⚠️ PARCIAL

## Sumário
- Total de Critérios: 4
- Completos: 3 (75%)
- Pendentes: 1
- Bloqueados: 0

## Dependências

| Milestone | Status | DoD Validado |
|-----------|--------|--------------|
| M1.1 | ✅ Completo | ✅ Sim |
| M1.2 | ✅ Completo | ✅ Sim |

## Critérios Detalhados

### ✅ Requisitos documentados
- **Evidência:** Projeto.md seção 4.2

### ✅ Ambiente preparado
- **Evidência:** venv criado, deps instaladas

### ✅ Decisões técnicas tomadas
- **Evidência:** ADR-002 aprovado

### ⏳ Dicionário de classificação definido
- **Gap:** Falta finalizar mapeamento de nomenclaturas
- **Ação necessária:** Completar data/dicionario.json
- **Responsável:** Equipe de negócio

## Decisão

[ ] DoR 100% completo - Milestone pode ser INICIADO
[x] DoR parcialmente completo - Ver pendências acima
[ ] DoR não completo - Milestone NÃO pode ser iniciado

**Recomendação:** Aguardar finalização do dicionário antes de iniciar M1.3.
Estimativa: 1-2 dias para completar.
```

---

**Versão:** 1.0.0
**Última atualização:** Template
