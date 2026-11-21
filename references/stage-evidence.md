# Stage Evidence

Reference for `funnel-bottleneck`: how to build comparable stage numbers, how much data a stage rate can carry, how to read changes, and how the stages look in different business models.

## Build stages on cohorts

- Group leads by lead date (or click date) and follow each cohort through booked, held and closed.
- A cohort is mature once it has had the measured lead-to-close lag. Measure the lag curve from the CRM's own lead and close dates rather than assuming a window. Exclude younger cohorts or label them immature, and state the share of each cohort still maturing.
- Show the ad-platform figure and the CRM figure side by side for each stage. Say which system each number comes from and when it was read or exported.
- Keep stage definitions constant across the comparison. If the meaning of "qualified" or of the conversion action changed, say so; the comparison breaks at that date.
- Split by source or campaign where you can. A blended funnel can hide a change in lead mix.

## How much data a rate can carry

It depends on the number of events, not on spend. Ask what one more or one fewer event does to the rate:

- 12 held calls: one deal moves close rate by about 8 points.
- 50 held calls: one deal moves it by 2 points.
- 200 held calls: one deal moves it by half a point.

When counts are small, pool a longer comparable window, say that you did, and treat a large-looking change as unconfirmed until more mature events arrive.

## Reading changes

- **One stage moved, the others held steady:** that stage is the first suspect. Confirm it with its own evidence (what changed, and when).
- **Adjacent stages moved together:** they may share one cause. A looser lead mix, for example, lowers both qualification and close rate. Test by segment before calling two separate breaks.
- **Everything a little soft at once:** check seasonality, lead-mix changes and measurement changes before optimizing any stage.
- **Everything steady, CAC still too high:** check whether the bid target, the budget or the available demand is the constraint before calling it unit economics (see CAC arithmetic below).

## CAC arithmetic

Break every comparison period into stage costs and stage yields, and run any scenario back through the stage rates. Compare same-term CPC beside blended CPC so a query-mix shift isn't read as an auction price change.

For a booked-call funnel:

CAC = CPC ÷ (LP CVR × booking rate × show rate × close rate)

It should match spend ÷ customers for the same cohort. In the SKILL.md example: $6.55 ÷ (0.050 × 0.69 × 0.23 × 0.29) ≈ $2,850, and $39,955 ÷ 14 customers ≈ $2,854.

Use it to test what one stage would have to be for CAC to meet the limit, holding the others at their observed values. If no plausible stage change gets there, check whether the effective bid target, budget or demand is the constraint: a tighter target CPA is a legitimate efficiency lever, with a volume tradeoff. If no workable target or stage change gets there, the constraint is economics, not a single stage.

Check KPI scope too. Campaign spend divided by customers from all sources isn't that campaign's cost per customer.

## Stage shapes by business model

These are the stages to measure, not target ranges.

| Model | Stages |
|---|---|
| B2B with booked calls | Click → lead → call booked → call held → opportunity → closed |
| Call-heavy healthcare or treatment | Click → call → qualified call (by duration or disposition) → admit or booked. The phone is the funnel: measure call quality by hour and source, not just volume. Admits can take weeks to mature; use the measured lag. Health-related outcome data has limits on what can be sent back to Google, so keep outcome evaluation in a system that's allowed to hold it. |
| Local services | Click → lead → appointment set → sold |
| E-commerce | Session → add to cart → checkout → purchase. Stages 3-5 collapse into cart and checkout steps. |
| Long-cycle B2B | Add opportunity and proposal stages, and allow a longer maturity window. |

## Why there are no benchmark tables

Earlier versions judged stages against industry ranges (LP CVR 3-8%, show rate 50-65%, close rate 15-30% and similar) and spend-based reliability floors (under $10K/mo is noise, $25K/mo is reliable). They're removed. Definitions, price and traffic mix vary too much for a borrowed range to call a stage broken, and reliability depends on event counts and cohort maturity, not spend.
