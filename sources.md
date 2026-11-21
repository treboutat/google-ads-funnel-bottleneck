# Sources & basis

This skill encodes TNT Growth's funnel bottleneck diagnostic, the stage-by-stage check run before touching an ad account. Its diagnostic rules follow TNT's approved Google Ads method, release `tnt-google-ads-2026-11-20.1`: the Account Audit book in performance-diagnosis mode and the Budget & Bid Optimization book. That means mature cohorts marked with the measured lag, ad-platform and CRM figures side by side, like-for-like comparisons with the account's own history, visible missing evidence, and no forced single root cause. Where this skill and the method disagree, the method governs.

## The stage model and decision tree
Localize the stage that accounts for the change, then route to the specific fix. The discipline: build stages on mature cohorts, don't scale spend into the stage that breaks the economics, and name one bottleneck when the evidence supports one, or the competing explanations and the deciding observation when it doesn't.

## What the November 2026 alignment changed
- **Cohort maturity** uses the lag curve measured from CRM dates in place of an assumed "normal" cycle, and states the share of each cohort still maturing.
- **Platform and CRM** figures are shown side by side for each stage, with a Coverage line in the output.
- **CPC** is read as same-term beside blended, so a query-mix shift isn't read as an auction price change.
- **"Everything steady, CAC still too high"** no longer goes straight to unit economics. The skill first checks whether the bid target, budget or demand is the constraint; a tighter target CPA is a legitimate efficiency lever with a volume tradeoff.
- **KPI scope and change ownership:** campaign spend divided by all-source customers isn't that campaign's cost per customer, and your own team's changes are ruled out first.
- **Budget:** no more budget into a broken stage still holds. Measurement doubt alone is no reason to cut working acquisition; size the exposure.
- **Lead quality** reads the qualified lead's customer rate per campaign or market.

No thresholds were added. The event-count examples (one deal on 12, 50 or 200 calls) are arithmetic, not rules.

## Comparisons
Stages are compared with the account's own comparable history and with what the acceptable cost per customer requires. Earlier versions used industry benchmark tables and spend-based reliability floors; both are removed, because stage definitions, price and traffic mix vary too much for borrowed ranges to decide that a stage is broken, and reliability depends on event counts and cohort maturity.

## Expected impact
Impact is stated as a direction plus scenario arithmetic on the user's own numbers, with the assumption labeled. It isn't a forecast.

## What this skill deliberately does not claim
- No client names or client results. Examples are hypothetical.
- No guaranteed outcomes and no universal benchmarks.
- Missing stage data isn't treated as proof of broken tracking or healthy ads.
