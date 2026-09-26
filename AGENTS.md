# Next Admin monorepo guide

Use pnpm 9.12.3 as pinned by `packageManager` and Node 20 as in E2E CI; the root's older minimum does not cover every workspace. `packages/` contains next-admin, CLI, Prisma generator, JSON-schema, database, and shared example code; `apps/` contains the Next, Remix, TanStack, and documentation examples. Keep fixes in the owning package and preserve public API/generated schema compatibility.

From the root, use `pnpm install --frozen-lockfile`, `pnpm setup:packages`, `pnpm lint`, and `pnpm typecheck`. `pnpm test` runs the configured workspace tests; use a non-watch invocation for a selected Vitest package if needed. `pnpm build:examples` and `pnpm start:examples` build/start example apps. There is no single build proving all framework integrations; select the affected example as well as library checks.

E2E CI uses Docker Compose, `pnpm database`, Playwright browsers, built examples, and `pnpm test:e2e` with explicit `BASE_URL`. Database setup/seed and Prisma `migrate reset --force` are destructive to their target: use only a disposable test database and don't copy reset commands onto a shared environment. Release, Vercel, and database-reset workflows have external effects. Report unit/type/build and end-to-end evidence separately.

## Completing work

Carry the authorized change through the relevant checks and repair failures it causes. Make routine, reversible implementation choices using existing patterns; ask only when missing information, a material product decision, or an authorization boundary prevents the next step. Existing authorization remains valid within its scope. If blocked, name the exact action and missing prerequisite, retain concise evidence, and continue independent work.

Choose verification proportional to the change. For instructions or prose, inspect changed paths, links, and local instruction precedence and run `git diff --check -- <changed-paths>`; don't install dependencies or run the application solely for a prose edit. For behavior changes, exercise the affected behavior and applicable checks below, then broaden only for failures or unresolved risk. Report files changed, checks actually run and their results, commands only inspected, and remaining limitations. A build or source inspection alone does not prove runtime behavior. Continue through already-authorized follow-through; stop at explicit review checkpoints or boundaries requiring new authorization.
