---
name: project-tooling-analyzer
description: Use when starting work on a new or unfamiliar project, when project dependencies change significantly, or when asked to recommend AI tooling. Analyzes project files to identify tech stack and suggests relevant skills and MCP servers.
---

# Project Tooling Analyzer

Analyzes project directories and recommends AI assistant skills and MCP servers for effective development, maintenance, and evolution.

## Overview

This skill performs three core functions:
1. **Inventory** - Detect currently installed skills/MCPs across AI assistants
2. **Analyze** - Identify project tech stack from config files
3. **Recommend** - Suggest relevant tools from marketplaces, or scaffold new ones

## When to Use

- Starting work on a new/unfamiliar codebase
- After significant dependency changes (new framework, database, etc.)
- When asked "what tools do I need for this project?"
- Periodically to check for new relevant tooling

## Step 1: Detect Current Setup

First, inventory what's already installed across AI assistants:

| Assistant | Check Locations |
|-----------|-----------------|
| **Claude Code** | `~/.claude/skills/*/SKILL.md`, `~/.claude/settings.json`, `.mcp.json` |
| **OpenAI Codex** | `~/.codex/skills/*/SKILL.md`, `codex.md`, `.mcp.json` |
| **Cursor** | `~/.cursor/`, `.cursorrules`, `.cursor/mcp.json` |
| **Windsurf** | `~/.windsurf/`, `.windsurfrules` |
| **Continue.dev** | `~/.continue/config.json` |
| **Copilot** | `.github/copilot-instructions.md` |
| **Cline** | Cline config locations |
| **Aider** | `.aider.conf.yml`, `aider.conf.yml` |

### Detection Commands

```bash
# Claude skills
ls ~/.claude/skills/*/SKILL.md 2>/dev/null

# Claude MCPs (from settings)
cat ~/.claude/settings.json 2>/dev/null | grep -A 20 '"mcpServers"'

# Project-local MCPs
cat .mcp.json 2>/dev/null

# Codex skills
ls ~/.codex/skills/*/SKILL.md 2>/dev/null

# Cursor rules
cat .cursorrules 2>/dev/null
```

## Step 2: Analyze Project Tech Stack

Detect technologies from config files:

| File | Indicates |
|------|-----------|
| `package.json` | Node.js, npm packages, frameworks (React, Next, Vue, etc.) |
| `composer.json` | PHP, Composer packages (Laravel, Symfony) |
| `requirements.txt` | Python, pip packages |
| `pyproject.toml` | Python, Poetry packages |
| `Cargo.toml` | Rust, crates |
| `go.mod` | Go, modules |
| `Gemfile` | Ruby, gems (Rails) |
| `*.csproj` / `*.sln` | .NET, C# |
| `pom.xml` / `build.gradle` | Java (Maven/Gradle) |
| `docker-compose.yml` | Services (databases, caches, queues) |
| `.github/workflows/*` | CI/CD (GitHub Actions) |
| `prisma/schema.prisma` | Prisma ORM |
| `supabase/` | Supabase BaaS |
| `firebase.json` | Firebase BaaS |
| `shopify.theme.toml` | Shopify |
| `vercel.json` | Vercel deployment |
| `netlify.toml` | Netlify deployment |

### Detection Commands

```bash
# List all config files in project root
ls -la package.json composer.json requirements.txt pyproject.toml \
   Cargo.toml go.mod Gemfile *.csproj docker-compose.yml 2>/dev/null

# Check package.json dependencies
cat package.json 2>/dev/null | grep -A 50 '"dependencies"'

# Check composer.json require
cat composer.json 2>/dev/null | grep -A 30 '"require"'

# Check docker services
cat docker-compose.yml 2>/dev/null | grep -E "image:|postgres|mysql|redis|mongo|elastic"
```

## Step 3: Search for Relevant Tools

### MCP Registries & Directories

| Source | URL | Notes |
|--------|-----|-------|
| **Official MCP Registry** | registry.modelcontextprotocol.io | Official, has API |
| **GitHub MCP Registry** | github.com/mcp | Integrated with repos |
| **Docker MCP Catalog** | docs.docker.com/ai/mcp-catalog | Verified Docker images |
| **MCP.SO** | mcp.so | Usage metrics, rankings |
| **MCPMarket** | mcpmarket.com | Marketplace |
| **Glama MCP** | glama.ai/mcp/servers | Curated |
| **Awesome MCP Servers** | github.com/punkpeye/awesome-mcp-servers | Community curated |

### Skills Marketplaces

| Source | URL | Size | Compatibility |
|--------|-----|------|---------------|
| **SkillsMP** | skillsmp.com | 63,000+ | Claude, Codex, ChatGPT |
| **SkillzWave** | skillzwave.ai | 44,000+ | Claude, Codex, Cursor, Gemini |
| **Agent Skills CLI** | agentskills.in | 50,000+ | Claude, Codex, Copilot, Cursor |
| **Claude Plugins** | claude-plugins.dev | - | Claude |
| **Cursor Directory** | cursor.directory | - | Cursor rules |

### Search Strategy

