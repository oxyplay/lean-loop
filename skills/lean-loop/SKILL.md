---
name: lean-loop
description: >
  Lightweight TDD system with PLAN/APPLY/UNIFY heartbeat cycle for structured development.
  Use when: implementing features with test-driven development, writing acceptance criteria,
  doing red-green-refactor cycles, planning before coding, or when user mentions
  "lean loop", "tdd workflow", "plan then code", "acceptance criteria", or structured development.
  Creates .system/ tracking files automatically if missing.
---

# Lean Loop: Structured TDD Workflow

A disciplined heartbeat cycle (PLAN → APPLY → UNIFY) for building software with acceptance-criteria-driven development, strict TDD, and mandatory reconciliation.

## Initialization

Before starting the loop, ensure the project has operational state files:

1. Check if `.system/` directory exists in the project root
2. If **missing**, create it by copying templates from this skill's bundled `templates/` directory:
   - `.system/PLAN.md` ← `templates/plan-template.md`
   - `.system/STATE.md` ← `templates/state-template.md`
   - `.system/LOG.md` ← `templates/log-template.md`
   - `.system/TDD_RULES.md` ← `templates/tdd-rules-template.md`
3. Read `.system/STATE.md` to understand current project state
4. Read `.system/TDD_RULES.md` to load execution rules

## Philosophy

- **In-Session Context:** All implementation happens in the main session. Do not use subagents for APPLY tasks — they lose context and reduce quality.
- **Vertical Slicing:** Build one behavior end-to-end ("Tracer Bullets" from *The Pragmatic Programmer*) rather than horizontal layers.
- **Acceptance-Driven:** Define "Done" via clear Acceptance Criteria before writing any code.
- **Behavior-First TDD:** Test public interfaces, not internal implementation.
- **Deep Modules:** Small public interfaces that hide complex implementations (*A Philosophy of Software Design*).

## The Heartbeat: PLAN → APPLY → UNIFY

### Phase 1: PLAN

Fill in `.system/PLAN.md` with:

1. **Objective** — one clear, specific goal
2. **Acceptance Criteria** — Given/When/Then format, each testable independently
3. **Boundaries** — files/modules that must NOT change
4. **Tasks** — broken into rows: Files | Action | Depends | Verify | AC Ref

> **Gate:** If ACs are unclear, contradictory, or untestable — STOP. Refine the PLAN. Do not proceed to APPLY.

> **Rule:** Set PLAN status to `APPROVED` before starting APPLY.

### Phase 2: APPLY

Execute Red-Green-Refactor cycles strictly. For each behavior:

1. **RED** — Write ONE test for ONE behavior. Confirm it fails with actual console output. Never guess error messages.
2. **GREEN** — Write only the minimal code to make the test pass. No future-proofing. No extra features.
3. **REFACTOR** — Improve design (deepen modules, remove duplication) only when test is green.

**Strict rules:**
- One test at a time. One behavior at a time.
- Smallest viable change: touch fewest files possible.
- If work expands beyond original ACs — STOP and return to PLAN.
- Test public interfaces, not internals. Mock only external APIs, databases, time, randomness.

### Phase 3: UNIFY (Mandatory)

After every APPLY session, perform reconciliation. No exceptions.

**Checklist:**
1. All tests are green — run the full test suite
2. All Acceptance Criteria are satisfied — check each one explicitly
3. Update `.system/STATE.md` — current phase, next action, progress
4. Document in `.system/LOG.md`:
   - Technical decisions made (if any)
   - Deferred issues / technical debt (if any)
   - RED phase failures (if any — console facts only)
5. Compare planned vs. actually done

**UNIFY output format:**
```
- **Planned:** [brief description from PLAN]
- **Actually done:** [what was actually changed]
- **AC satisfied:** [list each AC and whether met]
- **Deferred / Debt:** [if any]
- **Next Action:** [exactly one task]
```

## Exceptions (When to Break TDD)

Rare cases only. All must be documented in `.system/LOG.md`:

1. **Hotfixes** — production bugs requiring immediate recovery (write tests later)
2. **Legacy Code** — too tightly coupled, testing would require massive refactoring
3. **Spikes** — exploratory code for hypothesis validation, will be thrown away

## Anti-Patterns

- Skipping UNIFY ("tests pass, good enough")
- Writing multiple tests before making any pass
- Adding code not required by current AC ("might need it later")
- Using subagents for APPLY phase implementation
- Refactoring during RED phase
- Proceeding to APPLY with vague or untestable ACs
- Ignoring `.system/STATE.md` between sessions

## Template Files

Bundled templates for `.system/` initialization:

- [plan-template.md](templates/plan-template.md)
- [state-template.md](templates/state-template.md)
- [log-template.md](templates/log-template.md)
- [tdd-rules-template.md](templates/tdd-rules-template.md)
