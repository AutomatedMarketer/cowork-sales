# The 5-question Outreach Readiness Test

Before drafting ANY message, the user MUST answer these 5 questions. If they can't answer Q2, the skill halts and explains the RRO requirement.

## The 5 questions

1. **What are you selling, and who is it for?**
   - Format: `<offer name> | for <specific audience>`

2. **What changed that makes this message make sense today?** (THE RRO)
   - Must be a real, external-facing catalyst. Pick one of the 6 allowed categories (load banned-categories.md for the full list).

3. **What would a skeptical reader think?**
   - The user states what a skeptical reader might wonder. The skill uses this to pressure-test the RRO.

4. **What 3 facts prove your reason is real?**
   - Dates, numbers, names, events. Not vague claims. These become the proof density in lines 4-6 of the skeleton.

5. **What's the cleanest truthful explanation that benefits the buyer?**
   - One short sentence. This becomes line 7-9 of the skeleton.

## Validation rule

If any of the 5 questions returns vague or empty content, push back. Examples:
- ❌ Q2 = "It's been a while since I emailed" → fail (banned category — see banned-categories.md)
- ❌ Q4 = "Lots of clients have had results" → fail (no specifics)
- ✅ Q4 = "Tracy booked 2 interviews from one LinkedIn post last Tuesday" → pass

## After all 5 pass

Move to Step 3 of the SKILL.md flow (format selection).
