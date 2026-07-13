# The Cronos Framework

A Strategic Methodology for Human-Validated Vibe Coding and Agentic Software Engineering.

**Current version: v2.1** — see [doc/v2.1-amendments.md](doc/v2.1-amendments.md) for the full rationale behind each change, derived from four production cycle retrospectives.

## Overview

The software development landscape has been fundamentally reshaped by vibe coding, a paradigm shift where the developer's primary role transitions from manual code construction to high-level intent orchestration. The Cronos methodology is a formal response to the systemic risks of AI-driven development, establishing a structured framework that preserves generative velocity while embedding rigorous project management controls. By organizing development into deterministic five-day cycles, Cronos ensures that the "vibe" of creation is balanced by the "verify" of professional engineering standards.

## Repository Structure

```
cronos-framework/
├── doc/
│   ├── Cronos_Framework_v2.1.pdf # The methodology paper, v2.1 (Parts A–C + new Part D)
│   ├── learning-propagation.md   # The AI Toolkit layer: cross-cycle memory & promotion pipeline
│   └── v2.1-amendments.md        # Rationale for every v2.1 change, with retro evidence
├── examples/
│   └── 0001-payment-links-example/ # A complete worked cycle folder (plan → retro)
├── templates/
│   ├── agent-ready-prd.md        # Deterministic spec template for every cycle (the WHAT/WHY)
│   ├── cycle/                    # Cycle folder: kickoff, Mission Control plan (the HOW), prompts log, ADR log, validation, retro
│   ├── d5-checklist.md           # Validator survivability checklist (run on D5)
│   └── daily-pulse.md            # Three-line async end-of-day update
└── registry/
    ├── claude-skills/
    │   └── cronos/               # Behavioral agent skill: six cycle modes, gates, failure-mode catalog
    ├── cursorrules/
    │   ├── typescript.md         # Cursor rules for TypeScript projects
    │   └── python-agent.md       # Cursor rules for Python / agentic projects
    └── ci-cd/
        └── emergency-trigger-action.yml  # GitHub Action for reset trigger automation
```

### `templates/`

| File | Purpose | When to use |
|---|---|---|
| `agent-ready-prd.md` | Fill-in-the-blank PRD with metadata, success criteria, WBS, agent instructions, amendment log, and sign-off table | **D1 Initialization** — copy once per cycle before any vibe coding begins |
| `d5-checklist.md` | Validator survivability checklist covering correctness, security, tests, deployment artifacts, observability, and Cronos cadence compliance | **D5 Midday** — executed by the Validator, never the Implementer |
| `daily-pulse.md` | Three-line async update (Landed / Next / Friction) | **End of every cycle day** — posted by the Implementer; no meeting |

### `registry/cursorrules/`

Drop-in `.cursorrules` rule blocks that enforce Cronos hard constraints inside Cursor (or any editor that supports project-level agent instructions).

| File | Stack | Key guardrails |
|---|---|---|
| `typescript.md` | TypeScript 5 / Node 22 | Strict mode, no `any`, hexagonal architecture, TDD, typed error handling, Cronos process rules |
| `python-agent.md` | Python 3.12+ / LLM-orchestrated agents | `mypy --strict`, Google docstrings, `LLMGateway` abstraction, Pydantic response validation, max iteration count on agent loops, Cronos process rules |

Commit your chosen `.cursorrules` file on **D1 Initialization** so every agent context window in the cycle inherits the same constraints.

### `registry/ci-cd/`

| File | Purpose |
|---|---|
| `emergency-trigger-action.yml` | GitHub Actions workflow that auto-creates a `cronos:emergency-sync` issue whenever a Mandatory Reset Trigger fires |

#### Using the Emergency Trigger Action

**Installation** — copy the workflow file into your repository's workflows directory:
```bash
cp registry/ci-cd/emergency-trigger-action.yml .github/workflows/emergency-trigger-action.yml
```
Then commit and push the file. GitHub Actions only runs workflows stored in `.github/workflows/`.

**Slash-command** — comment on any PR or Issue:
```
/cronos-trigger <type> <solution_owner> [description]
```

