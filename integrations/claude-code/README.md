# Lean Loop — Claude Code Integration

## Setup

1. Copy `.system/` to your project root:
   ```bash
   cp -r path/to/lean-loop/.system/ /your/project/.system/
   ```

2. Copy this file as `CLAUDE.md` in your project root:
   ```bash
   cp path/to/lean-loop/integrations/claude-code/CLAUDE.md /your/project/CLAUDE.md
   ```

3. Claude Code will read `CLAUDE.md` automatically on every session.

## What this does

Claude Code follows the PLAN → APPLY → UNIFY cycle with:
- Gate-checked acceptance criteria before coding
- Strict Red-Green-Refactor with console confirmation
- Mandatory UNIFY with structured output
- `.system/` state tracking between sessions
