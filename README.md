# Cowork Sales

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](./LICENSE)
[![Version](https://img.shields.io/badge/version-0.1.0-brightgreen.svg?style=flat-square)](./CHANGELOG.md)
[![Platform: Mac · Windows · Linux](https://img.shields.io/badge/platform-Mac%20%C2%B7%20Windows%20%C2%B7%20Linux-blue.svg?style=flat-square)](#install)
[![Built for Claude Cowork](https://img.shields.io/badge/built%20for-Claude%20Cowork-7C3AED.svg?style=flat-square)](https://claude.com/product/claude-code)

**Your personalized daily sales ritual, attached to your Cowork AI OS.**

A [Claude Cowork](https://claude.com/product/claude-code) plugin that gives you a daily sales rhythm — personalized to where YOUR buyers actually hang out. 7-phase setup wizard. Channel-aware brief every morning. Reach-out writer for warm conversations. Optional Top 100 relationship engine. Everything ties back to what's already in your business brain, so it knows your offer, your buyers, and your voice before it gives you a single suggestion.

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

### Option 3 — Mac fallback (if marketplace has issues)

1. Download `cowork-sales.zip` from the [latest release](https://github.com/AutomatedMarketer/cowork-sales/releases/latest)
2. Open Claude Desktop → your name → **Settings**
3. **Plugins** → **Install from file** → pick the zip

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
