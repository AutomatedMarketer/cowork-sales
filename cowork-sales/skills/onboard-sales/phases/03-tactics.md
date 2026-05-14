# Phase 3 — Tactics

**Time budget:** 2 min

## What you read first (lazy-load)
- `channels/<id>.md` for EACH channel the user picked in Phase 2 (load only those files, nothing else)
- `projects/sales/sales-preferences.md` (to retrieve the Phase 2 channel picks)

## What to do

### Then (before Ask):
1. Read `sales-preferences.md` to get the user's chosen channel IDs.
2. For each chosen channel, read `channels/<channel-id>.md`.
3. Extract the "Suggested tactics" section from each channel file.
4. Merge and de-duplicate tactics across channels (if user picked 2 channels with overlapping tactics, list each tactic once).
5. Rank by effort-to-impact ratio — lowest effort first.
6. Prepare the auto-fill list (max 5 tactics total).

### Ask:
> "Here are the tactics I'd auto-pick from your channels:
>
> - [Tactic 1 — channel source]
> - [Tactic 2 — channel source]
> - [Tactic 3 — channel source]
> *(+ [N] more if applicable)*
>
> These are the ones with the best effort-to-impact ratio for your setup. Look good, or want to swap any out?"

### Tactic swap flow:
- If user says "looks good" → accept all auto-picks.
- If user wants to swap → show the full tactic list from the loaded channel files and let them pick.
- If user wants to add a tactic not on the list → accept it verbatim. Note `p3_custom_tactic: true` in state.
- Minimum 1 tactic, maximum 5 tactics total.

### Write:
`projects/sales/sales-preferences.md` — add or update the daily_tactics section:
```yaml
daily_tactics:
  - tactic: <tactic name>
    channel: <channel-id>
    source: auto-pick | user-swap | user-custom
  - tactic: <tactic name>
    channel: <channel-id>
    source: auto-pick | user-swap | user-custom
```

### Update state:
Set `current_phase: 4` and `p3: ✓` in `_aibos/state-sales.md`.

## Common failure modes
| Scenario | Recovery |
|---|---|
| Channel file has no "Suggested tactics" section | Use the channel's top-level description to infer 2 generic tactics. Note `p3_tactic_inferred: true` in state. |
| User rejects all auto-picks and picks nothing | Re-ask: "Pick at least 1 tactic — even if it's just 'send 1 message to a warm lead today'." |
| User wants more than 5 tactics | Push back: "5 is the daily max — more than that and nothing gets done consistently. Pick your top 5." |

## Next
→ Phase 4 via `phases/04-trigger-and-offer.md`
