> **AI Instruction (Pruning):** If this file exceeds 100 lines, compress older TDD cycle logs into one-line summaries.

# TDD Rules

## Core Rules

1. **One test at a time.** Never write a second test while the first is red.
2. **Confirm RED.** Paste actual console output showing the test fails. Never guess the error.
3. **Minimal GREEN.** Write only enough code to make the current test pass. No future-proofing.
4. **Refactor only on GREEN.** Never refactor with a failing test.
5. **Public interfaces only.** Test what the system does, not how it does it.
6. **Smallest viable change.** Touch the fewest files possible. If scope expands — return to PLAN.

## What to Mock
- External APIs, databases, filesystem, network
- Time (`Date.now`, `setTimeout`)
- Randomness (`Math.random`)
- **Never mock:** internal modules, pure functions, data transformations

## When to Break TDD
Document in `.system/LOG.md` with reason:
- Hotfix (production down, write tests after)
- Legacy code (too coupled for test-first)
- Spike (throwaway exploration)
