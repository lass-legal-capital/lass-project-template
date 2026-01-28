---
name: fresh-context
description: Gerar ou atualizar documento CONTEXT.md para handoff entre sessões ou subagentes. Use quando sessão >150k tokens, ao iniciar novo milestone, ao handoff para subagente, ou quando context rot degradar qualidade. Cria documento self-contained para continuação em janela limpa.
---

# Fresh Context - Handoff Document Generator

Gera documento CONTEXT.md self-contained para permitir continuação de trabalho em contexto limpo.

## Regra de Ouro

> **"Contexto fresco > contexto acumulado com noise"**

Sessões longas (>150k tokens) degradam qualidade. CONTEXT.md permite recomeço limpo sem perda de informação essencial.

## Quando Usar

- **Sessão >150k tokens** - Context rot detectado
- **Iniciar novo milestone** - Criar CONTEXT.md antes de começar
- **Handoff para subagente** - Fornecer contexto focado
- **Retomada após pausa** - Em vez de reler toda sessão anterior
- **Transição entre fases** - Capturar estado atual

## Workflow de Geração

```bash
1. Receber milestone-id (ex: M1.2) ou detectar atual via Roadmap.md

2. Ler documentos fonte:
   - Roadmap.md → Escopo (DoR/DoD do milestone)
   - TODO.md → Progresso e tarefas pendentes
   - Projeto.md → Decisões técnicas já tomadas (se aplicável)
   - Sessão atual → Decisões e discussões recentes

3. Preencher template CONTEXT.md:
   - <domain> → Escopo fixo do Roadmap.md
   - <decisions> → Decisões locked + discretion areas
   - <specifics> → Referências específicas do usuário
   - <deferred> → Ideias adiadas para evitar scope creep

4. Salvar em:
   .planning/context/{milestone-id}-CONTEXT.md

5. Gerar prompt de continuação (opcional):
   - Sugerir /clear com rationale
   - Incluir referências mínimas
```

## Template de Seções

### `<domain>` - Escopo Imutável

```markdown
<domain>
## Escopo do Milestone

**O que ESTÁ no scope:**
- [Extrair de DoR/DoD do Roadmap.md]

**O que NÃO ESTÁ no scope:**
- [Listar explicitamente para evitar scope creep]

**Referência:** Roadmap.md seção [MILESTONE-ID]
</domain>
```

### `<decisions>` - Decisões e Discretion

```markdown
<decisions>
## Decisões Locked

[Decisões já tomadas que NÃO devem ser re-questionadas]

- **Decisão 1:** Descrição
  - Motivo: Justificativa breve

## Claude's Discretion

[Áreas onde o agente pode decidir autonomamente]

- Estrutura interna de classes
- Nomes de variáveis locais
- Ordem de implementação de subtarefas
</decisions>
```

### `<specifics>` - Referências do Usuário

```markdown
<specifics>
## Referências Específicas

- "Requisito específico do usuário"
- "Formato ou padrão solicitado"

[Pode estar vazio se não há referências específicas]
</specifics>
```

### `<deferred>` - Ideias Adiadas

```markdown
<deferred>
## Ideias Adiadas

| Ideia | Fase Sugerida | Notas |
|-------|---------------|-------|
| Feature X | Fase 4 | Mencionado na discussão inicial |
| Integração Y | Backlog | Usuário não tem ainda |
</deferred>
```

## Exemplo de Uso

### Cenário: Sessão longa, iniciar milestone

**Input:** `fresh-context M1.2`

**Output:** Arquivo `.planning/context/M1.2-CONTEXT.md`

```markdown
# CONTEXT: M1.2 - Nome do Milestone

**Fase:** Fase 1
**Gerado em:** [DATA]
**Última atualização:** [DATA]

---

<domain>
## Escopo do Milestone

**O que ESTÁ no scope:**
- Funcionalidade principal A
- Funcionalidade principal B
- Validação de dados

**O que NÃO ESTÁ no scope:**
- Funcionalidades de outras fases
- Otimizações (fases posteriores)

**Referência:** Roadmap.md seção M1.2
</domain>

---

<decisions>
## Decisões Locked

### Tecnologia
- **Framework:** Escolha X
  - Alternativas: Y, Z
  - Motivo: Justificativa

### Formato de Dados
- **Fonte:** Formato escolhido
  - Alternativas: Outros formatos
  - Motivo: Justificativa

## Claude's Discretion

- Estrutura interna de classes
- Nomes de métodos auxiliares
- Estratégia de implementação interna
</decisions>

---

<specifics>
## Referências Específicas

- Credenciais em `.env`
- Timeout padrão: 30 segundos
- Retry: 3 tentativas com backoff
</specifics>

---

<deferred>
## Ideias Adiadas

| Ideia | Fase Sugerida | Notas |
|-------|---------------|-------|
| Feature avançada | Fase 3 | Hardening |
| Otimização | Fase 4 | Otimização futura |
</deferred>

---

## Próximos Passos

1. Implementar componente A
2. Implementar componente B
3. Testes unitários

**Skills aplicáveis:**
- `pre-commit-check` - Antes de commits
- `validate-testing` - Após implementar testes
```

### Prompt de Continuação Gerado

```markdown
/clear

Vamos continuar M1.2 (Nome do Milestone).

**Contexto:** Ver .planning/context/M1.2-CONTEXT.md

**Decisões locked:** [Lista resumida]

**Próxima tarefa:** [Tarefa específica]

**Referências:**
- @.planning/context/M1.2-CONTEXT.md (handoff)
- @documents/core/TODO.md (tracking)
- @rules/[regra-relevante].md (padrões)
```

## Parâmetros

### Milestone ID (obrigatório ou auto-detectado)

```bash
# Especificar milestone
fresh-context M1.2

# Auto-detectar do Roadmap.md
fresh-context

# Contexto de fase inteira
fresh-context Fase0
```

### Opções

| Opção | Descrição |
|-------|-----------|
| `--update` | Atualiza CONTEXT.md existente |
| `--prompt` | Gera também prompt de continuação |
| `--subagent` | Formato otimizado para subagente |

## Integração com generate-session-prompt

O skill `fresh-context` complementa `generate-session-prompt`:

| Skill | Propósito | Output |
|-------|-----------|--------|
| `generate-session-prompt` | Prompt curto (~250 tokens) | Texto para copiar |
| `fresh-context` | Documento persistente (~300-500 tokens) | Arquivo CONTEXT.md |

**Quando usar qual:**
- Pausa curta → `generate-session-prompt`
- Sessão longa/subagente → `fresh-context`
- Novo milestone → `fresh-context` primeiro, depois `generate-session-prompt` se precisar

## Referências

- **Template:** `.planning/context/template-CONTEXT.md`
- **Documentação:** `.planning/context/README.md`
- **Roadmap:** `documents/core/Roadmap.md`
- **TODO:** `documents/core/TODO.md`

## Skills Relacionadas

- `generate-session-prompt` - Prompt curto para retomada
- `validate-dor` - Validar DoR antes de iniciar
- `validate-dod` - Validar DoD ao concluir
