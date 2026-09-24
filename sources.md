# Sources & basis

This skill encodes TNT Growth's funnel bottleneck diagnostic, the stage-by-stage check run before touching an ad account. Its diagnostic rules follow TNT's approved Google Ads audit method (Account Audit book, release `tnt-google-ads-2026-09-07.1`): mature cohorts, the account's own comparable history, visible missing evidence, and no forced single root cause.

## The stage model and decision tree
Localize the stage that accounts for the change, then route to the specific fix. The discipline: build stages on mature cohorts, don't scale spend into the stage that breaks the economics, and name one bottleneck when the evidence supports one, or the competing explanations and the deciding observation when it doesn't.

## Comparisons
Stages are compared with the account's own comparable history and with what the acceptable cost per customer requires. Earlier versions used industry benchmark tables and spend-based reliability floors; both are removed, because stage definitions, price and traffic mix vary too much for borrowed ranges to decide that a stage is broken, and reliability depends on event counts and cohort maturity.

## Expected impact
Impact is stated as a direction plus scenario arithmetic on the user's own numbers, with the assumption labeled. It isn't a forecast.

## What this skill deliberately does not claim
- No client names or client results. Examples are hypothetical.
- No guaranteed outcomes and no universal benchmarks.
- Missing stage data isn't treated as proof of broken tracking or healthy ads.
