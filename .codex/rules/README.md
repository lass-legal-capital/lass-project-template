# Rules (Path-Targeted)

Regras técnicas carregadas automaticamente baseadas no contexto do arquivo.

## Regras Disponíveis

| Regra | Paths | Descrição |
|-------|-------|-----------|
| `code-quality-standards.md` | `src/**/*` | Padrões de código Python |
| `security-best-practices.md` | `src/**/*`, `.env*` | Segurança e secrets |
| `testing-requirements.md` | `tests/**/*` | Requisitos de testes |
| `api-integration-patterns.md` | `src/collectors/**/*` | Integração com APIs |
| `documentation-templates.md` | `*.md` | Templates de documentação |

## Como Funciona

As regras são carregadas automaticamente quando você edita arquivos nos paths especificados.
Isso garante que as práticas corretas sejam aplicadas ao contexto certo.
