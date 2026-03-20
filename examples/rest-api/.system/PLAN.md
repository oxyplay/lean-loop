# Active Plan: POST /api/todos — Create Todo

**Objective:** Implement `POST /api/todos` endpoint that validates input, stores a todo, and returns it with 201 status.

## Acceptance Criteria (AC)
- **AC-1:** Given `{ "text": "Buy milk" }`, When `POST /api/todos`, Then response is 201 with `{ id, text, done: false }`
- **AC-2:** Given `{ "text": "" }`, When `POST /api/todos`, Then response is 400 with `{ error: "text is required" }`
- **AC-3:** Given `{ }`, When `POST /api/todos`, Then response is 400 with `{ error: "text is required" }`

## Boundaries
- **Do Not Change:** `package.json`, existing GET endpoint

## Tasks
| Files | Action | Depends | Verify | AC Ref |
|-------|--------|---------|--------|--------|
| `src/routes/todos.js` | Add POST handler | None | `curl -X POST ...` | AC-1 |
| `src/middleware/validate.js` | Create body validation | None | `jest validate.test.js` | AC-2, AC-3 |
| `src/routes/todos.test.js` | Integration tests | todos.js | `jest todos.test.js` | AC-1, AC-2, AC-3 |

## Gate Check (AC Quality)
| AC | Specific Input | Observable Action | Verifiable Outcome | Independent | No Leakage |
|----|---------------|-------------------|-------------------|-------------|------------|
| AC-1 | `{ text: "Buy milk" }` | POST /api/todos | 201 + `{ id, text, done: false }` | ✅ | ✅ |
| AC-2 | `{ text: "" }` | POST /api/todos | 400 + `{ error: "text is required" }` | ✅ | ✅ |
| AC-3 | `{ }` (empty body) | POST /api/todos | 400 + `{ error: "text is required" }` | ✅ | ✅ |

**Status:** APPROVED
