# Roadmap - {{PROJECT_NAME}}

## Metadata

- **Versão:** 1.0.0
- **Status:** Em Planejamento
- **Última atualização:** {{DATE}}
- **Responsável:** {{RESPONSIBLE_NAME}}

---

## Referências Principais

- [Projeto.md](Projeto.md) - Fonte de verdade, regras de negócio, arquitetura
- [TODO.md](TODO.md) - Tarefas granulares e progresso diário
- [.claude/CLAUDE.md](../../.claude/CLAUDE.md) - Regras de desenvolvimento

## Links Relacionados

### Milestones

- [Fresh Context](../../.planning/context/README.md) - Handoff por milestone (gerado via `fresh-context`)
- [Template CONTEXT](../../.planning/context/template-CONTEXT.md) - Modelo para contexto de handoff

---

## Visão Geral do Roadmap

### Timeline Geral

```
┌─────────────┬────────────┬───────────┬───────────┬─────────────┐
│   Fase 0    │  Fase 1    │  Fase 2   │  Fase 3   │   Fase 4    │
│Planejamento │    PoV     │    MVP    │ Hardening │  Expansões  │
│   1 sem     │   3 sem    │  4 sem    │   3 sem   │ Incremental │
└─────────────┴────────────┴───────────┴───────────┴─────────────┘
     📝           🔬          🚀           🔒           ✨
   Decisões    Validação   Produção     Robusto      Valor++
```

### Fases

| Fase | Nome | Duração | Status | Objetivo |
|------|------|---------|--------|----------|
| **0** | Planejamento | 1 sem | ⏳ Aguardando | Decisões técnicas específicas |
| **1** | PoV | 3 sem | ⏳ Aguardando | Validação técnica |
| **2** | MVP | 4 sem | ⏳ Aguardando | Sistema completo |
| **3** | Hardening | 3 sem | ⏳ Aguardando | Confiabilidade e robustez |
| **4** | Expansões | Incremental | ⏳ Aguardando | Valor incremental |

---

## Fase 0: Planejamento

### Objetivo

Planejamento específico do projeto: decisões técnicas, setup de ambiente, validação de credenciais.

### Timeline

- **Início Previsto:** {{START_DATE}}
- **Conclusão Prevista:** {{END_DATE}}
- **Duração:** 1 semana
- **Status:** ⏳ Aguardando início

### Decisões Críticas

#### 1. {{DECISION_1_NAME}}

**Contexto:**
- {{CONTEXT}}

**Análise Necessária:**
- {{ANALYSIS_ITEM_1}}
- {{ANALYSIS_ITEM_2}}

**Impacta:** {{IMPACT}}
**Prazo:** Antes de iniciar {{MILESTONE}}

#### 2. {{DECISION_2_NAME}}

**Contexto:**
- {{CONTEXT}}

**Impacta:** {{IMPACT}}

### DoR (Definition of Ready)

**Pré-requisitos:**

- [ ] Acesso a sistemas externos disponível
- [ ] Credenciais validadas
- [ ] Ambiente de desenvolvimento disponível
- [ ] Requisitos documentados

### DoD (Definition of Done)

**Decisões Técnicas:**

- [ ] Stack tecnológico definido
- [ ] Decisões documentadas no Projeto.md
- [ ] Ambiente configurado

**Documentação:**

- [ ] Projeto.md atualizado com decisões
- [ ] Roadmap.md atualizado se timeline mudou
- [ ] TODO.md atualizado com tarefas da Fase 1

### Skills Aplicáveis

- **Antes:** `validate-dor Fase0`
- **Durante:** `pre-commit-check`, `update-docs system`
- **Após:** `validate-dod Fase0`, `update-docs task Fase0`

---

## Fase 1: PoV - Prova de Valor

### Objetivo

Validar viabilidade técnica com escopo reduzido, implementando fluxo end-to-end simplificado.

### Timeline

- **Início Previsto:** {{START_DATE}}
- **Conclusão Prevista:** {{END_DATE}}
- **Duração:** 3 semanas
- **Status:** ⏳ Aguardando Fase 0

### Milestones

#### M1.1: Setup de Ambiente

**Timeline:** Dias 1-2

**Objetivo:** Preparar ambiente de desenvolvimento local

**Entregas:**
- `requirements.txt` com dependências iniciais
- `.venv/` configurado
- `.env` com secrets (não comitar!)
- Testes de conectividade

**DoR:**
- [ ] Fase 0 completa (DoD 100%)
- [ ] Credenciais validadas

**DoD:**
- [ ] Ambiente virtual Python criado e ativado
- [ ] Dependências instaladas
- [ ] .env configurado
- [ ] Testes manuais bem-sucedidos
- [ ] README.md atualizado com instruções de setup

#### M1.2: {{MILESTONE_1_2_NAME}}

**Timeline:** Dias 3-7

**Objetivo:** {{OBJECTIVE}}

**Entregas:**
- {{DELIVERABLE_1}}
- {{DELIVERABLE_2}}

**DoR:**
- [ ] M1.1 completo (DoD 100%)
- [ ] {{PREREQUISITE}}

**DoD:**
- [ ] {{CRITERIA_1}}
- [ ] {{CRITERIA_2}}
- [ ] Testes unitários com >80% coverage
- [ ] Documentação inline completa
- [ ] Code review aprovado

**Skills Aplicáveis:**
- **Antes:** `validate-dor M1.2`
- **Durante:** `pre-commit-check`, `validate-testing`
- **Após:** `validate-dod M1.2`, `update-docs task M1.2`

