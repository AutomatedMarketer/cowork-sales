# Phase 7 — Live Demo and Schedule

**Time budget:** 2–3 min

## What you read first (lazy-load)
- `projects/sales/sales-preferences.md` (the full file — all phases now complete)

## What to do

### Step A — Live demo

### Then (Step A):
1. Read the full `sales-preferences.md` — channels, tactics, trigger_time, offer_snapshot.
2. Invoke `/daily-sales-ritual` ONCE using this session's data as context.
3. The ritual produces today's sales brief. Display it in full.
4. The brief MUST end with a `Next move:` block formatted as:
   ```
   Next move:
   - Subject: <who to contact or what action to take>
   - Verb: <exactly what to do — send, call, reply, post>
   - Timing: <today by [time] | within 24h | right now>
   - Why: <1-sentence reason this is the highest-leverage move today>
   ```

If `/daily-sales-ritual` cannot produce a brief (missing data, connector error) → produce a manual brief from `sales-preferences.md` directly. Note `p7_ritual_fallback: true` in state.

---

### Step B — Schedule

### Then (Step B):
After the brief is shown, set up the daily scheduled task:
- Task: run `/daily-sales-ritual` every day at the `trigger_time` from sales-preferences.md.
- Use Cowork's scheduled tasks system (same mechanism as cowork-ai-os daily brief).
- Confirm the schedule is active before moving on.

---

### Step C — Self-improvement ask

### Ask (Step C):
> "Setup complete! One last thing — what's one thing that would've made this setup 10% better or easier?"

### Then (Step C):
- Accept any answer (skip is fine — if user skips, log "no feedback").
- Append to `projects/sales/skill-memory.md`:
  ```markdown
  ## Session feedback — <YYYY-MM-DD>
  Trigger: Phase 7 self-improvement ask
  Feedback: <user answer or "no feedback">
  Phases completed: all 7
  Channels selected: <channel names>
  ```

---

### Write:
1. `projects/sales/rituals/<YYYY-MM-DD>.md` — today's full sales brief (everything from Step A including the Next move block).
2. `projects/sales/memory.md` — append first entry:
   ```markdown
   ## Entry — <YYYY-MM-DD>
   Channels: <channel names>
   Tactics: <tactic list>
   Trigger: <HH:MM>
   Setup complete: yes
   ```
3. `projects/sales/skill-memory.md` — append feedback from Step C.
4. `_aibos/state-sales.md` — mark COMPLETE:
   ```yaml
   current_phase: COMPLETE
   phases_complete:
     p1: ✓
     p2: ✓
     p3: ✓
     p4: ✓
     p5: ✓
     p6: ✓
     p7: ✓
   completed_at: <YYYY-MM-DD HH:MM>
   ```

### Update state:
Set `current_phase: COMPLETE` and `p7: ✓` in `_aibos/state-sales.md`.

---

### Exit message:
> "Setup complete. Your daily ritual fires tomorrow at **[trigger_time]**. Today's brief is above. Your next move is at the bottom of that brief."

## Common failure modes
| Scenario | Recovery |
|---|---|
| `/daily-sales-ritual` errors or returns nothing | Produce manual brief from sales-preferences.md. Note `p7_ritual_fallback: true` in state. Do NOT block completion. |
| Scheduler unavailable | Note `p7_schedule_failed: true` in state. Tell user: "I couldn't set the schedule automatically — add a reminder to run `/daily-sales-ritual` at [trigger_time] each day until we fix this." |
| `projects/sales/rituals/` directory doesn't exist | Create the directory, then write the file. |
| `projects/sales/memory.md` doesn't exist | Create it, then append. |
| `projects/sales/skill-memory.md` doesn't exist | Create it, then append. |
| User skips the improvement question | Log "no feedback" — do not re-ask. |

## Next
→ Exit — wizard complete.
