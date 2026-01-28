# {{PROJECT_NAME}}

{{PROJECT_DESCRIPTION}}

## Status

| Fase | Status | Progresso |
|------|--------|-----------|
| Fase 0 - Planejamento | ⏳ Aguardando | 0% |
| Fase 1 - PoV | ⏳ Aguardando | 0% |
| Fase 2 - MVP | ⏳ Aguardando | 0% |
| Fase 3 - Hardening | ⏳ Aguardando | 0% |
| Fase 4 - Expansões | ⏳ Aguardando | 0% |

---

## Quick Start

### Pré-requisitos

- Python 3.11+
- pip ou uv

### Instalação

```bash
# Clone o repositório
git clone https://github.com/{{GITHUB_ORG}}/{{PROJECT_SLUG}}.git
cd {{PROJECT_SLUG}}

# Crie ambiente virtual
python -m venv .venv
source .venv/bin/activate  # Linux/Mac
# .venv\Scripts\activate   # Windows

# Instale dependências
pip install -r requirements.txt

# Configure variáveis de ambiente
cp .env.example .env
# Edite .env com suas credenciais
```

### Execução

```bash
# Modo desenvolvimento
python -m src.main

# Ou usando o comando principal
python src/main.py
```

---

## Estrutura do Projeto

```
{{PROJECT_SLUG}}/
├── .claude/                    # Configuração Claude Code
│   ├── CLAUDE.md               # Regras operacionais
│   ├── rules/                  # Regras path-targeted
│   └── skills/                 # Workflows automatizados
├── documents/                  # Documentação do projeto
│   ├── core/                   # Docs principais (Projeto.md, Roadmap.md, TODO.md)
│   ├── technical/              # Documentação técnica
│   └── strategy/               # Análises e decisões
├── src/                        # Código fonte
│   └── ...
├── tests/                      # Testes
│   ├── unit/
│   └── integration/
├── data/                       # Dados (não commitados)
├── .env.example                # Template de variáveis de ambiente
├── requirements.txt            # Dependências Python
└── README.md                   # Este arquivo
```

---

## Documentação

| Documento | Descrição |
|-----------|-----------|
| [Projeto.md](documents/core/Projeto.md) | Fonte de verdade - regras de negócio, arquitetura |
| [Roadmap.md](documents/core/Roadmap.md) | Fases, milestones, DoR/DoD |
| [TODO.md](documents/core/TODO.md) | Tracking granular de tarefas |

---

## Desenvolvimento

### Comandos Úteis

```bash
# Testes
pytest                          # Todos os testes
pytest --cov=src                # Com cobertura
pytest tests/unit/              # Apenas unitários

# Code Quality
black src/ tests/               # Formatação
isort src/ tests/               # Organização de imports
pylint src/                     # Linting
mypy src/                       # Type checking

# Pre-commit
pre-commit install              # Instalar hooks
pre-commit run --all-files      # Executar em todos os arquivos
```

### Skills Disponíveis (Claude Code)

| Skill | Uso |
|-------|-----|
| `validate-dor [milestone]` | Validar Definition of Ready |
| `validate-dod [milestone]` | Validar Definition of Done |
| `pre-commit-check` | Checklist antes de commit |
| `validate-testing` | Validar cobertura de testes |
| `organize-commits` | Organizar commits atômicos |
| `fresh-context` | Gerar contexto para handoff |

---

## Contribuição

1. Crie uma branch para sua feature (`git checkout -b feature/nome-feature`)
2. Faça commits atômicos seguindo Conventional Commits
3. Certifique-se que testes passam (`pytest`)
4. Abra um Pull Request

### Conventional Commits

```
feat(scope): adiciona nova funcionalidade
fix(scope): corrige bug
docs(scope): atualiza documentação
refactor(scope): refatora código
test(scope): adiciona/atualiza testes
chore(scope): tarefas de manutenção
```

**Scopes:** {{COMMIT_SCOPES}}

---

## Licença

{{LICENSE_TYPE}}

---

## Contato

- **Responsável:** {{RESPONSIBLE_NAME}}
- **E-mail:** {{CONTACT_EMAIL}}
- **Organização:** {{ORGANIZATION_NAME}}

---

**Última atualização:** {{DATE}}
