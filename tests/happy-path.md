# Test: Happy path

**Scenario:** A B2B services company with full-funnel numbers on mature cohorts and a collapsed show rate. The skill should walk every stage with counts, compare each with the account's own history, name the bottleneck the evidence supports, and state impact as labeled scenario arithmetic.

## Input

"Our ads stopped working. CAC basically doubled. Here's the 60 days ending 10 days ago (in our CRM, lead to close runs under 10 days for nearly every deal): $40K spend, 6,100 clicks, $6.55 CPC (used to be ~$6.20). 305 leads. 210 calls booked but only 48 held. 14 closed. Historically we held about 55% of booked calls and closed ~27%. Same search terms cost about 3% more than before. Google Ads shows 305 leads; our CRM has 301. We moved our email sending domain on April 14. Nobody changed campaigns, targets or pages in the window."

## Expected behavior

- Computes every stage with counts: LP CVR 5.0% (305 of 6,100), booking rate 69% (210 of 305), show rate **23% (48 of 210) vs 55% history**, close rate 29% (14 of 48).
- Shows ad-platform and CRM lead counts side by side (305 vs 301) and splits the CPC rise into about 3% same-term and the rest query mix; neither explains a doubled CAC.
- Treats the lag as measured from CRM dates and says no cohort is still maturing.
- Names **one** bottleneck because the evidence supports one: Stage 3, Lead → call held. The other stages are within their own history.
- Connects the April 14 domain move to the show-rate drop only as far as the evidence goes, and asks for or cites confirming evidence (confirmation deliverability, timing of the drop) rather than asserting it.
- Doesn't recommend ad-account changes or more budget.
- Expected impact: if show rate returns to 55% at current booking volume, ~115 held calls instead of 48 over 60 days and ~33 closes instead of 14 at the current close rate, labeled as arithmetic on an assumption.
- Output follows the format: Where / Why / Fix (numbered, owners) / Expected impact / What to monitor next / Coverage.

## Pass criteria
- Every stage has a number, its count, a comparison with the account's history and a status.
- No industry benchmark range is used to judge a stage.
- Impact is labeled as scenario arithmetic, not a forecast.
- No "increase budget" or ad-optimization advice while the show-rate break is unresolved.
- The cause is stated with its evidence and confidence, not invented.
- Platform and CRM figures appear side by side where both exist, and the readout ends with a Coverage line (lag basis, share still maturing, sources and their dates).
