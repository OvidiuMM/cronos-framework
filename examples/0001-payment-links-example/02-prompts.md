# Working Prompt Log — 0001-payment-links-example

## Working entries

### Type-first refactor cascade
- **Prompt:** "Edit the central type definition first. Then fix every compiler error it produces, one file at a time. Do not widen types or add `any` to make errors disappear."
- **What it achieved:** 30 callsites updated with zero invented shapes; faster and more thorough than grep.
- **Promotion candidate:** yes → `prompts/refactor-type-cascade.md`

### Facade with a closed method set
- **Prompt:** "Rewrite this service with exactly these four public methods: create, get, revoke, listByMerchant. No other public members. Delete what the constraint makes unreachable."
- **What it achieved:** ~250 lines deleted instead of nullified; prevented shape-preserving rewrites.
- **Promotion candidate:** yes → `prompts/rewrite-service-as-facade.md`

## Cautionary entries

### Ran the repo-wide formatter
- **What was done:** `npm run format` after edits; reformatted ~60 unrelated files.
- **Why it backfired:** review-killer PR; reverted. Formatter scope must match edit scope.
- **Lesson captured in:** retro Lesson 2 (→ Mandate 6 conversion if it recurs)
