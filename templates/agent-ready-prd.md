# Agent-Ready PRD Template

> **Cronos Framework — Deterministic Spec**
> Fill every section. Ambiguity is the #1 cause of Vibe Drift.

---

## 1. Metadata

| Field | Value |
|---|---|
| PRD ID | `PRD-YYYY-WW-NNN` |
| Cycle Start | YYYY-MM-DD (Monday) |
| Solution Owner | @handle |
| Technical Product Owner | @handle |
| Developer | @handle |
| Peer Reviewer | @handle |
| Status | `Draft` / `TPO-Validated` / `In-Execution` / `Done` |

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

---

## 5. Technical Constraints

> TPO signs off on this section before execution begins.

| Constraint | Detail |
|---|---|
| Language / Runtime | e.g. TypeScript 5, Node 22 |
| Framework | e.g. Next.js 15 App Router |
| Architecture pattern | e.g. Domain-Driven hexagonal |
| Infra target | e.g. Vercel Edge + Supabase |
| Auth strategy | e.g. NextAuth v5 / JWT |
| Banned approaches | List anything the agent must not do |

**TPO sign-off:** ☐ Approved — @handle — YYYY-MM-DD

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
- If you are stuck for more than 4 hours on the same problem, stop and report.

Output format for each task:
1. Brief plan (3–5 bullets)
2. Implementation
3. Test file
4. Summary of what changed and why
```

---

## 7. Work Breakdown Structure (WBS)

| ID | Task | Owner | Day | Estimate | Status |
|---|---|---|---|---|---|
| T-01 | Scaffold project structure | Dev | Mon | 2 h | ☐ |
| T-02 | Implement feature A | Dev | Tue | 4 h | ☐ |
| T-03 | Write unit tests for A | Dev | Wed | 2 h | ☐ |
| T-04 | Security scan | Dev | Thu | 1 h | ☐ |
| T-05 | Peer review | Reviewer | Fri | 1 h | ☐ |

---

## 8. Reset Trigger Log

If a Mandatory Reset Trigger fires, record it here.

| # | Trigger Type | Timestamp | Description | Resolution |
|---|---|---|---|---|
| 1 | — | — | — | — |

---

## 9. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Hidden dependency discovered after Monday | Medium | High | Raise in Tuesday Path Sync |
| AI circular hallucination on X | Low | Medium | Pin to a known-good model snapshot |

---

## 10. Sign-Off

| Role | Name | Date | Signature |
|---|---|---|---|
| Solution Owner | | | ☐ |
| Technical Product Owner | | | ☐ |
| Peer Reviewer (Friday) | | | ☐ |
