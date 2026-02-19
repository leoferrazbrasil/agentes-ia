# Coding Standards — Synkra AIOS

> Projeto: `agentes-ia` | Versão AIOS: 2.1.0 | Runtime: Node.js ≥ 18

---

## Princípio Fundamental

**CLI First → Observability → UI**
Toda funcionalidade DEVE funcionar 100% via CLI antes de qualquer interface visual.

---

## Linguagem & Runtime

- **Linguagem:** JavaScript (ES2022+) / TypeScript onde explícito
- **Módulos:** CommonJS (`require/module.exports`) no core; ESM (`import/export`) em módulos marcados com `"module"` no `package.json`
- **Node.js:** ≥ 18.0.0 obrigatório
- **npm:** ≥ 9.0.0

---

## Estrutura de Arquivos

- Um conceito por arquivo — não misturar responsabilidades
- Nomes em `kebab-case` para arquivos e pastas: `user-service.js`, `auth-utils.js`
- Nomes em `PascalCase` para classes: `class SessionManager {}`
- Nomes em `camelCase` para funções e variáveis: `getUserById()`, `const sessionData`
- Constantes globais em `UPPER_SNAKE_CASE`: `const MAX_RETRIES = 3`

---

## Qualidade de Código

### Funções
- Máximo **50 linhas** por função — extrair lógica em subfunções se necessário
- Uma responsabilidade por função (Single Responsibility)
- Nomes verbais e descritivos: `loadAgentConfig()`, `validateStoryDraft()`

### Comentários
- Código auto-documentado tem preferência sobre comentários
- Comentários apenas onde a lógica **não é óbvia**
- JSDoc obrigatório para funções públicas exportadas:

```js
/**
 * Carrega a configuração do agente a partir do arquivo YAML.
 * @param {string} agentId - ID do agente (ex.: 'dev', 'qa')
 * @returns {Promise<object>} Configuração do agente
 */
async function loadAgentConfig(agentId) { ... }
```

### Error Handling
Tratar erros em todas as operações de I/O, rede e parsing:

```js
try {
  const config = await loadConfig(path);
} catch (error) {
  console.error(`Erro ao carregar config de ${path}:`, error.message);
  throw new Error(`Falha ao inicializar agente: ${error.message}`);
}
```

- **Nunca** engolir erros silenciosamente
- Mensagens de erro em português com contexto suficiente para diagnóstico
- Propagar erros com contexto adicional (`throw new Error(...)`)

---

## Padrões Assíncronos

- Usar `async/await` — evitar `.then().catch()` encadeado
- Operações independentes em paralelo com `Promise.all()`:

```js
// Correto
const [config, session, permissions] = await Promise.all([
  loadConfig(),
  loadSession(),
  loadPermissions()
]);

// Evitar
const config = await loadConfig();
const session = await loadSession();
```

---

## Validação

- Validar inputs **apenas nas fronteiras do sistema** (CLI args, APIs externas, arquivos do usuário)
- Não validar dados internos já garantidos pelo código
- Usar a lib `validator` para sanitização de strings externas

---

## Imports & Dependências

- Imports no topo do arquivo, agrupados:
  1. Módulos Node.js nativos (`fs`, `path`, `os`)
  2. Dependências npm externas (`chalk`, `commander`, etc.)
  3. Módulos internos do projeto (caminhos relativos)
- Sem `require()` dinâmicos dentro de funções, exceto quando necessário para lazy-loading

```js
// Ordem correta
const path = require('path');
const fs = require('fs-extra');

const chalk = require('chalk');
const yaml = require('js-yaml');

const { loadConfig } = require('../core/config');
```

---

## Testes

- Testes unitários em `tests/unit/` com cobertura dos casos principais e edge cases
- Testes de integração em `tests/integration/`
- Runner: **Jest** (`npm test`)
- Nomenclatura: `describe('nomeDaFunção', () => { it('deve fazer X quando Y', ...) })`
- **Obrigatório** para toda funcionalidade nova antes de marcar task como `[x]`

---

## Commits & Git

Seguir Conventional Commits:

```
feat: adiciona suporte a múltiplos agentes [Story X.Y.Z]
fix: corrige parsing de YAML com caracteres especiais
docs: atualiza guia de instalação
chore: atualiza dependências de segurança
refactor: extrai lógica de sessão para SessionManager
test: adiciona testes para loadAgentConfig
```

- Commits **atômicos e focados** — um propósito por commit
- Referenciar story ID quando aplicável: `[Story 1.2.3]`
- `git push` é **exclusivo do @devops** — nunca executar diretamente

---

## Proibições

- ❌ `console.log` em código de produção (usar logger estruturado)
- ❌ Credenciais ou tokens hardcoded — usar variáveis de ambiente (`.env`)
- ❌ `eval()` ou `Function()` dinâmico
- ❌ `git push` por qualquer agente exceto @devops
- ❌ Criar UI antes de CLI funcional
- ❌ Implementar sem story associada

---

## Linting & Verificação

```bash
npm run lint        # ESLint — deve passar com 0 erros
npm run typecheck   # TypeScript check — quando aplicável
npm test            # Jest — todos os testes devem passar
```

Todos os três devem passar **antes** de marcar qualquer task como concluída.
