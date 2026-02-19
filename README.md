# Synkra AIOS — AI-Orchestrated System

> Sistema de desenvolvimento orientado por agentes de IA, onde cada papel do processo de software é executado por um agente especializado.

---

## O que é o AIOS

O **Synkra AIOS** é um meta-framework que orquestra agentes de IA para conduzir workflows completos de desenvolvimento de software — da criação de histórias até o deploy. Cada agente tem autoridade exclusiva sobre seu domínio, princípios inegociáveis e comandos próprios.

A filosofia central é **CLI First**: toda inteligência, execução e automação vivem no CLI. Dashboards apenas observam, nunca controlam.

---

## Agentes

| Agente | Nome | Papel |
|--------|------|-------|
| `@dev` | Dex | Implementação de código e testes |
| `@qa` | Quinn | Revisão de qualidade e gates |
| `@architect` | Aria | Decisões de arquitetura e tecnologia |
| `@pm` | Morgan | Orquestração de épicos e requisitos |
| `@po` | Pax | Validação e priorização de histórias |
| `@sm` | River | Criação de histórias e facilitação |
| `@analyst` | — | Pesquisa e análise |
| `@devops` | Gage | Push, PRs, releases e CI/CD |
| `@data-engineer` | Dara | Schema, migrações e queries |
| `@ux-design-expert` | — | Design de interface |
| `@aios-master` | — | Governança do framework |

### Ativação

```bash
# Claude Code
@dev
@devops

# Codex CLI
/dev
/devops
```

---

## Workflow Principal

```
@sm *draft       →  cria história
@po *validate    →  valida (checklist 10 pontos)
@dev *develop    →  implementa + testes
@qa *qa-gate     →  revisão de qualidade
@devops *push    →  push + PR
```

---

## Estrutura do Projeto

```
agentes-ia/
├── .aios-core/          # Motor do framework (agentes, tasks, scripts)
├── .claude/             # Configuração do Claude Code
├── .codex/              # Configuração do Codex CLI
├── docs/
│   ├── framework/       # Padrões, tech stack e source tree
│   ├── stories/         # Histórias de desenvolvimento
│   ├── prd/             # Product Requirements Documents
│   └── architecture/    # Documentação de arquitetura
├── .env.example         # Template de variáveis de ambiente
└── AGENTS.md            # Instruções para o Codex CLI
```

---

## Requisitos

- **Node.js** ≥ 18.0.0
- **npm** ≥ 9.0.0
- **GitHub CLI** (`gh`) para operações remotas
- **Claude Code** ou **Codex CLI** como IDE

---

## Setup

```bash
# 1. Clonar o repositório
git clone https://github.com/leoferrazbrasil/agentes-ia.git
cd agentes-ia

# 2. Instalar dependências do framework
cd .aios-core && npm install && cd ..

# 3. Configurar variáveis de ambiente
cp .env.example .env
# editar .env com suas chaves de API

# 4. Verificar estrutura
npm run validate:structure
```

---

## Comandos Comuns

```bash
npm run lint              # Verificar estilo de código
npm run typecheck         # Verificação de tipos
npm test                  # Executar testes
npm run validate:agents   # Validar definições de agentes
npm run sync:ide          # Sincronizar configuração das IDEs
```

---

## Princípios (Constitution)

1. **CLI First** — toda funcionalidade nasce no CLI, nunca na UI
2. **Agent Authority** — cada agente tem autoridades exclusivas e invioláveis
3. **Story-Driven Development** — nenhum código sem história associada
4. **No Invention** — specs derivam dos requisitos, nunca inventam

---

## Versão

| Componente | Versão |
|-----------|--------|
| AIOS Framework | 2.1.0 |
| `@aios-fullstack/core` | 4.31.1 |
| Node.js (mínimo) | 18.0.0 |

---

## Licença

MIT — Synkra AIOS Team
