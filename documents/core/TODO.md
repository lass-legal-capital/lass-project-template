# TODO - {{PROJECT_NAME}}

## Metadata

- **Versão:** 1.0.0
- **Status:** Em Planejamento
- **Última atualização:** {{DATE}}
- **Responsável:** {{RESPONSIBLE_NAME}}

---

## Referências Principais

- [Roadmap.md](Roadmap.md) - Fases, milestones, DoR/DoD
- [Projeto.md](Projeto.md) - Fonte de verdade, regras de negócio
- [.claude/CLAUDE.md](../../.claude/CLAUDE.md) - Regras de desenvolvimento

---

## Progresso Geral

```
Fase 0:     ░░░░░░░░░░░░░  0.0% (0/X tarefas)    ⏳ Aguardando início
Fase 1:     ░░░░░░░░░░░░░  0.0% (0/4 milestones) ⏳ Aguardando Fase 0
Fase 2:     ░░░░░░░░░░░░░  0.0% (0/X milestones) ⏳ Aguardando Fase 1
Fase 3:     ░░░░░░░░░░░░░  0.0% (0/X milestones) ⏳ Aguardando Fase 2
Fase 4:     ░░░░░░░░░░░░░  0.0% (0/X expansões)  ⏳ Aguardando Fase 3
```

**Status Geral:** Em planejamento
**Próximo Milestone:** Iniciar Fase 0 (Planejamento)

---

## FASE 0: Planejamento

> **Pronto para iniciar quando:** Kick-off concluído

### Decisões Críticas Pendentes

#### [DECISÃO TÉCNICA #1] {{DECISION_NAME}}

**Status:** ⏳ Não iniciado

**Contexto:**
- {{CONTEXT}}

**Análise Necessária:**
- {{ANALYSIS_1}}
- {{ANALYSIS_2}}

**Impacta:**
- {{IMPACT}}

**Stakeholder:** {{STAKEHOLDER}}
**Prazo:** Durante Fase 0

---

### Tarefas da Fase 0

**Planejamento Técnico:**
- [ ] {{PLANNING_TASK_1}}
- [ ] {{PLANNING_TASK_2}}
- [ ] Atualizar Projeto.md com decisões tomadas

**Setup de Ambiente:**
- [ ] Configurar Python 3.11+ e venv
- [ ] Criar requirements.txt inicial
- [ ] Configurar .env.example com variáveis necessárias
- [ ] Testar acessos necessários

**Validação de Credenciais:**
- [ ] Validar credenciais de sistemas externos
- [ ] Validar configurações de e-mail/notificações

**Documentação:**
- [ ] Atualizar Roadmap.md com timeline ajustada (se necessário)
- [ ] Atualizar TODO.md com tarefas da Fase 1
- [ ] Validar DoD Fase 0 (via `validate-dod Fase0`)

---

## FASE 1: PoV - Prova de Valor

> **⏳ Aguardando:** Conclusão da Fase 0

### Milestones

- [ ] **M1.1:** Setup de Ambiente (Dias 1-2)
- [ ] **M1.2:** {{MILESTONE_NAME}} (Dias 3-7)
- [ ] **M1.3:** {{MILESTONE_NAME}} (Dias 8-11)
- [ ] **M1.4:** {{MILESTONE_NAME}} (Dias 12-14)

_Detalhamento será adicionado ao iniciar Fase 1._

---

## FASE 2: MVP - Sistema Completo

> **⏳ Aguardando:** Conclusão da Fase 1

### Milestones

- [ ] **M2.1:** {{MILESTONE_NAME}}
- [ ] **M2.2:** {{MILESTONE_NAME}}
- [ ] **M2.3:** {{MILESTONE_NAME}}

_Detalhamento será adicionado ao iniciar Fase 2._

---

## FASE 3: Hardening - Confiabilidade

> **⏳ Aguardando:** Conclusão da Fase 2

### Milestones

- [ ] **M3.1:** {{MILESTONE_NAME}}
- [ ] **M3.2:** {{MILESTONE_NAME}}

_Detalhamento será adicionado ao iniciar Fase 3._

---

## FASE 4: Expansões - Valor Incremental

> **⏳ Aguardando:** Conclusão da Fase 3

### Funcionalidades Planejadas

- [ ] **M4.1:** {{EXPANSION_NAME}}
- [ ] **M4.2:** {{EXPANSION_NAME}}

_Detalhamento será adicionado ao iniciar Fase 4._

---

## Skills Úteis

