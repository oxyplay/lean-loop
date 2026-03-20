# Lean Loop

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skill](https://img.shields.io/badge/opencode-skill-purple)](https://opencode.ai)

A disciplined heartbeat cycle for AI-assisted and human-driven TDD development.

```
    PLAN ──────► APPLY ──────► UNIFY
     ▲                              │
     └──────────────────────────────┘
```

## Why Lean Loop?

AI coding assistants are powerful but chaotic. They write code fast, skip tests, lose context, and rarely reconcile what was planned vs. what was built. Lean Loop fixes that with three simple rules:

- **Plan before you code.** Define acceptance criteria before touching any file.
- **Test every behavior.** Strict Red-Green-Refactor, one test at a time.
- **Reconcile every cycle.** Compare plan vs. actual, log decisions, update state.

The result: predictable, auditable, test-covered development — whether you're working solo, with a team, or alongside an AI.

## 1. Beginner-Friendly Onboarding: Your First Loop

Let's walk through your first complete Lean Loop cycle together. We'll build a simple `greet(name)` function that returns a greeting message. This tutorial takes about 5-10 minutes and requires no prior setup beyond having Node.js installed.

### Step 1: Initialize Lean Loop in Your Project

First, let's create a new project folder and set up Lean Loop:

```bash
mkdir my-first-loop && cd my-first-loop
npm init -y  # Creates a basic package.json
npx skills add oxyplay/lean-loop -g  # Installs the Lean Loop skill
```

This automatically creates a `.system/` folder with all the tracking files we need.

### Step 2: PLAN Phase - Define What We're Building

Open `.system/PLAN.md` in your editor and replace the content with:

```markdown
# Objective
Add a `greet(name)` function that returns `Hello, {name}!`

## Acceptance Criteria
Given name="World"
When greet() is called
Then it returns "Hello, World!"

## Tasks
- [ ] Create greet.js with the function
- [ ] Write a test that fails (RED)
- [ ] Make the test pass (GREEN)
- [ ] Improve the code if needed (REFACTOR)
- [ ] Update STATE.md with what we learned
```

### Step 3: APPLY Phase - Red-Green-Refactor

Now let's follow the TDD cycle:

#### RED: Write a Failing Test

Create a file called `test/greet.test.js` with this content:

```javascript
const { greet } = require('../greet');

test('greets World correctly', () => {
  expect(greet('World')).toBe('Hello, World!');
});
```

Run the test to see it fail (this is the RED phase):
```bash
npm test
# You should see a failure because greet.js doesn't exist yet
```

#### GREEN: Make It Pass

Create `greet.js` with the minimal code to make the test pass:

```javascript
function greet(name) {
  return `Hello, ${name}!`;
}

module.exports = { greet };
```

Run the test again:
```bash
npm test
# Now you should see the test pass! This is the GREEN phase.
```

#### REFACTOR: Improve the Design

Look at your code. Is it clear and simple? In this case, it's already good, so we can move on. (If we saw duplication or complexity, we'd improve it now while keeping the test green.)

### Step 4: UNIFY Phase - Reconcile and Reflect

Now we complete the loop by updating our tracking files:

1. **Check that all tests pass**: We already did this with `npm test`
2. **Verify acceptance criteria**: Our test confirms that given "World", we get "Hello, World!"
3. **Update `.system/STATE.md`**:

```markdown
# Current Phase
PLAN (we just completed a full loop)

# Next Action
Consider adding more test cases or move on to another feature

# What We Did
- Created greet.js function that returns a greeting
- Wrote and passed a test for the basic case
- Followed Red-Green-Refactor cycle

# Decisions & Debt
- No technical debt incurred
- Decision to keep the function simple and focused
```

4. **Log the cycle in `.system/LOG.md`**:
```markdown
## Loop Completed: [timestamp]
- Planned: Add greet(name) function returning Hello, {name}!
- Actually done: Created greet.js with one test covering the basic case
- AC satisfied: Yes - given "World", returns "Hello, World!"
- Deferred / Debt: None
- Next Action: Consider adding edge case tests (empty string, special characters)
```

### Step 5: Repeat the Loop

Now that you've completed one full PLAN → APPLY → UNIFY cycle, you can start another! Try adding a second test case:

1. Go back to `.system/PLAN.md` and add a new acceptance criterion
2. Write the failing test (RED)
3. Make it pass (GREEN)
4. Refactor if needed
5. Update STATE.md and LOG.md

## Quick Start (For Experienced Users)

If you just want to get started quickly:

### Install as an opencode skill

```bash
npx skills add oxyplay/lean-loop -g
```

The skill auto-creates `.system/` tracking files in your project on first use.

### Your first loop (60 seconds)

1. Open `.system/PLAN.md` and write:
   - **Objective:** "Add a `greet(name)` function that returns `Hello, {name}!`"
   - **AC:** `Given name="World", When greet() called, Then returns "Hello, World!"`
