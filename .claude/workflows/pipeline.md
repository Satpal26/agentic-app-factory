# MASTER PIPELINE — Autonomous Application Factory
## Authoritative Execution Workflow

The OrchestratorAgent reads and executes this file phase by phase.
No deviations. No shortcuts. No merged phases.

---

## PHASE 1 — PARSE PROMPT
**Agent:** OrchestratorAgent
**Skill:** `.claude/skills/prompt-analysis.md`
**Input:** User's initial prompt
**Output:** `.generated/blueprint.json`

1. Apply the full 6-step analysis from `prompt-analysis.md`
2. Expand all implicit requirements automatically (auth, pagination, etc.)
3. Resolve tech stack via decision tree
4. Write `blueprint.json` — complete, no placeholders
5. Log: `[PHASE 1 COMPLETE] blueprint.json written — N features, N entities`

---

## PHASE 2 — ARCHITECT THE SYSTEM
**Agent:** ArchitectAgent
**Skill:** `.claude/skills/api-design.md`
**Input:** `.generated/blueprint.json`
**Output:** `.generated/architecture.json`

1. Read blueprint.json in full
2. Select/confirm tech stack
3. Design complete folder structure for both frontend and backend
4. Define EVERY API endpoint: method, path, auth required, request schema, response schema, error cases
5. Define EVERY database entity: fields, types, constraints, relationships, indexes
6. Define EVERY frontend page: route, auth guard, components, data dependencies
7. Write `architecture.json`
8. Log: `[PHASE 2 COMPLETE] architecture.json — N endpoints, N models, N pages`

---

## PHASE 3 — DATABASE LAYER
**Agent:** DatabaseAgent
**Input:** `.generated/architecture.json` (dataModels section)
**Output:** `app/backend/prisma/`

1. Generate `schema.prisma` — every model from architecture.json
2. Every model has: `id String @id @default(cuid())`, `createdAt DateTime @default(now())`, `updatedAt DateTime @updatedAt`
3. Generate `prisma/seed.ts` — realistic seed data (15+ records per model)
4. Write `.generated/database-complete.json`
5. Log: `[PHASE 3 COMPLETE] N models, seed.ts ready`

---

## PHASE 4 — BACKEND API
**Agent:** BackendAgent
**Skill:** `.claude/skills/code-generation.md`
**Input:** `.generated/architecture.json` + `app/backend/prisma/schema.prisma`
**Output:** `app/backend/src/`

1. Generate `src/index.ts` — Express server entry
2. Generate `src/app.ts` — middleware stack: helmet, cors, morgan, express.json, rateLimit
3. Generate route files — one per domain
4. Generate controller files — full implementation, every endpoint
5. Generate middleware: `auth.ts` (JWT), `validate.ts` (Zod factory), `error.ts` (global handler)
6. Generate Zod validator schemas for every endpoint
7. Generate `lib/prisma.ts`, `lib/jwt.ts`, `lib/hash.ts`
8. Generate complete `package.json`, `tsconfig.json`
9. Generate `.env.example` with every variable
10. Write `api-contract.md` documenting all endpoints
11. Write `.generated/backend-complete.json`
12. Log: `[PHASE 4 COMPLETE] N endpoints across N route files`

---

## PHASE 5 — FRONTEND APPLICATION
**Agent:** FrontendAgent
**Skill:** `.claude/skills/ui-design.md`
**Input:** `.generated/architecture.json` + `.generated/api-contract.md`
**Output:** `app/frontend/src/`

1. Generate `src/lib/axios.ts` — base URL from env, JWT interceptor, 401 refresh + retry
2. Generate `src/store/authStore.ts` — Zustand with user, token, login, logout
3. Generate `src/types/index.ts` — TypeScript interfaces matching every Prisma model
4. Generate `src/App.tsx` — React Router setup with protected routes
5. Generate every page from architecture.json frontendPages — fully implemented
6. Generate shadcn/ui base components + feature components
7. Generate TanStack Query hooks per entity
8. Generate React Hook Form + Zod forms for every create/edit flow
9. Generate `package.json`, `vite.config.ts`, `tailwind.config.js`, `tsconfig.json`
10. Write `.generated/frontend-complete.json`
11. Log: `[PHASE 5 COMPLETE] N pages, N components, N hooks`

---

## PHASE 6 — CODE REVIEW
**Agent:** ReviewerAgent
**Workflow:** `.claude/workflows/review-cycle.md`
**Input:** All files in `app/backend/` and `app/frontend/`
**Output:** `.generated/review-report.json`

1. Audit every backend file against checklist in review-cycle.md
2. Audit every frontend file against checklist in review-cycle.md
3. Cross-check: every endpoint in architecture.json has implementation
4. Cross-check: every frontend API call matches backend route signature
5. Score each file 1-10
6. Write `review-report.json` with exact file paths, line numbers, severity
7. Log: `[PHASE 6 COMPLETE] N issues (C critical, H high, M medium, L low)`

---

## PHASE 7 — PATCH ISSUES
**Agents:** BackendAgent + FrontendAgent (re-spawned with review-report.json)
**Input:** `.generated/review-report.json`
**Output:** Updated files

1. Fix every CRITICAL and HIGH severity issue — directly in the file
2. Fix MEDIUM issues if fixable in under 10 lines
3. Log LOW issues — no action
4. Mark each fixed issue as `"resolved": true` in the report
5. Log: `[PHASE 7 COMPLETE] N issues patched`

---

## PHASE 8 — TEST SUITE
**Agent:** TesterAgent
**Input:** `.generated/architecture.json` + `app/backend/src/`
**Output:** `app/tests/`

1. Backend tests (Vitest + Supertest) — one file per domain
2. Every endpoint: happy path + 401 without token + 400 invalid input + 404 not found
3. Auth helper: register + login test user, return JWT
4. Frontend component tests (Vitest + Testing Library) — critical components
5. `vitest.config.ts` for both backend and frontend
6. Log: `[PHASE 8 COMPLETE] N backend tests, N frontend tests`

---

## PHASE 9 — DEVOPS & INFRASTRUCTURE
**Agent:** DevOpsAgent
**Input:** `.generated/architecture.json`
**Output:** Root config files

1. `app/docker-compose.yml` — postgres + backend + frontend with health checks
2. `app/backend/Dockerfile` — multi-stage, node:20-alpine
3. `app/frontend/Dockerfile` — build stage + nginx production stage
4. `app/backend/.env.example` — every env variable, no empty values
5. `app/frontend/.env.example` — VITE_ prefixed variables
6. `app/.github/workflows/ci.yml` — lint + type-check + test on push/PR
7. `app/README.md` — professional, complete, with API docs table
8. `app/.gitignore` — node_modules, .env, .generated, dist, coverage
9. Log: `[PHASE 9 COMPLETE] Docker + CI/CD + README ready`

---

## PHASE 10 — FINAL ASSEMBLY & VERIFICATION
**Agent:** OrchestratorAgent
**Input:** All of `app/`
**Output:** Assembly report + completion announcement

1. Verify every file referenced in architecture.json exists
2. Verify no TODO/FIXME in any generated file
3. Verify all package.json files have required scripts
4. Verify .env.example files are complete
5. Count: total files, endpoints, pages, tests
6. Print the COMPLETION OUTPUT block from claude.md
7. Log: `[PHASE 10 COMPLETE] Pipeline finished successfully`

---

## FAILURE RECOVERY
If any phase fails:
1. Log error with full context to pipeline.log
2. Retry once with enriched prompt context
3. If retry fails: Orchestrator executes the stage directly
4. Pipeline NEVER stops — all gaps filled by Orchestrator