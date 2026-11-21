# Funnel Bottleneck Diagnostic

Walk a paid acquisition funnel stage by stage (CPC → landing page CVR → booking and show rate → close rate → qualification rate) on mature cohorts with ad-platform and CRM numbers side by side, compare each stage with your own history and your acceptable cost per customer, and find where it's actually breaking before anyone touches the ad account.

Most "the ads aren't working" problems aren't ad problems. This skill finds out where the break is, says how confident it is, and tells you what would settle it when the evidence points two ways.

## Who it's for
Founders and operators running paid acquisition who have vague performance pain ("CAC doubled", "leads are bad", "it stopped scaling") and want a stage-level answer instead of another round of guessing.

## Install

```bash
mkdir -p ~/.claude/skills/funnel-bottleneck
cp SKILL.md ~/.claude/skills/funnel-bottleneck/SKILL.md
cp -r references ~/.claude/skills/funnel-bottleneck/
```
Then describe your performance problem and share your funnel numbers.

## What you provide
A recent window and a comparable prior period by lead date, from your own Google Ads export or API and your own CRM: spend, clicks, blended CPC and CPC for the same search terms in both periods; leads and LP CVR; calls booked vs held; calls → closes; the share of leads sales marked qualified and how it's defined; your lead-to-close time measured from CRM dates; your acceptable cost per customer; and what changed recently, including changes your own team made. Missing some? The skill marks those stages "insufficient evidence" and tells you where each number lives.

## Files
- `SKILL.md`: the diagnostic
- `references/stage-evidence.md`: cohort building, how much data a rate can carry, reading changes, CAC arithmetic, stage shapes by business model
- `tests/`: worked example and edge cases (no data, two stages moving at once)

## What changed in November 2026
Aligned with TNT's approved Google Ads method, release 2026-11-20.1. Cohort maturity now comes from the lead-to-close lag measured in your CRM, and the readout states the share of each cohort still maturing. Ad-platform and CRM figures sit side by side for each stage, with a new Coverage line in the output. CPC is read as same-term beside blended, so a query-mix shift isn't mistaken for an auction price change. Before calling a problem unit economics, the skill checks whether the bid target, budget or demand is the constraint. It checks KPI scope, asks who changes the account and rules out your own team's changes first, reads the qualified lead's customer rate per campaign or market, and says plainly that measurement doubt alone is no reason to cut working acquisition.

## What changed in September 2026
Stages are now judged against the account's own comparable history and the acceptable cost per customer; the industry benchmark tables and spend-based reliability floors are removed. Stage rates are built on mature cohorts from the same leads. The skill still names one bottleneck when the evidence supports it, but no longer forces one with an "upstream wins" tie-break; when two explanations remain, it names the observation that separates them. Expected impact is shown as labeled scenario arithmetic, not a forecast.

---
From [TNT Growth](https://tntgrowth.com/skills?utm_source=github&utm_campaign=treboutat). Want us to run the diagnosis on your account? Start at the link.
