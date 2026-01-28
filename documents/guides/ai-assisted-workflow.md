# Guia Conciso - Workflow de Desenvolvimento Assistido por IA

## Objetivo
Padronizar o fluxo de desenvolvimento usando Codex e/ou Claude Code, mantendo as regras do projeto, qualidade e rastreabilidade.

## 1) Antes de começar (sempre)
- Ler `documents/core/Roadmap.md` e `documents/core/TODO.md`.
- Validar DoR do milestone: `validate-dor [milestone-id]` (ex.: `validate-dor Fase0`).
- Ler `documents/core/Projeto.md` se a tarefa tocar regras de negócio/arquitetura.

## 2) Durante o desenvolvimento
- Trabalhar em **chunks ≤100 linhas**.
- Usar regras path-targeted:
  - `src/**/*` → `code-quality-standards.md`, `security-best-practices.md`
  - `tests/**/*` → `testing-requirements.md`
- Atualizar `documents/core/TODO.md` conforme o avanço.

## 3) Qualidade e validação
- Antes de commit: `pre-commit-check`.
- Cobertura mínima: >80% geral, >90% regras críticas.
- Se houver verificações programáticas: adicionar `verify:` no TODO.

## 4) Commits atômicos
- 1 task = 1 commit, máx 100 linhas, **nunca** `git add .`.
- Formato: `{type}({milestone}-{task}): {descricao}`.
- Rastrear hashes na seção "Commits do Milestone" do TODO.

## 5) Handoff / sessões longas
- Se sessão >150k tokens ou mudança de milestone: `fresh-context [milestone]`.
- Para retomada rápida: `generate-session-prompt`.

## 6) Ferramenta ativa
- **Codex:** usar `.codex/AGENTS.md`, `.codex/rules/`, `.codex/skills/`.
- **Claude Code:** usar `.claude/CLAUDE.md`, `.claude/rules/`, `.claude/skills/`.
- Manter ambos alinhados; escolher o conjunto conforme a ferramenta.
