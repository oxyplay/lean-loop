# Lean Loop Example: REST API (Express)

A full PLAN → APPLY → UNIFY cycle for building a `POST /api/todos` endpoint with input validation.

## The Task

Add a POST endpoint to an Express todo API:
- Valid body `{ "text": "Buy milk" }` → 201 + created todo
- Empty text → 400 error
- Missing text field → 400 error

---

## Phase 1: PLAN

**Objective:** Implement `POST /api/todos` with validation.

**ACs:**
- AC-1: `{ "text": "Buy milk" }` → 201 + `{ id, text, done: false }`
- AC-2: `{ "text": "" }` → 400 + `{ error: "text is required" }`
- AC-3: `{ }` → 400 + `{ error: "text is required" }`

**Gate check** — all 3 ACs pass the 5-point checklist:

| AC  | Specific Input | Observable Action | Verifiable Outcome | Independent | No Leakage |
|-----|---------------|-------------------|-------------------|-------------|------------|
| AC-1| `{ text: "Buy milk" }` | POST /api/todos | 201 + body | ✅ | ✅ |
| AC-2| `{ text: "" }` | POST /api/todos | 400 + error | ✅ | ✅ |
| AC-3| `{ }` | POST /api/todos | 400 + error | ✅ | ✅ |

All PASS → `Status: APPROVED`

**→ See full: [`.system/PLAN.md`](.system/PLAN.md)**

---

## Phase 2: APPLY

### Cycle 1: AC-1 — POST with valid body

**RED:**
```js
// todos.test.js
const request = require('supertest');
const app = require('./app');

test('POST /api/todos creates a todo', async () => {
  const res = await request(app)
    .post('/api/todos')
    .send({ text: 'Buy milk' });

  expect(res.status).toBe(201);
  expect(res.body).toMatchObject({ text: 'Buy milk', done: false });
  expect(res.body.id).toBeDefined();
});
```

```
$ npx jest todos.test.js
FAIL
  Expected: 201
  Received: 404
```

RED confirmed ✅

**GREEN:**
```js
// In app.js — add route
let todos = [];
let nextId = 1;

app.post('/api/todos', (req, res) => {
  const todo = { id: String(nextId++), text: req.body.text, done: false };
  todos.push(todo);
  res.status(201).json(todo);
});
```

```
PASS  ✓ POST /api/todos creates a todo (15 ms)
```

### Cycle 2: AC-2 — Empty text rejected

**RED:**
```js
test('POST /api/todos rejects empty text', async () => {
  const res = await request(app)
    .post('/api/todos')
    .send({ text: '' });

  expect(res.status).toBe(400);
  expect(res.body).toEqual({ error: 'text is required' });
});
```

```
FAIL
  Expected: 400
  Received: 201
```

**GREEN:**
```js
app.post('/api/todos', (req, res) => {
  if (!req.body.text || !req.body.text.trim()) {
    return res.status(400).json({ error: 'text is required' });
  }
  // ... existing creation logic
});
```

```
PASS  ✓ POST /api/todos creates a todo
      ✓ POST /api/todos rejects empty text
```

### Cycle 3: AC-3 — Missing text field

**RED:**
```js
test('POST /api/todos rejects missing text', async () => {
  const res = await request(app)
    .post('/api/todos')
    .send({});

  expect(res.status).toBe(400);
  expect(res.body).toEqual({ error: 'text is required' });
});
```

```
FAIL
  Expected: 400
  Received: 201
```

**GREEN:**
Already works — `!req.body.text` catches `undefined`. No code change needed.

```
PASS  ✓ POST /api/todos creates a todo
      ✓ POST /api/todos rejects empty text
      ✓ POST /api/todos rejects missing text
```

### REFACTOR

Extract validation to middleware:

```js
// src/middleware/validate.js
function validateTodoBody(req, res, next) {
  if (!req.body.text || !req.body.text.trim()) {
    return res.status(400).json({ error: 'text is required' });
  }
  next();
}
```

Tests still pass. Clean.

---

## Phase 3: UNIFY

```
=== UNIFY ===

1. TEST SUITE:
   PASS  ./todos.test.js
     ✓ POST /api/todos creates a todo (15 ms)
     ✓ POST /api/todos rejects empty text (8 ms)
     ✓ POST /api/todos rejects missing text (5 ms)
   Tests: 3 passed, 3 total

2. AC VERIFICATION:
   AC-1: Given { text: "Buy milk" }, When POST, Then 201 + { id, text, done } → ✅
   AC-2: Given { text: "" }, When POST, Then 400 + { error } → ✅
   AC-3: Given { }, When POST, Then 400 + { error } → ✅

3. PLAN vs ACTUAL:
   Planned: POST endpoint with validation
   Actually done: POST + validation middleware extracted for reuse
   Files changed: app.js, src/middleware/validate.js, todos.test.js

4. DEBT / DEFERRED:
   - No persistence (in-memory only)
   - No input sanitization (XSS risk)
   - No rate limiting

5. NEXT ACTION:
   Implement GET /api/todos — list all todos

Status: PASS → proceed to next PLAN
=== END UNIFY ===
```

**→ See full: [`.system/STATE.md`](.system/STATE.md) | [`.system/LOG.md`](.system/LOG.md)**

---

## Files in this example

```
examples/rest-api/
├── .system/
│   ├── PLAN.md          # Plan with 3 ACs + gate check (APPROVED)
│   ├── STATE.md         # After UNIFY: next action = GET /api/todos
│   ├── LOG.md           # 2 decisions, 3 debt items, 2 failure logs
│   └── TDD_RULES.md     # Execution rules
└── README.md            # This walkthrough
```
