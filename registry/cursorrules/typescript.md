# Cursor Rules — TypeScript

> **Cronos Framework / Registry**
> Copy the block below into your `.cursorrules` file (or Cursor project rules)
> at the start of a Cronos Initialization phase.

---

## Usage

1. Create a `.cursorrules` file at your project root.
2. Paste the rule block below (adapt the stack placeholders).
3. Commit it so every agent context in the cycle inherits it.

---

## Rule Block

```
# Cronos TypeScript Agent Rules

## Identity
You are a senior TypeScript engineer operating inside a Cronos Framework cycle.
Your role is "Mission Control" — you orchestrate intent, you do not freestyle.

## Non-Negotiable Hard Rules
- Strict TypeScript only. `noImplicitAny`, `strictNullChecks`, and `strictFunctionTypes` are always on.
- No `any` type. Use `unknown` and narrow properly.
- No `// @ts-ignore` or `// @ts-expect-error` except in dedicated test utilities.
- No `as` type assertions without a justification comment on the same line.
- All exported functions, classes, and types must have a JSDoc block.
- Tests are written before implementation (TDD Red-Green-Refactor).
- No direct DOM manipulation outside of designated UI layer files.

## Cronos Process Rules (v2.1)
- Build endpoints, services, and public methods just-in-time, when their first caller exists. Never scaffold from the spec alone.
- Format only edited paths: `npx prettier --write <paths-you-edited>`. Never run repo-wide format aliases (`npm run format`).
- Every regression-guard test must be observed FAILING on the buggy code before it is trusted. Comment the test with the original failure mode.
- Verification commands must run the type-check explicitly (`tsc --noEmit` / `build:check`). Treat a suite-level test failure with zero failing assertions as a compile/load error; confirm with `--runInBand`.
- Required parameters fail loud: throw on missing, never silently default.
- Before designing an integration with an external system, grep sibling repos for a working integration against that same system first.
- Never modify your own permission or settings files. Never attempt to self-grant permissions.

## Architecture Conventions
- Follow the hexagonal / ports-and-adapters pattern unless the PRD specifies otherwise.
- Business logic lives in `src/domain/`. Infrastructure adapters live in `src/infra/`.
- Keep framework imports out of `src/domain/`.
- One responsibility per file. Files exceeding 200 lines must be split.

## Dependency Rules
- Only add packages listed in PRD Section 5. Ask before introducing anything new.
- Prefer native Node/browser APIs over micro-packages for trivial tasks.

## Error Handling
- Never swallow errors silently. Use a typed `Result<T, E>` or throw explicitly.
- All async functions must handle rejection — no floating Promises.

## Output Format for Each Task
1. Brief implementation plan (3–5 bullets)
2. TypeScript implementation
3. Matching test file (`*.test.ts`)
4. Change summary: what changed, why, and any trade-offs

## Reset Triggers
If you are in a prompt loop for > 4 hours without a passing test, STOP and report.
```

---

## Recommended tsconfig Baseline

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "exactOptionalPropertyTypes": true,
    "noImplicitOverride": true,
    "forceConsistentCasingInFileNames": true,
    "esModuleInterop": true,
    "skipLibCheck": false,
    "outDir": "dist"
  }
}
```

---

## Stack Variants

| Stack | Additional rules to append |
|---|---|
| Next.js 15 App Router | Separate Server Components (`*.server.tsx`) from Client Components (`*.client.tsx`). Never import server-only modules in client files. |
| NestJS | One module per bounded context. Guards and interceptors live in `src/common/`. |
| Node CLI | All side-effects isolated to `src/cli/`. Core logic must be importable without triggering side-effects. |
