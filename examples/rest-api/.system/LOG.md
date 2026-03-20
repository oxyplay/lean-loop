> **AI Instruction (Pruning):** If this file exceeds 100 lines, compress only old closed `Deferred Issues` into one-line summaries.

# Decision & Debt Log

## Technical Decisions
- **D-001:** In-memory array for storage — acceptable for MVP, will need DB migration later
- **D-002:** Validation as middleware function — reusable across future endpoints

## Deferred Issues (Technical Debt)
- [ ] No persistence — todos lost on server restart
- [ ] No input sanitization (XSS via todo text)
- [ ] No rate limiting on POST

## Failure Log (Red Phase Post-Mortems)
- 2026-03-20 / AC-1: Test expected `id` to be a number, got UUID string — changed to check `typeof id === 'string'`
- 2026-03-20 / AC-2: Validation wasn't catching empty string — forgot to trim before checking length
