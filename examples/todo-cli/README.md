# Lean Loop Example: Todo CLI

A minimal example showing how Lean Loop's PLAN → APPLY → UNIFY cycle works on a real project.

## The Task

Build a simple `todo` CLI that can:
- Add a task
- List tasks
- Mark a task as done

## Cycle 1: Add a task

### PLAN.md

```
## Objective
Implement `todo add "Buy milk"` — stores the task in memory.

## Acceptance Criteria
- **AC1:** Given no tasks exist, When `add("Buy milk")` called, Then task list contains "Buy milk" with done=false
- **AC2:** Given task "Buy milk" exists, When `add("Walk dog")` called, Then task list has 2 items

## Tasks
| File        | Action | Depends | Verify           | AC  |
|-------------|--------|---------|------------------|-----|
| todo.js     | create | —       | node todo.js add | 1   |
| todo.test.js| create | todo.js | npm test         | 1,2 |
```

### APPLY (Red → Green → Refactor)

**RED:**
```js
// todo.test.js
const { add, list } = require('./todo');

test('add stores a task', () => {
  add('Buy milk');
  expect(list()).toEqual([{ text: 'Buy milk', done: false }]);
});
```
Run: `FAIL — add is not a function` ✓

**GREEN:**
```js
// todo.js
const tasks = [];

function add(text) {
  tasks.push({ text, done: false });
}

function list() {
  return [...tasks];
}

module.exports = { add, list };
```
Run: `PASS` ✓

**REFACTOR:** No refactor needed yet — minimal code.

### UNIFY

```
- **Planned:** Add function stores task in memory
- **Actually done:** add() and list() implemented with in-memory array
- **AC satisfied:** AC1 ✓, AC2 ✓
- **Deferred / Debt:** None
- **Next Action:** Implement `done` command
```

### STATE.md update

```
Phase: UNIFY
Next Action: Implement mark-as-done
Progress: 1/3 features complete
```

## Cycle 2 & 3

Follow the same pattern for `list` and `done` commands.

## Running the example

```bash
cd examples/todo-cli
npm install
npm test
node todo.js add "Buy milk"
node todo.js list
node todo.js done 0
```
