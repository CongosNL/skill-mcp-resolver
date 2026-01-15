# Known Conflicts Registry

Curated list of known conflicts between skills and MCP servers. Used by the conflict detection system to provide accurate recommendations.

## How to Read This File

- **Tools**: The tools that conflict with each other
- **Overlap/Issue**: What functionality overlaps or what incompatibility exists
- **Recommendation**: Which tool to keep (`context_dependent` means match to project stack)
- **Reason**: Why this recommendation is made

## Functional Overlaps

Tools that provide similar functionality. Usually safe to have both, but redundant.

| Tools | Overlap Area | Recommendation | Reason |
|-------|--------------|----------------|--------|
| postgres-mcp, supabase-mcp | Database queries | supabase-mcp | Includes Postgres plus auth/storage APIs |
| postgres-mcp, neon-mcp | Database queries | context_dependent | Match your Postgres provider |
| prisma-mcp, drizzle-mcp | ORM operations | context_dependent | Match project's ORM |
| prisma-mcp, typeorm-mcp | ORM operations | context_dependent | Match project's ORM |
| sequelize-mcp, typeorm-mcp | ORM operations | context_dependent | Match project's ORM |
| react-skill, nextjs-skill | React components | nextjs-skill | More specific if using Next.js |
| react-skill, remix-skill | React components | remix-skill | More specific if using Remix |
| vue-skill, nuxt-skill | Vue components | nuxt-skill | More specific if using Nuxt |
| express-skill, nestjs-skill | Node.js routing | context_dependent | Match project's framework |
| express-skill, fastify-skill | Node.js routing | context_dependent | Match project's framework |
| aws-mcp, aws-cdk-mcp | AWS operations | aws-cdk-mcp | More specific if using CDK |
| terraform-mcp, pulumi-mcp | Infrastructure provisioning | context_dependent | Match project's IaC tool |
| jest-skill, vitest-skill | JavaScript testing | context_dependent | Match project's test runner |
| pytest-skill, unittest-skill | Python testing | pytest-skill | More features, widely adopted |
| docker-mcp, docker-compose-mcp | Container operations | docker-compose-mcp | Superset of docker functionality |
| github-mcp, gitlab-mcp | Git hosting operations | context_dependent | Match project's git host |
| eslint-skill, biome-skill | JavaScript linting | context_dependent | Match project's linter |
| prettier-skill, biome-skill | Code formatting | context_dependent | Biome includes formatting |

## Incompatibilities

Tools that actively conflict or cause issues when used together.

| Tools | Issue | Recommendation | Reason |
|-------|-------|----------------|--------|
| prettier-skill, eslint-format-skill | Formatting race condition | prettier-skill | More widely adopted, clearer scope |
| npm-skill, yarn-skill, pnpm-skill | Conflicting lockfiles | context_dependent | Match project's package manager |
| cjs-patterns-skill, esm-patterns-skill | Module syntax conflicts | context_dependent | Match project's module system |

## Database Provider Overlaps

Common pattern: generic database MCP vs provider-specific MCP.

| Tools | Overlap Area | Recommendation | Reason |
|-------|--------------|----------------|--------|
| postgres-mcp, planetscale-mcp | SQL queries | planetscale-mcp | Provider-specific features |
| postgres-mcp, cockroachdb-mcp | SQL queries | cockroachdb-mcp | Provider-specific features |
| mongodb-mcp, mongodb-atlas-mcp | MongoDB operations | mongodb-atlas-mcp | Includes Atlas-specific features |
| redis-mcp, upstash-mcp | Redis operations | upstash-mcp | Includes Upstash-specific features |

## Auth Provider Overlaps

| Tools | Overlap Area | Recommendation | Reason |
|-------|--------------|----------------|--------|
| nextauth-skill, clerk-skill | Authentication | context_dependent | Match project's auth provider |
| nextauth-skill, auth0-skill | Authentication | context_dependent | Match project's auth provider |
| clerk-skill, auth0-skill | Authentication | context_dependent | Match project's auth provider |
| lucia-skill, nextauth-skill | Authentication | context_dependent | Match project's auth library |

## CMS/Headless Overlaps

| Tools | Overlap Area | Recommendation | Reason |
|-------|--------------|----------------|--------|
| strapi-mcp, contentful-mcp | CMS operations | context_dependent | Match project's CMS |
| sanity-mcp, contentful-mcp | CMS operations | context_dependent | Match project's CMS |
| strapi-mcp, payload-mcp | CMS operations | context_dependent | Match project's CMS |

## Known Non-Conflicts

Tool pairs that heuristic detection may flag but are actually complementary (different domains/platforms).

| Tools | Why Not a Conflict |
|-------|-------------------|
| bol-retailer-api, marktplaats-api | Different platforms (bol.com vs marktplaats.nl), both needed for Dutch market |
| code-review-specialist, skill-evaluator | Different domains (reviews code vs reviews skills) |
| prd, ralph | Complementary workflow (prd creates PRDs, ralph converts to JSON) |
| shopify, bol-retailer-api | Different e-commerce platforms |
| shopify, marktplaats-api | Different platforms (e-commerce vs classifieds) |

## Contributing

To add a new conflict:
1. Verify the conflict exists (both tools cover same functionality or cause issues)
2. Add to appropriate section
3. Provide clear recommendation and reason
4. If context-dependent, explain what context determines the choice

To add a known non-conflict:
1. Identify tool pairs flagged by heuristic detection
2. Verify they serve different domains/platforms/purposes
3. Add to "Known Non-Conflicts" with explanation
