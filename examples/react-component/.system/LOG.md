> **AI Instruction (Pruning):** If this file exceeds 100 lines, compress only old closed `Deferred Issues` into one-line summaries.

# Decision & Debt Log

## Technical Decisions
- **D-001:** Used `<button>` over `<div role="switch">` — native keyboard support, no custom keydown handler needed for Space/Enter
- **D-002:** CSS-only visual states (no JS class toggling for animation) — simpler, more performant

## Deferred Issues (Technical Debt)
- [ ] No `aria-checked` attribute (relying on button pressed state)
- [ ] No disabled state support
- [ ] No size variants (small/medium/large)

## Failure Log (Red Phase Post-Mortems)
- 2026-03-20 / AC-4: Space key wasn't toggling — was testing on `<div>` not `<button>`, switched to button
- 2026-03-20 / AC-5: Label not linked — forgot `htmlFor` attribute on label element
