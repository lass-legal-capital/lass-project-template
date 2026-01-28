# Context Handoff Pattern

## Metadata

- **Versão:** 1.0.0
- **Status:** Ativo
- **Última atualização:** {{DATE}}

---

## O Que é Este Diretório

Este diretório contém **CONTEXT.md** files que servem como documentos de handoff entre sessões e subagentes. Eles capturam o contexto essencial de cada milestone para permitir continuação de trabalho em janelas de contexto limpas.

## Problema que Resolve

**Context Rot:** Em sessões longas (>150k tokens), o contexto acumula noise que degrada a qualidade das respostas. O padrão CONTEXT.md permite:

1. **Fresh Context** - Subagentes iniciam com contexto limpo e focado
2. **Handoff Eficiente** - Transições entre sessões sem perda de informação
3. **Decisões Locked** - Escolhas já feitas não precisam ser re-discutidas

## Estrutura do CONTEXT.md

Cada arquivo CONTEXT.md usa **tags semânticas XML-style** para organizar informação:

```markdown
<domain>
  Escopo fixo do milestone (vem do Roadmap.md).
  Define o que ESTÁ e NÃO ESTÁ no scope.
  Esta seção é IMUTÁVEL durante o milestone.
</domain>

<decisions>
  ## Decisões Locked
  Escolhas já confirmadas que NÃO devem ser re-questionadas.
  Ex: "Usar Selenium (não Playwright)"

  ## Claude's Discretion
  Áreas onde o agente pode tomar decisões sem perguntar.
  Ex: "Estrutura interna de classes"
</decisions>

<specifics>
  Referências específicas do usuário/stakeholder.
  Ex: "E-mail deve parecer com o relatório semanal atual"
  Pode estar vazio se não há referências específicas.
</specifics>

<deferred>
  Ideias e features para outras fases.
  Previne scope creep mantendo registro do que foi adiado.
  Ex: "Dashboard histórico → Fase 4"
</deferred>
```

## Nomenclatura de Arquivos

**Formato:** `M{X}.{Y}-CONTEXT.md`

**Exemplos:**
- `M1.2-CONTEXT.md` - Contexto do milestone M1.2
- `Fase0-CONTEXT.md` - Contexto da Fase 0 inteira
- `pre-fase-0-CONTEXT.md` - Contexto de pré-setup

## Quando Criar/Atualizar

### Criar CONTEXT.md

1. **Ao iniciar um milestone** - Skill `fresh-context` gera automaticamente
2. **Após sessão longa** (>150k tokens) - Capturar estado atual
3. **Antes de handoff para subagente** - Fornecer contexto focado

### Atualizar CONTEXT.md

1. **Após decisão técnica** - Mover para "Decisões Locked"
2. **Quando ideia é adiada** - Adicionar em `<deferred>`
3. **Quando referência específica surge** - Adicionar em `<specifics>`

## Integração com Outros Documentos

```
Roadmap.md (DoR/DoD)
    ↓ domain
CONTEXT.md (handoff)
    ↓ context
Subagente/Nova Sessão
    ↓ execução
TODO.md (tracking)
```

**Não duplicar:**
- DoR/DoD vem do Roadmap.md (referência, não cópia)
- Tarefas granulares vem do TODO.md
- Regras de negócio vem do Projeto.md

## Uso com /clear

Ao usar CONTEXT.md para nova sessão:

```markdown
/clear

[Colar conteúdo do CONTEXT.md aqui]

Vamos continuar a implementação do [MILESTONE-ID].
```

**Rationale para /clear:**
- Limpa contexto degradado
- CONTEXT.md fornece essencial em ~200-300 tokens
- Subagente inicia com foco máximo

## Referências

- **Template:** `template-CONTEXT.md` neste diretório
- **Skill:** `.claude/skills/fresh-context/SKILL.md`
- **Roadmap:** `documents/core/Roadmap.md`
- **TODO:** `documents/core/TODO.md`

---

**Última atualização:** {{DATE}}
