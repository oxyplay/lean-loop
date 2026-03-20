# Active Plan: Toggle Switch Component

**Objective:** Build a controlled `<Toggle>` component with on/off states, keyboard accessibility, and label support.

## Acceptance Criteria (AC)
- **AC-1:** Given `checked={false}`, When rendered, Then shows "off" state visually
- **AC-2:** Given `checked={false}`, When clicked, Then calls `onChange(true)`
- **AC-3:** Given `checked={true}`, When clicked, Then calls `onChange(false)`
- **AC-4:** Given focus on toggle, When Space key pressed, Then toggles state
- **AC-5:** Given `label="Dark mode"`, When rendered, Then label text visible next to toggle

## Boundaries
- **Do Not Change:** existing Button, Input components

## Tasks
| Files | Action | Depends | Verify | AC Ref |
|-------|--------|---------|--------|--------|
| `Toggle.jsx` | Create component | None | Render in test | AC-1, AC-2, AC-3 |
| `Toggle.test.jsx` | Unit tests with RTL | Toggle.jsx | `npx jest Toggle` | AC-1-5 |
| `Toggle.css` | Styling (on/off visual) | Toggle.jsx | Visual check | AC-1 |

## Gate Check (AC Quality)
| AC | Specific Input | Observable Action | Verifiable Outcome | Independent | No Leakage |
|----|---------------|-------------------|-------------------|-------------|------------|
| AC-1 | checked=false | renders | has "off" visual state | ✅ | ✅ |
| AC-2 | checked=false | user.click() | onChange(true) called | ✅ | ✅ |
| AC-3 | checked=true | user.click() | onChange(false) called | ✅ | ✅ |
| AC-4 | focused | Space key | toggles state | ✅ | ✅ |
| AC-5 | label="Dark mode" | renders | label text in DOM | ✅ | ✅ |

**Status:** APPROVED
