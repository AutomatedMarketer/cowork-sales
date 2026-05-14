# Phase 4 — Trigger and Offer

**Time budget:** 2 min

## What you read first (lazy-load)
- `about-me/business-brain.md` (offer section only — look for `## Offer` or `## What I sell`)
- `projects/sales/sales-preferences.md` (to append to)

## What to do

### Step A — Trigger time

### Ask (Step A):
> "What time of day do you want the daily ritual to fire? I'll default to **3pm** if you just hit enter."

### Then (Step A):
- Accept any valid time (e.g., "9am", "14:00", "after lunch").
- Normalize to HH:MM 24h format for storage.
- Default = 15:00 if user skips or types "default".

---

### Step B — Offer snapshot (value check)

### Ask (Step B):
> "Quick check on your offer — I want to make sure your daily brief frames it right. Answer these fast:
>
> 1. **Dream outcome**: What result does your client get? *(e.g., 'closes 3 more deals a month')*
> 2. **Likelihood**: How confident are they it'll work? *(1 = no trust, 10 = absolute certainty)*
> 3. **Time to result**: How long until they see it? *(e.g., '30 days', '3 months')*
> 4. **Effort required**: How hard is it for them? *(e.g., 'just show up', '10 hrs/week')*"

### Then (Step B):
- Accept answers in any format (sentence, list, short phrases).
- Do NOT score or grade the offer — just capture it.
- If any field is blank → leave it as `<not specified>` in storage.
- Synthesize into a 1–2 sentence offer snapshot for the sales brief: "[Dream outcome] for [audience], in [time], with [effort level]."

### Write:
`projects/sales/sales-preferences.md` — add or update:
```yaml
trigger_time: "15:00"  # HH:MM 24h
offer_snapshot:
  dream_outcome: <user answer>
  perceived_likelihood: <1-10>
  time_to_result: <user answer>
  effort_sacrifice: <user answer>
  synthesized: "<1-2 sentence summary>"
```

### Update state:
Set `current_phase: 5` and `p4: ✓` in `_aibos/state-sales.md`.

## Common failure modes
| Scenario | Recovery |
|---|---|
| User skips the value check entirely | Accept skip — set all offer_snapshot fields to `<not specified>`. Note `p4_offer_skipped: true` in state. The daily brief will use the raw offer text from business-brain.md instead. |
| User gives a likelihood of 1 or 2 | Note it but do not comment — that's for them to work on outside this wizard. |
| User gives time like "eventually" or "never" | Accept verbatim — store as-is. |
| User changes their mind on trigger time later | They can update sales-preferences.md directly or re-run this phase. |

## Next
→ Phase 5 via `phases/05-network-gate.md`