#### M1.3: {{MILESTONE_1_3_NAME}}

**Timeline:** Dias 8-11

**Objetivo:** {{OBJECTIVE}}

**DoR:**
- [ ] M1.2 completo (DoD 100%)

**DoD:**
- [ ] {{CRITERIA_1}}
- [ ] Testes unitários com >80% coverage
- [ ] Documentação inline completa

#### M1.4: {{MILESTONE_1_4_NAME}}

**Timeline:** Dias 12-14

**Objetivo:** {{OBJECTIVE}}

**DoR:**
- [ ] M1.3 completo (DoD 100%)

**DoD:**
- [ ] {{CRITERIA_1}}
- [ ] Testes unitários com >90% coverage (core business logic)
- [ ] Testes de integração

### DoD Fase 1 (Consolidado)

**Funcional:**
- [ ] Fluxo end-to-end funciona
- [ ] Validado com dados reais

**Qualidade:**
- [ ] Cobertura de testes >80% overall, >90% em business logic
- [ ] Todos os testes passando (pytest)
- [ ] Code quality OK (black, isort, pylint)

**Documentação:**
- [ ] README.md atualizado
- [ ] Projeto.md atualizado se arquitetura mudou
- [ ] Todos os módulos com docstrings

**Segurança:**
- [ ] Nenhum secret hardcoded
- [ ] Secrets via pydantic-settings + .env

---

## Fase 2: MVP - Sistema Completo

### Objetivo

Sistema completo com todas as funcionalidades principais.

### Timeline

- **Início Previsto:** {{START_DATE}}
- **Conclusão Prevista:** {{END_DATE}}
- **Duração:** 4 semanas
- **Status:** ⏳ Aguardando Fase 1

### Milestones

#### M2.1: {{MILESTONE_NAME}}

**DoR:**
- [ ] Fase 1 completa (DoD 100%)

**DoD:**
- [ ] {{CRITERIA}}

#### M2.2: {{MILESTONE_NAME}}

**DoD:**
- [ ] {{CRITERIA}}

#### M2.3: {{MILESTONE_NAME}}

**DoD:**
- [ ] {{CRITERIA}}

### DoD Fase 2 (Consolidado)

**Funcional:**
- [ ] Sistema completo funcionando
- [ ] Todas funcionalidades principais implementadas

**Qualidade:**
- [ ] Cobertura de testes >80% overall
- [ ] Performance aceitável

**Operacional:**
- [ ] Deployment configurado
- [ ] Monitoramento básico implementado

---

## Fase 3: Hardening - Confiabilidade

### Objetivo

Tornar o sistema robusto, confiável e resiliente a falhas.

### Timeline

- **Início Previsto:** {{START_DATE}}
- **Conclusão Prevista:** {{END_DATE}}
- **Duração:** 3 semanas
- **Status:** ⏳ Aguardando Fase 2

### Milestones

#### M3.1: {{MILESTONE_NAME}}

**Objetivo:** {{OBJECTIVE}}

**DoD:**
- [ ] {{CRITERIA}}

#### M3.2: {{MILESTONE_NAME}}

**DoD:**
- [ ] {{CRITERIA}}

### DoD Fase 3 (Consolidado)

**Confiabilidade:**
- [ ] Taxa de sucesso >95%
- [ ] Falhas tratadas gracefully

**Manutenibilidade:**
- [ ] Documentação de troubleshooting criada
- [ ] Logs facilitam diagnóstico

---

## Fase 4: Expansões - Valor Incremental

### Objetivo

Funcionalidades adicionais de alto valor agregado.

### Timeline

- **Início Previsto:** Pós-Hardening
- **Duração:** Incremental (sob demanda)
- **Status:** ⏳ Aguardando Fase 3

### Milestones

#### M4.1: {{EXPANSION_NAME}}

**Objetivo:** {{OBJECTIVE}}

**Valor:** {{VALUE}}

#### M4.2: {{EXPANSION_NAME}}

**Objetivo:** {{OBJECTIVE}}

---

## Quando Atualizar Este Documento

Atualize este documento quando:

- **Milestones são completados** (atualizar status)
- **Timeline muda** (atrasos, aceleração)
- **DoR/DoD são ajustados** (novos critérios identificados)
- **Novos milestones são adicionados**
- **Dependências mudam** (bloqueios, desbloqueios)

**Processo:**

1. Atualizar seção relevante
2. Incrementar versão (semver)
3. Adicionar entrada no Changelog
4. Commitar com mensagem descritiva

---

## Changelog

### v1.0.0 ({{DATE}})

**Criação Inicial:**
- Estrutura completa com 4 fases de desenvolvimento
- DoR/DoD templates para cada milestone
- Timeline detalhada
- Skills aplicáveis por milestone

**Autor:** {{AUTHOR_NAME}}
**Contexto:** Kick-off do projeto

---

## Skills Aplicáveis

**Por Milestone:**
- `validate-dor [milestone-id]` - Validar DoR antes de iniciar
- `validate-dod [milestone-id]` - Validar DoD ao concluir

**Qualidade e Validação:**
- `pre-commit-check` - Checklist completo antes de commit
- `validate-testing` - Validar cobertura de testes

**Manutenção:**
- `update-docs system` - Atualizar docs técnicos após mudanças arquiteturais
- `update-docs task [milestone-id]` - Salvar implementation plan de milestone
- `audit-rules` - Auditar regras e documentação
- `validate-docs-links` - Validar links em documentação

---

**Última atualização:** {{DATE}}
**Versão:** 1.0.0
**Mantido por:** {{RESPONSIBLE_NAME}}
