# Check: identity files present

Run BEFORE Phase 1 starts.

| File | Required | If missing |
|---|---|---|
| `about-me/about-me.md` | Yes | HALT — "Run `/onboard` from cowork-ai-os first." |
| `about-me/business-brain.md` | Yes | HALT — "Fill business-brain.md via `/onboard` Phase 3." |
| `about-me/connections.md` | Yes | HALT — "Run `/onboard` from cowork-ai-os first." |

If file exists but is empty (0 bytes OR < 50 words of content), treat as missing.
