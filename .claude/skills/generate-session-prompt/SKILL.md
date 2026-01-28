---
name: generate-session-prompt
description: Gerar prompt otimizado para retomada de desenvolvimento em nova sessão. Use quando sessão atual >150k tokens, ao retomar trabalho após pausa, ao trocar de ferramenta, ou em mudança de contexto entre milestones para criar contexto limpo e eficiente.
---

# Generate Session Prompt

Gera prompt otimizado para retomada de desenvolvimento em nova sessão, minimizando uso de tokens.

## Quando Usar

- Sessão atual >150k tokens (performance degradada)
- Retomar trabalho após pausa (dias/semanas)
- Trocar de ferramenta (ex: Cursor → Claude Code)
- Mudança de contexto (ex: finalizou M1.2, vai iniciar M1.3)

## Princípios

1. **Concisão** - Máximo 250 tokens no prompt
2. **Contexto mínimo** - Apenas essencial para continuar
3. **Referências @** - Facilita navegação do Claude
4. **Skills** - Quando aplicável

## Objetivo do Prompt

Criar um prompt que:
1. Resume contexto atual concisamente
2. Estabelece objetivos claros
3. Lista próximas tarefas
4. Inclui referências aos arquivos principais
5. Segue princípios de eficiência de tokens

## Estrutura do Prompt

### Formato Obrigatório

```markdown
Vamos continuar o desenvolvimento do {{PROJECT_NAME}} no milestone [MILESTONE-ID] ([NOME]).

**Referências principais:**
- @[arquivo1] (contexto sobre X)
- @[arquivo2] (tarefas e checklist)
- @[arquivo3] (plano de implementação, se aplicável)

**Objetivo:** [Descrição concisa do objetivo principal]

**Contexto atual:**
- [Ponto 1 - ambiente/docs/progresso]
- [Ponto 2 - validações concluídas]
- [Ponto 3 - próxima fase]

**Por favor:**
1. [Tarefa 1 - específica e acionável]
2. [Tarefa 2 - com princípio aplicável]
3. [Tarefa 3 - com critério de quando aplicável]
4. [Tarefa 4 - com marcação de conclusão]
```

## Procedimento de Geração

```bash
1. Analisar estado atual
   - Ler Roadmap.md - Milestone atual e DoR/DoD
   - Ler TODO.md - Tarefas pendentes e progresso
   - Ler plans em .claude/plans/ (se existir)
   - Verificar último commit - O que foi feito
   - Ler Projeto.md - Regras de negócio (se relevante)

2. Identificar informações essenciais
   - Milestone/tarefa atual (ex: M1.2)
   - Objetivo principal
   - Metas quantitativas (ex: >80% coverage)
   - Contexto mínimo
   - Próxima fase/tarefa pendente

3. Gerar prompt seguindo formato obrigatório
   - Max 250 tokens
   - 3-5 referências @
   - 3-4 tarefas específicas

4. Validar prompt gerado
   - Checklist de qualidade
   - Confirmar concisão
```

## Templates por Tipo

### Template 1: Retomada de Planejamento

```markdown
Vamos continuar o desenvolvimento do {{PROJECT_NAME}} no milestone [MILESTONE-ID] ([NOME]).

**Referências principais:**
- @.claude/plans/[plano].md (plano de implementação detalhado)
- @documents/core/TODO.md (seção [MILESTONE-ID] com checklist)
- @documents/core/Roadmap.md (contexto de DoR/DoD)

**Objetivo:** [Objetivo principal]

**Contexto atual:**
- Planejamento completo documentado em @.claude/plans/[plano].md
- DoR validado ✅
- Próxima fase: [Nome da próxima fase]

**Por favor:**
1. Leia o plano em @.claude/plans/[plano].md
2. Identifique próxima tarefa [ ] no TODO.md (seção [MILESTONE-ID])
3. Implemente seguindo:
   - pre-commit-check (padrões Python, qualidade, segurança)
   - Chunks ≤100 linhas (princípios CLAUDE.md)
   - rules/api-integration-patterns.md (quando API externa)
4. Atualize TODO.md marcando [x] ao concluir
```

### Template 2: Retomada de Implementação

```markdown
Vamos continuar a implementação do milestone [MILESTONE-ID] ([NOME]).

**Referências principais:**
- @documents/core/TODO.md (seção [MILESTONE-ID] - [N]% concluído)
- @documents/core/Roadmap.md (DoD e critérios)
- @src/[módulo]/[arquivo] (última implementação)

**Objetivo:** [Objetivo principal]

**Progresso atual:**
- [N]% concluído ([X]/[Y] tarefas)
- Última implementação: [descrição breve]
- Próxima tarefa: [nome da tarefa]

**Por favor:**
1. Revise tarefa [ ] em TODO.md seção [MILESTONE-ID]
2. Implemente seguindo pre-commit-check (chunks ≤100 linhas)
3. Execute testes (validate-testing)
4. Atualize TODO.md marcando [x] ao concluir
```

