# Lean Loop — TDD Workflow

This project uses Lean Loop: a PLAN → APPLY → UNIFY heartbeat cycle for structured development.

## Before You Start

Read these files every session:
- `.system/STATE.md` — current phase, next action, backlog
- `.system/PLAN.md` — active plan with acceptance criteria
- `.system/TDD_RULES.md` — Red-Green-Refactor execution rules

## The Heartbeat

### PLAN Phase

When asked to plan or implement a feature:

1. Fill in `.system/PLAN.md` with objective, ACs, boundaries, tasks
2. Run AC Quality Gate — every AC must pass all 5 checks:

| Check | What to verify |
|-------|---------------|
| Specific Input | "Given" names concrete values |
| Observable Action | "When" describes one triggerable action |
| Verifiable Outcome | "Then" states something a test can assert |
| Independent | AC doesn't depend on another AC passing first |
| No Leakage | AC doesn't prescribe internal implementation |

3. Show the gate table with PASS/FAIL for each AC
4. Only proceed to APPLY if ALL ACs pass. If any FAIL, ask user to refine.

### APPLY Phase

Follow Red-Green-Refactor strictly:

1. **RED:** Write ONE test for ONE behavior. Paste actual failing console output.
2. **GREEN:** Minimal code to make it pass. No future-proofing.
3. **REFACTOR:** Improve design only when green.

Rules:
- One test at a time. One behavior at a time.
- Touch fewest files possible.
- If scope expands beyond ACs → stop and return to PLAN.
- Test public interfaces, not internals.

### UNIFY Phase

After every APPLY session, output this exact format:

```
=== UNIFY ===

1. TEST SUITE:
   [paste full test output]

2. AC VERIFICATION:
   AC-1: [quote AC] → ✅/❌ [why]
   AC-2: ...

3. PLAN vs ACTUAL:
   Planned: [from PLAN.md]
   Actually done: [files changed]
   Files: [list]

4. DEBT / DEFERRED:
   - [items or "None"]

5. NEXT ACTION:
   [exactly one task]

Status: PASS → proceed to next PLAN
        FAIL → stay in APPLY, fix outstanding ACs
=== END UNIFY ===
```

Then update `.system/STATE.md` and append to `.system/LOG.md`.

## Exceptions

Break TDD only for:
- Hotfixes (production down, write tests after)
- Legacy code (too coupled for test-first)
- Spikes (throwaway exploration)

Always document exceptions in `.system/LOG.md`.