For each detected technology, search:
1. MCP registries: `"mcp server [technology]"`
2. Skills marketplaces: `"[assistant] skill [technology]"`
3. GitHub: `"[technology] mcp server"`, `"[technology] claude skill"`
4. npm: `mcp-server-[technology]`, `@modelcontextprotocol/server-[technology]`

## Step 4: Evaluate Tool Quality

### Quality Criteria

| Criterion | Weight | Good | Excellent |
|-----------|--------|------|-----------|
| GitHub stars | 20% | >100 | >500 |
| Recent activity | 25% | <6 months | <3 months |
| Documentation | 20% | README exists | Examples included |
| Issue response | 15% | Some activity | Active maintainer |
| Downloads | 10% | >100/week | >1000/week |
| Official/curated | 10% | In a list | Official registry |

### Quality Classification

| Rating | Score | Meaning |
|--------|-------|---------|
| ⭐⭐⭐ Aanbevolen | >75% | Actively maintained, good docs |
| ⭐⭐ Bruikbaar | 50-75% | Works but less active |
| ⭐ Experimenteel | <50% | May work, has risks |
| ❌ Afraden | - | Abandoned, broken, security issues |

## Output Format

Present findings in this structure:

```
┌─────────────────────────────────────────────────────────────────────┐
│           PROJECT TOOLING ANALYSE: [project-naam]                   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  📊 GEDETECTEERDE STACK                                             │
│  • [Technology 1]                                                   │
│  • [Technology 2]                                                   │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ✅ REEDS BESCHIKBAAR                                               │
│  • [Installed skill/MCP] → [what it helps with]                     │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  🔍 AANBEVOLEN TOEVOEGINGEN                                         │
│                                                                     │
│  1. [Tool name]                                      [Rating]       │
│     Bron: [URL]                                                     │
│     Compatibel: [Assistants]                                        │
│     Installatie: [command]                                          │
│     → [What it enables]                                             │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ⚠️  GAPS - GEEN KWALITATIEVE TOOL GEVONDEN                         │
│  • [Technology without good tooling]                                │
│    → Scaffold beschikbaar: [command]                                │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

## Interactive Actions

After presenting recommendations, offer these actions:

| Action | Description |
|--------|-------------|
| **Install [tool]** | Add to `.mcp.json` or assistant config |
| **Install all** | Batch install all recommended tools |
| **Details [tool]** | Show README, examples, issues |
| **Scaffold [name]** | Create new skill or MCP for gap |
| **Ignore [tool]** | Add to ignore list for future runs |
| **Export** | Save report to `docs/tooling-analysis.md` |

### Installation Commands by Assistant

**Claude MCP:**
```bash
# Add to .mcp.json
claude mcp add [server-name]
```

**Cursor:**
```bash
# Add rules from cursor.directory
curl -o .cursorrules https://cursor.directory/api/rules/[rule-name]
```

**Continue.dev:**
```bash
# Edit ~/.continue/config.json to add context provider
```

## Scaffold Process

When no quality tool exists, offer to create one.

### Scaffold Skill

Ask these questions:
1. What is the skill's purpose?
2. What tasks should it support?
3. Which AI assistants should it support?

Generate SKILL.md with:
- Frontmatter (name, description with "Use when...")
- Overview section
- When to Use section
- Core patterns/commands
- Common mistakes
- Quick reference

**Output location:** `~/.claude/skills/[name]/SKILL.md` (or equivalent for other assistants)

### Scaffold MCP Server

Ask these questions:
1. Which language? (TypeScript recommended)
2. What tools should it provide?
3. What resources (read-only data)?
4. Where to create the project?

Generate project structure:
```
[project-name]/
├── package.json
├── tsconfig.json
├── README.md
├── src/
│   ├── index.ts
│   ├── server.ts
│   ├── tools/
│   │   └── [tool-name].ts
│   └── resources/
│       └── [resource-name].ts
└── .mcp.json
```

Provide next steps:
1. `cd [project] && npm install`
2. Implement tool logic
3. Test locally: `npm run dev`
4. Add to config: `claude mcp add ./`
5. (Optional) Publish to npm
6. (Optional) Submit to MCP Registry

## Quick Reference

| Tech Stack | Recommended Tools |
|------------|-------------------|
| Node.js/React/Next | - |
| PHP/Laravel | moai-lang-php skill, laravel-boost MCP |
| Python/FastAPI | python MCP |
| PostgreSQL | postgres MCP |
| Redis | redis MCP |
| GitHub | github MCP |
| Shopify | shopify skill |
| Stripe | stripe MCP |

## Common Mistakes

### Not checking installed tools first
**Problem:** Recommending tools already installed
**Fix:** Always run detection commands before searching marketplaces

### Ignoring cross-platform compatibility
**Problem:** Recommending Claude-only tools to Cursor user
**Fix:** Check active assistant and prioritize compatible tools

### Recommending abandoned tools
**Problem:** Tool looks good but hasn't been updated in years
**Fix:** Always check last commit date and issue activity

### Over-recommending
**Problem:** Suggesting 10+ tools overwhelms the user
**Fix:** Limit to 3-5 most relevant recommendations per category