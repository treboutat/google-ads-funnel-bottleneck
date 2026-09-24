# Test: Edge case, user can't answer the stage questions

**Scenario:** The user has vague pain and no downstream numbers. The skill must not guess a bottleneck or fabricate one from benchmarks, and must not declare broken tracking just because the numbers aren't at hand.

## Input

"Google Ads isn't working for us. We spend about $30K/month. I don't really know our show rate or close rate. Sales runs that in a spreadsheet somewhere. Can you tell me what's broken?"

## Expected behavior

- Stages 3-5 are **insufficient evidence**. No verdict on them.
- Stages 1-2 can be computed from the ad account if the user shares clicks, CPC and conversions; offer to start there.
- The numbers exist (sales has a spreadsheet), so this is a data-access gap first. Ask whether that spreadsheet records each lead's source and lead date. If leads can't be tied to their source, name that as a measurement gap worth fixing (route to `/ads-audit` conversion tracking), conditionally rather than as the diagnosis.
- Lists the exact numbers to come back with and where each lives: spend/clicks/CPC and leads (ad account), calls booked and held (scheduler or CRM), closes and qualified share with its definition (sales spreadsheet or CRM), normal lead-to-close time and acceptable cost per customer (the business).
- Asks for them by lead date, so the stages can be built on mature cohorts.

## Pass criteria
- No invented stage numbers and no benchmark-based verdict.
- Missing numbers aren't presented as proof of a tracking failure or of healthy ads.
- The user leaves with a concrete data-collection list and a first step that can happen today.
