# Retro — 0001-payment-links-example

**Started:** 2026-03-04 (D1) · **Closed:** 2026-03-10
**Implementer:** @edgar · **Validator:** @omar · **Plan approved by:** @dana (through amendment 2)
**Risk:** Medium

## What worked
- **Type-first refactor.** The compiler walked the agent through all 30 callsites; no invented types. Faster than grep.
- **Facade with a closed method set** prevented shape-preserving rewrites: ~250 lines deleted, not nullified.
- **Sibling-repo check reversed a wrong integration lean before any code** (ADR 2).
- **Best-effort QR** gave a degraded-not-broken failure mode (ADR 1). Reusable pattern.
- **Gate 1 held under the D2 descope:** amendment 1 blocked code until the PM re-approved — the right person back in at the right moment.

## What didn't work
- **Repo-wide formatter overreach:** ~60 unrelated files reformatted, reverted. First occurrence — watch for recurrence.
- **Webhook shipped signature-only** (no IP allowlist). Carried as a condition, not forced into scope.

## Surprises
- Backend tests passed first try after the rewrite — suspicious for this scope. Either coverage is genuinely strong or it misses what the Validator's adversarial pass would catch. The Validator's cold run is what makes this readable either way.

## Lessons (carry into next cycle)
1. **Type-first refactors propagate cleanly.** Edit the definition, walk the errors. Generalize as a prompt.
2. **Scope formatters to edited paths.** If this recurs next cycle, Mandate 6 converts it to a skill.
3. **Best-effort > blocking for sidecar data** (QRs, thumbnails, indexes).

## Promotion candidates
- **Prompts:** `refactor-type-cascade.md` → ✅ promoted → `ai-toolkit/prompts/refactor-type-cascade.md` · `rewrite-service-as-facade.md` → ✅ promoted
- **Skills:** none — formatter lesson at first occurrence, below the Mandate 6 bar.
- **Knowledge:** best-effort-sidecar pattern *(seen: 0001)* — held per the 3-cycle rule.

## Open follow-ups
| Item | Severity | Owner |
|---|---|---|
| Webhook IP allowlist or vendor-signed payloads | High | Cycle 0002 Validator |
| Bulk-send (descoped amendment 1) | Medium | Future cycle |

## Release decision
- [x] **Shipped with conditions** — production 2026-03-10; condition: webhook hardening tracked above. Decision reopens if it surfaces a real problem.

---
## Validator section
Adversarial webhook replay was the highest-value hour of the cycle. Nothing else to report.

## PM section
The D2 descope was the cycle's best decision — the 72-hour rule made it mechanical rather than negotiable.
