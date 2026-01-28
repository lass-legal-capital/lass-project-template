# Agent Skills

## Metadata

- **Versão:** 1.0.0
- **Status:** Template
- **Última atualização:** Template
- **Responsável:** {{RESPONSIBLE_NAME}}

---

## Sobre Este Diretório

Este diretório contém **Agent Skills** - instruções especializadas que ensinam o agente de IA a executar tarefas específicas do projeto.

**Skills vs Commands:**
- **Commands**: Documentação de procedimentos para execução manual ou pelo agente
- **Skills**: Instruções otimizadas para o agente, seguindo padrão MCP Agent Skills

**Benefícios das Skills:**
- Descoberta automática pelo agente (via description triggers)
- Formato otimizado para consumo por IA
- Progressive disclosure (carga no context apenas quando necessário)
- Integração com MCP (Model Context Protocol)

---

## Índice de Skills

### Skills Essenciais (7)

Operações recorrentes de documentação, validação e manutenção.

| Skill | Arquivo | Descrição | Uso Frequente |
|-------|---------|-----------|---------------|
| `audit-rules` | [audit-rules/SKILL.md](audit-rules/SKILL.md) | Auditar qualidade e integridade das regras | Antes de commits, ao completar fases |
| `audit-roadmap-refs` | [audit-roadmap-refs/SKILL.md](audit-roadmap-refs/SKILL.md) | Auditar referências a skills em Roadmap/TODO | Após criar skill, auditoria periódica |
| `audit-architecture` | [audit-architecture/SKILL.md](audit-architecture/SKILL.md) | Auditar redundância e sincronização entre arquivos | Antes de completar fase, após criar docs |
| `organize-commits` | [organize-commits/SKILL.md](organize-commits/SKILL.md) | Organizar mudanças em commits granulares | Após trabalho extenso, antes de push |
| `update-docs` | [update-docs/SKILL.md](update-docs/SKILL.md) | Atualizar documentação técnica | Após milestone, decisão arquitetural |
| `validate-docs-links` | [validate-docs-links/SKILL.md](validate-docs-links/SKILL.md) | Validar links e backlinks | Antes de completar DoD, após criar docs |
| `generate-session-prompt` | [generate-session-prompt/SKILL.md](generate-session-prompt/SKILL.md) | Gerar prompt para retomada de sessão | Sessão >150k tokens, mudança de contexto |

### Skills de Validação (4)

Validação de qualidade, testes, e processos (Definition of Ready/Done).

| Skill | Arquivo | Descrição | Uso Frequente |
|-------|---------|-----------|---------------|
| `validate-dod` | [validate-dod/SKILL.md](validate-dod/SKILL.md) | Validar Definition of Done | **OBRIGATÓRIO** antes de marcar milestone completo |
| `validate-dor` | [validate-dor/SKILL.md](validate-dor/SKILL.md) | Validar Definition of Ready | **OBRIGATÓRIO** antes de iniciar milestone |
| `pre-commit-check` | [pre-commit-check/SKILL.md](pre-commit-check/SKILL.md) | Checklist completo pré-commit (inclui code quality) | **SEMPRE** antes de git commit |
| `validate-testing` | [validate-testing/SKILL.md](validate-testing/SKILL.md) | Validar cobertura de testes | Após feature, pré-commit, DoD |

---

## Como o Agente Usa as Skills

### 1. Descoberta Automática

O agente lê o **description** de cada skill para decidir quando aplicar:

```yaml
description: Validar Definition of Done de um milestone antes de marcá-lo
como completo. Use OBRIGATORIAMENTE antes de marcar milestone como completo,
durante desenvolvimento como checklist de progresso, ou antes de transição
para próximo milestone.
```

**Triggers identificados:**
- "antes de marcar milestone completo"
- "checklist de progresso"
- "transição para próximo milestone"

### 2. Carregamento Just-in-Time

**Metadata sempre em contexto (~100 palavras por skill):**
- `name` e `description`

**Body carregado apenas quando skill trigga (<5k palavras):**
- Procedimentos detalhados
- Exemplos
- Referências

### 3. Progressive Disclosure

Skills podem referenciar recursos adicionais que são lidos apenas se necessário:

```markdown
## Referências Detalhadas

Para procedimento completo de correção automática, veja:
- [auto-fix-guide.md](references/auto-fix-guide.md)
```

---

## Workflow Típico por Fase

### Fase de Setup

**Skills usadas:**
1. `validate-docs-links` - Validar arquivos criados
2. `audit-rules` (full) - Auditar todas as regras
3. `organize-commits` - Organizar commits granulares
4. `validate-dod` - Validar DoD completo

**Ordem:**
```
[Criar arquivos] → validate-docs-links → [Fix links] →
audit-rules full → [Resolver issues] → organize-commits →
validate-dod
```

### Fase de Planejamento

**Skills usadas:**
1. `validate-dor` - Validar pré-requisitos
2. `update-docs` (system) - Se arquitetura decidida
3. `validate-dod` - Validar decisões tomadas

### Fase de Desenvolvimento

#### Antes de Milestone

```bash
# Validar pré-requisitos
→ validate-dor [milestone-id]
```

#### Durante Milestone

