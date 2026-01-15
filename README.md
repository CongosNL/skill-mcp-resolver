# Skill MCP Resolver

Resolves and provisions the skills and MCP servers needed for any project.

## What it does

This skill for AI coding assistants (Claude Code, Codex, Cursor, etc.) analyzes your project and:

1. **Inventories** currently installed skills and MCPs across AI assistants
2. **Resolves** which tools are needed based on your tech stack
3. **Provisions** missing tools by installing or scaffolding them

## Installation

### Claude Code

```bash
# Copy to your skills directory
cp -r skill/skill-mcp-resolver ~/.claude/skills/
```

### Other Assistants

Copy the `SKILL.md` to your assistant's skills directory:
- **Codex**: `~/.codex/skills/skill-mcp-resolver/`
- **Cursor**: Use as `.cursorrules` reference

## Usage

The skill activates when:
- Starting work on a new or unfamiliar project
- Project dependencies change significantly
- You ask "what tools do I need for this project?"

## Supported AI Assistants

| Assistant | Detection Locations |
|-----------|---------------------|
| Claude Code | `~/.claude/skills/`, `~/.claude/settings.json`, `.mcp.json` |
| OpenAI Codex | `~/.codex/skills/`, `codex.md`, `.mcp.json` |
| Cursor | `~/.cursor/`, `.cursorrules`, `.cursor/mcp.json` |
| Windsurf | `~/.windsurf/`, `.windsurfrules` |
| Continue.dev | `~/.continue/config.json` |
| Copilot | `.github/copilot-instructions.md` |
| Cline | `~/.cline/`, `cline_mcp_settings.json` |
| Aider | `.aider.conf.yml` |

## Detected Tech Stacks

Automatically detects technologies from config files:

| Category | Files | Technologies |
|----------|-------|--------------|
| **Languages** | | |
| Node.js | `package.json` | React, Next.js, Vue, Angular, Express, etc. |
| PHP | `composer.json` | Laravel, Symfony, WordPress |
| Python | `requirements.txt`, `pyproject.toml` | Django, FastAPI, Flask |
| Rust | `Cargo.toml` | Actix, Rocket, Tokio |
| Go | `go.mod` | Gin, Echo, Fiber |
| Ruby | `Gemfile` | Rails, Sinatra |
| .NET | `*.csproj`, `*.sln` | ASP.NET, Blazor |
| Java | `pom.xml`, `build.gradle` | Spring, Quarkus |
| **Databases & Services** | | |
| Docker | `docker-compose.yml` | PostgreSQL, MySQL, Redis, MongoDB, Elasticsearch |
| Prisma | `prisma/schema.prisma` | Database ORM |
| **Backend as a Service** | | |
| Supabase | `supabase/` | Auth, Database, Storage |
| Firebase | `firebase.json` | Auth, Firestore, Functions |
| **E-commerce** | | |
| Shopify | `shopify.theme.toml` | Themes, Apps, Liquid |
| **Deployment** | | |
| Vercel | `vercel.json` | Serverless, Edge |
| Netlify | `netlify.toml` | JAMstack, Functions |
| **CI/CD** | | |
| GitHub Actions | `.github/workflows/*` | Automation, Testing |

## Tool Sources

Searches these registries and marketplaces:

**MCP Servers:**
- [Official MCP Registry](https://registry.modelcontextprotocol.io)
- [MCP.SO](https://mcp.so)
- [MCPMarket](https://mcpmarket.com)
- [Awesome MCP Servers](https://github.com/punkpeye/awesome-mcp-servers)

**Skills:**
- [SkillsMP](https://skillsmp.com) (63,000+)
- [SkillzWave](https://skillzwave.ai) (44,000+)
- [Agent Skills CLI](https://agentskills.in) (50,000+)
- [Cursor Directory](https://cursor.directory)

## Quality Ratings

Tools are rated based on GitHub stars, recent activity, documentation, and official status:

| Rating | Meaning |
|--------|---------|
| ⭐⭐⭐ Recommended | >75% score, actively maintained |
| ⭐⭐ Usable | 50-75% score, works but less active |
| ⭐ Experimental | <50% score, may have risks |
| ❌ Avoid | Abandoned or broken |

## Scaffolding

When no quality tool exists, the skill can scaffold new ones:

- **Skills**: Generates `SKILL.md` with proper frontmatter
- **MCP Servers**: Generates TypeScript starter project (see `templates/`)

## License

MIT
