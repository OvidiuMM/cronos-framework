# D5 Validation — Survivability Checklist

> **Cronos Framework — Extra Human Validation (Gate 2)**
> Executed by the Validator at the D5 Midday Demo & Review.
> The Implementer must NOT run this checklist on their own work.

---

## Metadata

| Field | Value |
|---|---|
| PRD ID | `PRD-YYYY-NNN` |
| Validator | @handle |
| Review Date | YYYY-MM-DD (D5) |
| Repo / Branch | `owner/repo` @ `branch` |
| Commit SHA | `abc1234` |
| Risk tier | Low / Medium / High |
| Validator ≠ Implementer confirmed | ☐ (mandatory at Medium+ risk) |

---

## 1. Functional Correctness

- [ ] All PRD Section 3 success criteria pass end-to-end
- [ ] The D5 demo matches the spec — no "almost works" accepted
- [ ] Edge cases documented in the PRD are handled without crashing
- [ ] No regressions introduced in previously passing functionality

---

## 2. Code Survivability

- [ ] Code is readable without the Implementer present — no "tribal knowledge" required
- [ ] Every public function / method has a docstring or JSDoc
- [ ] No `TODO` / `FIXME` comments left in production paths
- [ ] No hardcoded secrets, credentials, or environment-specific values in source
- [ ] Dependency list (`package.json`, `requirements.txt`, etc.) is minimal and intentional
- [ ] No dormant code: every endpoint / public method has a live caller (just-in-time construction rule)
- [ ] Diff contains only files actually in scope — no wide-formatter overreach, no unrelated workspace artifacts

---

## 3. Test Coverage

- [ ] Unit tests exist for all new business-logic functions
- [ ] Tests are deterministic — no flaky async races or time-dependent assertions
- [ ] All tests pass locally on a clean checkout (`npm ci && npm test` / equivalent)
- [ ] The verification command runs the type-check explicitly (`tsc --noEmit` / `build:check`) — a jest-only parallel gate can pass a red build
- [ ] Every regression-guard test has a recorded **red run** — it was observed failing on the buggy code before being trusted
- [ ] Test descriptions are human-readable and map to acceptance criteria

---

## 4. Fresh-Eyes Audit

- [ ] An audit by a fresh agent context (or fresh human) was run between "tests pass" and this review, against an explicit file list, with a 🔴/🟠/🟡/✅ rubric
- [ ] Every audit finding was **verified against the actual code** before being fixed or dismissed — findings are claims, not facts
- [ ] 🔴/🟠 findings are resolved or explicitly carried as tracked follow-ups

---

## 5. Security Baseline

- [ ] No new attack surface introduced (open redirects, SSRF, XSS vectors)
- [ ] User input is validated and sanitised before processing
- [ ] Auth/authorisation checks are present on all protected routes/actions
- [ ] No sensitive data logged to stdout or persisted in plaintext
- [ ] Required parameters fail loud — no silent defaults on missing env/params

---

## 6. Performance & Scalability

- [ ] No N+1 query patterns or unbounded loops on data sets
- [ ] Expensive operations are async and non-blocking where applicable
- [ ] Bundle / image sizes are within agreed limits (if applicable)

---

## 7. Deployment Artifacts (release-critical)

- [ ] Every deployment-adjacent artifact is enumerated in the PRD and **verified deployed or explicitly gated**: security rules, IAM grants/scopes, bucket lifecycle rules, env config, feature flags, webhooks
- [ ] IAM scopes are minimal — no over-scoped roles left "to validate later"
- [ ] Assumed infrastructure safety nets (e.g. lifecycle auto-delete rules) are **confirmed to exist**, not assumed

---

## 8. Observability

- [ ] Errors are caught and surfaced — not silently swallowed
- [ ] Parallel operations with independent failure modes report per-branch outcomes (`allSettled`-style), not a single generic failure
- [ ] Key actions emit structured log lines or events for debugging
- [ ] Health/readiness endpoints (if applicable) return meaningful status

---

## 9. Documentation Sync

- [ ] README reflects any new setup steps or environment variables
- [ ] Architecture diagram updated if the system topology changed
- [ ] Repo agent-guidance files (`CLAUDE.md`, `.cursorrules`) do not contradict actual tooling config (lint ignores, test placement, scripts)
- [ ] Changelog / release notes entry drafted

---

## 10. Cronos Cadence Compliance

- [ ] The 72-Hour Modularisation Mandate was respected — no chunk exceeded 3 days
- [ ] All Reset Trigger events are logged in PRD Section 8
- [ ] Every plan amendment is classified (Material / Verification-fix / Cosmetic) and Material rows show PM re-approval before code proceeded (Gate 1)
- [ ] Daily Pulses exist for every cycle day
- [ ] WBS task statuses are up to date in the PRD
- [ ] The retro (`05-retro.md` / equivalent) is filled by all three roles — the cycle does not close without it

---

## Validator Verdict

| Outcome | Notes |
|---|---|
| ✅ **Approved — ship it** | Maps to release decision: Shipped |
| ⚠️ **Approved with follow-up items** | Maps to: Shipped with conditions — list items as tracked follow-ups |
| ⏸️ **Held** | Name the unblock condition |
| 🚫 **Blocked — rework required** | Describe blockers below |

**Rework notes (if blocked):**

---

**Validator sign-off:** _________________________________ Date: __________
