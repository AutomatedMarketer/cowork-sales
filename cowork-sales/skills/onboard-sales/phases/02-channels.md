# Phase 2 — Channels

**Time budget:** 2 min

## What you read first (lazy-load)
- `channels/_index.md`
- `personalization/_classifier.md`
- The `personalization/profile-NN.md` that matches the user's business type (determined by classifier — do NOT load all profiles upfront)

## What to do

### Pre-flight check
Run `checks/business-brain-not-empty.md` before applying the classifier.

### Then (before Ask):
1. Read `channels/_index.md` to get the full 8-channel list.
2. Read `personalization/_classifier.md` — apply its scoring rules against business-brain.md content (role, audience, offer).
3. Identify the top-matching profile (e.g., `profile-03.md`) and read ONLY that file.
4. From the profile, extract the 2 recommended primary channels (the "smart suggestion").
5. Prepare the full 8-channel menu for display.

### Ask:
> "Based on your business, I'd suggest **[Channel #X — name]** and **[Channel #Y — name]** as your starting channels. But here's the full list — pick the 1 or 2 that actually fit how you work:
>
> 1. [Channel name + 1-line description]
> 2. [Channel name + 1-line description]
> 3. [Channel name + 1-line description]
> 4. [Channel name + 1-line description]
> 5. [Channel name + 1-line description]
> 6. [Channel name + 1-line description]
> 7. [Channel name + 1-line description]
> 8. [Channel name + 1-line description]
>
> Which 1–2 feel right for you?"

### Cap enforcement:
- If user picks exactly 1 or 2 → accept.
- If user picks 3 or more → push back once: "For day-1 success, I'd really push you to pick just 2. More channels = scattered energy. Which 2 feel strongest?"
- If user insists on 3 after pushback → accept 3 with a note: log `p2_override: true` in state-sales.md.
- Never accept more than 3.

### Write:
`projects/sales/sales-preferences.md` — create or update the channels section:
```yaml
channels:
  primary:
    - id: <channel-id>
      name: <channel-name>
    - id: <channel-id>
      name: <channel-name>
  smart_suggestion_was: [<id1>, <id2>]
  user_override: <true|false>
```

### Update state:
Set `current_phase: 3` and `p2: ✓` in `_aibos/state-sales.md`.

## Common failure modes
| Scenario | Recovery |
|---|---|
| Classifier can't determine business type | Default to top 2 channels by general-purpose score in `_index.md`. Note `p2_classifier_fallback: true` in state. |
| User picks 0 channels | Re-ask: "You need at least 1 to build a ritual. Which channel is where your best clients actually are?" |
| Channel #07 is among user's picks | Note it in state-sales.md as `p2_network_channel: true` — Phase 5 will use this to auto-fill the network gate. |

## Next
→ Phase 3 via `phases/03-tactics.md`
