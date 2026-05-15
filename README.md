# Cowork Sales

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](./LICENSE)
[![Version](https://img.shields.io/badge/version-0.1.0-brightgreen.svg?style=flat-square)](./CHANGELOG.md)
[![Platform: Mac · Windows · Linux](https://img.shields.io/badge/platform-Mac%20%C2%B7%20Windows%20%C2%B7%20Linux-blue.svg?style=flat-square)](#install)
[![Built for Claude Cowork](https://img.shields.io/badge/built%20for-Claude%20Cowork-7C3AED.svg?style=flat-square)](https://claude.com/product/cowork)

**Your personalized daily sales ritual, attached to your Cowork AI OS.**

A [Claude Cowork](https://claude.com/product/cowork) plugin (also runs in [Claude Code](https://claude.com/product/claude-code)) that gives you a daily sales rhythm — personalized to where YOUR buyers actually hang out. 7-phase setup wizard. Channel-aware brief every morning. Reach-out writer for warm conversations. Optional Top 100 relationship engine. Everything ties back to what's already in your business brain, so it knows your offer, your buyers, and your voice before it gives you a single suggestion.

Built by [Nuno Tavares](https://nunomtavares.com) for [VCInc](https://vcinc.com) cohort students and anyone who knows they should do daily sales activity — but keeps skipping it because they don't have a clear system.

---

## The 4 skills

| Skill | What it does |
|---|---|
| `/onboard-sales` | 7-phase personalized wizard. Reads your business context, figures out which of the 8 channels fits you best, sets up your preferences, and ends with your first brief in hand. ~13 minutes. |
| `/daily-sales-ritual` | Channel-aware daily fire. 3-column brief (what to do today, who to reach out to, what to say) plus a `Next Move` so you always know the one action to take right now. |
| `/rro-email` | Universal reach-out writer. 12-line email skeleton built around a real readiness check. Works for warm intros, re-engagement, referral asks, and partnership outreach. Three sequence variants included. |
| `/dream-100` | Top 100 relationship engine. Tracks the 100 people who could change your business — and builds toward it even if your list starts at zero. Switches modes automatically as your list grows. |

---

## Install

### Option 1 — Marketplace UI (recommended)

1. Open Claude Cowork → click your name (top right) → **Customize**
2. Click **+Plugins** → **Add Marketplace**
3. Search for `automatedmarketer/cowork-sales` → click **Install**

### Option 2 — Slash command

```
/plugin marketplace add automatedmarketer/cowork-sales
/plugin install cowork-sales@cowork-sales
```

## 🍎 ✅ Mac install (recommended): zip upload

This is the recommended install path for all Mac users. It bypasses Anthropic's open Cowork-on-macOS bugs (🚧 [#26951](https://github.com/anthropics/claude-code/issues/26951), 🚧 [#28125](https://github.com/anthropics/claude-code/issues/28125)) and works on every Cowork build that supports plugin uploads. Workaround confirmed by users in [#39400](https://github.com/anthropics/claude-code/issues/39400).

### ⏱️ 6 steps, ~30 seconds

1. **📦 Download** the latest **`cowork-sales-v0.1.0.zip`** (or `cowork-sales.zip`) from the [**Releases page → Assets**](https://github.com/AutomatedMarketer/cowork-sales/releases/latest). **Don't extract it.** Keep the file as a single `.zip`.
   > ⚠️ **Important:** download the zip from the **Releases page**, NOT the green **❌ Download ZIP** button at the top of the repo page. That button wraps the repo in an outer folder (`cowork-sales-main/`) which double-nests the plugin and breaks Cowork's validator.
2. **⚙️ Open Claude Cowork** (the middle tab in Claude Desktop) → click your name (top right) → **Settings**.
3. **🔌 Customize → Browse plugins** → look for the option to **upload a custom plugin file**.
   > 💡 Menu wording varies slightly between Cowork versions — look for "Upload", "Custom plugin", or "From file".
4. **📤 Drag in the zip.** Wait for confirmation.
5. **🚀 Open a brand new Cowork task** (skills load on session start, not retroactively).
6. Type `/onboard-sales` and follow the wizard.

> 💡 **Why this is the recommended Mac path:** Anthropic closed [#27196](https://github.com/anthropics/claude-code/issues/27196) ("All Anthropic plugins fail in Cowork on macOS") as **not planned** — they don't currently intend to fix the marketplace path on Mac. The zip-upload path is effectively the supported install method on macOS going forward.

### 🐛 Troubleshooting

| Symptom | What to do |
|---|---|
| 🔍 Can't find "Upload" / "Custom plugin" option | Look for "From file" / "Local plugin" / "Add manually". If genuinely absent, your Cowork version is older than the upload feature — 🔄 quit, update Claude Desktop, relaunch. |
| 📄 Upload rejects the file | Confirm the file extension is `.zip` (not `.plugin`). Re-download directly from the [Releases page](https://github.com/AutomatedMarketer/cowork-sales/releases/latest); don't rename. |
| 🚫 Plugin uploads but `/onboard-sales` does nothing | Open a **brand new** Cowork task. Skills load on session start, not retroactively. |
| 👻 Plugin disappears after restart | That's 🚧 [#38429](https://github.com/anthropics/claude-code/issues/38429) — Anthropic-side persistence bug. 🔄 Re-upload the zip after restart. |

---

## Quick start

```
/onboard-sales
```

That's it. The wizard walks you through 7 phases — about 13 minutes total. It reads your `business-brain.md` to understand your offer and your buyers, then asks a few questions to pick the right channels for you. When it's done, you have your first daily brief ready to act on.

The wizard is resumable — close it any time, pick up where you left off.

---

## Requirements

- **`cowork-ai-os >= 0.10`** — must be installed and onboarded first (the wizard needs `about-me/business-brain.md` to exist)
- **Gmail connector** — for reading sent history and drafting reach-outs
- **Fathom connector** — for pulling context from past sales calls

---

## Optional pairings

| Plugin | What it adds |
|---|---|
| `cowork-obsidian >= 0.5` | Mirror your briefs + contact notes into your vault automatically |
| `cowork-research >= 0.1` | Pull prospect intel (website audits, LinkedIn context) directly into your reach-out drafts |

---

## The 8 channels

The wizard will suggest 1–2 of these based on your business type. You confirm which ones fit, and your daily ritual pulls tactics from those channels every day.

| Channel | What it is |
|---|---|
| **Owned email list** | Your newsletter or broadcast list — people who already said yes |
| **Social presence** | Your profile + content on whichever platform your buyers use |
| **Online communities** | Groups, forums, Slack channels, Discord servers where your buyers gather |
| **Search & content** | Blog posts, YouTube videos, SEO — buyers finding you |
| **Cold outreach** | Direct messages to people you haven't met yet |
| **In-person & events** | Conferences, meetups, local networking |
| **Borrowed audience** | Podcasts, newsletters, joint ventures — showing up where someone else built the crowd |
| **Paid ads** | Running ads on any platform to put your offer in front of buyers |

---

## The 3 foundations

Every skill in this plugin is built on the same three rules:

- **Lazy-load** — Sales context only loads when a sales skill fires. Your session doesn't carry the weight of your entire contact list and offer library unless you're actually doing sales work.
- **Self-improving** — Every time a skill runs, it captures what worked and what didn't. Your daily ritual gets sharper the longer you use it.
- **Actionable** — Every output ends with a `Next move:` block. One action, clearly stated, with a reason. No output leaves you wondering what to do next.

---

## License

[MIT](./LICENSE) — yours forever.

## Author

[Nuno Tavares](https://nunomtavares.com) — Newsletter: [automatedmarketer.net](https://automatedmarketer.net) · YouTube: [@AutomatedMarketer](https://youtube.com/@AutomatedMarketer)

## Issues / contact

[github.com/AutomatedMarketer/cowork-sales/issues](https://github.com/AutomatedMarketer/cowork-sales/issues)
