# Documentação - {{PROJECT_NAME}}

## Estrutura

```
documents/
├── README.md                    # Este arquivo (índice)
├── core/                        # Documentos principais
│   ├── Projeto.md               # Fonte de verdade (living document)
│   ├── Roadmap.md               # Fases, milestones, DoR/DoD
│   └── TODO.md                  # Tracking granular de tarefas
├── archive/                     # Documentos de kick-off (histórico)
│   └── README.md                # Instruções para arquivos de kick-off
├── technical/                   # Documentação técnica detalhada
│   └── .gitkeep
└── strategy/                    # Análises estratégicas e decisões
    └── .gitkeep
```

---

## Documentos Core

| Documento | Propósito | Quando Consultar |
|-----------|-----------|------------------|
| [Projeto.md](core/Projeto.md) | **Fonte de verdade** - Regras de negócio, arquitetura, decisões | Sempre que precisar de contexto |
| [Roadmap.md](core/Roadmap.md) | Fases, milestones, DoR/DoD | Planejamento, validação de progresso |
| [TODO.md](core/TODO.md) | Tracking granular, progresso diário | Durante desenvolvimento |

---

## Documentos de Kick-off (Archive)

A pasta `archive/` contém documentos originais do kick-off do projeto:

- **TAP** (Termo de Abertura do Projeto) - PDF ou Word
- **Transcrições de reuniões** - TXT
- **Especificações técnicas originais** - Se houver

> **Nota:** Estes documentos são históricos. Para decisões atuais, consulte sempre `core/Projeto.md`.

---

## Documentação Técnica (Technical)

Documentação técnica detalhada para aspectos específicos:

- `architecture.md` - Visão técnica da arquitetura
- `integrations.md` - Detalhes de integrações externas
- `implementation-plans/` - Planos de implementação por milestone

> **Salvaguarda:** Todo documento em `technical/` deve linkar para a seção correspondente em `core/Projeto.md`.

---

## Análises Estratégicas (Strategy)

Documentos de análise e decisões estratégicas:

- `technology-choices.md` - Decisões de stack e justificativas
- `risk-analysis.md` - Riscos e mitigações

> **Salvaguarda:** Decisões finais devem ser refletidas em `core/Projeto.md`.

---

## Regras de Documentação

### Single Source of Truth

1. `core/Projeto.md` é a **fonte única de verdade**
2. `technical/` e `strategy/` são **suplementares**
3. Se houver conflito, **Projeto.md prevalece**

### Salvaguardas

- Todo documento suplementar deve **linkar** para Projeto.md
- Evite duplicação de conteúdo entre diretórios
- Atualize `Roadmap.md` e `TODO.md` quando status mudar

### Navegação

- Máximo **3 cliques** entre quaisquer 2 documentos
- Use links relativos (`[link](./path/to/file.md)`)
- Mantenha índices atualizados

---

## Skills Relacionadas

- `validate-docs-links check` - Validar integridade de links
- `update-docs system` - Atualizar documentação técnica
- `audit-architecture` - Auditar redundância entre documentos

---

**Última atualização:** {{DATE}}
**Versão:** 1.0.0
