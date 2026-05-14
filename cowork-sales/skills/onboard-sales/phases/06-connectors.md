# Phase 6 — Connectors

**Time budget:** 2 min

## What you read first (lazy-load)
- `about-me/connections.md`
- `checks/connectors-authorized.md`

## What to do

### Then (before Ask):
1. Read `checks/connectors-authorized.md` for the exact detection rules.
2. Read `about-me/connections.md` — check for `gmail: authorized: yes` and `fathom: authorized: yes`.
3. For each authorized connector, run a small live read test:
   - **Gmail test**: Read the subject line of 1 most-recent email.
   - **Fathom test**: List 1 most-recent transcript title.
4. Record test results (pass/fail) for display to the user.

### Authorization check results:

#### If BOTH pass:
Proceed to Ask (pass).

#### If Gmail missing or unauthorized:
HALT — say: "Gmail isn't wired yet. Run `/browse-connectors` to authorize it, then come back and we'll resume at Phase 6."
Set `current_phase: 6` in state (do not advance). Stop.

#### If Fathom missing or unauthorized:
HALT — say: "Fathom isn't wired yet. Run `/browse-connectors` to authorize it, then come back and we'll resume at Phase 6."
Set `current_phase: 6` in state (do not advance). Stop.

#### If authorized but live test fails:
HALT — surface the error: "Gmail/Fathom is marked authorized but the live test failed: [error message]. Run `/browse-connectors` to re-authorize, then come back."
Set `current_phase: 6` in state (do not advance). Stop.

---

### Ask (pass path — both connectors live):
> "Connectors look good:
> - Gmail ✓ *(most recent: '[email subject]')*
> - Fathom ✓ *(most recent: '[transcript title]')*
>
> These feed your daily brief with real intel. Ready for the last phase?"

### Then:
- Wait for confirmation (any positive response).
- No writes needed — connections.md is read-only here.

### Write:
Nothing — this phase is read-only on connections.md.

Log in state only:
```
p6_gmail_test: pass | fail
p6_fathom_test: pass | fail
```

### Update state:
Set `current_phase: 7` and `p6: ✓` in `_aibos/state-sales.md`.

## Common failure modes
| Scenario | Recovery |
|---|---|
| `connections.md` file missing entirely | HALT — "Run `/onboard` from cowork-ai-os first to create your connections file." |
| `connections.md` present but no connector entries | HALT — "No connectors set up yet. Run `/browse-connectors` to wire Gmail and Fathom." |
| Gmail authorized, Fathom not | HALT on Fathom. Give specific instruction for that connector only. |
| Live test times out | Treat as fail — surface timeout error. Do NOT skip to Phase 7. |
| User asks if both connectors are required | "Yes — Gmail feeds your outreach activity, Fathom feeds your call insights. Both power the daily brief." |

## Next
→ Phase 7 via `phases/07-live-demo-and-schedule.md`
