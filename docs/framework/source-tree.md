# Source Tree — Synkra AIOS

> Projeto: `agentes-ia` | Versão AIOS: 2.1.0 | Atualizado: 2026-02-18

---

## Raiz do Projeto

```
agentes-ia/
├── .aios-core/              # Framework AIOS — motor principal
├── .claude/                 # Configuração do Claude Code (regras, MCP)
├── .codex/                  # Configuração do Codex CLI (agentes, skills)
├── docs/                    # Documentação do projeto
│   ├── framework/           # Padrões, stack e estrutura (este diretório)
│   ├── stories/             # Stories de desenvolvimento
│   ├── prd/                 # Product Requirements Documents (sharded)
│   ├── architecture/        # Documentação de arquitetura (sharded)
│   └── qa/                  # Relatórios de QA e CodeRabbit
├── .env                     # Variáveis de ambiente (NÃO commitar)
├── .env.example             # Template de variáveis de ambiente
├── .gitignore               # Arquivos ignorados pelo git
└── AGENTS.md                # Instruções do projeto para Codex CLI
```

---

## `.aios-core/` — Framework Principal

```
.aios-core/
├── cli/                     # Entrypoints e comandos do CLI
│   ├── commands/            # Implementação de cada comando
│   ├── utils/               # Utilitários do CLI
│   └── index.js             # Entrypoint principal do CLI
│
├── core/                    # Módulos do motor interno
│   ├── code-intel/          # Análise e inteligência de código
│   ├── config/              # Carregamento e gerenciamento de config
│   ├── elicitation/         # Interação e coleta de inputs do usuário
│   ├── events/              # Sistema de eventos internos
│   ├── execution/           # Execução de tasks e workflows
│   ├── health-check/        # Verificação de saúde do sistema
│   ├── ideation/            # Geração de ideias e sugestões
│   ├── ids/                 # Incremental Development System
│   ├── manifest/            # Gerenciamento de manifests
│   ├── mcp/                 # Integração com MCP servers
│   ├── memory/              # Memória persistente de agentes
│   ├── migration/           # Migrações de versão do framework
│   ├── orchestration/       # Orquestração de agentes e workflows
│   ├── permissions/         # Sistema de permissões por agente
│   ├── quality-gates/       # Gates de qualidade automáticos
│   ├── registry/            # Registry de entidades e artefatos (IDS)
│   ├── session/             # Gerenciamento de sessões de agente
│   ├── synapse/             # Comunicação inter-agente
│   ├── ui/                  # Interface de observabilidade (CLI)
│   └── utils/               # Utilitários compartilhados
│       ├── output-formatter.js
│       ├── security-utils.js
│       └── yaml-validator.js
│
├── development/             # Artefatos de desenvolvimento (agentes usam estes)
│   ├── agents/              # Definições de personas de agentes (.md)
│   │   ├── dev.md           # @dev — Full Stack Developer (Dex)
│   │   ├── qa.md            # @qa — QA Engineer (Quinn)
│   │   ├── architect.md     # @architect — Arquiteta (Aria)
│   │   ├── pm.md            # @pm — Product Manager (Morgan)
│   │   ├── po.md            # @po — Product Owner (Pax)
│   │   ├── sm.md            # @sm — Scrum Master (River)
│   │   ├── analyst.md       # @analyst — Analista
│   │   ├── devops.md        # @devops — DevOps (Gage)
│   │   ├── data-engineer.md # @data-engineer — Engenheiro de Dados (Dara)
│   │   ├── ux-design-expert.md
│   │   ├── squad-creator.md
│   │   └── aios-master.md   # @aios-master — Governança do framework
│   ├── agent-teams/         # Configurações de times de agentes
│   ├── checklists/          # Checklists de validação
│   │   ├── story-dod-checklist.md
│   │   └── self-critique-checklist.md
│   ├── data/                # Dados de referência para desenvolvimento
│   ├── scripts/             # Scripts executáveis por agentes
│   ├── tasks/               # Workflows de tasks executáveis (.md)
│   │   ├── dev-develop-story.md
│   │   ├── create-next-story.md
│   │   ├── validate-next-story.md
│   │   ├── apply-qa-fixes.md
│   │   ├── build-autonomous.md
│   │   └── ... (outros workflows)
│   ├── templates/           # Templates de documentos e código
│   └── workflows/           # Definições de workflows multi-step
│
├── data/                    # Dados persistentes do framework
├── docs/                    # Documentação interna do framework
│   ├── standards/           # Padrões internos do AIOS
│   ├── component-creation-guide.md
│   ├── session-update-pattern.md
│   └── troubleshooting-guide.md
│
├── elicitation/             # Módulos de elicitação interativa
├── infrastructure/          # Contratos, integrações e schemas
│   ├── contracts/
│   ├── integrations/
│   ├── schemas/
│   ├── scripts/
│   ├── templates/
│   └── tests/
│
├── manifests/               # Manifests de instalação e configuração
├── monitor/                 # Dashboards e monitoramento
├── presets/                 # Configurações pré-definidas
├── product/                 # Artefatos de produto
├── schemas/                 # JSON Schemas de validação
├── scripts/                 # Scripts de manutenção do framework
│   ├── diagnostics/         # Health dashboard
│   ├── update-aios.sh       # Atualização do framework
│   └── session-context-loader.js
│
├── workflow-intelligence/   # WIS — sistema de análise de workflows
├── constitution.md          # Constituição do AIOS (lei máxima)
├── core-config.yaml         # Configuração central do projeto
├── install-manifest.yaml    # Manifesto de instalação
├── index.js                 # Entrypoint CommonJS
├── index.esm.js             # Entrypoint ESM
└── package.json             # Dependências do framework
```

