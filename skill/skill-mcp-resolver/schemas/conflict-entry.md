# Conflict Entry Schema

Documentation for adding entries to the [conflicts registry](../references/conflicts.md).

## Entry Format

Conflicts are documented in markdown tables with the following columns:

### Functional Overlaps

| Column | Required | Description |
|--------|----------|-------------|
| Tools | Yes | Comma-separated list of conflicting tool names |
| Overlap Area | Yes | Brief description of what functionality overlaps |
| Recommendation | Yes | Which tool to keep, or `context_dependent` |
| Reason | Yes | Why this recommendation is made |

### Incompatibilities

| Column | Required | Description |
|--------|----------|-------------|
| Tools | Yes | Comma-separated list of incompatible tool names |
| Issue | Yes | What goes wrong when both are used |
| Recommendation | Yes | Which tool to keep, or `context_dependent` |
| Reason | Yes | Why this recommendation is made |

## Recommendation Values

| Value | Meaning |
|-------|---------|
| `[tool-name]` | Always recommend keeping this specific tool |
| `context_dependent` | Recommendation depends on project tech stack |

When using `context_dependent`, the reason should explain what context determines the choice (e.g., "Match project's ORM").

## Tool Naming Conventions

Use the canonical tool name as it appears in:
- MCP server package name (e.g., `postgres-mcp`, `supabase-mcp`)
- Skill directory name (e.g., `react-skill`, `nextjs-skill`)

Include common variants if applicable (e.g., both `postgres-mcp` and `postgresql-mcp` if both exist).

## Examples

### Good Entry

```markdown
| prisma-mcp, drizzle-mcp | ORM operations | context_dependent | Match project's ORM |
```

- Clear overlap area
- Context-dependent because both are valid choices
- Actionable reason

### Bad Entry

```markdown
| postgres, supabase | database | supabase | better |
```

- Missing `-mcp` suffix
- Overlap area too vague
- Reason not informative

## Adding New Entries

1. **Verify the conflict** - Ensure both tools actually overlap or conflict
2. **Choose the right section** - Functional overlap vs incompatibility
3. **Be specific** - Clearly describe the overlap area or issue
4. **Provide reasoning** - Explain why one tool is preferred (or why it depends on context)
5. **Test the recommendation** - If possible, verify on a real project

## When to Use `context_dependent`

Use `context_dependent` when:
- Both tools are equally valid for different use cases
- The choice depends on what the project already uses
- There's no clear "better" option

Examples:
- `prisma-mcp` vs `drizzle-mcp` - depends on project's ORM
- `jest-skill` vs `vitest-skill` - depends on project's test runner
- `npm-skill` vs `pnpm-skill` - depends on project's package manager

## When to Recommend a Specific Tool

Recommend a specific tool when:
- One tool is a superset of the other (e.g., `supabase-mcp` includes `postgres-mcp` functionality)
- One tool is clearly more specific to common use cases (e.g., `nextjs-skill` over `react-skill` for Next.js projects)
- One tool is abandoned or has known issues
- One tool is officially maintained while the other is community-maintained
