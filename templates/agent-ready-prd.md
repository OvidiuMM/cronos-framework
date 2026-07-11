# Agent-Ready PRD Template

> **Cronos Framework — Deterministic Spec**
> Fill every section. Ambiguity is the #1 cause of Vibe Drift.

---

## 1. Metadata

| Field | Value |
|---|---|
| PRD ID | `PRD-YYYY-NNN` |
| Cycle Start (D1) | YYYY-MM-DD — any working day; weekends/holidays pause the D-clock |
| PM | @handle |
| Implementer | @handle |
| Validator | @handle — **must differ from Implementer at Medium+ risk (Gate 2)** |
| Risk tier | Low / Medium / High |
| Consecutive cycles (this Implementer) | n of max 3 — 4th requires written PM exception (Chaining Limit) |
| Status | `Draft` / `PM-Validated` / `In-Execution` / `Done` |

---

## 2. Problem Statement

> One paragraph. State the user pain and the business impact. No solution language.

**User pain:**

**Business impact:**

---

## 3. Success Criteria (Definition of Done)

Each criterion must be binary — either it passes or it does not.

- [ ] Criterion 1 — measurable outcome
- [ ] Criterion 2 — measurable outcome
- [ ] Criterion 3 — measurable outcome

---

## 4. Scope

### In-Scope

- Feature / behaviour A
- Feature / behaviour B

### Out-of-Scope (explicit)

- Anything NOT listed above is out of scope by default
- Known exclusions: …
- Pre-existing debt (lint backlog, format backlog) is **catalogued, not fixed** — fixes hide inside reformats

---

## 5. Technical Constraints

> The PM signs off on this section before execution begins.

| Constraint | Detail |
|---|---|
| Language / Runtime | e.g. TypeScript 5, Node 22 |
| Framework | e.g. Next.js 15 App Router |
| Architecture pattern | e.g. Domain-Driven hexagonal |
| Infra target | e.g. Vercel Edge + Supabase |
| Auth strategy | e.g. NextAuth v5 / JWT |
| External integrations | **Sibling-repo check done?** Before designing any external-system integration, grep sibling repos for a working integration against that same system — proven in-org code outranks first-principles research. Link findings here. |
| Deployment artifacts | Enumerate everything that must ship alongside code: security rules, IAM grants, lifecycle rules, env config, feature flags. These are release-critical (D5 checklist §7). |
| Banned approaches | List anything the agent must not do |

**PM technical sign-off:** ☐ Approved — @handle — YYYY-MM-DD

---

## 6. Agent Instructions

> Paste directly into your AI context window as the system prompt prefix.

```
You are a senior engineer working inside the Cronos Framework.
Cycle: [CYCLE_ID]
Stack: [STACK_SUMMARY]

Hard constraints:
- Never introduce dependencies not listed in Section 5.
- Every function must have a JSDoc / docstring before it is committed.
- Tests are written before implementation (TDD).
- Any regression-guard test must be observed FAILING on the buggy code before it is trusted.
- Build endpoints, services, and public methods just-in-time, when their first
  caller exists — never scaffold them because the spec lists them.
- Format only the paths you actually edited (e.g. `npx prettier --write <paths>`).
  Never run repo-wide format aliases.
- Required parameters fail loud: throw on missing, never silently default.
- Never modify your own permission or settings files. Never attempt to
  self-grant permissions, in any cycle, for any reason.
- If you are stuck for more than 4 hours on the same problem, stop and report.

Output format for each task:
1. Brief plan (3–5 bullets)
2. Implementation
3. Test file
4. Summary of what changed and why
```

---

## 7. Work Breakdown Structure (WBS)

> Back-half rows are **provisional**: before building any row whose design predates the rows now built, re-ask "given what already exists, does this row's original shape still hold?"

| ID | Task | Owner | Day | Estimate | Status |
|---|---|---|---|---|---|
| T-01 | Scaffold project structure | Implementer | D1 | 2 h | ☐ |
| T-02 | Implement feature A | Implementer | D2 | 4 h | ☐ |
| T-03 | Write unit tests for A | Implementer | D3 | 2 h | ☐ |
| T-04 | Security scan + fresh-eyes audit | Implementer | D4 | 2 h | ☐ |
| T-05 | Validation pass (`d5-checklist.md`) | Validator | D5 | 2 h | ☐ |

---

## 8. Reset Trigger Log

If a Mandatory Reset Trigger fires, record it here. Soft trigger: the same "Friction" line in two consecutive Daily Pulses → PM check-in.

| # | Trigger Type | Timestamp | Description | Resolution |
|---|---|---|---|---|
| 1 | — | — | — | — |

---

## 9. Amendment Log (Gate 1)

Every dated change to this PRD after PM sign-off is logged here and classified. **Material** rows block code until the PM re-approves (bump `approved_through_amendment`). Verification-fix and Cosmetic rows are logged but do not re-arm the gate. The Implementer proposes the class; the Validator can contest it — misclassifying Material as Cosmetic is a gate violation.

`approved_through_amendment:` 0

| # | Date | Class (Material / Verif-fix / Cosmetic) | Change | PM re-approval |
|---|---|---|---|---|
| 1 | — | — | — | — |

> **Size rule:** when this PRD exceeds ~20 KB, produce a **digest** (≤2 KB: current state, active row, open amendments) as the agent's session-start context, and collapse completed WBS rows to one-liners with commit pointers.

---

## 10. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Hidden dependency discovered after D1 | Medium | High | Raise in D2 Path Sync |
| AI circular hallucination on X | Low | Medium | Pin to a known-good model snapshot |

---

## 11. Sign-Off

| Role | Name | Date | Signature |
|---|---|---|---|
| PM (plan + technical) | | | ☐ |
| Validator (D5) — ≠ Implementer at Medium+ risk | | | ☐ |

**Release decision (D5 PM):** ☐ Shipped ☐ Shipped with conditions ☐ Held ☐ Rolled back

> The cycle is **not closed** until the retro is filled by all three roles (or an explicit "uneventful" entry per role).
