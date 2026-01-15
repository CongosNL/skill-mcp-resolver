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