# v0.1.0 Test Report — 2026-05-14

## Summary

- Tests passing: 16/17
- Static checks run: 3 (Tests 12, 13, 9-static)
- Inspection checks: 14 (Tests 1–11 + 14–17, plus 9-dynamic)
- Final verdict: RED — 1 test FAIL blocks green gate

---

## Test results

| Test | Type | Result | Notes |
|---|---|---|---|
| 1. Wizard golden path | Inspection | PASS | All 7 phase files present (01–07). Phase dispatch table in SKILL.md maps every phase. Phase 7 invokes `/daily-sales-ritual`. State tracked in `_aibos/state-sales.md`. All checks wired in Phase 1 and Phase 6. |
| 2. Halt on missing identity | Inspection | PASS | `checks/identity-files-present.md` defines exact halt rules for `about-me.md`, `business-brain.md`, `connections.md`. `phases/01-welcome.md` runs both identity checks before any Ask block and surfaces `/onboard` redirect messages verbatim. Empty-file (<50 words) treated as missing. |
| 3. Halt on missing connectors | Inspection | PASS | `checks/connectors-authorized.md` defines Gmail + Fathom detection. `phases/06-connectors.md` halts for each connector independently with `/browse-connectors` redirect. Live read test enforced; timeout treated as fail. State held at Phase 6 — does not advance. |
| 4. Channel personalization | Inspection | PASS | `daily-sales-ritual/SKILL.md` Foundation 1 explicitly reads `channels/<user's-chosen>.md` files (not all 8). Step 3 of build-brief pulls `channels/<id>.md` "Sample outbound prompt" line and personalizes it. 8 channel files exist with individual prompts. `brief-template.md` includes a `TODAY'S OUTBOUND PROMPT (rotating from your tactics)` row. |
| 5. Smart-suggestion accuracy | Inspection | PASS | All 7 profile files verified against classifier. Suggestions consistent with business logic: B2B→[02,01]; Course→[01,02]; Local→[06,04]; Creator→[02,07]; Ecommerce→[08,01]; Coach-network→[01,07]; New-solo→[03,05]. Each profile's smart-suggestion prose matches its `suggested_channels[]` frontmatter. |
| 6. /dream-100 Build mode | Inspection | PASS | `modes/build-mode.md` walks exactly 3 questions (Q1: list owners, Q2: admired, Q3: adjacent). Each question collects names and saves rows to `dream-100.md`. Auto-switch fires at 5+ names with explicit message. Next Move block present at end. |
| 7. /dream-100 Operate mode | Inspection | PASS | `modes/operate-mode.md` surfaces exactly 3 buckets (A: overdue >30 days, B: ripe for activation ≥3 contributions, C: contribution:ask ratio < 1.5). Drafts contributions via `templates/contribution-suggestions.md`. Next Move block present. |
| 8. Build → Operate auto-switch | Inspection | PASS | `dream-100/SKILL.md` mode detection reads `projects/sales/dream-100.md` row count on every invocation. File missing OR 0-4 names → Build; 5-99 → Operate; 100+ → Operate+prune. No manual flag — purely file-state driven. |
| 9. Lazy-load discipline | Static + Inspection | PASS | Static: all 4 SKILL.md files contain explicit lazy-load sections listing specific files. `onboard-sales/SKILL.md`: "Read each phase file ONLY when you enter that phase." `daily-sales-ritual/SKILL.md`: lists exact files. `rro-email/SKILL.md`: lists exact templates. `dream-100/SKILL.md`: reads only mode-specific file. Each phase file has its own "What you read first (lazy-load)" header listing only phase-specific files. |
| 10. Self-improvement append | Inspection | PASS | `templates/self-improvement-close.md` specifies append format `<YYYY-MM-DD> | /<skill-name> | <answer verbatim>` to `projects/sales/skill-memory.md`. Format matches test expectation `YYYY-MM-DD \| /skill-name \| <answer>`. |
| 11. Self-improvement flag trigger | Inspection | PASS | Same file: recurrence check reads `skill-memory.md` for 3+ entries with ≥60% substring overlap or same keyword match. If found: surfaces "I've seen this 3+ times" prompt and offers to draft `skill-improvements.md` entry in table format with recurrence_count and reviewed:no. |
| 12. Actionability close | Static | FAIL | **GAP:** `⚡ NEXT MOVE: <Subject> <Verb> <Timing>` block is present in: `next-move-block.md` ✓, `rro-email/SKILL.md` ✓, `dream-100/modes/operate-mode.md` ✓, `dream-100/modes/build-mode.md` ✓. **Missing** in `skills/onboard-sales/phases/07-live-demo-and-schedule.md` — that file uses `Next move:` (lowercase, no ⚡) in its inline format rather than the canonical `⚡ NEXT MOVE:` block. The architecture doc (`docs/architecture.md` line 233) mandates "Every skill output must end with a parseable `⚡ NEXT MOVE:` block." Phase 07 invokes `/daily-sales-ritual` which produces the correct format via `brief-template.md`, but the phase file itself does not reference or emit the canonical format directly. **Test: 4/5 files pass; 1/5 fails.** |
| 13. No guru names | Static (grep) | PASS | `grep -ri -l -E "(julie\|chenell\|brunson\|hormozi\|belcher\|dotcom secrets\|expert secrets\|acquisition\.com\|\$100M offers\|\$100M leads\|funnel hacking\|war room\|native commerce\|russell\|perry\|alex\|chenell)" .` — NO MATCHES. Zero files contain any guru name. |
| 14. Missed-day forgiveness (2-3 day gap) | Inspection | PASS | `daily-sales-ritual/SKILL.md` missed-day policy table: 2-3 day gap → "Streak preserved with flag. Brief offers 60-second re-engagement prompt at top." `templates/brief-template.md` contains explicit `⚠️ 60-SECOND RE-ENGAGEMENT` block for missed 2-3 days with re-orient content. No shaming language present. |
| 15. Missed-day reset (7+ day gap) | Inspection | PASS | `daily-sales-ritual/SKILL.md` missed-day policy: 7+ days → "Streak resets. Soft restart." `templates/brief-template.md` contains `SOFT RESTART` block: "Big gap since your last ritual. Streak reset. That's fine — the system is designed for 365 days, not 30." Explicitly limits to 1-2 reach-outs. No shaming language. |
| 16. Single-CTA enforcement | Inspection | PASS | `rro-email/SKILL.md` Step 5 enforces "Single CTA (Buy / Apply / Reply — pick exactly one)". `templates/12-line-skeleton.md` Rules section: "One CTA. Pick one of: Buy, Apply, Reply." Weak example explicitly flagged for "Three CTAs instead of one." |
| 17. Banned RRO hard-block | Inspection | PASS | `templates/banned-categories.md` lists exactly 6 banned patterns (fake scarcity, excitement-only, guilt, manufactured urgency, vague opening, fake scarcity closes) and exactly 6 allowed alternatives (Market Shift, Client Result, Mistake, Real Deadline, Controversy, New Access). Hard-block message specifies rejection language and redirects to the 6 allowed categories. |

