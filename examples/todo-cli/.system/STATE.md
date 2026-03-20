> **AI Instruction (Pruning):** If this file exceeds 100 lines, compress completed items in `Progress Trace` into a short summary. Keep `Recent Decisions` as complete as possible unless absolutely necessary to compress.

# Project State

**Current Phase:** Feature: greet function
**Loop Position:** UNIFY
**Last Milestone:** greet() implemented with 3 ACs passing

## Next Action
- Write the RED test for AC-1: confirm `greet("World")` returns `"Hello, World!"`

## Backlog (Max 3)
1. Add `farewell(name)` function
2. Add input validation (non-string rejection)
3. Export as npm module

## Progress Trace
- [x] AC-1: greet("World") returns "Hello, World!"
- [x] AC-2: greet("Alice") returns "Hello, Alice!"
- [x] AC-3: greet() returns "Hello, stranger!"
- [ ] farewell() function

## Recent Decisions
- 2026-03-20: Used default parameter `name = 'stranger'` instead of explicit check for cleaner code
