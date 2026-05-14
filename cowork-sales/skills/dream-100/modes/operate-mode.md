# Operate mode — running the engine on a populated list

The user has 5-100 names. Goal: surface today's highest-value relationship action.

## Flow

### 1. Read dream-100.md
Parse all rows. For each person, compute:
- Days since last touch
- Total contributions ever
- Total asks ever
- Contribution:ask ratio
- Last contribution date

### 2. Surface today's targets (3 buckets)

**Bucket A — Overdue touches (>30 days since last touch)**
List up to 5 people who haven't been touched in 30+ days. Suggest one contribution move each (load `templates/contribution-suggestions.md`).

**Bucket B — Ripe for activation (≥3 contributions, no asks, > 3 months since first contact)**
List up to 3 people whose runway is mature. Suggest: "These are ripe for a real RRO ask — but only if you have one. Got one today?"

**Bucket C — In delicate territory (contribution:ask ratio < 1.5)**
List anyone with an unhealthy give-to-ask ratio. Surface: "You've asked <X> times and given <Y>. Sit on these — give twice before asking again."

### 3. Help draft today's action

If user picks a Bucket A target:
- Load `templates/contribution-suggestions.md`
- Suggest 3 contribution moves (share their work, refer a client, intro them, comment thoughtfully)
- Help draft (1-3 sentences)
- Save to `projects/sales/drafts/<YYYY-MM-DD>-dream-100-<name>.md`

If user picks a Bucket B target AND has an RRO:
- Hand off to `/rro-email` with the RRO + recipient context
- Receive draft back, save

If user picks a Bucket C target:
- HARD-BLOCK. Load `templates/ask-blocker.md` for the message.

### 4. Update dream-100.md
- Update last_touched + contribution_count or ask_count for the chosen person

### 5. Self-improvement close + Next Move

```
⚡ NEXT MOVE: <Subject> <Verb> <Timing>
   Why: <reason from the chosen bucket — e.g., "ripe for activation after 5 contributions over 4 months">
```
