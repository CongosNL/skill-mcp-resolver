# Project Tooling Analyzer - Design Document

**Datum:** 2026-01-15
**Status:** Draft
**Skill naam:** `project-tooling-analyzer`

---

## 1. Overzicht

### Kernfunctie

Analyseert een projectmap en adviseert welke AI assistant skills en MCP servers nodig zijn voor effectief onderhoud en doorontwikkeling.

### Gebruiksmodi

| Modus | Wanneer |
|-------|---------|
| **Initieel** | Bij het starten met een nieuw/onbekend project |
| **Periodiek** | Wanneer het project evolueert en nieuwe tooling nodig kan zijn |

### Workflow

```
┌─────────────────────────────────────────────────────────────────────┐
│                         ANALYSE FLOW                                 │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  1. INVENTARISATIE HUIDIGE SETUP                                    │
│     └── Welke skills/MCPs zijn al geïnstalleerd? (LLM-onafhankelijk)│
│                                                                     │
│  2. PROJECT ANALYSE                                                 │
│     └── Detecteer tech stack, patterns, dependencies                │
│                                                                     │
│  3. MATCH & GAP ANALYSE                                             │
│     ├── Wat heb je al dat relevant is?                              │
│     ├── Wat mis je nog?                                             │
│     └── Wat heb je dat niet relevant is? (optioneel signaleren)     │
│                                                                     │
│  4. ZOEK OPLOSSINGEN (voor gaps)                                    │
│     └── Marketplaces, registries, package managers                  │
│                                                                     │
│  5. OUTPUT                                                          │
│     ├── Bestaande relevante tools (al geïnstalleerd)                │
│     ├── Aanbevolen nieuwe tools + installatie-hulp                  │
│     └── Scaffold voorstel als niets bestaat                         │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Triggers

- "Welke skills heb ik nodig voor dit project?"
- "Analyseer de tooling requirements"
- "Wat voor MCPs zou ik kunnen gebruiken?"
- Bij het openen van een nieuwe codebase

---

## 2. Detectie-logica

### Stap 1: Inventarisatie huidige AI assistant setup (LLM-onafhankelijk)

| Assistant | Locaties | Wat wordt gedetecteerd |
|-----------|----------|------------------------|
| **Claude Code** | `~/.claude/skills/`, `~/.claude/settings.json`, `.mcp.json` | Skills, MCP servers |
| **OpenAI/Codex** | `~/.codex/skills/`, `codex.md`, `.mcp.json` | Skills, agents |
| **ChatGPT** | GPT configuraties | Custom GPTs, actions |
| **Cursor** | `~/.cursor/`, `.cursorrules` | Extensions, rules, MCP config |
| **Windsurf** | `~/.windsurf/`, `.windsurfrules` | Rules, configuraties |
| **Continue.dev** | `~/.continue/config.json` | Context providers, slash commands |
| **Copilot** | `.github/copilot-instructions.md` | Custom instructions |
| **Cline** | Cline config locaties | Tools, configs |
| **Aider** | Aider config locaties | Conventions, configs |
| **Generiek** | `.mcp.json`, `mcp.json` | MCP servers (standaard) |

**Auto-detectie actieve assistant:**

1. Check welke assistant momenteel actief is (environment/process)
2. Prioriteer die assistant's configuratie
3. Toon ook cross-compatible opties (MCPs werken vaak cross-platform)

### Stap 2: Project tech stack detectie

| Bestand/Pattern | Detecteert |
|-----------------|------------|
| `package.json` | Node.js, frameworks (React, Next, Vue), dependencies |
| `composer.json` | PHP, Laravel, Symfony |
| `requirements.txt` / `pyproject.toml` | Python, Django, FastAPI, ML libs |
| `Cargo.toml` | Rust |
| `go.mod` | Go |
| `Gemfile` | Ruby, Rails |
| `*.csproj` / `*.sln` | .NET, C# |
| `docker-compose.yml` | Services (postgres, redis, elasticsearch) |
| `.github/workflows/*` | CI/CD patterns |
| `prisma/schema.prisma` | Prisma ORM |
| `supabase/`, `firebase.json` | BaaS platforms |
| `shopify.theme.toml` | Shopify development |

### Stap 3: Mapping naar skill/MCP categorieën

```
Tech Stack Detection → Categorie → Mogelijke Tools

PHP + Laravel       → php-dev        → moai-lang-php skill, laravel-boost MCP
Shopify config      → shopify        → shopify skill
React + TypeScript  → frontend       → frontend-design skill
PostgreSQL          → database       → postgres MCP
GitHub workflows    → git/ci         → github MCP
Python + FastAPI    → python-api     → python skill, fastapi MCP
```

---

## 3. Zoek-logica externe bronnen

### MCP Registries & Directories

| Bron | URL | Bijzonderheid |
|------|-----|---------------|
| **Official MCP Registry** | registry.modelcontextprotocol.io | Officieel, API beschikbaar |
| **GitHub MCP Registry** | github.com/mcp | Geïntegreerd met repos |
| **Docker MCP Catalog** | docs.docker.com/ai/mcp-catalog | Verified Docker images |
| **MCP.SO** | mcp.so | Call ranking, usage metrics |
| **MCPMarket** | mcpmarket.com | Marketplace |
| **Glama MCP** | glama.ai/mcp/servers | Curated directory |
| **Awesome MCP Servers** | GitHub | Community curated |

### Skills Marketplaces (cross-LLM)

| Bron | URL | Omvang | Compatibiliteit |
|------|-----|--------|-----------------|
| **SkillsMP** | skillsmp.com | 63,000+ skills | Claude, Codex, ChatGPT |
| **SkillzWave** | skillzwave.ai | 44,000+ skills | Claude, Codex, Cursor, Gemini |
| **Agent Skills CLI** | agentskills.in | 50,000+ skills | Claude, Codex, Copilot, Cursor |
| **Claude Plugins** | claude-plugins.dev | - | Claude specifiek |
| **n-skills** | GitHub | Curated | Multi-platform |

### Cursor-specifieke bronnen

| Bron | URL |
|------|-----|
| **Cursor Directory** | cursor.directory |

### Package Managers

| Manager | Zoektermen |
|---------|------------|
| **npm** | `mcp-server-*`, `@modelcontextprotocol/*` |
| **PyPI** | `mcp-server-*`, `mcp-*` |

### Zoekstrategie per technologie

```
Gedetecteerd: Laravel + PostgreSQL + Stripe

Zoekqueries per platform:
├── MCP (universeel):
│   ├── "mcp server laravel/php"
│   ├── "mcp server postgres"
│   └── "mcp server stripe"
│
├── Claude:
│   └── "claude skill php", "claude skill laravel"
│
├── OpenAI/Codex:
│   ├── "codex skill php/laravel"
│   └── GPT Store: "Laravel developer"
│
├── Cursor:
│   └── cursor.directory → php, laravel rules
│
└── Continue/Copilot/Cline/Aider:
    └── "[assistant] [tech] config/rules"
```

### Kwaliteitsevaluatie criteria

| Criterium | Gewicht | Hoe meten |
|-----------|---------|-----------|
| **GitHub stars** | 20% | >100 = goed, >500 = excellent |
| **Recent activity** | 25% | Laatste commit <3 maanden |
| **Documentatie** | 20% | README completeness, examples |
| **Issues/maintenance** | 15% | Open issues ratio, response time |
| **Downloads** | 10% | npm/PyPI weekly downloads |
| **Officieel/gecureerd** | 10% | In awesome-list of official registry |

### Kwaliteitsclassificatie

| Score | Label | Criteria |
|-------|-------|----------|
| ⭐⭐⭐ | Aanbevolen | >75%, actief maintained, goede docs |
| ⭐⭐ | Bruikbaar | 50-75%, werkt maar minder actief |
| ⭐ | Experimenteel | <50%, kan werken maar risico's |
| ❌ | Afraden | Abandoned, broken, security issues |

---

## 4. Output & Advies

### Output structuur

```
┌─────────────────────────────────────────────────────────────────────┐
│           PROJECT TOOLING ANALYSE: [project-naam]                   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  📊 GEDETECTEERDE STACK                                             │
│  ───────────────────────                                            │
│  • Laravel 11 + PHP 8.3                                             │
│  • PostgreSQL + Redis                                               │
│  • Stripe integratie                                                │
│  • GitHub Actions CI/CD                                             │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ✅ REEDS BESCHIKBAAR (geïnstalleerd)                               │
│  ────────────────────────────────────                               │
│  • moai-lang-php skill        → PHP/Laravel development             │
│  • github MCP                 → GitHub integratie                   │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  🔍 AANBEVOLEN TOEVOEGINGEN                                         │
│  ──────────────────────────                                         │
│                                                                     │
│  1. postgres MCP server                              ⭐⭐⭐           │
│     Bron: mcp.so/servers/postgres                                   │
│     Compatibel: Claude, Cursor, Codex, Continue                     │
│     Installatie: npx @modelcontextprotocol/server-postgres          │
│     → Direct database queries vanuit je assistant                   │
│                                                                     │
│  2. stripe MCP server                                ⭐⭐            │
│     Bron: github.com/stripe/mcp-server                              │
│     Compatibel: Claude, Cursor                                      │
│     Installatie: npm install @stripe/mcp-server                     │
│     → Stripe API documentatie en testing                            │
│                                                                     │
│  3. redis MCP server                                 ⭐⭐⭐           │
│     Bron: mcpmarket.com/redis                                       │
│     Compatibel: Alle MCP clients                                    │
│     Installatie: npx mcp-server-redis                               │
│     → Cache management en debugging                                 │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ⚠️  GAPS - GEEN KWALITATIEVE TOOL GEVONDEN                         │
│  ──────────────────────────────────────────                         │
│                                                                     │
│  • Laravel Horizon monitoring                                       │
│    Geen bestaande MCP/skill gevonden (beste match: ⭐ abandoned)    │
│    → Scaffold beschikbaar: /scaffold horizon-mcp                    │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Interactieve acties na output

| Actie | Commando | Wat gebeurt er |
|-------|----------|----------------|
| Installeer tool | `/install postgres-mcp` | Voegt toe aan `.mcp.json` of `settings.json` |
| Installeer alle aanbevolen | `/install-all` | Batch installatie met confirmatie |
| Bekijk details | `/details stripe-mcp` | Toont README, voorbeelden, issues |
| Scaffold nieuwe tool | `/scaffold horizon-mcp` | Start scaffold proces |
| Negeer suggestie | `/ignore stripe-mcp` | Voegt toe aan ignore-list |
| Exporteer rapport | `/export` | Markdown rapport naar `docs/` |

---

## 5. Scaffold-proces

### Wanneer scaffolden?

```
Geen tool gevonden OF beste match scoort <50% (⭐ of ❌)
         │
         ▼
┌─────────────────────────────────────────┐
│  Wil je zelf een tool ontwikkelen?      │
│                                         │
│  [Skill maken]  [MCP maken]  [Nee]      │
└─────────────────────────────────────────┘
```

### Scaffold opties

| Type | Wanneer | Output |
|------|---------|--------|
| **Skill** | Kennis/patterns/workflows nodig | `~/.claude/skills/[naam]/SKILL.md` |
| **MCP Server** | API/data/tool integratie nodig | Volledig MCP project met boilerplate |
| **Cursor Rules** | Cursor-specifieke regels | `.cursorrules` of `cursor.directory` format |
| **Codex Skill** | OpenAI Codex specifiek | `~/.codex/skills/[naam]/SKILL.md` |

### Skill Scaffold Flow

```
/scaffold skill horizon-monitoring
         │
         ▼
┌─────────────────────────────────────────────────────────────────┐
│  SKILL SCAFFOLD: horizon-monitoring                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. Wat is het doel van deze skill?                             │
│     > Laravel Horizon queue monitoring en debugging             │
│                                                                 │
│  2. Welke taken moet de skill ondersteunen?                     │
│     [x] Queue status bekijken                                   │
│     [x] Failed jobs analyseren                                  │
│     [x] Performance metrics interpreteren                       │
│     [ ] Andere: _______                                         │
│                                                                 │
│  3. Welke LLM(s) moeten ondersteund worden?                     │
│     [x] Claude                                                  │
│     [x] Codex                                                   │
│     [ ] Cursor (rules)                                          │
│     [ ] Andere: _______                                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
         │
         ▼
    Genereer SKILL.md met:
    • Frontmatter (name, description)
    • When to Use sectie
    • Core patterns/commands
    • Common mistakes
    • Quick reference
```

**Gegenereerde Skill structuur:**

```
~/.claude/skills/horizon-monitoring/
├── SKILL.md              # Hoofdbestand
└── examples/             # (optioneel)
    └── common-issues.md
```

### MCP Server Scaffold Flow

```
/scaffold mcp horizon-mcp
         │
         ▼
┌─────────────────────────────────────────────────────────────────┐
│  MCP SERVER SCAFFOLD: horizon-mcp                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. Welke taal voor de MCP server?                              │
│     (•) TypeScript (Recommended)                                │
│     ( ) Python                                                  │
│     ( ) Go                                                      │
│                                                                 │
│  2. Welke tools moet de MCP server bieden?                      │
│     [x] horizon_status    - Huidige queue status                │
│     [x] horizon_jobs      - Lijst jobs (pending/failed/etc)     │
│     [x] horizon_metrics   - Performance metrics                 │
│     [x] horizon_retry     - Retry failed job                    │
│     [ ] Andere: _______                                         │
│                                                                 │
│  3. Resources (read-only data)?                                 │
│     [x] horizon://queues          - Queue configuratie          │
│     [x] horizon://workers         - Worker status               │
│     [ ] Andere: _______                                         │
│                                                                 │
│  4. Waar moet het project komen?                                │
│     > ~/projects/horizon-mcp                                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

**Gegenereerde MCP structuur (TypeScript):**

```
~/projects/horizon-mcp/
├── package.json
├── tsconfig.json
├── README.md
├── src/
│   ├── index.ts           # Entry point
│   ├── server.ts          # MCP server setup
│   ├── tools/
│   │   ├── horizon_status.ts
│   │   ├── horizon_jobs.ts
│   │   ├── horizon_metrics.ts
│   │   └── horizon_retry.ts
│   └── resources/
│       ├── queues.ts
│       └── workers.ts
├── .mcp.json              # Lokale test config
└── .github/
    └── workflows/
        └── publish.yml    # npm publish workflow
```

**Gegenereerde code voorbeeld (src/index.ts):**

```typescript
#!/usr/bin/env node
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { registerTools } from "./tools/index.js";
import { registerResources } from "./resources/index.js";

const server = new McpServer({
  name: "horizon-mcp",
  version: "0.1.0",
});

registerTools(server);
registerResources(server);

const transport = new StdioServerTransport();
await server.connect(transport);
```

### Na scaffold: volgende stappen

```
✅ Scaffold compleet: ~/projects/horizon-mcp

Volgende stappen:
1. cd ~/projects/horizon-mcp && npm install
2. Implementeer de tool logic in src/tools/
3. Test lokaal: npm run dev
4. Voeg toe aan je config: claude mcp add ./
5. (Optioneel) Publiceer naar npm: npm publish
6. (Optioneel) Submit naar MCP Registry
```

---

## 6. Implementatie Overwegingen

### Benodigde tools/resources voor de skill

- WebSearch/WebFetch voor marketplace queries
- Glob/Read voor lokale config detectie
- Bash voor installatie commando's
- Write voor scaffold output

### Caching strategie

- Cache marketplace resultaten voor 24 uur
- Cache project analyse voor sessie-duur
- Invalidate bij config file changes

### Error handling

- Graceful fallback als marketplace offline is
- Duidelijke feedback bij installatie failures
- Rollback optie bij mislukte installaties

---

## 7. Open Vragen

1. Moet de skill automatisch draaien bij project open, of alleen on-demand?
2. Hoe om te gaan met conflicterende tools (bijv. twee postgres MCPs)?
3. Moet er een "project tooling config" file komen om preferences op te slaan?

---

## Referenties

- [Official MCP Registry](https://registry.modelcontextprotocol.io)
- [GitHub MCP Registry](https://github.blog/ai-and-ml/github-copilot/meet-the-github-mcp-registry-the-fastest-way-to-discover-mcp-servers/)
- [SkillsMP](https://skillsmp.com/)
- [SkillzWave](https://skillzwave.ai/)
- [Agent Skills CLI](https://www.agentskills.in/)
