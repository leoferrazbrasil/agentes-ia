# Tech Stack — Synkra AIOS

> Projeto: `agentes-ia` | Versão AIOS: 2.1.0 | Atualizado: 2026-02-18

---

## Runtime & Linguagem

| Tecnologia | Versão | Papel |
|------------|--------|-------|
| **Node.js** | ≥ 18.0.0 | Runtime principal |
| **npm** | ≥ 9.0.0 | Gerenciador de pacotes |
| **JavaScript** | ES2022+ | Linguagem principal |
| **TypeScript** | Opcional | Tipagem em módulos marcados |

---

## Core Framework

| Pacote | Versão | Uso |
|--------|--------|-----|
| `@aios-fullstack/core` | 4.31.1 | Motor do meta-agente e geração de componentes |
| `commander` | ^12.1.0 | Parsing de CLI e subcomandos |
| `inquirer` | ^8.2.6 | Prompts interativos no CLI |
| `js-yaml` | ^4.1.0 | Parsing e serialização de arquivos YAML |
| `fs-extra` | ^11.3.0 | Operações de sistema de arquivos estendidas |
| `glob` | ^10.4.4 | Matching de padrões de arquivos |
| `execa` | ^5.1.1 | Execução de subprocessos |
| `chalk` | ^4.1.2 | Colorização de output no terminal |
| `diff` | ^5.2.0 | Comparação de texto (diffs) |
| `validator` | ^13.15.15 | Sanitização e validação de strings |
| `highlight.js` | ^11.9.0 | Syntax highlighting no terminal |

---

## Pacotes Peer (Opcionais)

| Pacote | Papel |
|--------|-------|
| `@aios-fullstack/memory` | Memória persistente de agentes |
| `@aios-fullstack/security` | Camada de segurança e permissões |
| `@aios-fullstack/performance` | Métricas e otimização de performance |
| `@aios-fullstack/telemetry` | Observabilidade e rastreamento |

---

## Integrações de LLM

| Provider | Variável de Ambiente | Uso |
|----------|---------------------|-----|
| **Anthropic (Claude)** | `ANTHROPIC_API_KEY` | LLM principal — Claude Sonnet/Opus |
| **OpenRouter** | `OPENROUTER_API_KEY` | Roteamento multi-modelo |
| **OpenAI** | `OPENAI_API_KEY` | Modelos GPT quando necessário |
| **DeepSeek** | `DEEPSEEK_API_KEY` | Alternativa econômica |

---

## Banco de Dados & Backend

| Tecnologia | Variáveis | Uso |
|------------|-----------|-----|
| **Supabase** | `SUPABASE_URL`, `SUPABASE_ANON_KEY`, `SUPABASE_SERVICE_ROLE_KEY` | DB PostgreSQL, Auth, Storage |

---

## Ferramentas de Pesquisa (via MCP/Docker)

| Ferramenta | Variável | Uso |
|------------|----------|-----|
| **EXA** | `EXA_API_KEY` | Busca web para agentes |
| **Context7** | `CONTEXT7_API_KEY` | Documentação de bibliotecas |

---

## Automação & Workflows

| Tecnologia | Variáveis | Uso |
|------------|-----------|-----|
| **n8n** | `N8N_API_KEY`, `N8N_WEBHOOK_URL` | Orquestração de workflows |

---

## DevOps & Deploy

| Tecnologia | Variável | Uso |
|------------|----------|-----|
| **GitHub CLI** | `GITHUB_TOKEN` | PRs, Issues, API GitHub |
| **Railway** | `RAILWAY_TOKEN` | Deploy de backend |
| **Vercel** | `VERCEL_TOKEN` | Deploy de frontend/edge |

---

## Monitoramento

| Tecnologia | Variável | Uso |
|------------|----------|-----|
| **Sentry** | `SENTRY_DSN` | Rastreamento de erros em produção |

---

## Ferramentas de Qualidade

| Ferramenta | Comando | Uso |
|------------|---------|-----|
| **ESLint** | `npm run lint` | Análise estática de código |
| **TypeScript** | `npm run typecheck` | Verificação de tipos |
| **Jest** | `npm test` | Testes unitários e integração |
| **CodeRabbit CLI** | `~/.local/bin/coderabbit` | Revisão de código pré-commit (via WSL) |

---

## IDEs Suportados

| IDE | Status |
|-----|--------|
| **Claude Code** | ✅ Ativo |
| **Codex CLI** | ✅ Ativo |
| VS Code | Desabilitado |
| Cursor | Desabilitado |
| GitHub Copilot | Desabilitado |

---

## Configuração de Ambiente

```bash
# Copiar template e preencher credenciais
cp .env.example .env

# Instalar dependências do core
cd .aios-core && npm install

# Verificar estrutura do projeto
npm run validate:structure

# Validar definição de agentes
npm run validate:agents
```

---

## Decisões de Arquitetura

- **CLI First** — toda funcionalidade nasce no CLI, nunca na UI
- **CommonJS** como padrão no core para compatibilidade com Node.js ≥ 18
- **YAML** como formato de configuração (legível por humanos e agentes)
- **Sem framework web obrigatório** — o projeto é focado em CLI e automação
- **Docker MCP Toolkit** para MCPs que necessitam isolamento (EXA, Context7, Apify)