### Validação de Milestones
- `validate-dor [milestone-id]` - Validar Definition of Ready antes de iniciar
- `validate-dod [milestone-id]` - Validar Definition of Done ao concluir

### Qualidade de Código
- `pre-commit-check` - Checklist completo antes de commit
- `validate-testing` - Validar cobertura de testes

### Documentação
- `update-docs system` - Atualizar documentação técnica
- `update-docs task [milestone-id]` - Salvar implementation plan de milestone
- `validate-docs-links check` - Validar sistema de links

### Auditoria
- `audit-rules quick` - Auditar regras (quick check)
- `audit-rules full` - Auditar todas as regras (completo)
- `audit-architecture` - Auditar redundância em documentação

### Git
- `organize-commits` - Guiar organização de commits (atomic commits, máx 100 linhas)

### Context Management
- `fresh-context [milestone]` - Gerar CONTEXT.md para handoff (usar quando sessão >150k tokens)
- `generate-session-prompt` - Gerar prompt curto para retomada

---

## Progresso Semanal

### Semana 1 ({{WEEK_DATES}}) - Fase 0

**Meta:** Completar planejamento e decisões técnicas

**Progresso:**
- [ ] **Segunda:** {{TASK}}
- [ ] **Terça:** {{TASK}}
- [ ] **Quarta:** {{TASK}}
- [ ] **Quinta:** {{TASK}}
- [ ] **Sexta:** {{TASK}}

**Status:** ⏳ Aguardando início

---

## Bloqueios e Dependências

### Bloqueios Ativos

**Nenhum bloqueio ativo no momento.**

### Dependências

1. **Fase 0 → Fase 1:**
   - ⏳ Decisões técnicas pendentes
   - ⏳ Setup de ambiente

2. **Fase 1 → Fase 2:**
   - ⏳ Validação técnica
   - ⏳ Todos DoD de M1.1-M1.4 cumpridos

---

## Próximas Ações (Top 3)

1. **[AGORA]** {{ACTION_1}}
2. **[DEPOIS]** {{ACTION_2}}
3. **[EM SEGUIDA]** {{ACTION_3}}

---

## Formato de Tarefas com Verificação

Para tarefas que requerem validação programática, use o formato `verify:`:

```markdown
#### M1.X: Nome do Milestone

- [x] Nome da tarefa
  - files: src/path/to/file.py
  - verify: `pytest tests/unit/test_file.py -v`
  - verify: `python -c "from src.module import X; print('OK')"`
  - done: Descrição do critério de conclusão
```

**Regras:**
- `files:` - Arquivos criados/modificados pela tarefa
- `verify:` - Comandos executáveis para validação (exit code 0 = PASS)
- `done:` - Critério humano de conclusão
- O skill `validate-dod` executa automaticamente os `verify:` steps

---

## Template: Commits do Milestone

Após cada commit, rastrear hash na seção do milestone:

```markdown
### Commits do Milestone M1.X

| # | Task | Hash | Type | Linhas |
|---|------|------|------|--------|
| 1 | Task name | `abc123f` | feat | 85 |
| 2 | Task tests | `def456g` | test | 42 |

**Total:** N commits, M linhas
```

---

## Quando Atualizar Este Documento

Atualize este documento quando:

- **Tarefas são completadas** (mover para ✅ Completo)
- **Novas tarefas são identificadas** (adicionar em ⏳ Pendentes)
- **Bloqueios surgem ou são resolvidos** (atualizar seção de Bloqueios)
- **Progresso semanal avança** (atualizar checkboxes da semana)
- **Milestones são completados** (atualizar barras de progresso)
- **Decisões pendentes são resolvidas** (atualizar status de decisões)
- **Commits são feitos** (atualizar seção "Commits do Milestone")

**Processo:**
1. Atualizar seção relevante
2. Incrementar versão (semver) se mudança significativa
3. Commitar com mensagem descritiva

---

## Changelog

### v1.0.0 ({{DATE}})

**Criação Inicial:**
- Estrutura completa com tracking visual de todas as fases
- Seção de decisões técnicas pendentes
- Skills úteis por contexto
- Progresso semanal com timeline
- Bloqueios e dependências rastreados
- Próximas ações (Top 3)
- Formato de tarefas com verificação

**Autor:** {{AUTHOR_NAME}}
**Contexto:** Kick-off do projeto

---

**Última atualização:** {{DATE}}
**Versão:** 1.0.0
**Mantido por:** {{RESPONSIBLE_NAME}}