2. Open `.system/TDD_RULES.md` — follow Red-Green-Refactor
3. Write one failing test → make it green → refactor
4. Open `.system/STATE.md` — update phase, log what you did, set next action
5. Repeat

## The Heartbeat

Operational state lives in the `.system/` folder.

```mermaid
graph LR
    PLAN["PLAN<br/><i>Define objective,<br/>write ACs, break tasks</i>"]
    APPLY["APPLY<br/><i>Red → Green → Refactor<br/>one behavior at a time</i>"]
    UNIFY["UNIFY<br/><i>Reconcile plan vs actual,<br/>update state, log decisions</i>"]
    PLAN --> APPLY --> UNIFY --> PLAN
```

### Phase 1: PLAN

Fill in `.system/PLAN.md` with objective, Given/When/Then acceptance criteria, boundaries, and task breakdown.

> **Gate:** If ACs are unclear, contradictory, or untestable — stop and refine. Do not proceed to APPLY.

### Phase 2: APPLY

Execute Red-Green-Refactor cycles strictly:

1. **RED** — Write ONE failing test. Confirm with actual console output.
2. **GREEN** — Minimal code to pass. No future-proofing.
3. **REFACTOR** — Improve design only when green.

> **Rule:** If work expands beyond original ACs — stop and return to PLAN.

### Phase 3: UNIFY

Mandatory reconciliation after every APPLY session:

1. All tests green? Run the full suite.
2. All ACs satisfied? Check each one explicitly.
3. Update `.system/STATE.md` with current phase and next action.
4. Log decisions and debt in `.system/LOG.md`.
5. Compare planned vs. actually done.

```
- **Planned:** [what you set out to do]
- **Actually done:** [what changed]
- **AC satisfied:** [each AC and whether met]
- **Deferred / Debt:** [if any]
- **Next Action:** [exactly one task]
```

## Project Structure

```
your-project/
├── .system/
│   ├── PLAN.md          # Active plan with ACs and tasks
│   ├── STATE.md         # Current phase, next action, backlog
│   ├── LOG.md           # Decisions, debt, and failure log
│   └── TDD_RULES.md     # Red-Green-Refactor execution rules
└── ...
```

## Philosophy

- **In-Session Context** — All work happens in the main session. No subagent handoffs during implementation.
- **Vertical Slicing** — Build one behavior end-to-end (Tracer Bullets), not horizontal layers.
- **Acceptance-Driven** — Define "Done" via clear criteria before writing code.
- **Behavior-First TDD** — Test public interfaces, not internal implementation.
- **Deep Modules** — Small public interfaces that hide complex internals.

## When to Break TDD

Rare exceptions, all must be logged in `.system/LOG.md`:

- **Hotfixes** — production bugs requiring immediate recovery
- **Legacy Code** — too tightly coupled for test-first approach
- **Spikes** — exploratory code, will be thrown away

## Examples

Each example includes real `.system/` files showing the exact state after PLAN, APPLY, and UNIFY phases.

| Example | Stack | What it builds |
|---------|-------|---------------|
| [greet(name)](examples/todo-cli/) | Node.js | Simple function — your first loop |
| [POST /api/todos](examples/rest-api/) | Express + Jest | REST endpoint with validation |
| [Toggle component](examples/react-component/) | React + RTL | Accessible UI component |

Browse all: [`examples/`](examples/)

## Integrations

Lean Loop works with any AI coding tool. Drop-in configs for your stack:

| Tool | Setup | File |
|------|-------|------|
| **opencode** | `npx skills add oxyplay/lean-loop -g` | [SKILL.md](skills/lean-loop/SKILL.md) |
| **Claude Code** | Copy `CLAUDE.md` to project root | [integrations/claude-code/](integrations/claude-code/) |
| **Cursor** | Copy `.cursorrules` to project root | [integrations/cursor/](integrations/cursor/) |

See [`integrations/`](integrations/) for setup instructions.

## FAQ

**Q: Do I need opencode to use this?**
A: No. The `.system/` templates work with any editor. The opencode skill just auto-initializes them.

**Q: Can I use this with my team?**
A: Yes. Commit `.system/` to your repo. Everyone shares the same plan, state, and decision log.

**Q: What if my project already has tests?**
A: Lean Loop works alongside existing test suites. Use it for new features and incremental improvements.

**Q: Is this only for AI-assisted development?**
A: No. The PLAN → APPLY → UNIFY cycle works for human-only teams too. AI just makes the discipline easier to maintain.

## References

- [The Pragmatic Programmer](https://pragprog.com/titles/tpp20/) — Tracer Bullets concept
- [A Philosophy of Software Design](https://www.amazon.com/Philosophy-Software-Design-John-Ousterhout/dp/1732102201) — Deep Modules
- [Test-Driven Development: By Example](https://www.amazon.com/Test-Driven-Development-Kent-Beck/dp/0321146530) — Kent Beck's TDD approach

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

[MIT](LICENSE) © 2026 Max