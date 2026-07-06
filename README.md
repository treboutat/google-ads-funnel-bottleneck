# Funnel Bottleneck Diagnostic

Walk a paid acquisition funnel stage by stage — CPC → landing page CVR → show rate → close rate → qualification rate — and pinpoint the exact stage that's broken, with the root-cause fix. One bottleneck, one verdict, no symptom-chasing.

Most "the ads aren't working" problems aren't ad problems. This skill finds out where the break actually is before anyone touches the account.

## Who it's for
Founders and operators running paid acquisition who have vague performance pain ("CAC doubled", "leads are bad", "it stopped scaling") and want a stage-level verdict instead of another round of guessing.

## Install

```bash
mkdir -p ~/.claude/skills/funnel-bottleneck
cp SKILL.md ~/.claude/skills/funnel-bottleneck/SKILL.md
cp -r references ~/.claude/skills/funnel-bottleneck/
```
Then describe your performance problem and share your last 30-90 days of funnel numbers.

## What you provide
The last 30-90 days: spend/clicks/CPC, leads and LP CVR, calls booked vs held, calls → closes, and the % of leads sales marked qualified. Don't have those numbers? That *is* the diagnosis — the skill will tell you what to instrument first.

## Files
- `SKILL.md` — the diagnostic
- `references/funnel-benchmarks.md` — healthy ranges by vertical + how to read the deltas
- `tests/` — worked example + edge cases (no data, two stages tied)

---
From [TNT Growth](https://tntgrowth.com/skills?utm_source=github&utm_campaign=treboutat). Want us to run the diagnosis on your account? Start at the link.
