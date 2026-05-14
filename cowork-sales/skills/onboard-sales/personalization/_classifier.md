# Business-type classifier

> Used by `/onboard-sales` Phase 2 to pick a personalization profile from `business-brain.md`.

## Detection logic (in order — first match wins)

1. If business-brain mentions **B2B audience, CEOs, founders, agency owners, SaaS, enterprise** → Profile 01 (B2B services)
2. If business-brain mentions **course creator, info-product, online course, students, students-as-buyers** → Profile 02 (Course creator)
3. If business-brain mentions **local business, walk-in, neighborhood, city-specific, brick-and-mortar** → Profile 03 (Local service)
4. If business-brain mentions **creator, influencer, content creator, audience-based business, monetize content** → Profile 04 (Creator/influencer)
5. If business-brain mentions **ecommerce, e-com, physical product, dropshipping, brand, DTC** → Profile 05 (E-commerce)
6. If business-brain mentions **coach + existing network OR Top 100 OR podcast guesting** → Profile 06 (Coach with network)
7. If business-brain mentions **new, just started, no audience yet, building from scratch, brand new** → Profile 07 (New solopreneur)
8. Default if none match → Profile 07 (New solopreneur) with note: "I wasn't sure which profile fits you. I'll start with the most universal setup. You can override during Phase 2."

## After classification

The wizard MUST:
- Tell the user which profile was detected
- Show the user the suggested channels
- Explicitly allow override: "Here are all 8 — pick 1-2 PRIMARY for YOU."
- Save the chosen profile + channels in `sales-preferences.md`
