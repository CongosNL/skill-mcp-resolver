---
name: skill-mcp-resolver
description: Use when starting work on a new or unfamiliar project, when project dependencies change significantly, or when asked to recommend AI tooling. Resolves which skills and MCPs are needed and provisions missing ones.
---

# Skill MCP Resolver

Resolves required AI assistant skills and MCP servers for a project, and provisions missing ones.

## Contents

- [Overview](#overview)
- [Step 1: Detect Current Setup](#step-1-detect-current-setup)
- [Step 2: Analyze Project Tech Stack](#step-2-analyze-project-tech-stack)
- [Step 3: Search for Relevant Tools](#step-3-search-for-relevant-tools)
- [Step 4: Evaluate Tool Quality](#step-4-evaluate-tool-quality)
- [Output Format](#output-format)
- [Interactive Actions](#interactive-actions)
- [Scaffold Process](#scaffold-process)
- [Quick Reference](#quick-reference)
- [Error Handling](#error-handling)
- [Common Mistakes](#common-mistakes)

## Overview

This skill performs three core functions:
1. **Inventory** - Detect currently installed skills/MCPs across AI assistants
2. **Resolve** - Identify project tech stack and determine required tools
3. **Provision** - Install recommended tools or scaffold new ones

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
| **Cline** | `~/.cline/`, `cline_mcp_settings.json` |
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

# Cursor rules and MCP
cat .cursorrules 2>/dev/null
cat .cursor/mcp.json 2>/dev/null

# Windsurf rules
cat .windsurfrules 2>/dev/null
ls ~/.windsurf/ 2>/dev/null

# Continue.dev config
cat ~/.continue/config.json 2>/dev/null | grep -A 30 '"contextProviders"'

# Cline MCP settings
cat ~/.cline/cline_mcp_settings.json 2>/dev/null

# Copilot instructions
cat .github/copilot-instructions.md 2>/dev/null

# Aider config
cat .aider.conf.yml aider.conf.yml 2>/dev/null
```

## Step 2: Analyze Project Tech Stack

Detect 100+ technologies from config files. See [references/tech-detection.md](references/tech-detection.md) for the complete detection matrix.

**Categories:** Languages & Frameworks, Databases & ORMs, Infrastructure & DevOps, CI/CD, Cloud & Deployment, BaaS, E-commerce & CMS, API & GraphQL, Auth & Identity, Testing, Build & Bundling, Monitoring

### Quick Detection Commands

```bash
# Scan common config files
ls package.json composer.json requirements.txt pyproject.toml \
   Cargo.toml go.mod Gemfile docker-compose.yml vercel.json 2>/dev/null

# Check frameworks in package.json
cat package.json 2>/dev/null | grep -E "next|react|vue|angular|express"

# Check infrastructure
ls -d terraform/ kubernetes/ helm/ .github/workflows/ 2>/dev/null
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
| ⭐⭐⭐ Recommended | >75% | Actively maintained, good docs |
| ⭐⭐ Usable | 50-75% | Works but less active |
| ⭐ Experimental | <50% | May work, has risks |
| ❌ Avoid | - | Abandoned, broken, security issues |

## Output Format

Present findings in this structure:

```
┌─────────────────────────────────────────────────────────────────────┐
│           PROJECT TOOLING ANALYSIS: [project-name]                  │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  📊 DETECTED STACK                                                  │
│  • [Technology 1]                                                   │
│  • [Technology 2]                                                   │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ✅ ALREADY AVAILABLE                                               │
│  • [Installed skill/MCP] → [what it helps with]                     │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  🔍 RECOMMENDED ADDITIONS                                           │
│                                                                     │
│  1. [Tool name]                                      [Rating]       │
│     Source: [URL]                                                   │
│     Compatible: [Assistants]                                        │
│     Install: [command]                                              │
│     → [What it enables]                                             │
│                                                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ⚠️  GAPS - NO QUALITY TOOL FOUND                                   │
│  • [Technology without good tooling]                                │
│    → Scaffold available: [command]                                  │
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

Generate SKILL.md from this template:

```markdown
---
name: [skill-name]
description: Use when [specific triggering conditions]
---

# [Skill Name]

[One-sentence description of what this skill does]

## Overview

[2-3 sentences explaining the core purpose and approach]

## When to Use

- [Trigger condition 1]
- [Trigger condition 2]
- When NOT to use: [exclusion]

## Quick Reference

| Action | Command/Pattern |
|--------|-----------------|
| [Action 1] | `[command]` |
| [Action 2] | `[command]` |

## Common Mistakes

### [Mistake name]
**Problem:** [What goes wrong]
**Fix:** [How to fix it]
```

**Output location:** `~/.claude/skills/[name]/SKILL.md` (or equivalent for other assistants)

### Scaffold MCP Server

Ask these questions:
1. Which language? (TypeScript recommended)
2. What tools should it provide?
3. What resources (read-only data)?
4. Where to create the project?

Use the starter template in [templates/mcp-server-starter.md](templates/mcp-server-starter.md) which includes:
- `package.json` with MCP SDK dependency
- `tsconfig.json` for TypeScript
- `src/index.ts` with basic tool handler
- `.mcp.json` for local testing
- Next steps for implementation and publishing

## Quick Reference

| Tech Stack | Recommended Tools |
|------------|-------------------|
| Node.js/React/Next | Search marketplaces for framework-specific tools |
| PHP/Laravel | moai-lang-php skill, laravel-boost MCP |
| Python/FastAPI | python MCP |
| PostgreSQL | postgres MCP |
| Redis | redis MCP |
| GitHub | github MCP |
| Shopify | shopify skill |
| Stripe | stripe MCP |

## Error Handling

### Marketplace Unavailable
If a marketplace fails to respond or times out:
- Skip that source, continue with others
- Note the failure in output: "⚠️ [source] unavailable, results may be incomplete"
- Rely more heavily on GitHub search as fallback

### No Results Found
If no tools found for a technology:
- Verify technology name spelling variants (e.g., "PostgreSQL" vs "Postgres")
- Search for broader category (e.g., "database" instead of specific DB)
- Offer scaffold option as primary action

### Conflicting Recommendations
If multiple tools exist for same purpose:
- Compare quality scores and pick highest
- If scores equal, prefer official/curated sources
- Note alternatives in output for user choice

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