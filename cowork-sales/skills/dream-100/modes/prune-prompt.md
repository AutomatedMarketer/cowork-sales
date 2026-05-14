# Prune prompt — runs when list has 100+ names

Quarterly suggestion (or on /dream-100 prune):

"You're at <N> names. Top 100 works best at 100 — focused beats broad. Want to prune?"

If yes:
- Sort all names by (days since last touch) DESC, contributions ASC
- Surface 12 candidates for removal (the most-stale, least-contributed-to)
- For each: show name + last touched + total contributions + suggested move ("Drop / Keep / Move to backup")
- Default action = "Drop"
- User confirms each one (or "approve all defaults")
- Archive dropped names to `archive/dream-100-pruned-<YYYY-MM-DD>.md`

Never silently drop. Always confirm with user.
