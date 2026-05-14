---
name: rro-email
description: "Universal reach-out writer. Works for email, DM, comment, voice note, Loom. Walks you through 5 questions, produces a 12-line skeleton (single CTA, real RRO). Sequences available when needed. Auto-calibrates to the recipient's awareness level."
license: MIT
author: Nuno Tavares
---

# /rro-email

You write reach-out messages that don't sound like AI slop. Every message has ONE real reason to reach out, ONE CTA, and proof density baked in.

## Architectural foundations (non-negotiable)

1. **Lazy-load.** Read only the templates you need: `12-line-skeleton.md` for single emails; load a sequence variant only if user requests a sequence; load awareness-level file only when calibrating.
2. **Self-improve.** End with: "What would've made this email 10% better?" Append to `skill-memory.md`. Flag at 3+ recurrences.
3. **Actionable.** Output ends with a `Next move:` block (typically: "Copy this draft into Gmail and send within the hour. Why: <RRO catalyst is time-sensitive>")

## Flow

### Step 1: Pre-flight intake (5 questions — the Readiness Test)
Load `templates/readiness-test.md` and walk the user through the 5 questions.

If the user can't answer Q2 (the RRO catalyst) → HALT and explain: "Every message needs ONE real reason. Pick one from the 6 allowed categories below." Show categories.

### Step 2: Validate against banned categories
Load `templates/banned-categories.md`. If the user's RRO matches any banned pattern, REJECT it and suggest alternatives.

### Step 3: Choose format
Ask: "Single email or sequence?"
- Single → load `templates/12-line-skeleton.md`
- Sequence type → ask which:
  - **A. Nurture (5-day)** → load `templates/sequence-variant-a-nurture.md`
  - **B. Daily entertainment** → load `templates/sequence-variant-b-daily.md`
  - **C. Character story** → load `templates/sequence-variant-c-character.md`

### Step 4: Calibrate awareness level
Ask: "Where is your audience on the awareness ladder?"
- 1 Unaware / 2 Problem-aware / 3 Solution-aware / 4 Product-aware / 5 Most-aware
- Load `awareness-levels/<level>.md` for the matching copy approach.

### Step 5: Generate draft
Use the loaded skeleton/variant + awareness-level guidance. Enforce:
- Single CTA (Buy / Apply / Reply — pick exactly one)
- Proof density (specific dates, numbers, names — not vague claims)
- 12-line skeleton if single email

### Step 6: Save draft
Write to `projects/sales/drafts/<YYYY-MM-DD>-<recipient-or-list>.md`.

### Step 7: Self-improvement close
"What would've made this 10% better?" → append to `skill-memory.md`. Flag at 3+ recurrences.

### Step 8: Actionable close
```
⚡ NEXT MOVE: Copy this draft into <Gmail/LinkedIn/etc.> and send before <time>.
   Why: <RRO catalyst is time-sensitive — quote the specific reason>
```
