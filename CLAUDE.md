# TripTracker Project

Nx monorepo (`@trip-tracker/source`) with Angular frontend, NestJS API, and shared TypeScript library.

## Project Overview

- **Angular** (`~22.0.4`) — web frontend app
- **NestJS** (`^11.0.0`) — REST API backend
- **Nx** (`23.1.1`) — monorepo tooling with caching
- **TypeScript** (`~6.0.3`, `strict: false`)
- **Jest** (`~30.3.0`) + **Playwright** (`^1.37.0`) for testing

## Apps

| App | Purpose | Port | Key Files |
|-----|---------|------|-----------|
| `web` | Angular frontend | 4200 | `apps/web/src/main.ts`, `apps/web/src/app/app.ts` |
| `api` | NestJS REST API | 3000 (default) | `apps/api/src/main.ts`, `apps/api/src/app/app.module.ts` |
| `web-e2e` | Playwright E2E tests for web | — | `apps/web-e2e/src/example.spec.ts` |
| `api-e2e` | Jest E2E tests for API | — | `apps/api-e2e/src/support/` |

## Libs

| Lib | Path Alias | Purpose |
|-----|-----------|---------|
| `shared/data-access` | `@trip-tracker/data-access` | Shared data-access code (stub) |

## Key Config Files

- `nx.json` — Nx plugins, target defaults, caching
- `tsconfig.base.json` — root TypeScript config, path aliases
- `jest.config.ts` / `jest.preset.js` — Jest setup
- `eslint.config.mjs` — ESLint flat config with module-boundary rules
- `.prettierrc` — `{ "singleQuote": true }`

## Path Aliases

```
@trip-tracker/data-access → libs/shared/data-access/src/index.ts
```

## Common Commands

```bash
# Build
nx build web       # Build Angular app
nx build api       # Build NestJS API (webpack)

# Serve
nx serve web       # Serve Angular on :4200
nx serve api       # Serve NestJS on :3000/api

# Test
nx test web        # Jest for Angular
nx test api        # Jest for NestJS
nx e2e web-e2e     # Playwright E2E

# Lint
nx lint web
nx lint api

# Entire workspace
nx run-many -t build
nx run-many -t test
```

## Architecture Notes

- Angular app uses standalone bootstrap (`bootstrapApplication`)
- NestJS API uses Express platform, routes prefixed `/api`
- `shared/data-access` lib is built with esbuild and published as `@trip-tracker/data-access`
- Module boundaries enforced with `enforceBuildableLibDependency: true`
- TypeScript `strict: false` at root level

## VSCode

Recommended extensions (see `.vscode/extensions.json`).
