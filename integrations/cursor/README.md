# Lean Loop — Cursor Integration

## Setup

1. Copy `.system/` to your project root:
   ```bash
   cp -r path/to/lean-loop/.system/ /your/project/.system/
   ```

2. Copy `.cursorrules` to your project root:
   ```bash
   cp path/to/lean-loop/integrations/cursor/.cursorrules /your/project/.cursorrules
   ```

3. Cursor reads `.cursorrules` automatically for all AI interactions.

## What this does

Cursor's AI follows the PLAN → APPLY → UNIFY cycle with:
- Gate-checked acceptance criteria before coding
- Strict Red-Green-Refactor with console confirmation
- Mandatory UNIFY with structured output
- `.system/` state tracking between sessions
