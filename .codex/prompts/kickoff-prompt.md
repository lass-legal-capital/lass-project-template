# Prompt de Kick-off de Projeto Lass

## Contexto

Você está configurando um novo projeto da organização Lass usando o template padrão.
Sua tarefa é preencher os templates com informações específicas do projeto.

---

## Documentos de Entrada

Analise os arquivos em `documents/archive/`:
- TAP (Termo de Abertura do Projeto)
- Transcrições de reuniões
- Especificações técnicas
- Qualquer outro documento de contexto

---

## Tarefas

### 1. Extrair Informações-Chave

Dos documentos de kick-off, extraia:

**Informações Básicas:**
- Nome do projeto (formal e slug para paths)
- Descrição breve (1-2 frases)
- Contexto de negócio (problema a resolver)
- Organização responsável
- Responsável/owner do projeto

**Objetivos e Escopo:**
- Objetivo principal
- Objetivos específicos (3-5)
- O que está no escopo (MVP)
- O que está fora do escopo

**Aspectos Técnicos:**
- Stack tecnológica proposta
- Integrações necessárias
- Dependências externas
- Requisitos de infraestrutura

**Gestão:**
- Fases propostas
- Timeline estimada
- Riscos identificados
- Stakeholders

---

### 2. Preencher Templates

Substitua os placeholders `{{PLACEHOLDER}}` nos seguintes arquivos:

#### Arquivos a Preencher

1. **README.md** (root)
   - `{{PROJECT_NAME}}` - Nome formal
   - `{{PROJECT_DESCRIPTION}}` - Descrição breve
   - `{{PROJECT_SLUG}}` - Nome para URLs/paths (lowercase, hifens)
   - `{{GITHUB_ORG}}` - Organização no GitHub
   - `{{COMMIT_SCOPES}}` - Scopes para conventional commits
   - `{{RESPONSIBLE_NAME}}` - Nome do responsável
   - `{{CONTACT_EMAIL}}` - E-mail de contato
   - `{{ORGANIZATION_NAME}}` - Nome da organização
   - `{{LICENSE_TYPE}}` - Tipo de licença (ex: "Proprietário - Uso Interno")
   - `{{DATE}}` - Data atual

2. **.claude/CLAUDE.md**
   - `{{PROJECT_NAME}}` - Nome formal
   - `{{COMMIT_SCOPES}}` - Scopes específicos do projeto
   - `{{DATE}}` - Data atual
   - `{{AUTHOR_NAME}}` - Nome do autor

3. **documents/core/Projeto.md**
   - Todos os placeholders de contexto, objetivos, arquitetura
   - Regras de negócio específicas
   - Stack tecnológico
   - Riscos e dependências

4. **documents/core/Roadmap.md**
   - Fases com datas estimadas
   - Milestones detalhados
   - DoR/DoD específicos

5. **documents/core/TODO.md**
   - Tarefas da Fase 0
   - Decisões técnicas pendentes
   - Próximas ações

6. **documents/README.md**
   - `{{PROJECT_NAME}}` - Nome formal
   - `{{DATE}}` - Data atual

7. **.env.example**
   - Descomente e ajuste variáveis relevantes para o projeto
   - Remova variáveis não aplicáveis
   - Adicione variáveis específicas necessárias

---

### 3. Definir Scopes de Commit

Baseado na arquitetura do projeto, defina scopes apropriados:

**Exemplos por tipo de projeto:**

| Tipo | Scopes Sugeridos |
|------|------------------|
| API REST | api, auth, db, models, routes, middleware, docs |
| Automação | collector, processor, storage, alerting, config |
| CLI Tool | cli, commands, config, utils, docs |
| Web App | frontend, backend, api, auth, components, pages |

---

### 4. Criar Estrutura de Diretórios

Se necessário, crie diretórios específicos em `src/`:

```bash
# Exemplo para projeto de automação
mkdir -p src/{collectors,processors,storage,alerting,utils}

# Exemplo para API REST
mkdir -p src/{api,models,routes,services,utils}
```

---

### 5. Validar Estrutura

Após preencher, valide:

- [ ] Todos os `{{PLACEHOLDER}}` foram substituídos
- [ ] Links entre documentos funcionam (usar `validate-docs-links`)
- [ ] Roadmap tem fases realistas com datas
- [ ] TODO.md reflete primeira fase (Fase 0)
- [ ] .env.example tem apenas variáveis relevantes
- [ ] Scopes de commit estão definidos
- [ ] Estrutura de `src/` faz sentido para o projeto

---

## Output Esperado

Arquivos preenchidos e prontos para desenvolvimento, mantendo:

- **Arquitetura Single Source of Truth** - CLAUDE.md → Projeto.md → rules/*.md
- **Padrões de qualidade Lass** - Code quality, testing, security
- **Integração com GSD patterns** - Fresh Context, Atomic Commits, Verify Steps

---

## Notas Importantes

1. **Não invente informações** - Se algo não está nos documentos de kick-off, use placeholder ou pergunte
2. **Mantenha consistência** - Use os mesmos termos em todos os documentos
3. **Seja específico** - Evite descrições genéricas como "sistema de gestão"
4. **Documente decisões** - Se tomar decisões durante o preenchimento, documente em Projeto.md

---

## Comando de Validação Final

Após preencher, execute:

```bash
# Verificar placeholders restantes
grep -r "{{" --include="*.md" . | grep -v ".claude/prompts"

# Validar links
# Use skill: validate-docs-links check
```

---

**Versão:** 1.0.0
**Template Lass:** v1.0.0
