# Phase 5 — Network Gate

**Time budget:** 2 min

## What you read first (lazy-load)
- `projects/sales/sales-preferences.md` (check `channels.primary` for Channel #07)

## What to do

### Auto-fill check (run BEFORE Ask):
1. Read `sales-preferences.md` — check if any entry in `channels.primary` has `id: channel-07` (or equivalent network/referral channel ID from `channels/_index.md`).
2. If Channel #07 is in the primary list → set `network_status: yes` automatically. Skip the yes/no ask below. Jump directly to "Name your 5-10" ask.
3. If Channel #07 is NOT in the primary list → proceed with the standard yes/no ask.

---

### Ask (standard path — Channel #07 NOT picked):
> "Do you have 5+ peers, podcasters, influencers, or list-owners in your network whose audiences match your ideal client? Think: people who already have your buyers' attention."

### Then (standard path):
- If **Yes** → proceed to "Name your 5-10" ask below.
- If **No** → say "No problem — that channel requires a warm network to work. We'll skip it for now. You can add it later when you've built those relationships." Set `network_status: no` in sales-preferences.md. Do NOT create dream-100.md. Move to Phase 6.

---

### Ask (if Yes or auto-fill from Channel #07):
> "Name 5–10 of them now — just their name and where they have an audience. I'll seed your dream-100 list."
>
> *(Examples: "Jane Doe — newsletter 10k subs", "TechPodcast — 50k listeners", "Mike Smith — LinkedIn 8k followers")*

### Then:
- Accept the list in any format.
- Parse into name + platform/channel pairs.
- Create `projects/sales/dream-100.md` with the seeded list.

### Write (if network_status = yes):
`projects/sales/dream-100.md`:
```markdown
# Dream 100

Seeded: <YYYY-MM-DD>

| Name | Platform / Audience | Status | Notes |
|---|---|---|---|
| <name> | <platform> | Identified | |
| <name> | <platform> | Identified | |
```

`projects/sales/sales-preferences.md` — add:
```yaml
network_status: yes
dream_100_seeded: true
dream_100_count: <N>
```

### Write (if network_status = no):
`projects/sales/sales-preferences.md` — add:
```yaml
network_status: no
dream_100_seeded: false
```

Do NOT create `dream-100.md`.

### Update state:
Set `current_phase: 6` and `p5: ✓` in `_aibos/state-sales.md`.
Also log `p5_network_status: yes|no` and `p5_auto_filled: true|false`.

## Common failure modes
| Scenario | Recovery |
|---|---|
| User names fewer than 5 people | Accept what they have. Note `dream_100_count: <actual count>` in state. Say: "You can add more later by editing dream-100.md directly." |
| User names more than 10 | Accept all of them — no cap on the dream-100 list itself. |
| User says yes but then can't name anyone | Treat as No — set network_status: no, skip dream-100.md creation. Say: "No problem — brainstorm them later and add manually to dream-100.md." |
| Channel #07 auto-fill fires but user says "I don't have a network" | Override auto-fill → set network_status: no. Log `p5_auto_fill_overridden: true`. |

## Next
→ Phase 6 via `phases/06-connectors.md`
