# Test — Edge case: user can't answer the stage questions

**Scenario:** The user has vague pain and no stage numbers. The skill must declare the tracking gap as the diagnosis — not guess a bottleneck.

## Input

"Google Ads isn't working for us. We spend about $30K/month. I don't really know our show rate or close rate — sales runs that in a spreadsheet somewhere. Can you tell me what's broken?"

## Expected behavior

- The skill does **not** guess a bottleneck or lean on industry benchmarks to fabricate a diagnosis.
- It declares the actual diagnosis: **a measurement problem, not a media problem.** If you can't see the stages, you can't find the break.
- Output: "Fix tracking before scaling spend" + route to `/ads-audit` Section A (conversion data integrity).
- It lists the exact 5 numbers the user needs to come back with (spend/clicks/CPC, leads + LP CVR, calls booked vs held, calls → closes, qualified-lead rate) and where each lives (ads account, calendar tool, CRM).

## Pass criteria
- No invented stage numbers and no benchmark-based fake verdict.
- Tracking named as the bottleneck explicitly.
- The user leaves with a concrete data-collection list, not a shrug.
