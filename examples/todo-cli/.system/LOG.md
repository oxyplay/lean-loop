> **AI Instruction (Pruning):** If this file exceeds 100 lines, compress only old closed `Deferred Issues` into one-line summaries. Keep `Technical Decisions` detailed if they remain relevant.

# Decision & Debt Log

## Technical Decisions
- **D-001:** Used ES modules (`module.exports`) for compatibility with plain `node` execution without build step

## Deferred Issues (Technical Debt)
- [ ] greet() does not validate input type — passing a number silently coerces to string

## Failure Log (Red Phase Post-Mortems)
- 2026-03-20 / AC-3: Test expected `"Hello, undefined!"` but default param returns `"Hello, stranger!"` — fixed test expectation
