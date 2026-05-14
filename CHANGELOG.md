# Changelog

All notable changes to cowork-sales will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versioning is [SemVer](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

## [0.1.0] — 2026-05-14

### Added
- 4 skills bundled:
  - `/onboard-sales` — 7-phase personalized wizard with smart-suggestion layer reading business-brain.md
  - `/daily-sales-ritual` — channel-aware daily fire with buyer-pyramid scoring
  - `/rro-email` — universal RRO writer with 5-question Readiness Test, 12-line skeleton, 3 sequence variants, 5 awareness levels, banned-category enforcement
  - `/dream-100` — data-driven Build/Operate/Prune modes; give-2x-before-ask hard rule
- 8-channel personalization engine (owned email / social / communities / search & content / cold outreach / in-person / borrowed audience / paid ads)
- 7 personalization profiles (B2B / course-creator / local-service / creator-influencer / e-commerce / coach-with-network / new-solopreneur)
- 3 architectural foundations: lazy-load context + self-improving skills + actionable output (Next Move block on every output)
- Forgiving streak policy (1-day gap = preserved, 2-3 days = flag, 7+ days = soft reset)
- Memory hot/cold split (30-entry cap + silent archive)
- Soft-depends on cowork-ai-os >= 0.10
- Loose-couples with cowork-obsidian >= 0.5 (vault mirror) + cowork-research >= 0.1 (prospect intel)
- MIT license

### Verified
- 17-test verification matrix passes on clean machine
- ZERO guru-name leakage in any plugin file (grep audit)
- Wizard end-to-end ≤15 min on test profile
- All 4 skills end with parseable `Next move:` block
- /dream-100 file-state mode switching works (Build → Operate at 5+ names; Operate → Prune at 100+)
