# Tech Stack Detection Reference

Complete detection matrix for identifying project technologies from config files.

## Languages & Frameworks

| File | Indicates |
|------|-----------|
| `package.json` | Node.js (React, Next.js, Vue, Angular, Svelte, Express, Nest.js) |
| `composer.json` | PHP (Laravel, Symfony, WordPress, Drupal) |
| `requirements.txt` / `pyproject.toml` | Python (Django, FastAPI, Flask, Celery) |
| `Cargo.toml` | Rust (Actix, Rocket, Axum, Tokio) |
| `go.mod` | Go (Gin, Echo, Fiber, Chi) |
| `Gemfile` | Ruby (Rails, Sinatra, Hanami) |
| `*.csproj` / `*.sln` | .NET (ASP.NET, Blazor, MAUI) |
| `pom.xml` / `build.gradle` | Java/Kotlin (Spring, Quarkus, Micronaut) |
| `pubspec.yaml` | Dart/Flutter |
| `Package.swift` | Swift |
| `mix.exs` | Elixir (Phoenix) |
| `deno.json` | Deno |
| `bun.lockb` | Bun runtime |

## Databases & ORMs

| File | Indicates |
|------|-----------|
| `prisma/schema.prisma` | Prisma ORM |
| `drizzle.config.ts` | Drizzle ORM |
| `knexfile.js` | Knex.js |
| `typeorm.config.ts` | TypeORM |
| `sequelize.config.js` | Sequelize |
| `alembic.ini` | SQLAlchemy migrations |
| `diesel.toml` | Diesel (Rust) |
| `.pgpass` | PostgreSQL |
| `mongod.conf` | MongoDB |
| `redis.conf` | Redis |

## Infrastructure & DevOps

| File | Indicates |
|------|-----------|
| `docker-compose.yml` / `Dockerfile` | Docker |
| `kubernetes/` / `k8s/` | Kubernetes |
| `helm/` / `Chart.yaml` | Helm charts |
| `terraform/` / `*.tf` | Terraform |
| `pulumi/` / `Pulumi.yaml` | Pulumi |
| `serverless.yml` | Serverless Framework |
| `sam.yaml` / `template.yaml` | AWS SAM |
| `cdk.json` | AWS CDK |
| `bicep/` / `*.bicep` | Azure Bicep |
| `ansible/` / `playbook.yml` | Ansible |

## CI/CD

| File | Indicates |
|------|-----------|
| `.github/workflows/*` | GitHub Actions |
| `.gitlab-ci.yml` | GitLab CI |
| `.circleci/config.yml` | CircleCI |
| `Jenkinsfile` | Jenkins |
| `.travis.yml` | Travis CI |
| `azure-pipelines.yml` | Azure DevOps |
| `bitbucket-pipelines.yml` | Bitbucket Pipelines |
| `.buildkite/` | Buildkite |

## Cloud & Deployment

| File | Indicates |
|------|-----------|
| `vercel.json` | Vercel |
| `netlify.toml` | Netlify |
| `fly.toml` | Fly.io |
| `render.yaml` | Render |
| `railway.json` | Railway |
| `heroku.yml` / `Procfile` | Heroku |
| `app.yaml` | Google App Engine |
| `amplify.yml` | AWS Amplify |
| `cloudflare.toml` | Cloudflare Workers/Pages |

## Backend as a Service

| File | Indicates |
|------|-----------|
| `supabase/` | Supabase |
| `firebase.json` | Firebase |
| `appwrite.json` | Appwrite |
| `convex/` | Convex |
| `pocketbase/` | PocketBase |
| `nhost/` | Nhost |

## E-commerce & CMS

| File | Indicates |
|------|-----------|
| `shopify.theme.toml` | Shopify |
| `medusa-config.js` | Medusa |
| `saleor/` | Saleor |
| `strapi/` / `config/database.js` | Strapi |
| `sanity.config.ts` | Sanity |
| `contentful.json` | Contentful |
| `payload.config.ts` | Payload CMS |
| `keystonejs/` | KeystoneJS |
| `directus/` | Directus |

## API & GraphQL

| File | Indicates |
|------|-----------|
| `openapi.yaml` / `swagger.json` | OpenAPI/Swagger |
| `schema.graphql` / `*.graphql` | GraphQL |
| `apollo.config.js` | Apollo GraphQL |
| `graphql-codegen.yml` | GraphQL Code Generator |
| `trpc/` | tRPC |

## Auth & Identity

| File | Indicates |
|------|-----------|
| `auth.config.ts` / `[...nextauth].ts` | NextAuth.js |
| `clerk.config.ts` | Clerk |
| `auth0.config.js` | Auth0 |
| `lucia.config.ts` | Lucia Auth |
| `kinde.config.ts` | Kinde |

## Testing

| File | Indicates |
|------|-----------|
| `jest.config.*` | Jest |
| `vitest.config.*` | Vitest |
| `playwright.config.*` | Playwright |
| `cypress.config.*` | Cypress |
| `pytest.ini` / `conftest.py` | Pytest |
| `.rspec` | RSpec |

## Build & Bundling

| File | Indicates |
|------|-----------|
| `vite.config.*` | Vite |
| `webpack.config.*` | Webpack |
| `rollup.config.*` | Rollup |
| `esbuild.config.*` | esbuild |
| `turbo.json` | Turborepo |
| `nx.json` | Nx monorepo |
| `lerna.json` | Lerna |
| `pnpm-workspace.yaml` | pnpm workspace |

## Monitoring & Analytics

| File | Indicates |
|------|-----------|
| `sentry.*.config.js` | Sentry |
| `datadog.yaml` | Datadog |
| `newrelic.js` | New Relic |
| `.env` with `POSTHOG_` | PostHog |
| `logstash.conf` | ELK Stack |
