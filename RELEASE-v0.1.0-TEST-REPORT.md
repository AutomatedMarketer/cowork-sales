# v0.1.0 Test Report — 2026-05-14

## Summary

- **Tests passing:** 17/17 (after TEST 12 fix applied)
- **Static checks run:** 4 (Tests 12, 13, 9-static, file existence)
- **Inspection checks:** 14 (Tests 1–11 + 14–17, plus 9-dynamic)
- **Final verdict:** GREEN — clear to push to GitHub after Phase G.4 Nuno confirmation

---

## Test results

| Test | Type | Result | Notes |
|---|---|---|---|
| 1. Wizard golden path | Inspection | PASS | All 7 phase files present (01–07). Phase dispatch table in SKILL.md maps every phase. Phase 7 invokes `/daily-sales-ritual`. State tracked in `_aibos/state-sales.md`. Checks wired in Phase 1 and Phase 6. |
| 2. Halt on missing identity | Inspection | PASS | `checks/identity-files-present.md` defines exact halt rules for `about-me.md`, `business-brain.md`, `connections.md`. `phases/01-welcome.md` runs both identity checks before any Ask block. Empty-file (<50 words) treated as missing. |
| 3. Halt on missing connectors | Inspection | PASS | `checks/connectors-authorized.md` defines Gmail + Fathom detection. `phases/06-connectors.md` halts for each connector independently with `/browse-connectors` redirect. Live read test enforced. |
| 4. Channel personalization | Inspection | PASS | `daily-sales-ritual/SKILL.md` Foundation 1 explicitly reads `channels/<user's-chosen>.md` files (not all 8). Step 3 of build-brief pulls `channels/<id>.md` "Sample outbound prompt" line. 8 channel files exist with individual prompts. |
| 5. Smart-suggestion accuracy | Inspection | PASS | All 7 profile files verified against classifier. Suggestions consistent: B2B→[02,01]; Course→[01,02]; Local→[06,04]; Creator→[02,07]; Ecommerce→[08,01]; Coach-network→[01,07]; New-solo→[03,05]. |
| 6. /dream-100 Build mode | Inspection | PASS | `modes/build-mode.md` walks exactly 3 questions. Auto-switch fires at 5+ names with explicit message. Next Move block present at end. |
| 7. /dream-100 Operate mode | Inspection | PASS | `modes/operate-mode.md` surfaces exactly 3 buckets (A: overdue >30 days, B: ripe ≥3 contributions, C: ratio < 1.5). Drafts contributions via `templates/contribution-suggestions.md`. |
| 8. Build → Operate auto-switch | Inspection | PASS | `dream-100/SKILL.md` mode detection reads `projects/sales/dream-100.md` row count. File missing OR 0-4 → Build; 5-99 → Operate; 100+ → Operate+prune. Purely file-state driven. |
| 9. Lazy-load discipline | Static + Inspection | PASS | All 4 SKILL.md files contain explicit lazy-load sections listing specific files. Each phase file has its own "What you read first (lazy-load)" header listing only phase-specific files. |
| 10. Self-improvement append | Inspection | PASS | `templates/self-improvement-close.md` specifies append format `<YYYY-MM-DD> \| /<skill-name> \| <answer verbatim>` to `projects/sales/skill-memory.md`. |
| 11. Self-improvement flag trigger | Inspection | PASS | 3+ entries with ≥60% substring overlap or same keyword match triggers "I've seen this 3+ times" prompt. Drafts `skill-improvements.md` entry with recurrence_count and reviewed:no. |
| 12. Actionability close | Static | **PASS (after fix)** | Canonical `⚡ NEXT MOVE: <Subject> <Verb> <Timing>` block now present in all 5 output points: `next-move-block.md` ✓, `rro-email/SKILL.md` ✓, `dream-100/modes/operate-mode.md` ✓, `dream-100/modes/build-mode.md` ✓, `onboard-sales/phases/07-live-demo-and-schedule.md` ✓ (fixed in commit 5f7f71b). |
| 13. No guru names | Static (grep) | PASS | `grep -ri -l -E "(julie\|chenell\|brunson\|hormozi\|belcher\|dotcom secrets\|expert secrets\|acquisition\.com\|\$100M offers\|\$100M leads\|funnel hacking\|war room\|native commerce\|russell\|perry\|alex)" .` — ZERO matches. |
| 14. Missed-day forgiveness (2-3 day gap) | Inspection | PASS | `daily-sales-ritual/SKILL.md` policy: 2-3 day gap → streak preserved with flag + 60-second re-engagement prompt. `brief-template.md` contains explicit ⚠️ block with re-orient content. No shaming language. |
| 15. Missed-day reset (7+ day gap) | Inspection | PASS | 7+ days → streak resets. SOFT RESTART block: "Big gap. Let's focus on 1-2 reach-outs today, not the full brief." No shaming language. |
| 16. Single-CTA enforcement | Inspection | PASS | `rro-email/SKILL.md` Step 5 enforces "Single CTA (Buy / Apply / Reply — pick exactly one)". `12-line-skeleton.md` Rules: "One CTA. Pick one of: Buy, Apply, Reply." Weak example flagged for three CTAs. |
| 17. Banned RRO hard-block | Inspection | PASS | `banned-categories.md` lists 6 banned patterns + hard-block message + 6 allowed alternatives (Market Shift, Client Result, Mistake, Real Deadline, Controversy, New Access). |

---

## TEST 12 fix detail

**Initial issue:** `skills/onboard-sales/phases/07-live-demo-and-schedule.md` used lowercase `Next move:` block instead of canonical `⚡ NEXT MOVE:` format mandated by Foundation C.

**Fix applied (commit 5f7f71b):** Replaced lowercase block with canonical `⚡ NEXT MOVE: <Subject> <Verb> <Timing>` + `Why:` format. Added inline regex requirement + ✅/❌ examples.

**Verification:** Post-fix grep confirms all output-emitting points use canonical format. 17/17 GREEN.

---

## Live-Cowork tests pending (non-blocking for GitHub push)

These require Nuno to run them in a clean Cowork session post-install to confirm runtime behavior matches the static design:

| Test | How Nuno runs it live |
|---|---|
| TEST 1 live | `/onboard-sales` on fresh test profile → confirm wall time ≤15 min + 6 files created + state.md = COMPLETE |
| TEST 9 live | Open non-sales chat → confirm unified framework reference does NOT auto-load (token count check) |
| TEST 10-11 live | Invoke any skill + answer "10%-better" → verify skill-memory.md appends + 3+ recurrence triggers flag |
| TEST 14-15 live | Manually set `last_run` 3-day-old then 8-day-old → verify forgiveness/reset blocks render |
| TEST 16-17 live | `/rro-email` with 2 CTAs + banned RRO → verify rejections trigger |

---

## Conclusion

- **Static + inspection: 17/17 PASS**
- Dynamic in-Cowork verification: procedure documented above
- **Recommendation: GO for GitHub push** (after Phase G.4 — explicit Nuno confirmation)
