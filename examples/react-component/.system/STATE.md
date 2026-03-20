> **AI Instruction (Pruning):** If this file exceeds 100 lines, compress completed items in `Progress Trace` into a short summary.

# Project State

**Current Phase:** Feature: Toggle component
**Loop Position:** UNIFY
**Last Milestone:** Toggle component — all 5 ACs passing

## Next Action
- Build `<Select>` dropdown component

## Backlog (Max 3)
1. `<Select>` dropdown with keyboard navigation
2. `<Slider>` range input component
3. `<DatePicker>` calendar component

## Progress Trace
- [x] Toggle — on/off states (AC-1)
- [x] Toggle — click handler (AC-2, AC-3)
- [x] Toggle — keyboard a11y (AC-4)
- [x] Toggle — label support (AC-5)
- [ ] Select — dropdown

## Recent Decisions
- 2026-03-20: Used `<button>` instead of `<div role="switch">` — native keyboard support without extra ARIA
- 2026-03-20: Label via `<label htmlFor>` for screen reader association
