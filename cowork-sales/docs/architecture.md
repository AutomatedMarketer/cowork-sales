# cowork-sales — architecture (v0.1.0)

Internal contributor doc. For the user-facing pitch see the [root README](../../README.md).

## Overview

`cowork-sales` is a modular add-on in the Cowork AI OS family. It soft-depends on `cowork-ai-os` for identity (`about-me/about-me.md`, `business-brain.md`, `connections.md`). It has no hard dependency on any other plugin — `cowork-obsidian` and `cowork-research` are detected at runtime and change behavior if present, but are never required.

The v0.1.0 surface is **4 skills** (1 wizard + 3 operational), built on **3 architectural foundations**: lazy-load context, self-improving skills, and actionable output.

---

## The 3 foundations as code constraints

### Foundation 1 — Lazy-load

Sales context is heavy. A full load of identity + sales preferences + people log + top 100 list could easily run 15,000–40,000 tokens. The lazy-load rule means every skill only embeds the sections it actually needs.

| Skill | Sections always loaded | Sections loaded on demand |
|---|---|---|
| `/onboard-sales` | Identity (about-me + business-brain) | Channel files (only the selected 1–2); sales preferences template | 
| `/daily-sales-ritual` | Identity, sales preferences, channel files (user's active 1–2) | People log (only today's candidates); Top 100 (only if user is in Operate mode) |
| `/rro-email` | Identity, sales preferences, RRO skeleton | People log entry for the specific contact being drafted to |
| `/dream-100` | Identity, Top 100 file (current mode slice only) | Full Top 100 rows (only when editing or pruning specific entries) |

**The rule in practice:** each SKILL.md opens with an explicit `## Context to load` section listing exactly which files to read before doing anything else. No skill reads files not in its declared list.

### Foundation 2 — Self-improve

Every skill closes with the same execute → learn → flag pattern:

```
1. Execute the core task.
2. After delivering output: read sales-skill-improvements.md.
3. Append one line: what worked, what the user changed, what to do differently next time.
4. If the same correction appears 3+ times: flag it in the improvement file with [PATTERN] prefix so the next session can surface it as a standing rule.
```

The improvement file lives at `projects/sales/sales-skill-improvements.md`. It is append-only — skills never rewrite it. The `/onboard-sales` Phase 7 seals the initial version; subsequent runs only append.

### Foundation 3 — Actionable

Every output from every skill must end with a parseable `Next move:` block. The regex the test harness checks:

```
⚡ NEXT MOVE: .+ .+ .+\n   Why: .+
```

Required structure:
- **Subject** — who is acting (you, implied)
- **Verb** — one clear action (send, reply, post, call, add)
- **Timing** — when (today before noon, within 24h, this week)
- **Why** — one sentence on why this move, not a different one

Output that doesn't parse against this regex fails the 17-test verification matrix.

---

## Memory architecture (10 tiers)

| Tier | What | Path | Lifecycle |
|---|---|---|---|
| 1 | Identity | `about-me/about-me.md`, `about-me/business-brain.md`, `about-me/connections.md` | Written by `cowork-ai-os`; read-only here |
| 2 | Sales preferences | `projects/sales/sales-preferences.md` | Written by `/onboard-sales` Phase 5; updated by wizard re-runs only |
| 3 | People log | `projects/sales/people-log.md` | Appended by `/daily-sales-ritual` + `/rro-email` after every outreach action |
| 4 | Daily briefs | `projects/sales/briefs/YYYY-MM-DD.md` | Written by `/daily-sales-ritual` on each run; never edited after creation |
| 5 | Top 100 | `projects/sales/dream-100.md` | Managed by `/dream-100`; structured rows, one per relationship target |
| 6 | Drafts | `projects/sales/drafts/<contact-slug>.md` | Written by `/rro-email`; overwritten on each new draft for same contact |
| 7 | Skill memory (hot) | `projects/sales/sales-skill-memory.md` | Appended after every skill run; capped at 30 entries (see Tier 9→10 flush) |
| 8 | Skill improvements | `projects/sales/sales-skill-improvements.md` | Append-only; skills write one line per run; [PATTERN] prefix on recurring items |
| 9 | Session memory hot | `about-me/memory.md` | Shared with cowork-ai-os; this plugin appends sales-relevant session notes |
| 10 | Session memory cold | `about-me/archive/memory-log.md` | Overflow from Tier 9 when entry count exceeds 30; silent append, never pruned |

