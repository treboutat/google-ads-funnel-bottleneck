# Test: Edge case, two stages moving at once

**Scenario:** Two stages look worse at the same time, but one rests on a small, immature sample. The skill must weigh the evidence behind each rate and cohort maturity, not apply an "upstream wins" tie-break or a spend-based reliability rule.

## Input

"$12K/mo spend, last 30 days: LP CVR dropped from 6% to 3.8% (about 2,000 clicks). Close rate dropped from 25% to 15% (3 closes from 20 held calls). Our sales cycle is about 3 weeks. We swapped in a new landing page three weeks ago. Which do we fix?"

## Expected behavior

- **LP CVR** is the supported constraint: about 76 leads instead of roughly 120 on ~2,000 clicks, a material change that lines up with the page swap. Fix list targets the page (form, mobile rendering, message fit, what changed in the swap).
- **Close rate** is reported with its count and maturity: 3 of 20 vs an expected 5, a two-deal difference, and most of those calls are younger than the 3-week cycle. Status: insufficient evidence. It isn't declared broken.
- Asks whether the 3-week cycle is measured from CRM lead and close dates. Until it is, the maturity call rests on an assumed window, and the readout states the share of post-swap cohorts still maturing.
- Confirms the page swap was the user's own change and checks whether anything else changed in the window (targets, campaigns, tracking) before attributing the LP CVR drop to it.
- Checks that the conversion action still counts the same thing on the new page, using CRM lead counts beside Google Ads leads, so a tracking change isn't read as a conversion-rate drop.
- Says why the two might be linked (the new page may attract a different lead mix, which would lower close rate too) and names the observation that separates them: close rate on mature cohorts, split by old-page vs new-page leads.
- Close rate becomes a monitoring item with a re-read date once the post-swap cohorts are older than 3 weeks.

## Pass criteria
- One stage is named because the evidence supports it, not because of an upstream tie-break rule.
- The close-rate change is shown with its event count and cohort maturity.
- No "under $25K/mo is unreliable" spend rule.
- The second stage gets a specific re-read condition, not a second simultaneous fix.
- The Coverage line names the lag basis (assumed until measured) and the share of cohorts still maturing.
