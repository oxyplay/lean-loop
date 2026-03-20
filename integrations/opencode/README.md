# Lean Loop — opencode Integration

## Setup

```bash
npx skills add oxyplay/lean-loop -g
```

The skill auto-creates `.system/` tracking files on first use.

## What this does

opencode loads Lean Loop as a skill with:
- Auto-initialization of `.system/` from bundled templates
- SKILL.md with full methodology, anti-patterns, exceptions
- Trigger words: "lean loop", "tdd workflow", "plan then code", "acceptance criteria"

## How to use

Just start coding. When you say things like:
- "Let's plan this feature"
- "Run TDD on this"
- "Do acceptance criteria"
- "Run UNIFY"

opencode will follow the PLAN → APPLY → UNIFY cycle automatically.

## Customization

Edit `.system/TDD_RULES.md` to add project-specific rules.
Edit `.system/PLAN.md` template to match your team's AC format.
