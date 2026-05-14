# Phase 1 — Welcome

**Time budget:** 1 min

## What you read first (lazy-load)
- `about-me/about-me.md`
- `about-me/business-brain.md`
- `about-me/connections.md`
- `checks/identity-files-present.md`
- `checks/business-brain-not-empty.md`

## What to do

### Pre-flight checks (run before Ask)
1. Run `checks/identity-files-present.md` — halt immediately if any file is missing or empty.
2. Run `checks/business-brain-not-empty.md` — halt immediately if any required section is missing.

### Ask:
> "Hey! Quick check before we start — I see you're a **[role from about-me.md]** selling **[offer from business-brain.md]** to **[audience from business-brain.md]**. Today we're turning that into a daily sales rhythm you'll actually do. Takes about 13 minutes. Ready to go?"

### Then:
- Wait for yes (any positive confirmation).
- If user corrects any detail in the summary → note the correction but do NOT rewrite about-me or business-brain now. Log the note in state-sales.md under `p1_corrections`. Tell the user: "Noted — update that in business-brain.md when we're done. For now let's keep moving."
- If user says no or not now → say "No problem. Come back when you're ready and we'll pick up here." Then stop.

### Write:
`_aibos/state-sales.md` — create or update with:
```
current_phase: 2
phases_complete:
  p1: ✓
p1_corrections: <any corrections noted, or "none">
```

### Update state:
Set `current_phase: 2` in `_aibos/state-sales.md`.

## Common failure modes
| Scenario | Recovery |
|---|---|
| `about-me.md` missing | HALT — "Run `/onboard` from cowork-ai-os first. I need your identity files before I can set up your sales ritual." |
| `business-brain.md` missing | HALT — "Fill business-brain.md via `/onboard` Phase 3, then come back here." |
| `business-brain.md` present but missing Role/Audience/Offer sections | HALT — "Your business-brain is missing [section]. Fill it in via `/onboard` Phase 3, then come back." |
| `connections.md` missing | HALT — "Run `/onboard` from cowork-ai-os first to set up your connections file." |
| User is mid-wizard (state shows current_phase > 1) | Resume from that phase instead — say "Looks like we got partway through. Picking up at Phase [N]." |

## Next
→ Phase 2 via `phases/02-channels.md`
