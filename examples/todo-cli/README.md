# Lean Loop Example: `greet(name)` function

A complete walkthrough of one PLAN → APPLY → UNIFY cycle, showing what `.system/` files look like after each phase.

## The Task

Build a `greet(name)` function:
- `greet("World")` → `"Hello, World!"`
- `greet("Alice")` → `"Hello, Alice!"`
- `greet()` → `"Hello, stranger!"`

---

## Phase 1: PLAN

Open `.system/PLAN.md` and fill in:

```markdown
## Objective
Implement a `greet(name)` function that returns `Hello, {name}!`

## Acceptance Criteria
- **AC-1:** Given name="World", When greet() called, Then returns "Hello, World!"
- **AC-2:** Given name="Alice", When greet() called, Then returns "Hello, Alice!"
- **AC-3:** Given no name, When greet() called, Then returns "Hello, stranger!"

## Tasks
| Files        | Action                   | Depends | Verify                       | AC Ref |
|--------------|--------------------------|---------|------------------------------|--------|
| greet.js     | Create greet function    | None    | node -e "console.log(...)"   | AC-1   |
| greet.test.js| Write tests for all ACs  | greet.js| npx jest greet.test.js       | AC-1-3 |
```

### Gate Check

Run the AC Quality Checklist:

| AC  | Specific Input | Observable Action  | Verifiable Outcome          | Independent | No Leakage |
|-----|---------------|--------------------|-----------------------------|-------------|------------|
| AC-1| name="World"  | greet() called     | returns "Hello, World!"     | ✅          | ✅         |
| AC-2| name="Alice"  | greet() called     | returns "Hello, Alice!"     | ✅          | ✅         |
| AC-3| no name       | greet() called     | returns "Hello, stranger!"  | ✅          | ✅         |

All PASS → set `Status: APPROVED`.

**→ See full file: [`.system/PLAN.md`](.system/PLAN.md)**

---

## Phase 2: APPLY

### Cycle 1: AC-1 (RED → GREEN → REFACTOR)

**RED** — Write the failing test:

```js
// greet.test.js
const { greet } = require('./greet');

test('greet("World") returns "Hello, World!"', () => {
  expect(greet("World")).toBe("Hello, World!");
});
```

```
$ npx jest greet.test.js
FAIL  ./greet.test.js
  ✕ greet("World") returns "Hello, World!" (2 ms)

  TypeError: greet is not a function
```

Test fails. Console output confirms RED ✅

**GREEN** — Minimal code:

```js
// greet.js
function greet(name) {
  return `Hello, ${name}!`;
}

module.exports = { greet };
```

```
$ npx jest greet.test.js
PASS  ./greet.test.js
  ✓ greet("World") returns "Hello, World!" (1 ms)
```

**REFACTOR** — Nothing to refactor yet. Code is minimal.

### Cycle 2: AC-2

**RED:**
```js
test('greet("Alice") returns "Hello, Alice!"', () => {
  expect(greet("Alice")).toBe("Hello, Alice!");
});
```
```
PASS — already works because greet() is generic
```

This is expected — the implementation already handles any name. Green without additional code.

### Cycle 3: AC-3

**RED:**
```js
test('greet() with no name returns "Hello, stranger!"', () => {
  expect(greet()).toBe("Hello, stranger!");
});
```
```
FAIL
  Expected: "Hello, stranger!"
  Received: "Hello, undefined!"
```

**GREEN:**
```js
function greet(name = 'stranger') {
  return `Hello, ${name}!`;
}
```
```
PASS
  ✓ greet("World") returns "Hello, World!"
  ✓ greet("Alice") returns "Hello, Alice!"
  ✓ greet() returns "Hello, stranger!"
```

All 3 tests green. Done.

---

## Phase 3: UNIFY

Run the UNIFY command. Output:

```
=== UNIFY ===

1. TEST SUITE:
   PASS  ./greet.test.js
     ✓ greet("World") returns "Hello, World!" (1 ms)
     ✓ greet("Alice") returns "Hello, Alice!" (1 ms)
     ✓ greet() returns "Hello, stranger!" (1 ms)
   Tests: 3 passed, 3 total

2. AC VERIFICATION:
   AC-1: Given name="World", When greet() called, Then returns "Hello, World!" → ✅ pass
   AC-2: Given name="Alice", When greet() called, Then returns "Hello, Alice!" → ✅ pass
   AC-3: Given no name, When greet() called, Then returns "Hello, stranger!" → ✅ pass

3. PLAN vs ACTUAL:
   Planned: Implement greet(name) that returns "Hello, {name}!"
   Actually done: Created greet.js with default param, greet.test.js with 3 tests
   Files changed: greet.js, greet.test.js

4. DEBT / DEFERRED:
   - greet() does not validate input type (number silently coerces)

5. NEXT ACTION:
   Add `farewell(name)` function returning "Goodbye, {name}!"

Status: PASS → proceed to next PLAN
=== END UNIFY ===
```

### Updates applied

**STATE.md** — updated:
- Loop Position: UNIFY → PLAN
- Next Action: Write RED test for `farewell(name)`
- Progress Trace: AC-1 ✅, AC-2 ✅, AC-3 ✅

**LOG.md** — appended:
- Decision: used default param instead of explicit undefined check
- Debt: no input type validation
- Failure log: AC-3 initially expected `"Hello, undefined!"`, fixed test

**→ See full files:**
- [`.system/STATE.md`](.system/STATE.md)
- [`.system/LOG.md`](.system/LOG.md)

---

## Running this example

```bash
cd examples/todo-cli
npm install    # (if using jest)
npx jest
node -e "const {greet} = require('./greet'); console.log(greet('World'))"
# → Hello, World!
```

## Files in this example

```
examples/todo-cli/
├── .system/
│   ├── PLAN.md          # Plan with ACs and gate check (APPROVED)
│   ├── STATE.md         # After UNIFY: next action set
│   ├── LOG.md           # Decisions, debt, failure log
│   └── TDD_RULES.md     # TDD execution rules
├── greet.js             # Implementation (not written — follow the cycle!)
├── greet.test.js        # Tests (not written — follow the cycle!)
└── README.md            # This walkthrough
```

Try implementing it yourself! Delete `greet.js` and `greet.test.js`, follow the PLAN above, and run through the cycle.