---

## The one failing test — TEST 12 fix required

**File:** `skills/onboard-sales/phases/07-live-demo-and-schedule.md`

**Problem:** Phase 7 uses `Next move:` (lowercase, no ⚡ lightning prefix) in its inline Step A description rather than the canonical `⚡ NEXT MOVE: <Subject> <Verb> <Timing>` format. The architecture doc explicitly states this regex must pass: `` ⚡ NEXT MOVE: .+ .+ .+\n   Why: .+ ``

**Fix needed:** Change the `Next move:` block definition in Step A of Phase 7 to use the canonical `⚡ NEXT MOVE:` format, OR add an explicit instruction that the brief produced by `/daily-sales-ritual` supplies this block (and remove the inline definition that conflicts).

**Effort:** 2-line edit to `phases/07-live-demo-and-schedule.md`.

---

## Live-Cowork tests still pending (informational — not blocking GitHub push)

These require Nuno to run them in a clean Cowork session post-install:

**TEST 1 live:** Run `/onboard-sales` on a fresh profile. Verify: (a) wall time ≤15 minutes, (b) all 7 phases complete, (c) `_aibos/state-sales.md` shows `current_phase: COMPLETE`, (d) `projects/sales/sales-preferences.md` exists with channels populated, (e) `projects/sales/rituals/<today>.md` written.

**TEST 9 live:** Open a non-sales chat. Confirm the unified sales framework docs do NOT auto-load. Run `/dream-100` and verify only `dream-100.md` + one mode file load (not all skill files simultaneously).

**TEST 10-11 live:** Invoke each skill, answer the "10% better" question. Open `projects/sales/skill-memory.md` and verify one new line appended in `YYYY-MM-DD | /skill-name | answer` format. Run the same skill 3 times with similar feedback answers, verify `skill-improvements.md` receives a `[PATTERN]`-prefixed entry.

---

## Conclusion

Static and inspection checks: **16/17 PASS, 1 FAIL**

Failing test: **TEST 12** — `phases/07-live-demo-and-schedule.md` uses `Next move:` instead of canonical `⚡ NEXT MOVE: <Subject> <Verb> <Timing>` format.

Dynamic in-Cowork verification: documented above, awaits Nuno's live test.

Recommendation: **BLOCK — fix the one-file TEST 12 issue, re-run TEST 12 static check, then push.**
