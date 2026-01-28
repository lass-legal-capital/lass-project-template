# Guia de Kick-off do Projeto

Este guia explica como usar o template Lass para iniciar um novo projeto.

---

## Passo 1: Criar Repositório

### Via GitHub UI

1. Acesse o repositório template
2. Clique em **"Use this template"** → **"Create new repository"**
3. Preencha:
   - **Owner:** sua organização
   - **Repository name:** nome-do-projeto (slug)
   - **Description:** descrição breve
   - **Visibility:** Private (recomendado para projetos internos)

### Via CLI (GitHub CLI)

```bash
gh repo create org/nome-projeto --template lass-legal-capital/lass-project-template --private
cd nome-projeto
```

---

## Passo 2: Preparar Documentos de Kick-off

Coloque na pasta `documents/archive/` todos os documentos relevantes:

| Tipo | Formato | Descrição |
|------|---------|-----------|
| **TAP** | PDF, Word, TXT | Termo de Abertura do Projeto |
| **Transcrições** | TXT | Reuniões de kick-off, discovery |
| **Especificações** | PDF, MD | Requisitos técnicos, mockups |
| **Referências** | Qualquer | Documentos de apoio |

> **Dica:** Quanto mais contexto você fornecer, melhor será o preenchimento automático.

---

## Passo 3: Executar Prompt de Kick-off

### Opção A: Usar o Skill (Recomendado)

Abra o Claude Code no repositório e execute:

```
/kickoff
```

O skill irá:
1. Ler os documentos em `documents/archive/`
2. Extrair informações-chave
3. Preencher todos os templates automaticamente
4. Gerar commit inicial

### Opção B: Prompt Manual

Se preferir controle manual, copie o conteúdo de `.claude/prompts/kickoff-prompt.md` e forneça ao Claude Code como prompt.

---

## Passo 4: Revisar e Ajustar

Após o preenchimento automático:

### Verificar Arquivos Principais

- [ ] `README.md` - Descrição e status do projeto
- [ ] `.claude/CLAUDE.md` - Regras operacionais
- [ ] `documents/core/Projeto.md` - Fonte de verdade
- [ ] `documents/core/Roadmap.md` - Fases e milestones
- [ ] `documents/core/TODO.md` - Tarefas iniciais
- [ ] `.env.example` - Variáveis de ambiente

### Validar Placeholders

Busque por `{{` para encontrar placeholders não preenchidos:

```bash
grep -r "{{" --include="*.md" .
```

### Ajustar Conforme Necessário

- Adicione/remova fases no Roadmap se necessário
- Ajuste scopes de commit no CLAUDE.md
- Configure .env.example com as variáveis do seu projeto

---

## Passo 5: Commit Inicial

```bash
# Verificar mudanças
git status

# Stage todos os arquivos modificados
git add -A

# Commit inicial
git commit -m "chore(init): setup projeto {{PROJECT_SLUG}} a partir do template Lass"

# Push
git push origin main
```

---

## Estrutura Resultante

Após o kick-off, você terá:

```
seu-projeto/
├── .claude/
│   ├── CLAUDE.md               # ✅ Preenchido com regras do projeto
│   ├── settings.json           # ✅ Configurações Claude Code
│   ├── rules/                  # ✅ Regras técnicas (prontas para uso)
│   ├── skills/                 # ✅ Workflows (prontos para uso)
│   └── prompts/
│       └── kickoff-prompt.md   # Referência do prompt usado
├── .codex/                     # ✅ Mirror para Codex/Cursor
├── documents/
│   ├── README.md               # ✅ Índice da documentação
│   ├── core/
│   │   ├── Projeto.md          # ✅ Fonte de verdade preenchida
│   │   ├── Roadmap.md          # ✅ Fases e milestones definidos
│   │   └── TODO.md             # ✅ Tarefas da Fase 0
│   ├── archive/                # ✅ Documentos originais de kick-off
│   ├── technical/              # Vazio (preencher durante desenvolvimento)
│   └── strategy/               # Vazio (preencher conforme necessário)
├── src/                        # Vazio (código será adicionado)
├── tests/                      # Vazio (testes serão adicionados)
├── .env.example                # ✅ Template de variáveis
├── README.md                   # ✅ README do projeto
└── requirements.txt            # Criar durante Fase 0
```

---

## Próximos Passos

Após o kick-off, siga o workflow padrão:

1. **Fase 0 - Planejamento**
   - Execute `validate-dor Fase0` para verificar pré-requisitos
   - Complete decisões técnicas pendentes
   - Configure ambiente de desenvolvimento
   - Execute `validate-dod Fase0` ao concluir

2. **Fase 1 - PoV**
   - Siga os milestones no Roadmap
   - Use `validate-dor M1.X` antes de cada milestone
   - Use `validate-dod M1.X` ao concluir cada milestone

3. **Desenvolvimento Contínuo**
   - Use `pre-commit-check` antes de commits
   - Use `organize-commits` para commits atômicos
   - Use `fresh-context` quando contexto ficar grande (>150k tokens)

---

## Skills Disponíveis

| Skill | Quando Usar |
|-------|-------------|
| `validate-dor [id]` | Antes de iniciar milestone |
| `validate-dod [id]` | Ao concluir milestone |
| `pre-commit-check` | Antes de cada commit |
| `validate-testing` | Para validar cobertura de testes |
| `organize-commits` | Quando há múltiplas mudanças |
| `fresh-context` | Quando sessão fica grande |
| `update-docs system` | Após mudanças arquiteturais |
| `audit-rules` | Periodicamente |
| `audit-architecture` | Ao completar fases |
| `validate-docs-links` | Ao completar fases |
| `generate-session-prompt` | Para retomada de sessões |

---

## Troubleshooting

### Placeholders não preenchidos

Se alguns `{{PLACEHOLDER}}` não foram preenchidos:
1. Verifique se os documentos de kick-off contêm a informação necessária
2. Preencha manualmente consultando os documentos em `archive/`
3. Ou adicione mais contexto e execute o kick-off novamente

### Skill não encontrado

Se um skill não for reconhecido:
1. Verifique se `.claude/settings.json` está configurado
2. Execute `ls .claude/skills/` para ver skills disponíveis
3. Reinicie o Claude Code

### Conflito de versões

Se houver conflito entre template e projeto existente:
1. O template é projetado para **novos projetos**
2. Para projetos existentes, copie apenas os arquivos necessários manualmente

---

## Manutenção do Template

O template Lass é versionado. Para atualizar um projeto existente:

```bash
# Verificar versão atual
cat .claude/CLAUDE.md | grep "Versão"

# Comparar com template
# (verificar changelog do template para mudanças relevantes)
```

---

**Versão do Guia:** 1.0.0
**Template Lass:** v1.0.0
**Última atualização:** {{DATE}}
