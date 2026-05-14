# Next Move block — universal format

Every skill output ends with this block.

```
⚡ NEXT MOVE: <Subject> <Verb> <Timing>
   Why: <one-sentence reason>
```

## Examples (the bar to hit)
- ✅ `⚡ NEXT MOVE: Reply to Sarah's email today before 5pm. Why: She's opened 6x silently + clicked twice — warmest lead on your list.`
- ✅ `⚡ NEXT MOVE: Send post-conference Loom to Janet today. Why: She asked yesterday + the 48-hour window closes tonight.`
- ❌ `⚡ NEXT MOVE: Consider warm outreach.` (no subject, no timing, abstract — REJECT)
- ❌ `⚡ NEXT MOVE: Reply to everyone.` (no specific subject — REJECT)

## Validation pattern
The block MUST match:
`⚡ NEXT MOVE: .+ .+ .+\n   Why: .+`

If it doesn't match, the skill output is incomplete — regenerate.

## When picking the Next Move
Priority order:
1. Buying-now prospect waiting on a reply → reply today
2. Overdue warm follow-up past 14 days → reach out today
3. High-quality recent inbound or call mention → follow up within 48 hours
4. Active outbound tactic from today's prompt → execute today

Always specific. Always timed. Always justified in one sentence.
