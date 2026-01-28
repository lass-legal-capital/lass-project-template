# Projeto: {{PROJECT_NAME}}

## Sobre Este Documento

Este é um **living document** - a fonte ATUAL de verdade do projeto {{PROJECT_NAME}}.

- **Atualizado conforme decisões evoluem** - Reflete descobertas técnicas e mudanças de planejamento
- **Documenta mudanças** - Changelog detalhado com justificativas
- **Fonte primária de consulta** - Use este documento para decisões atuais

**Última revisão:** {{DATE}} | **Versão:** 1.0.0

---

## Metadata

- **Versão:** 1.0.0
- **Status:** Em Planejamento
- **Última atualização:** {{DATE}}
- **Responsável:** {{RESPONSIBLE_NAME}}
- **Organização:** {{ORGANIZATION_NAME}}
- **Tipo:** {{PROJECT_TYPE}}

<!--
PROJECT_TYPE pode ser: Sistema de automação, API REST, Aplicação web, CLI tool, etc.
-->

---

## Referências Principais

- [Roadmap.md](Roadmap.md) - Fases, milestones e DoR/DoD (gestão)
- [TODO.md](TODO.md) - Tarefas granulares e progresso diário
- [.claude/CLAUDE.md](../../.claude/CLAUDE.md) - Regras de desenvolvimento sempre ativas

## Links Relacionados

### Documentação Técnica (Futuro)

- [Arquitetura](../technical/architecture.md) - Visão técnica completa
- [Integrações](../technical/integrations.md) - Detalhes de integrações externas

### Estratégia (Futuro)

- [Escolhas Tecnológicas](../strategy/technology-choices.md) - Decisões de stack e justificativas
- [Análise de Riscos](../strategy/risk-analysis.md) - Riscos e mitigações

---

## 1. Resumo Executivo

### Contexto

{{PROJECT_CONTEXT}}

<!--
Preencher com:
- Qual o contexto organizacional?
- Qual problema está sendo resolvido?
- Por que este projeto existe?
-->

### Problema

{{PROJECT_PROBLEM}}

<!--
Preencher com:
- Quais são as dores atuais?
- Por que a solução atual é insuficiente?
- Qual o impacto de não resolver?
-->

### Solução Proposta

{{PROJECT_SOLUTION}}

<!--
Preencher com:
- O que o sistema faz?
- Como resolve o problema?
- Quais são os principais componentes?
-->

### Valor Esperado

**Redução de Riscos:**

- {{RISK_REDUCTION_1}}
- {{RISK_REDUCTION_2}}

**Ganhos Operacionais:**

- {{OPERATIONAL_GAIN_1}}
- {{OPERATIONAL_GAIN_2}}

---

## 2. Objetivos e Escopo

### Objetivos do Projeto

#### Objetivo Principal

{{MAIN_OBJECTIVE}}

#### Objetivos Específicos

1. **{{SPECIFIC_OBJECTIVE_1}}**
   - {{DETAILS}}

2. **{{SPECIFIC_OBJECTIVE_2}}**
   - {{DETAILS}}

3. **{{SPECIFIC_OBJECTIVE_3}}**
   - {{DETAILS}}

### Escopo

#### Incluído (MVP)

**Funcional:**

- [ ] {{FUNCTIONAL_ITEM_1}}
- [ ] {{FUNCTIONAL_ITEM_2}}
- [ ] {{FUNCTIONAL_ITEM_3}}

#### Não Incluído (MVP)

**Fora de Escopo Inicial:**

- {{OUT_OF_SCOPE_1}}
- {{OUT_OF_SCOPE_2}}

**Expansões Futuras (Fase 4):**

- {{FUTURE_EXPANSION_1}}
- {{FUTURE_EXPANSION_2}}

---

## 3. Arquitetura do Sistema

### Visão Geral

```mermaid
graph TD
    A[{{COMPONENT_1}}] --> B[{{COMPONENT_2}}]
    B --> C[{{COMPONENT_3}}]
    C --> D[{{COMPONENT_4}}]
```

<!--
Substituir pelo diagrama real da arquitetura.
Use formato Mermaid para diagramas.
-->

### Componentes Principais

#### 1. **{{COMPONENT_NAME_1}}**

**Responsabilidade:** {{RESPONSIBILITY}}

**Componentes:**
- `{{file_name}}.py` - {{DESCRIPTION}}

#### 2. **{{COMPONENT_NAME_2}}**