---

## `docs/` — Documentação do Projeto

```
docs/
├── framework/               # ← Este diretório
│   ├── coding-standards.md  # Padrões de código
│   ├── tech-stack.md        # Stack tecnológico
│   └── source-tree.md       # Este arquivo
│
├── stories/                 # Stories de desenvolvimento
│   └── {epicNum}.{storyNum}.story.md
│
├── prd/                     # PRD sharded
│   └── epic-{n}*.md
│
├── architecture/            # Arquitetura sharded
│   ├── padroes-de-codigo.md
│   ├── pilha-tecnologica.md
│   └── arvore-de-origem.md
│
└── qa/                      # Qualidade
    └── coderabbit-reports/  # Relatórios do CodeRabbit CLI
```

---

## `.claude/` — Configuração Claude Code

```
.claude/
├── CLAUDE.md                # Instruções principais para o Claude Code
└── rules/                   # Regras detalhadas
    ├── agent-authority.md   # Matriz de autoridades dos agentes
    ├── story-lifecycle.md   # Ciclo de vida das stories
    ├── workflow-execution.md # Regras de execução de workflows
    ├── coderabbit-integration.md
    ├── ids-principles.md
    └── mcp-usage.md
```

---

## `.codex/` — Configuração Codex CLI

```
.codex/
└── agents/                  # Atalhos de agentes para o Codex CLI
    └── dev.md               # Alias local para .aios-core/development/agents/dev.md
```

---

## Convenções de Localização

| O que procurar | Onde encontrar |
|----------------|---------------|
| Persona de um agente | `.aios-core/development/agents/{id}.md` |
| Workflow de uma task | `.aios-core/development/tasks/{task}.md` |
| Configuração do projeto | `.aios-core/core-config.yaml` |
| Stories ativas | `docs/stories/` |
| PRD do produto | `docs/prd/` |
| Arquitetura do sistema | `docs/architecture/` |
| Regras dos agentes | `.claude/rules/` |
| Scripts de manutenção | `.aios-core/scripts/` |
| Schemas de validação | `.aios-core/schemas/` |
