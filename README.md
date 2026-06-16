# The Cronos Framework

A Strategic Methodology for Human-Validated Vibe Coding and Agentic Software Engineering.

## Overview

The software development landscape has been fundamentally reshaped by vibe coding, a paradigm shift where the developer's primary role transitions from manual code construction to high-level intent orchestration. The Cronos methodology is a formal response to the systemic risks of AI-driven development, establishing a structured framework that preserves generative velocity while embedding rigorous project management controls. By organizing development into deterministic one-week cycles, Cronos ensures that the "vibe" of creation is balanced by the "verify" of professional engineering standards.

## Repository Structure

```
cronos-framework/
├── templates/
│   ├── agent-ready-prd.md        # Deterministic spec template for every cycle
│   └── friday-checklist.md       # Peer review survivability checklist
└── registry/
    ├── cursorrules/
    │   ├── typescript.md         # Cursor rules for TypeScript projects
    │   └── python-agent.md       # Cursor rules for Python / agentic projects
    └── ci-cd/
        └── emergency-trigger-action.yml  # GitHub Action for reset trigger automation
```

### `templates/`

| File | Purpose | When to use |
|---|---|---|
| `agent-ready-prd.md` | Fill-in-the-blank PRD with metadata, success criteria, WBS, agent instructions, and sign-off table | **Monday Initialization** — copy once per cycle before any vibe coding begins |
| `friday-checklist.md` | Peer Reviewer survivability checklist covering correctness, security, tests, observability, and Cronos cadence compliance | **Friday Midday** — executed by the Peer Reviewer, never the author |

### `registry/cursorrules/`

Drop-in `.cursorrules` rule blocks that enforce Cronos hard constraints inside Cursor (or any editor that supports project-level agent instructions).

| File | Stack | Key guardrails |
|---|---|---|
| `typescript.md` | TypeScript 5 / Node 22 | Strict mode, no `any`, hexagonal architecture, TDD, typed error handling |
| `python-agent.md` | Python 3.12+ / LLM-orchestrated agents | `mypy --strict`, Google docstrings, `LLMGateway` abstraction, Pydantic response validation, max iteration count on agent loops |

Commit your chosen `.cursorrules` file on **Monday Initialization** so every agent context window in the cycle inherits the same constraints.

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
- `solution_owner` — GitHub handle of the Solution Owner

The action creates a labelled issue, @mentions the Solution Owner, and records the timestamp — ready to paste into PRD Section 8 (Reset Trigger Log).

---

## Core Roles

To ensure that development speed never outpaces architectural governance, Cronos relies on a strict hierarchy:

* **Solution Owner (SO):** A merged Product Manager and Product Owner role. The SO crafts agent-ready Product Requirement Documents (PRDs), manages the Work Breakdown Structure (WBS), and holds final release authority.
* **Technical Product Owner (TPO):** Validates technical constraints in the PRDs. The TPO ensures architectural blueprints are followed and bridges business needs with technical reality.
* **Developer:** Acts as "Mission Control" for AI agents. The Developer handles intent orchestration and daily vibe coding execution.
* **Peer Reviewer:** Provides "Extra Human Validation". The Reviewer executes the survivability checklist to prevent author bias.

---

## The 7-Day Cronos Rhythm

| Day | Phase | Key activity |
|---|---|---|
| Monday | Initialization | Scaffold project; commit `.cursorrules`; fill PRD template |
| Tuesday AM | Path Sync | 15–30 min SO + Developer alignment; zero logic doubts |
| Tue – Wed | High-Vibe Execution | "See stuff, say stuff, run stuff" loop with the AI |
| Thursday AM | Checkpoint & QA Sync | SO + TPO + Developer review checkpoint; build test suites |
| Thursday | Rigorous Verification | Automated tests, security scans, visual audits |
| Friday Midday | Demo & Review | Formal demo; Peer Reviewer runs `friday-checklist.md` |
| Friday PM | Polish & Release | AI-generated doc sync; deploy to production-ready environment |

---

## Key Mandates & Guardrails

### 1. The Focus Mandate

* The Developer's calendar is 100% blocked for the cycle duration.
* No external meetings are permitted except for methodology-specified syncs.

### 2. The 72-Hour Modularization Mandate

* Any feature estimated at more than 3 days of active development must be modularized.
* Breaking the project into functional "chunks" prevents Vibe Drift and ensures comprehensive verification.

### 3. Mandatory Reset Triggers

An Emergency Sync Meeting with the Solution Owner is automatically triggered if development hits any of the following:

| Trigger | Condition |
|---|---|
| 🔄 Prompt Loop Stagnation | > 4 consecutive hours in a loop without a functional state |
| 🤖 Circular Hallucination | AI proposes the same failing solution 3+ times |
| ⏰ 72-Hour Chunk Breach | Hidden dependencies found by Tuesday that will block Friday demo |
| 🔧 Toolchain Interruption | Critical agentic infra outage lasting > 2 hours |

Log every trigger in **PRD Section 8** and use `emergency-trigger-action.yml` to notify the Solution Owner automatically.

---

## Theoretical Modeling of Cronos Efficiency

$$P=\frac{T_{traditional}}{T_{cronos}}=\frac{\sum T_{manual}}{\sum\left(\frac{T_{vibe}}{S_{i}}\right)+T_{validation}}$$

This model indicates a Cronos team can complete the equivalent of a traditional 40-hour week in approximately 11–14 hours — an efficiency gain of **2.85×–3.64×**.

---

## Contributing

See [doc/CONTRIBUTING.md](doc/CONTRIBUTING.md) for submission guidelines. Contributions to `/templates` and `/registry` are licensed under the MIT License.
