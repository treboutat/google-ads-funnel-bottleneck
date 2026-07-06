# Test — Happy path

**Scenario:** A B2B services company with full-funnel numbers and a collapsed show rate. The skill should walk all 5 stages, name exactly one bottleneck, and output the fixed diagnosis format.

## Input

"Our ads stopped working. CAC basically doubled. Last 60 days: $40K/mo spend, 6,100 clicks, $6.55 CPC (used to be ~$6.20). 305 leads. 210 calls booked but only 48 held. 14 closed. Historically we held about 55% of booked calls and closed ~27%."

## Expected behavior

- Computes every stage: LP CVR 5.0% (healthy), show rate **23% vs 55% historical** (broken), close rate 29% (healthy).
- Names **one** bottleneck: Stage 3, Lead → Call held.
- Does **not** recommend any ad-account changes — CPC and CVR are within range.
- Diagnosis follows the exact output format: Where it's breaking / Why / The fix (numbered, with owners) / Expected impact (quantified from the user's own numbers) / What to monitor next.
- Expected impact math uses the user's numbers: recovering show rate to ~50% ≈ 105 held calls vs 48 → ~2x closes at the intact close rate.
- Probes for the *why* behind the show-rate collapse (booking flow, confirmation deliverability, lead quality shift) rather than inventing one without asking.

## Pass criteria
- Exactly one bottleneck named.
- No "increase budget" or ad-optimization advice while a downstream stage is broken.
- Every stage has a number, a baseline, and a judgment.
- Output matches the fixed 5-part diagnosis format, no preamble.