**Hot/cold flush rule (Tiers 7 + 9 → 10):** when `sales-skill-memory.md` hits 30 entries, the next skill run moves the oldest 10 entries to `about-me/archive/memory-log.md` before appending its new entry. Same rule applies to `about-me/memory.md`. The archive is cold storage — loaded only when explicitly needed, never auto-loaded.

---

## The 8-channel personalization engine

Data flow from business context to daily ritual output:

```
business-brain.md
    │
    ▼
[business-brain classifier]
    Reads: offer type, ICP description, current focus, past channels mentioned
    Outputs: business_type (one of 7 profiles)
    │
    ▼
[profile match]
    Loads: personalization/<business_type>.md
    Outputs: channel_scores{} — weighted score (0–10) for each of the 8 channels
    │
    ▼
[suggested channels]
    Top 2 scoring channels surfaced to user with one-line rationale each
    │
    ▼
[user picks 1–2 channels]
    Stored in sales-preferences.md: active_channels: [channel_a, channel_b]
    │
    ▼
[tactic auto-fill from channel files]
    skills/onboard-sales/channels/<channel_slug>.md loaded
    Tactic rotation pool populated for daily ritual
    │
    ▼
[daily ritual prompt rotation]
    /daily-sales-ritual reads active_channels → pulls today's tactic from rotation pool
    Rotation tracked in sales-skill-memory.md to avoid repeats within a 7-day window
```

**The 7 personalization profiles:**

1. B2B service (agency, consulting)
2. Course creator / educator
3. Local service business
4. Creator / influencer (content-first)
5. E-commerce / product
6. Coach with existing network
7. New solopreneur (no established network yet)

Each profile file declares default `channel_scores{}`, a `suggested_channels[]` shortlist, and per-channel tactic seeds for the daily ritual.

---

## `/onboard-sales` 7-phase state machine

State tracked in `_aibos/state-sales.md`. The wizard is resumable — re-invocation reads `next_pending_phase` and continues from there.

| Phase | Name | What happens | Gate |
|---|---|---|---|
| 0 | Prereq check | Reads `cowork-ai-os` version, verifies `business-brain.md` exists and is non-empty | Halts with paste-ready prompt if check fails |
| 1 | Identity read | Loads and summarizes `about-me.md` + `business-brain.md` for the user to confirm | User confirms or corrects |
| 2 | Offer clarity | Surfaces offer from business-brain; runs offer-doctor questions if offer is vague | User approves final offer statement |
| 3 | Channel selection | Classifier runs; top 2 channels surfaced with rationale; user picks 1–2 active channels | User confirms active_channels |
| 4 | Outreach history | Asks about past outreach attempts; captures what worked and what didn't | None — informational |
| 5 | Preferences setup | Writes `sales-preferences.md` (cadence, streak policy, channel settings) | User approves before write |
| 6 | First brief | Runs `/daily-sales-ritual` logic to produce Day 1 brief | User sees output |
| 7 | Seal + next steps | Writes initial `sales-skill-improvements.md`; shows streak rules; surfaces next commands | Wizard complete |

**State file fields tracked:** `install_complete`, `current_phase`, `next_pending_phase`, `business_type`, `active_channels[]`, `offer_statement`, `preferences_written`, `first_brief_done`.

**Identity check failure (Phase 0):** wizard writes nothing to disk, surfaces a single paste-ready block directing the user to run `/onboard` in `cowork-ai-os` first. No partial state is saved.

---

## `/dream-100` mode switching

Mode is derived from the live row count in `dream-100.md`. No manual mode setting — the skill re-derives mode on every invocation.

| Condition | Mode | Behavior |
|---|---|---|
| File missing OR fewer than 5 rows | **Build** | Focuses on adding new names. Asks qualifying questions for each addition. No pruning prompts. Sourcing suggestions active. |
| 5–99 rows | **Operate** | Focuses on maintaining cadence with existing names. Give-2x-before-ask rule enforced. Warm-up queue surfaced. |
| 100+ rows | **Operate + Prune** | Operate behavior plus automatic prune prompts for dormant or misaligned entries (30+ days no interaction, or ICP drift flagged). |

**Give-2x-before-ask hard rule (enforced in Operate mode):** the skill tracks `value_given_count` and `ask_count` per row. Any `ask_count` increment where `value_given_count < (ask_count * 2)` triggers a hard block: "You haven't given enough value to this person yet. Add a give action first." This is not a warning — the skill refuses to draft an ask until the count is satisfied.