**Manual dispatch** — after copying this workflow into `.github/workflows/` in your project repo, run it from the Actions tab with:
- `trigger_type` — one of `prompt-loop-stagnation`, `circular-hallucination`, `chunk-breach`, `toolchain-interruption`
- `description` — brief situation summary
- `solution_owner` — GitHub handle of the PM (the workflow input keeps its legacy name for compatibility)

The action creates a labelled issue, @mentions the PM, and records the timestamp — ready to paste into PRD Section 8 (Reset Trigger Log).

---

## Core Roles

Cronos v2.1 uses a three-role model. (v2.0 used four roles — Solution Owner, Technical Product Owner, Developer, Peer Reviewer; the SO and TPO responsibilities are merged into the PM, and the remaining roles are renamed to match how the framework is run in practice.)

* **PM:** Crafts agent-ready PRDs, manages the Work Breakdown Structure (WBS), validates technical constraints, arms the plan-approval gate (Gate 1), and holds final release authority. *(absorbs the former Solution Owner + Technical Product Owner roles)*
* **Implementer:** Acts as "Mission Control" for AI agents — intent orchestration and daily vibe coding execution. Posts the Daily Pulse. *(formerly Developer)*
* **Validator:** Provides "Extra Human Validation." Runs the D5 survivability checklist and the adversarial validation pass. **Must not be the same person as the Implementer at Medium+ risk** (Gate 2; recommended at every tier). *(formerly Peer Reviewer)*

---

## The Cronos Rhythm (D1–D5)

A cycle is exactly **5 working days** and may start on **any working day** — the rhythm is relative, not bound to the calendar week. Weekends and holidays pause the clock: a cycle started Thursday runs Thu (D1), Fri (D2), Mon (D3), Tue (D4), Wed (D5).

| Day | Phase | Key activity |
|---|---|---|
| D1 | Initialization | Scaffold project; commit `.cursorrules`; fill PRD template |
| D2 AM | Path Sync | 15–30 min PM + Implementer alignment; zero logic doubts |
| D2 – D3 | High-Vibe Execution | "See stuff, say stuff, run stuff" loop with the AI |
| D4 AM | Checkpoint & QA Sync | PM + Implementer review checkpoint; build test suites |
| D4 | Rigorous Verification | Automated tests, security scans, fresh-eyes audit |
| D5 Midday | Demo & Review | Formal demo; Validator runs `d5-checklist.md` |
| D5 PM | Polish & Release | Doc sync; retro; release decision |
| Daily EOD | **Daily Pulse** | Implementer posts the three-line async update (`daily-pulse.md`) — no meeting |

The fixed five-day length is the framework's core control. Decoupling from weekdays is **not** license to stretch to six days or compress to four.

---

## Key Mandates & Guardrails

### 1. The Focus Mandate

* The Implementer's calendar is 100% blocked for the cycle duration.
* No external meetings are permitted except for methodology-specified syncs.
* The Daily Pulse is the connection valve: the team sees daily progress without a meeting.

### 2. The 72-Hour Modularization Mandate

* Any feature estimated at more than 3 days of active development must be modularized.
* Breaking the project into functional "chunks" prevents Vibe Drift and ensures comprehensive verification.

### 3. Mandatory Reset Triggers

An Emergency Sync Meeting with the PM is automatically triggered if development hits any of the following:

| Trigger | Condition |
|---|---|
| 🔄 Prompt Loop Stagnation | > 4 consecutive hours in a loop without a functional state |
| 🤖 Circular Hallucination | AI proposes the same failing solution 3+ times |
| ⏰ 72-Hour Chunk Breach | Hidden dependencies found by D2 that will block the D5 demo |
| 🔧 Toolchain Interruption | Critical agentic infra outage lasting > 2 hours |

**Soft trigger (early warning):** the same "Friction" line appearing in two consecutive Daily Pulses prompts a PM check-in — catching stagnation from outside before the 4-hour hard trigger fires from inside.

Log every trigger in **PRD Section 8** and use `emergency-trigger-action.yml` to notify the PM automatically.

### 4. The Cycle Chaining Limit

