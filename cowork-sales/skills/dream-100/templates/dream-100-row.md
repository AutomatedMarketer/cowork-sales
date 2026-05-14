# dream-100.md row schema

Each person is one row in the markdown table.

```
| Name | Category | First contact | Last touched | Contributions | Asks | Notes |
|---|---|---|---|---|---|---|
| Jane Doe | list_owner | 2026-03-15 | 2026-05-10 | 3 | 0 | Newsletter overlap with our ICP |
```

Columns:
- **Name** — full name (no honorifics in this column)
- **Category** — list_owner / admired / adjacent / past_client
- **First contact** — YYYY-MM-DD when first added to Top 100
- **Last touched** — YYYY-MM-DD of most recent contribution or ask
- **Contributions** — integer count
- **Asks** — integer count
- **Notes** — free-text, multi-sentence OK

Append-only via `/dream-100 add`. Edits via `/dream-100` operate mode after each touch.