---

## Sister-plugin loose coupling

Both `cowork-obsidian` and `cowork-research` are detected at runtime. Detection runs once per session in Phase 0 of the wizard, and on first invocation of each operational skill.

**Detection logic:**

```
cowork-obsidian present = plugin_manifest contains "cowork-obsidian"
                          AND vaults.md exists AND is non-empty

cowork-research present = plugin_manifest contains "cowork-research"
                          AND reference/_research-hot.md exists
```

**Behavior matrix:**

| Condition | cowork-obsidian absent | cowork-obsidian present |
|---|---|---|
| **cowork-research absent** | All outputs → `projects/sales/`. No vault mirror. No prospect intel. | Briefs + people log optionally mirrored to `wiki/sales/`. Vault destination surfaced in Phase 3 of wizard. |
| **cowork-research present** | `/rro-email` + `/dream-100` can trigger `/research-brief` on a contact before drafting. Output stays in `projects/sales/`. | Full stack: vault mirror + prospect intel + reach-out drafts that cite the brief. |

Neither plugin is required. Degraded behavior (no vault mirror, no prospect intel) is still fully functional.

---

## What's NOT in v0.1

Deferred to keep the initial release tight. Tracked here so contributors know what's intentionally absent:

- **`/offer-doctor` standalone** — offer clarity logic exists inside `/onboard-sales` Phase 2 only. A standalone `/offer-doctor` skill that can be run anytime was scoped but deferred.
- **`/buyer-pyramid` standalone** — the 5-level awareness model is referenced in `/daily-sales-ritual` scoring. A standalone quiz + output skill was scoped but deferred.
- **`/awareness-classifier` standalone** — classifies a piece of content or a contact against the 5-level awareness model. Deferred.
- **`/seinfeld-email` standalone** — daily story-based email generator using the entertainment-first approach. Lives partially in `/rro-email` variants; a standalone daily-email skill was scoped but deferred.
- **`/find-leads` channel-specific prospecting** — for each active channel, surfaces new prospecting targets. Deferred to v0.2.
- **GHL / Apollo / HubSpot connectors** — no CRM connector in v0.1. People log is flat markdown. CRM sync deferred.
- **Auto-send to Gmail** — the plugin drafts emails but does NOT send. Sending requires explicit user action. Auto-send is a v0.2+ feature gated behind a hard confirmation step.
- **Webinar diagnostic** — multi-step wizard for diagnosing a webinar offer's conversion problems. Scoped for v0.2.
- **Content lifecycle pyramid tool** — maps existing content to awareness stages + surfaces gaps. Deferred.

---

## v0.2 candidates

Ordered by cohort demand signal:

1. **`/find-leads`** — channel-specific prospecting (different tactics per channel: LinkedIn search, community member scraping, referral-ask flow, etc.)
2. **`/offer-doctor` standalone** — runnable anytime, not just during onboarding
3. **Paid-ads management subcommands** — for users on Channel 8 (paid ads); budget tracking, copy rotation, A/B log
4. **GHL / HubSpot / Apollo connectors** — per business type (B2B users hit this wall fast)
5. **Auto-send gate for Gmail** — opt-in, hard confirmation, send log written to people log on every send

---

## Manifest version policy

- **Single source of truth:** `cowork-sales/.claude-plugin/plugin.json` `version` field
- **Mirrors:** `marketplace.json`, `CHANGELOG.md`, `RELEASE-vX.Y.Z.md`, all 4 SKILL.md frontmatter `version:` fields
- **Semver:** patch for bug fixes, minor for new skills/phases, major for breaking schema changes (state-sales.md structure, plugin.json, or removed skills)
- **Rule:** bump every mirror in the same commit as `plugin.json`. Don't trust manual chases.

---

## Hard rules (contributor checklist)

- Never re-collect identity — read `about-me/`, never overwrite
- Append-only on `about-me/connections.md`, `about-me/memory.md`, and all `projects/sales/` log files
- Plan-then-approve for every write outside declared safe-zones
- 3rd–4th-grade reading level for every prompt the wizard shows the user
- Resumable: every wizard phase reads + writes `state-sales.md`
- No course SOPs in this repo (private workspace only)
- Every skill output must end with a parseable `⚡ NEXT MOVE:` block
- Give-2x-before-ask rule enforced in `/dream-100` Operate mode — no exceptions
- Zero guru names anywhere in any plugin file