* No person runs more than **3 consecutive delivery cycles** in the same role. After 3 chained cycles, the next week is mandatory non-delivery time: a **Technical Health Cycle** or unblocked calendar.
* The Technical Health Cycle is not optional recovery that can be traded away — it is the scheduled owner of the deferred-debt rows ("Tech Health Cycle") in every retro's Open Follow-ups table.
* Switching roles (Implementer → Validator) resets the chain, since validation is a half-day commitment, not a blocked week.
* Assigning a 4th consecutive delivery cycle requires an explicit, written, time-bounded exception from the PM.
* The limit counts **cycles, not calendar weeks** — weekend-straddling starts (see D1–D5 rhythm) don't reset it.

### 5. The Independent Validation Gate (Gate 2)

* Any cycle at **Medium risk or higher** must name a Validator who is not the Implementer, in the PRD header, at D1.
* A solo cycle at that tier is a framework deviation requiring written sign-off from the release authority plus a stated compensating control.
* Evidence: the one production cycle that skipped this gate carried its two riskiest changes as unresolved follow-ups for two subsequent cycles.

### 6. The Recurrence Rule

* Any lesson that appears in **two consecutive retros** must be converted into an enforced rule — a `.cursorrules` entry, a CI check, or a skill — in the following cycle.
* A twice-written lesson is a process bug: written lessons demonstrably do not propagate on their own.

---

## Verification & Release Gates

**Gate 1 — Mission Control.** The Implementer's file-level plan (`templates/cycle/01-plan.md`) is approved by the PM before any code — the cheapest hour of the cycle.  Plan amendments are classified as **Material** (new scope / changed design / superseded decision → blocks code until the PM re-approves), **Verification-fix** (in-scope fix from the verification phase → logged, no re-arm), or **Cosmetic** (→ logged, no re-arm). The Implementer proposes the class; the Validator can contest it.

**Fresh-eyes audit.** Between "tests pass" and the D5 demo, a fresh agent context (or fresh human) audits an explicit file list against a 🔴/🟠/🟡/✅ rubric. Audit findings are claims, not facts — the Implementer verifies each against the actual code before acting.

**Proven-red regression tests.** A regression test that has never been observed failing does not count as a regression guard. The verification record must show the red run.

**Deployment artifacts are release-critical.** Security rules, IAM grants, bucket lifecycle rules, env config, and feature flags are enumerated in the PRD and verified deployed — or explicitly gated — before the release decision is marked Shipped.

**Release decision (four states):**

| State | Meaning |
|---|---|
| ✅ **Shipped** | Production, unconditional |
| ✅⚠️ **Shipped with conditions** | Deployed (possibly staging-only); named conditions tracked as follow-ups; decision reopens if a condition surfaces a real problem |
| ⏸️ **Held** | Not released; named unblock condition |
| ↩️ **Rolled back** | Released then reverted; reason recorded |

**Gate 3 — the human release gate.** The agent does not push, merge, or open PRs. Cycle close hands off to the human, who owns the release decision.

**Retro is a close gate.** A cycle is not closed until the retro has all three role sections filled (or an explicit "uneventful, nothing to report" per role). Learning promotion runs only against closed cycles.

**Learning propagation.** What a cycle learns must outlive the cycle: prompts, skills, and knowledge promote into a versioned AI Toolkit at close, with thresholds and backlinks. See [doc/learning-propagation.md](doc/learning-propagation.md) and the worked example in [examples/](examples/0001-payment-links-example/).

**Run Cronos with Claude Code.** [`registry/claude-skills/cronos/`](registry/claude-skills/cronos/) is a drop-in behavioral skill: six operating modes (bootstrap → close) with the gates enforced in-session, a failure-modes catalog distilled from production retros, and paste-ready phase prompts.

---

## Theoretical Modeling of Cronos Efficiency

$$P=\frac{T_{traditional}}{T_{cronos}}=\frac{\sum T_{manual}}{\sum\left(\frac{T_{vibe}}{S_{i}}\right)+T_{validation}}$$

This model indicates a Cronos team can complete the equivalent of a traditional 40-hour week in approximately 11–14 hours — an efficiency gain of **2.85×–3.64×**.

---

## Contributing

See [doc/CONTRIBUTING.md](doc/CONTRIBUTING.md) for submission guidelines. Contributions to `/templates` and `/registry` are licensed under the MIT License.
