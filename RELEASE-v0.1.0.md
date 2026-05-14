# v0.1.0 — Initial Release: Cowork Sales

I built this because every solopreneur, coach, and agency owner hits the same wall: knowing they should do daily sales activity but not having a rhythm. Cowork Sales fixes that — personalized to where YOUR buyers actually live.

---

## What's in v0.1.0

- **4 skills:** `/onboard-sales`, `/daily-sales-ritual`, `/rro-email`, `/dream-100`
- **8-channel personalization** — owned email / social presence / online communities / search & content / cold outreach / in-person & events / borrowed audience / paid ads. The wizard picks the right 1–2 for your business type and builds your ritual around them.
- **Smart suggestions from your business-brain.md** — the wizard reads your offer, your ICP, and your current focus before it suggests anything. No generic advice.
- **`/dream-100` Build mode** — works even if your network starts at zero. The skill helps you find and warm up the right 100 people, not just manage ones you already have.
- **3 foundations baked into every skill:**
  - **Lazy-load** — sales context only loads when a sales skill fires. Clean sessions.
  - **Self-improving** — every skill run appends what worked and what didn't. Gets sharper over time.
  - **Actionable** — every output ends with a `Next move:` block. Subject + verb + timing + why. Always.

---

## Install

### Visual UI (easiest)

1. Open Claude Cowork → click your name (top right) → **Customize**
2. Click **+Plugins** → **Add Marketplace**
3. Search `automatedmarketer/cowork-sales` → click **Install**

### Slash commands

```
/plugin marketplace add automatedmarketer/cowork-sales
/plugin install cowork-sales@cowork-sales
```

### Mac fallback (if marketplace has issues)

1. Download `cowork-sales.zip` from the assets below
2. Open Claude Desktop → your name → **Settings**
3. **Plugins** → **Install from file** → select the zip

---

## Quick start

Run this:

```
/onboard-sales
```

The wizard walks you through 7 phases. Here's what each one does:

1. **Prereq check** — confirms cowork-ai-os is installed and your business-brain.md exists
2. **Identity read** — summarizes what it knows about you so you can confirm or correct it
3. **Offer clarity** — makes sure your offer is sharp enough to actually use in outreach
4. **Channel selection** — picks the 1–2 channels where your buyers actually are
5. **Outreach history** — captures what you've tried before (so it doesn't repeat your mistakes)
6. **Preferences setup** — cadence, streak rules, tone
7. **First brief** — hands you your Day 1 daily ritual, ready to act on

Total time: about 13 minutes. The wizard is resumable — stop any time, pick up where you left off.

---

## What this requires

- **`cowork-ai-os >= 0.10`** — must be installed and onboarded first. The wizard needs `about-me/business-brain.md` to exist before it can personalize anything.
- **Gmail connector** — for drafting and tracking outreach
- **Fathom connector** — for pulling context from past sales calls into your ritual

---

## What's coming in v0.2

- **`/find-leads`** — channel-specific prospecting. Different tactics per channel: LinkedIn search flow for B2B, community warm-up for course creators, referral-ask flow for coaches.
- **`/offer-doctor` standalone** — right now offer clarity lives inside `/onboard-sales` Phase 2 only. In v0.2 you'll be able to run it anytime your offer feels flat.
- **GHL + Apollo + HubSpot connectors** — for B2B users who are already working a CRM. People log syncs both ways.
- **Paid-ads management subcommands** — for users on Channel 8. Budget tracking, copy rotation log, A/B test notes, all inside your daily ritual.

---

Daily sales beats luck. This is the system. Run `/onboard-sales` — your future self will thank you.
