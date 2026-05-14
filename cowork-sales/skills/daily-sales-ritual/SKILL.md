---
name: daily-sales-ritual
description: "The 3pm fire. Reads your channels + tactics. Builds your 3-column brief (Email Pipeline + Yesterday's Activity + Overdue Follow-Ups). Rotates an outbound prompt SPECIFIC to your channels. Ends with a Next Move you can do in 20-60 minutes."
license: MIT
author: Nuno Tavares
---

# /daily-sales-ritual

You are the host of the daily sales ritual. Build today's brief, score the prospects, suggest the outbound, end with a concrete Next Move.

## Architectural foundations (non-negotiable)

1. **Lazy-load.** Read only `sales-preferences.md` + `people-log.md` + `templates/brief-template.md` + `channels/<user's-chosen>.md` files. Do NOT load the full framework reference.
2. **Self-improve.** At the end of every run, ask: "What would've made this 10% better?" Append to `projects/sales/skill-memory.md`. If similar learning appeared 3+ times → flag.
3. **Actionable.** Output ENDS with `Next move:` block (Subject + Verb + Timing + Why).

## Pre-flight check

Before producing the brief:
- Verify `projects/sales/sales-preferences.md` exists and has `channels:` populated
- If missing → "Run `/onboard-sales` first."

## Build the brief

### 1. Read inputs
- `projects/sales/sales-preferences.md` → channels + tactics + trigger time
- Gmail inbox (last 24h via connector) → email pipeline column
- Fathom (yesterday's transcripts via connector) → activity column
- `projects/sales/people-log.md` → overdue follow-ups column (anyone > 14 days since last touch)

### 2. Score each name (buyer-pyramid Tool 4.2)
For each prospect in email pipeline + Fathom mentions:
- **Buying now:** clicked a price/buy link, replied with intent, asked for proposal
- **Open:** opened 3+ times this week, attended a webinar, downloaded high-intent asset
- **Interested:** opened 1-2 times, reading content, hasn't acted
- **Quiet but listening:** silent openers, lurkers — period

### 3. Pick today's outbound prompt
Rotate through tactics from `sales-preferences.md`. Read the matching `channels/<id>.md` file and pull the "Sample outbound prompt" line, personalize with one specific user detail.

### 4. Build the brief using `templates/brief-template.md`

### 5. Generate `Next move:` block (use `templates/next-move-block.md`)

The Next Move MUST be the single highest-value action from the brief. Usually:
- Buying-now prospect → reply today
- Overdue 14+ days warm prospect → reach out today
- High-quality activity mention → follow up within 48h

### 6. Self-improvement close (Foundation B)

Use `templates/self-improvement-close.md`.

### 7. Save brief

Save to `projects/sales/rituals/<YYYY-MM-DD>.md`.

### 8. Update streak

Edit `projects/sales/sales-preferences.md`:
- Increment `total_runs`
- Update `last_run` to today
- Update `current_streak` based on missed-day policy (see below)

## Missed-day policy

| Gap since last_run | Behavior |
|---|---|
| 0-1 days | Streak preserved. Standard brief. |
| 2-3 days | Streak preserved with flag. Brief offers 60-second re-engagement prompt at top. |
| 7+ days | Streak resets. Soft restart: "Big gap. Let's focus on 1-2 reach-outs today, not the full brief." |

## Sister-plugin loose coupling

- If `cowork-obsidian` is detected → mirror today's brief to vault `wiki/sales/rituals/<YYYY-MM-DD>.md`
- If `cowork-research` is detected → for any prospect in the pipeline who needs deeper intel, suggest "Run `/research-brief` on <name>"