```bash
# Validações rápidas durante desenvolvimento
→ validate-testing

# Antes de commit (inclui code quality, testing, security)
→ pre-commit-check
→ organize-commits (se múltiplas mudanças)
```

#### Ao Completar Milestone

```bash
# 1. Validar DoD
→ validate-dod [milestone-id]

# 2. Salvar implementation plan
→ update-docs task [milestone-id]

# 3. Atualizar arquitetura (se necessário)
→ update-docs system

# 4. Validar links
→ validate-docs-links check

# 5. Organizar commits
→ organize-commits

# 6. Commit final
git commit -m "docs(milestone): finaliza [milestone-id]"
```

---

## Convenções de Nomenclatura

### Padrão de Nomes

**Skills (diretórios):**
- `kebab-case` (lowercase, hyphens)
- Verbo-led quando possível
- Máximo 64 caracteres
- Exemplo: `validate-dod`, `organize-commits`, `audit-rules`

**Arquivo principal:**
- `SKILL.md` (uppercase, obrigatório)

### Estrutura de Diretório

```
.claude/skills/
├── README.md                           # Este arquivo
├── audit-architecture/
│   └── SKILL.md
├── audit-roadmap-refs/
│   └── SKILL.md
├── audit-rules/
│   └── SKILL.md
├── fresh-context/
│   └── SKILL.md
├── generate-session-prompt/
│   └── SKILL.md
├── organize-commits/
│   └── SKILL.md
├── pre-commit-check/
│   └── SKILL.md
├── update-docs/
│   └── SKILL.md
├── validate-docs-links/
│   └── SKILL.md
├── validate-dod/
│   └── SKILL.md
├── validate-dor/
│   └── SKILL.md
└── validate-testing/
    └── SKILL.md
```

---

## Ciclo de Vida das Skills

### Criar Nova Skill

**1. Identificar necessidade:**
- Processo recorrente (>3 vezes)
- Validação complexa padronizada
- Checklist extenso consistente
- Tarefa propensa a erros

**2. Planejar skill:**
- Nome (kebab-case, verbo-led)
- Description (triggers claros)
- Conteúdo essencial (<500 linhas)
- Referências externas (se necessário)

**3. Criar estrutura:**
```bash
mkdir .claude/skills/skill-name
touch .claude/skills/skill-name/SKILL.md
```

**4. Escrever SKILL.md:**
```markdown
---
name: skill-name
description: [O que faz] + [Quando usar com triggers claros]
---

# Skill Title

[Conteúdo conciso, imperativo, acionável]
```

**5. Adicionar ao índice:**
- Atualizar este README.md
- Testar em cenário real
- Commitar: `docs(skills): adiciona skill [nome]`

### Atualizar Skill Existente

**Gatilhos para atualização:**
- Processo subjacente evolui
- Feedback de uso (confuso, incompleto)
- Integração com novas skills
- Fase do projeto muda

**Processo:**
1. Ler skill existente
2. Atualizar conteúdo
3. Manter estrutura (não quebrar formato)
4. Adicionar exemplos se necessário
5. Atualizar este README se mudou triggers
6. Commitar: `docs(skills): atualiza [skill] - [contexto]`

---

## Integração com Outras Ferramentas

### MCP Agent Skills

Skills seguem padrão MCP (Model Context Protocol) Agent Skills:

**Benefícios:**
- Descoberta automática via description
- Carregamento eficiente (metadata + body sob demanda)
- Compartilhamento entre projetos
- Versionamento independente

**Compatibilidade:**
- Cursor AI (via MCP)
- OpenAI Codex (via Agent Skills)
- Claude Code (via Agent Skills)
- Outros editores com suporte MCP

---

## Métricas de Qualidade

### Por Skill

**Checklist de qualidade:**
- [ ] Name: kebab-case, <64 chars
- [ ] Description: triggers claros, <1024 chars
- [ ] Body: <500 linhas
- [ ] Instruções imperativas/infinitivas
- [ ] Exemplos contextualizados
- [ ] Procedimentos acionáveis
- [ ] Referências funcionais

### Conjunto de Skills

**Métricas:**
- Total de skills: 11
- Skills essenciais: 7
- Skills de validação: 4
- Linhas médias por skill: ~350
- Coverage de workflows: 100%

---

## Referências

### Documentação Core
- `documents/core/Projeto.md` - Contexto do projeto
- `documents/core/Roadmap.md` - Milestones e fases
- `documents/core/TODO.md` - Tracking granular
- `CLAUDE.md` - Regras sempre ativas

### Regras
- `.claude/rules/README.md` - Índice de regras
- `.claude/rules/*.md` - Regras path-targeted

---

## Uso Rápido

**Durante desenvolvimento:**
```bash
→ validate-testing
```

**Antes de commit:**
```bash
→ pre-commit-check
→ organize-commits  # Se múltiplas mudanças
```

**Antes de iniciar milestone:**
```bash
→ validate-dor [milestone-id]
```

**Ao completar milestone:**
```bash
→ validate-dod [milestone-id]
→ update-docs task [milestone-id]
→ update-docs system  # Se arquitetura mudou
```

**Antes de completar fase:**
```bash
→ validate-docs-links check
→ audit-rules full
```

---

**Última atualização:** Template
**Versão:** 1.0.0
