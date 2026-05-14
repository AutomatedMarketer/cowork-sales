# Check: Gmail + Fathom authorized

Run during Phase 6.

| Connector | Detection | If missing |
|---|---|---|
| Gmail | `connections.md` has `gmail: authorized: yes` | HALT — "Run `/browse-connectors` to wire Gmail." |
| Fathom | `connections.md` has `fathom: authorized: yes` | HALT — "Run `/browse-connectors` to wire Fathom." |

If authorized but `gmail.last_test` or `fathom.last_test` failed, attempt a small read call:
- Gmail: "Read 1 most-recent email subject"
- Fathom: "List 1 most-recent transcript"

If the read fails, HALT and surface the error.
