# Skill: update-docs

Atualizar documentação técnica do projeto.

---
name: update-docs
description: Atualizar documentação técnica do projeto (arquitetura, planos de implementação, SOPs). Use após completar milestone que mudou arquitetura, após decisão técnica significativa, após refactoring estrutural, ou quando estabelecer processo padronizado que precisa ser documentado.
---

## Quando Usar

- Após completar milestone que mudou arquitetura
- Após decisão técnica significativa (ADR)
- Após refactoring estrutural
- Quando estabelecer processo padronizado (SOP)
- Após implementar task que precisa documentação

## Input Esperado

```
update-docs [tipo] [contexto]
```

Tipos disponíveis:
- `system` - Documentação de arquitetura/sistema
- `task` - Implementation plan de task/milestone
- `sop` - Standard Operating Procedure

Exemplos:
- `update-docs system M1.2` - Atualizar arquitetura após M1.2
- `update-docs task M1.3-01` - Documentar implementation plan da task
- `update-docs sop deployment` - Criar/atualizar SOP de deployment

## Workflow por Tipo

### Tipo: `system`

Atualizar documentação de arquitetura em `documents/technical/`.

```
1. Identificar mudanças de arquitetura no milestone
2. Atualizar diagrama de componentes (se aplicável)
3. Documentar decisões técnicas (ADR format)
4. Atualizar fluxos de dados
5. Validar links com validate-docs-links
```

Output esperado:
- Arquivo atualizado em `documents/technical/`
- ADR criado se decisão significativa
- Diagramas atualizados

### Tipo: `task`

Salvar implementation plan de uma task em `documents/technical/implementation-plans/`.

```
1. Extrair contexto da task do TODO.md
2. Documentar abordagem técnica escolhida
3. Listar arquivos criados/modificados
4. Documentar trade-offs e decisões
5. Incluir snippets de código relevantes
```

Output esperado:
```markdown
# Implementation Plan: [TASK-ID]

## Contexto
[Descrição da task e objetivo]

## Abordagem
[Decisões técnicas e rationale]

## Arquivos Modificados
- `path/to/file.py` - [descrição da mudança]

## Trade-offs
- [Decisão]: [Alternativas consideradas]

## Código Relevante
[Snippets com explicação]

## Testes
[Como a implementação foi validada]
```

### Tipo: `sop`

Criar/atualizar Standard Operating Procedure em `documents/guides/`.

```
1. Identificar processo a documentar
2. Listar pré-requisitos
3. Documentar passos step-by-step
4. Incluir troubleshooting comum
5. Adicionar exemplos práticos
```

Output esperado:
```markdown
# SOP: [Nome do Processo]

## Objetivo
[O que este SOP documenta]

## Pré-requisitos
- [ ] [Requisito 1]
- [ ] [Requisito 2]

## Procedimento

### Passo 1: [Título]
[Instruções detalhadas]

### Passo 2: [Título]
[Instruções detalhadas]

## Troubleshooting

### Problema: [descrição]
**Solução:** [como resolver]

## Referências
- [Link para doc relacionada]
```

## Estrutura de Documentação

```
documents/
├── core/                    # Documentos principais (Projeto, Roadmap, TODO)
├── technical/               # Documentação técnica
│   ├── architecture.md      # Visão geral de arquitetura
│   ├── decisions/           # ADRs (Architecture Decision Records)
│   │   └── ADR-001-*.md
│   └── implementation-plans/ # Planos de implementação
│       └── M1.2-plan.md
├── guides/                  # SOPs e guias operacionais
│   └── deployment.md
└── strategy/                # Documentos de estratégia
```

## Templates

### ADR Template

```markdown
# ADR-XXX: [Título da Decisão]

## Status
[Proposto | Aceito | Rejeitado | Substituído por ADR-YYY]

## Contexto
[Por que precisamos decidir isso?]

## Decisão
[O que foi decidido?]

## Alternativas Consideradas
1. [Opção 1] - Pros: ... / Cons: ...
2. [Opção 2] - Pros: ... / Cons: ...

## Consequências
### Positivas
- [Benefício 1]

### Negativas
- [Custo/Trade-off 1]

## Referências
- [Links relevantes]
```

## Regras

1. **Docs seguem código** - Quando código muda, docs devem ser atualizados
2. **ADRs são imutáveis** - Não edite, crie novo ADR que substitui
3. **Backlinks obrigatórios** - Referencie Projeto.md quando relevante
4. **Validar links** - Use `validate-docs-links` após atualizar

## Integração com Outros Skills

| Skill | Quando Usar |
|-------|-------------|
| `validate-docs-links` | Após atualizar documentação |
| `validate-dod` | Inclui critério de docs atualizados |
| `audit-architecture` | Verificar redundância em docs |

## Exemplo de Uso

```
User: update-docs task M1.2-03

Claude:
Criando implementation plan para task M1.2-03...

# Implementation Plan: M1.2-03 - Implementar Parser de Relatórios

## Contexto
Task para implementar o parser que extrai dados dos relatórios baixados.

## Abordagem
- Usar pandas para parsing de Excel
- Normalizar nomes de colunas automaticamente
- Validar schema antes de processar

## Arquivos Modificados
- `src/processors/parser.py` - Novo arquivo com classe ReportParser
- `src/processors/__init__.py` - Export do parser
- `tests/unit/test_parser.py` - Testes unitários

## Trade-offs
- **pandas vs openpyxl puro**: pandas escolhido pela API mais simples
  e melhor integração com processamento posterior

## Código Relevante
```python
class ReportParser:
    def parse(self, file_path: Path) -> DataFrame:
        """Parse relatório Excel para DataFrame normalizado."""
        ...
```

## Testes
- 12 testes unitários cobrindo happy path e edge cases
- Coverage: 92% do módulo parser

---
Arquivo salvo em: documents/technical/implementation-plans/M1.2-03-plan.md
```

---

**Versão:** 1.0.0
**Última atualização:** Template