### Template 3: Retomada de Testes/Validação

```markdown
Vamos validar a implementação do milestone [MILESTONE-ID] ([NOME]).

**Referências principais:**
- @documents/core/Roadmap.md (seção DoD do [MILESTONE-ID])
- @documents/core/TODO.md (checklist de validação)
- @tests/[tipo]/[arquivo].py (testes implementados)

**Objetivo:** Validar DoD antes de marcar completo

**Status atual:**
- Implementação concluída ✅
- Testes pendentes: [lista]
- Métricas a validar: [lista]

**Por favor:**
1. Execute validate-dod [MILESTONE-ID]
2. Execute testes pendentes (validate-testing)
3. Valide métricas contra DoD
4. Documente evidências em TODO.md
5. Se tudo passar, marque milestone como ✅
```

### Template 4: Retomada de Troubleshooting

```markdown
Vamos resolver o issue [DESCRIÇÃO] no contexto do milestone [MILESTONE-ID].

**Referências principais:**
- @[arquivo-com-erro] (código com issue)
- @documents/core/TODO.md (contexto do milestone)
- @[log-ou-erro] (evidência do problema)

**Problema:** [Descrição concisa]

**Contexto:**
- Sintoma: [o que está acontecendo]
- Esperado: [o que deveria acontecer]
- Tentativas: [o que já foi tentado]

**Por favor:**
1. Analise erro em @[arquivo-com-erro]
2. Consulte rules/api-integration-patterns.md se for API externa
3. Implemente correção seguindo pre-commit-check
4. Teste para confirmar resolução
5. Considere criar SOP via update-docs se erro não documentado
```

## Regras de Geração

### SEMPRE:

1. Ser conciso (≤250 tokens)
2. Usar @ references (facilita navegação)
3. Incluir métricas (progresso %, coverage)
4. Referenciar skills aplicáveis
5. Listar próximas tarefas (max 4)
6. Manter contexto mínimo
7. Usar checkboxes
8. Incluir validações

### NUNCA:

1. ❌ Incluir histórico completo da sessão
2. ❌ Duplicar conteúdo dos arquivos referenciados
3. ❌ Usar descrições genéricas ("continue o trabalho")
4. ❌ Omitir referências aos arquivos principais
5. ❌ Criar prompts >300 tokens sem justificativa
6. ❌ Esquecer de mencionar milestone/tarefa atual

## Validação do Prompt

Após gerar, verificar:

- [ ] Concisão: ≤250 tokens (justificar se >300)
- [ ] Referências: 3-5 arquivos @
- [ ] Objetivo: Declarado claramente
- [ ] Contexto: 3-5 bullets de status
- [ ] Tarefas: 3-4 ações específicas
- [ ] Skills: Referencia skills aplicáveis
- [ ] Métricas: Inclui progresso % ou metas
- [ ] Milestone: Identifica claramente qual

## Fluxo de Uso

### Cenário 1: Sessão Extensa

```bash
# No final da sessão:
"A sessão ficou extensa. Gere um prompt para continuar."

# Gerar prompt
→ generate-session-prompt [milestone-id]

# Copiar e usar em nova sessão
```

### Cenário 2: Retomada Após Pausa

```bash
# Nova sessão após dias/semanas
→ generate-session-prompt [milestone-id]

# Gera prompt apropriado
```

### Cenário 3: Mudança de Ferramenta

```bash
# Cursor → Claude Code
→ generate-session-prompt [milestone-id]

# Prompt otimizado para nova ferramenta
```

## Troubleshooting

### Problema: Prompt muito genérico

**Causa:** Milestone não identificado ou TODO.md desatualizado

**Solução:** Atualizar TODO.md primeiro ou especificar milestone

### Problema: Prompt muito longo

**Causa:** Contexto excessivo ou múltiplos objetivos

**Solução:** Focar em um milestone específico, resumir contexto

### Problema: Referências quebradas

**Causa:** Arquivos movidos ou renomeados

**Solução:** Executar validate-docs-links primeiro

## Referências

- `documents/core/Roadmap.md` - Milestones e DoR/DoD
- `documents/core/TODO.md` - Tarefas e progresso
- `documents/core/Projeto.md` - Regras de negócio
- `CLAUDE.md` - Regras gerais

## Skills Relacionadas

- `validate-dor` - Validar DoR
- `validate-dod` - Validar DoD
- `update-docs` - Atualizar documentação
- `pre-commit-check` - Qualidade antes de commit
