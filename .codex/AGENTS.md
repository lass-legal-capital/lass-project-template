# Claude Code - Regras do Projeto {{PROJECT_NAME}}

Este arquivo contém as **regras operacionais sempre ativas** para o projeto {{PROJECT_NAME}}.

> **Arquitetura Single Source of Truth:**
> - Regras operacionais → Este arquivo
> - Contexto de negócio e arquitetura → @documents/core/Projeto.md
> - Detalhes técnicos → @rules/*.md (path-targeted)
> - Workflows → @skills/*/SKILL.md

---

## 1. Acompanhamento de Roadmap e TODO

### Responsabilidade Contínua

**Antes de começar qualquer tarefa:**
- Consultar @documents/core/Roadmap.md para verificar o milestone atual
- **Invocar skill `validate-dor [milestone-id]`** para validar pré-requisitos
- Se DoR não estiver completo, PARE e trabalhe nas dependências primeiro
- Consultar @documents/core/TODO.md para tarefas granulares

**Durante o desenvolvimento:**
- Consultar periodicamente o **DoD (Definition of Done)** no Roadmap
- **Invocar skill `validate-testing`** para validar cobertura de testes
- Marcar checkboxes no TODO.md conforme avança
- Usar formato `- verify:` nas tarefas para verificações programáticas

**Antes de commit:**
- **Invocar skill `pre-commit-check`** (inclui code quality, testing, security)
- **Invocar skill `organize-commits`** se múltiplas mudanças pendentes

**Ao completar uma tarefa:**
- **Invocar skill `validate-dod [milestone-id]`** para validar conclusão
  - Executa `verify:` steps do TODO.md automaticamente
  - Gera Verification Report com PASS/FAIL
- **Invocar skill `update-docs task [milestone-id]`** para salvar implementation plan
- Atualizar checkboxes no TODO.md
- Documentar evidências (testes, screenshots, métricas)

**Ao completar uma fase:**
- **Invocar skill `validate-docs-links check`** para validar links
- **Invocar skill `audit-rules full`** para auditar regras
- **Invocar skill `audit-architecture`** para verificar redundâncias

### Regra de Ouro

**"Se DoR não está completo, NÃO comece. Se DoD não está 100% atendido, NÃO está done."**

---

## 2. Context Engineering e Uso de Subagentes

### Otimização de Contexto

Você tem 200,000 tokens de contexto. Para maximizar performance:

**Trigger de Fresh Context (>150k tokens):**
- Quando sessão ultrapassar **150k tokens**, invocar skill `fresh-context`
- Gera CONTEXT.md self-contained para handoff limpo
- Previne "context rot" que degrada qualidade

**Reduza Noise no Contexto:**
- **Leia apenas docs relevantes** para a tarefa atual
- **Use `documents/README.md` como índice** - não leia todos os docs de uma vez
- **Consulte SOPs específicos** ao invés de explorar todo o codebase

### Salvaguardas de Documentação (IA)

- `documents/core/Projeto.md` é a **fonte de verdade** para decisões de negócio e arquitetura.
- `documents/technical/` e `documents/strategy/` são **suplementares**; qualquer decisão final deve ser refletida em `Projeto.md`.
- Se houver conflito, **`Projeto.md` prevalece**. Adicione backlinks quando usar docs suplementares.

**Use Subagentes Estrategicamente (Task Tool):**
- Pesquisas exploratórias extensas
- Análise de múltiplos arquivos para decisões de design
- Investigação de bugs complexos
- Comparação de abordagens alternativas

### Regra "Docs First"

**Antes de qualquer grep, glob ou leitura extensiva:**
1. Consulte `documents/README.md` primeiro
2. Se docs estão atualizados → Use diretamente
3. Se docs desatualizados → Use Task tool (subagente) para pesquisa

---

## 3. Princípios de Desenvolvimento

### Chunks Gerenciáveis
- **Máximo 100 linhas** por implementação
- **Quebrar** funcionalidades complexas em partes menores

### Explicação Contínua
- **Sempre explicar** o "porquê" das decisões técnicas
- **Documentar** trade-offs e alternativas consideradas

### Prova de Correção
- **Validar** implementação contra requisitos
- **Testar** com dados reais quando possível

---

## 4. Segurança - Regras Essenciais

### Regra de Ouro

**NUNCA commitar dados sensíveis no repositório.**

### Checklist Obrigatório

- [ ] Nenhum secret hardcoded no código
- [ ] Todas credenciais via environment variables
- [ ] .env no .gitignore
- [ ] .env.example documentado
- [ ] Error handling não expõe credenciais

> **Detalhes técnicos:** @rules/security-best-practices.md

---

## 5. Commit Strategy

### Regra de Ouro

**"1 task = 1 commit. NUNCA use git add . ou git add -A"**

Commits atômicos permitem:
- Git bisect eficiente (encontrar bugs)
- Reverts cirúrgicos (desfazer apenas uma mudança)
- Code review focado (revisar por contexto)

### Protocolo Atomic Commits

1. **NUNCA** usar `git add .` ou `git add -A`
2. **SEMPRE** stage arquivos individualmente por task
3. **MÁXIMO** 100 linhas por commit
4. **FORMATO:** `{type}({milestone}-{task}): {description}`
5. **RASTREAR** hashes em TODO.md seção "Commits do Milestone"

### Triggers para Commits

1. Após completar DoR de milestone → `chore(milestone): prepara ambiente para M1.X`
2. Após implementar task (≤100 linhas) → `feat(M1.X-NN): implementa X`
3. Após testes passarem → `test(M1.X-NN): adiciona testes para X`
4. Após completar DoD → `docs(milestone): finaliza M1.X`

### Conventional Commits

**Formato:** `<type>(<scope>): <subject>`

**Types:** feat, fix, docs, refactor, test, chore, perf, style, ci, build

**Scopes:** {{COMMIT_SCOPES}}

<!--
Preencher com os scopes específicos do projeto.
Exemplo para monitor-fundos: collector, processor, storage, alerting, config, docs, milestone
Exemplo para API: api, auth, db, models, routes, middleware, docs
-->

### Política de Atribuição

1. **NUNCA** mencionar assistentes de IA (Claude, Cursor AI agents, etc.)
2. **NUNCA** incluir co-autoria com IA
3. **SEMPRE** apresentar como trabalho do desenvolvedor
4. **SEMPRE** usar conventional commits padrão

---

## 6. Referências

### Contexto do Projeto

Para regras de negócio, arquitetura e decisões técnicas:
@documents/core/Projeto.md

### Detalhes Técnicos (Path-Targeted)

Os seguintes arquivos são carregados automaticamente conforme contexto:
- @rules/code-quality-standards.md → Quando editando src/**/*
- @rules/security-best-practices.md → Quando editando src/**/*
- @rules/testing-requirements.md → Quando editando tests/**/*

### Timeline e Gestão

- @documents/core/Roadmap.md → Fases, milestones, DoR/DoD
- @documents/core/TODO.md → Tarefas granulares

---

**Versão:** 1.0.0
**Última atualização:** {{DATE}}
**Autor:** {{AUTHOR_NAME}}

<!--
INSTRUÇÕES DE PREENCHIMENTO:

1. Substitua {{PROJECT_NAME}} pelo nome do projeto
2. Substitua {{COMMIT_SCOPES}} pelos scopes específicos do projeto
3. Substitua {{DATE}} pela data atual
4. Substitua {{AUTHOR_NAME}} pelo responsável
5. Remova todos os comentários <!-- --> após preencher
-->
