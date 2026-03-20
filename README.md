# Lean Loop: Lightweight TDD System

A disciplined heartbeat cycle (PLAN → APPLY → UNIFY) for building software with acceptance-criteria-driven development, strict TDD, and mandatory reconciliation.

## Installation

### As an opencode / Claude skill (recommended)

```bash
npx skills add oxyplay/lean-loop -g
```

The skill auto-creates `.system/` tracking files in your project on first use.

### Manual

Copy the `.system/` directory into your project root:

```bash
cp -r .system/ /path/to/your/project/.system/
```

## Philosophy
- **In-Session Context:** All implementation happens in the main session to maintain 100% quality and avoid subagent launch costs.
- **Vertical Slicing:** Build one behavior end-to-end (Tracer Bullets) rather than horizontal layers.
- **Acceptance-Driven:** Define "Done" via clear Acceptance Criteria (AC) before writing any code.
- **Behavior-First TDD:** Tests verify what the system does through public interfaces, not internal implementation details.

## The Heartbeat: PLAN → APPLY → UNIFY

Operational state and artifacts are stored in the `.system/` folder.

1. **PLAN:** Define Objective, Acceptance Criteria (Given/When/Then), and specific Tasks.
   > **Rule:** If ACs are unclear, contradictory, or untestable — stop and refine the PLAN. Do not proceed to APPLY.

2. **APPLY:** Execute Red-Green-Refactor cycles strictly following TDD_RULES.md.
   > **Strict APPLY Checklist (one behavior at a time):**
   > - Only **one** test for **one** behavior
   > - Confirm RED using actual console output
   > - Write minimal code to make it GREEN (no future-proofing)
   > - Refactor **only** after GREEN
   > - **Smallest Viable Change:** Touch the fewest files possible. If the task starts expanding beyond original ACs — stop and return to PLAN.

3. **UNIFY:** Mandatory reconciliation. Compare plan vs. actual, log decisions, and update state.
   > **Definition of Done:**
   > 1. All tests are green.
   > 2. All Acceptance Criteria are fully satisfied.
   > 3. `STATE.md` is updated.
   > 4. Any RED phase failures are documented in the 💥 Failure Log section of `.system/LOG.md` (based on console facts only).

   > **UNIFY Template:**
   > - **Planned:** [brief description]
   > - **Actually done:** [what was changed]
   > - **AC satisfied:** [list]
   > - **Deferred / Technical Debt:** [if any]
   > - **Next Action:** [exactly one task]

## Project Structure

```
your-project/
├── .system/
│   ├── PLAN.md          # Active plan with ACs and tasks
│   ├── STATE.md         # Current phase, next action, backlog
│   ├── LOG.md           # Decisions, debt, and failure log
│   └── TDD_RULES.md     # Red-Green-Refactor execution rules
└── ...
```

## How It Works

1. **PLAN** — Fill in `PLAN.md`: define objective, write Given/When/Then acceptance criteria, list boundaries, break into tasks
2. **APPLY** — Follow `TDD_RULES.md`: one failing test at a time, minimal code to pass, refactor only when green
3. **UNIFY** — Reconcile: verify all ACs met, update `STATE.md` with next action, log decisions in `LOG.md`
4. **Repeat** — Return to PLAN for the next task

## References

- [The Pragmatic Programmer](https://pragprog.com/titles/tpp20/) — Tracer Bullets concept
- [A Philosophy of Software Design](https://www.amazon.com/Philosophy-Software-Design-John-Ousterhout/dp/1732102201) — Deep Modules
- [Test-Driven Development: By Example](https://www.amazon.com/Test-Driven-Development-Kent-Beck/dp/0321146530) — Kent Beck's TDD approach