**Responsabilidade:** {{RESPONSIBILITY}}

### Stack Tecnológico

**Linguagem:** {{LANGUAGE}}

**Bibliotecas Principais:**
- **{{LIB_CATEGORY_1}}:** {{LIB_NAME}}
- **{{LIB_CATEGORY_2}}:** {{LIB_NAME}}

**Infraestrutura (MVP):**
- {{INFRA_DESCRIPTION}}

---

## 4. Regras de Negócio Críticas

### 4.1. {{BUSINESS_RULE_1_NAME}}

**Objetivo:** {{OBJECTIVE}}

**Regras:**
- {{RULE_1}}
- {{RULE_2}}

**Fórmula (se aplicável):**
```python
# Exemplo
resultado = (valor_a / valor_b) * 100
```

### 4.2. {{BUSINESS_RULE_2_NAME}}

**Objetivo:** {{OBJECTIVE}}

**Regras:**
- {{RULE_1}}
- {{RULE_2}}

---

## 5. Fases do Projeto

### Visão Geral

| Fase | Nome | Duração | Status | Objetivo |
|------|------|---------|--------|----------|
| **0** | Planejamento | 1 sem | Aguardando | Decisões técnicas |
| **1** | PoV | 3 sem | Aguardando | Validação técnica |
| **2** | MVP | 4 sem | Aguardando | Sistema completo |
| **3** | Hardening | 3 sem | Aguardando | Confiabilidade |
| **4** | Expansões | Incremental | Aguardando | Valor incremental |

> **Detalhes completos:** Ver [Roadmap.md](Roadmap.md)

---

## 6. Métricas de Sucesso

### Métricas de Qualidade

**Cobertura de Testes:**
- Core business logic: >90%
- Integrações: >80%
- Overall: >80%

**Confiabilidade:**
- Taxa de sucesso de execução: >95%
- Tempo de detecção de falhas: <1h

### Métricas de Valor

- {{VALUE_METRIC_1}}
- {{VALUE_METRIC_2}}

---

## 7. Riscos e Dependências

### Riscos Técnicos

#### Alto Impacto

1. **{{RISK_NAME}}**
   - **Probabilidade:** {{PROBABILITY}}
   - **Impacto:** {{IMPACT}}
   - **Mitigação:** {{MITIGATION}}

### Dependências Externas

**Críticas:**
- {{CRITICAL_DEPENDENCY_1}}
- {{CRITICAL_DEPENDENCY_2}}

---

## 8. Glossário

**{{TERM_1}}:** {{DEFINITION}}

**{{TERM_2}}:** {{DEFINITION}}

---

## 9. FAQ

### Sobre o Projeto

**P: {{QUESTION}}?**
R: {{ANSWER}}

---

## 10. Quando Atualizar Este Documento

Este documento deve ser atualizado quando:

- **Decisões técnicas são tomadas** (ex: escolha de fonte de dados, stack)
- **Descobertas técnicas ocorrem**
- **Regras de negócio evoluem**
- **Arquitetura é modificada**
- **Milestones são completados** (atualizar status das fases)
- **Riscos se materializam ou novos são identificados**

**Processo de Atualização:**

1. Fazer mudança no documento (seção relevante)
2. Atualizar versão (semver: MAJOR.MINOR.PATCH)
3. Adicionar entrada no Changelog abaixo
4. Atualizar "Última revisão" no topo
5. Commitar com mensagem descritiva

---

## 11. Changelog

### v1.0.0 ({{DATE}})

**Criação Inicial:**
- Estrutura completa baseada no template Lass
- Seções: Resumo, Objetivos, Arquitetura, Regras de Negócio, Fases, Métricas, Riscos, Glossário, FAQ
- Living document configurado

**Autor:** {{AUTHOR_NAME}}
**Contexto:** Kick-off do projeto

---

## Skills Aplicáveis

**Antes de Iniciar Milestone:**
- `validate-dor [milestone-id]` - Validar Definition of Ready

**Durante Desenvolvimento:**
- `pre-commit-check` - Checklist completo antes de commit
- `validate-testing` - Validar cobertura de testes

**Após Completar Milestone:**
- `validate-dod [milestone-id]` - Validar Definition of Done
- `update-docs system` - Atualizar documentação técnica

---

**Última atualização:** {{DATE}}
**Versão:** 1.0.0
**Mantido por:** {{RESPONSIBLE_NAME}}
