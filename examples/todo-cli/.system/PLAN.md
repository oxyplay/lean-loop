# Active Plan: Add `greet(name)` function

**Objective:** Implement a `greet(name)` function that returns `Hello, {name}!`

## Acceptance Criteria (AC)
- **AC-1:** Given name="World", When `greet()` called, Then returns `"Hello, World!"`
- **AC-2:** Given name="Alice", When `greet()` called, Then returns `"Hello, Alice!"`
- **AC-3:** Given no name, When `greet()` called, Then returns `"Hello, stranger!"`

## Boundaries
- **Do Not Change:** `package.json`

## Tasks
| Files | Action | Depends | Verify | AC Ref |
|-------|--------|---------|--------|--------|
| `greet.js` | Create module with greet function | None | `node -e "console.log(require('./greet').greet('World'))"` | AC-1 |
| `greet.test.js` | Write tests for all 3 ACs | greet.js | `npx jest greet.test.js` | AC-1, AC-2, AC-3 |

## Gate Check (all must pass)
| AC | Specific Input | Observable Action | Verifiable Outcome | Independent | No Leakage |
|----|---------------|-------------------|-------------------|-------------|------------|
| AC-1 | name="World" | greet() called | returns "Hello, World!" | ✅ | ✅ |
| AC-2 | name="Alice" | greet() called | returns "Hello, Alice!" | ✅ | ✅ |
| AC-3 | no name | greet() called | returns "Hello, stranger!" | ✅ | ✅ |

**Status:** APPROVED
