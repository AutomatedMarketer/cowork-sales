---
name: dream-100
description: "The relationship engine. Helps you cultivate 100 deliberate relationships with people whose audiences match your ICP. Two modes — Build (if your list is empty, helps you start) or Operate (if you have 5+ names, surfaces touches and enforces give-2x-before-ask). Data-driven mode switching."
---

# /dream-100

You manage the user's Top 100 list. Mode is decided by FILE STATE, not flags.

## Architectural foundations (non-negotiable)

1. **Lazy-load.** Read `projects/sales/dream-100.md` to determine mode. Then load ONLY the mode-specific file (`modes/build-mode.md` OR `modes/operate-mode.md`).
2. **Self-improve.** End with: "What would've made this session 10% better?" Append to `skill-memory.md`.
3. **Actionable.** Output ends with `Next move:` block — specific person + specific action + specific timing.

## Mode detection (read first)

Read `projects/sales/dream-100.md`. Count the rows of populated names.

| File state | Mode | Load |
|---|---|---|
| File missing OR 0-4 names | **Build mode** | `modes/build-mode.md` |
| 5-99 names | **Operate mode** | `modes/operate-mode.md` |
| 100+ names | **Operate mode + prune** | `modes/operate-mode.md` + `modes/prune-prompt.md` |

## Subcommands

- `/dream-100` (no args) → run in detected mode
- `/dream-100 add` → force Build mode (helpful if user wants to add names mid-operate)
- `/dream-100 prune` → force prune prompt
- `/dream-100 reset` → archive current list to `archive/dream-100-<YYYY-MM-DD>.md`, start fresh

## Hard rule: give-2x-before-ask

The skill REFUSES to draft an "ask" message for a person if their contribution log shows < 2 recent gives. Load `templates/ask-blocker.md` for the rejection message.

## Loose coupling with sister plugins

- If `cowork-research` is detected → for any new Top 100 candidate, offer "Run `/research-brief` on this person?" before adding
- If `cowork-obsidian` is detected → mirror dream-100.md changes to `wiki/sales/dream-100.md`
