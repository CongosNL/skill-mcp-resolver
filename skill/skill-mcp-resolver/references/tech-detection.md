# Tech Stack Detection Reference

Complete detection matrix for identifying project technologies from config files.

## Contents

- [Languages & Frameworks](#languages--frameworks)
- [Databases & ORMs](#databases--orms)
- [Infrastructure & DevOps](#infrastructure--devops)
- [CI/CD](#cicd)
- [Cloud & Deployment](#cloud--deployment)
- [Backend as a Service](#backend-as-a-service)
- [E-commerce & CMS](#e-commerce--cms)
- [API & GraphQL](#api--graphql)
- [Auth & Identity](#auth--identity)
- [Testing](#testing)
- [Build & Bundling](#build--bundling)
- [Monitoring & Analytics](#monitoring--analytics)
- [Tool Keyword Mappings](#tool-keyword-mappings)

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

## Tool Keyword Mappings

Maps tool name patterns to technology keywords for heuristic conflict detection. When a tool name contains these patterns, associate it with the listed keywords.

### Database Tools

| Pattern | Keywords |
|---------|----------|
| `*postgres*` | postgres, postgresql, database, sql, relational |
| `*mysql*` | mysql, database, sql, relational |
| `*mongo*` | mongodb, mongo, database, nosql, document |
| `*redis*` | redis, cache, database, keyvalue |
| `*sqlite*` | sqlite, database, sql, embedded |
| `*supabase*` | supabase, postgres, database, auth, storage, baas |
| `*planetscale*` | planetscale, mysql, database, serverless |
| `*neon*` | neon, postgres, database, serverless |
| `*cockroach*` | cockroachdb, postgres, database, distributed |
| `*upstash*` | upstash, redis, cache, serverless |

### ORM Tools

| Pattern | Keywords |
|---------|----------|
| `*prisma*` | prisma, orm, database, schema, migrations |
| `*drizzle*` | drizzle, orm, database, sql, typescript |
| `*typeorm*` | typeorm, orm, database, typescript |
| `*sequelize*` | sequelize, orm, database, javascript |
| `*knex*` | knex, query-builder, database, sql |
| `*sqlalchemy*` | sqlalchemy, orm, database, python |
| `*diesel*` | diesel, orm, database, rust |

### JavaScript Frameworks

| Pattern | Keywords |
|---------|----------|
| `*react*` | react, jsx, components, hooks, frontend |
| `*next*` | nextjs, react, ssr, routing, fullstack |
| `*vue*` | vue, components, reactive, frontend |
| `*nuxt*` | nuxt, vue, ssr, routing, fullstack |
| `*angular*` | angular, typescript, components, frontend |
| `*svelte*` | svelte, components, compiler, frontend |
| `*solid*` | solidjs, reactive, components, frontend |

### Backend Frameworks

| Pattern | Keywords |
|---------|----------|
| `*express*` | express, nodejs, routing, middleware, http |
| `*nest*` | nestjs, nodejs, typescript, decorators, enterprise |
| `*fastify*` | fastify, nodejs, routing, performance, http |
| `*koa*` | koa, nodejs, middleware, http |
| `*hono*` | hono, edge, routing, http, lightweight |

### Python Frameworks

| Pattern | Keywords |
|---------|----------|
| `*django*` | django, python, orm, fullstack, admin |
| `*fastapi*` | fastapi, python, async, openapi, typing |
| `*flask*` | flask, python, lightweight, routing |

### Infrastructure Tools

| Pattern | Keywords |
|---------|----------|
| `*docker*` | docker, container, image, compose |
| `*kubernetes*`, `*k8s*` | kubernetes, k8s, container, orchestration, pods |
| `*terraform*` | terraform, iac, infrastructure, hcl |
| `*pulumi*` | pulumi, iac, infrastructure, typescript |
| `*ansible*` | ansible, automation, configuration, yaml |
| `*helm*` | helm, kubernetes, charts, deployment |

### Cloud Providers

| Pattern | Keywords |
|---------|----------|
| `*aws*` | aws, amazon, cloud, s3, lambda, ec2 |
| `*gcp*`, `*google-cloud*` | gcp, google, cloud, gcs, functions |
| `*azure*` | azure, microsoft, cloud, blob, functions |
| `*vercel*` | vercel, deployment, edge, serverless |
| `*netlify*` | netlify, deployment, jamstack, functions |
| `*cloudflare*` | cloudflare, workers, edge, cdn |

### Auth Providers

| Pattern | Keywords |
|---------|----------|
| `*nextauth*`, `*auth.js*` | nextauth, authjs, authentication, session, oauth |
| `*clerk*` | clerk, authentication, users, session |
| `*auth0*` | auth0, authentication, identity, oauth |
| `*lucia*` | lucia, authentication, session, typescript |
| `*kinde*` | kinde, authentication, users, oauth |

### Testing Tools

| Pattern | Keywords |
|---------|----------|
| `*jest*` | jest, testing, javascript, unit, snapshot |
| `*vitest*` | vitest, testing, vite, unit, typescript |
| `*playwright*` | playwright, testing, e2e, browser, automation |
| `*cypress*` | cypress, testing, e2e, browser, component |
| `*pytest*` | pytest, testing, python, unit, fixtures |

### Git Hosting

| Pattern | Keywords |
|---------|----------|
| `*github*` | github, git, repository, pr, issues, actions |
| `*gitlab*` | gitlab, git, repository, mr, ci, devops |
| `*bitbucket*` | bitbucket, git, repository, pipelines |

### Package Managers

| Pattern | Keywords |
|---------|----------|
| `*npm*` | npm, nodejs, packages, registry |
| `*yarn*` | yarn, nodejs, packages, workspaces |
| `*pnpm*` | pnpm, nodejs, packages, monorepo |
| `*pip*` | pip, python, packages, pypi |
| `*cargo*` | cargo, rust, packages, crates |

### CMS Tools

| Pattern | Keywords |
|---------|----------|
| `*strapi*` | strapi, cms, headless, content, api |
| `*sanity*` | sanity, cms, headless, content, groq |
| `*contentful*` | contentful, cms, headless, content, graphql |
| `*payload*` | payload, cms, headless, typescript |
| `*directus*` | directus, cms, headless, database |

### E-commerce

| Pattern | Keywords |
|---------|----------|
| `*shopify*` | shopify, ecommerce, storefront, checkout |
| `*stripe*` | stripe, payments, checkout, subscriptions |
| `*medusa*` | medusa, ecommerce, headless, commerce |
