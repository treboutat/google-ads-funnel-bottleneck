---
name: funnel-bottleneck
description: Diagnose where a paid acquisition funnel is broken. Use when a user says "ads aren't working", "CAC is too high", "leads are bad", "find the bottleneck", "why isn't this scaling", or describes vague performance pain. Walks the funnel stage-by-stage (CPC → LP CVR → lead-to-call show → call-to-close → qualification rate) and pinpoints the exact stage that is broken with the root-cause fix.
---

# Funnel Bottleneck Diagnostic

The framework that separates operators who scale from operators who guess: **"Where is performance breaking?"** Strong answers pinpoint the exact stage. Weak answers cite symptoms ("CPCs are too high"). This skill forces a strong answer.

## How to use

When a user surfaces a paid acquisition problem, never solve at the symptom layer. Walk the funnel from top to bottom, get a number for each stage, then declare the bottleneck.

## The 5 stages (in order)

For each stage, you need: **actual number**, **target/expected number**, **delta**, and a **judgment** (healthy / soft / broken).

| # | Stage | Metric | Healthy benchmark (B2B SaaS, $50-500K/mo) |
|---|-------|--------|-------------------------------------------|
| 1 | Click acquisition | CPC | Within 1.5x of competitor median |
| 2 | Click → Lead | Landing page CVR | 3-8% on cold paid traffic |
| 3 | Lead → Call held | Show rate | 50-65% on inbound, 25-40% on outbound |
| 4 | Call → Close | Close rate | 15-30% of calls held |
| 5 | All-funnel | Qualified-lead rate | 40-60% of raw leads |

Benchmarks vary by industry — quote them as guidance, not verdict. Always ask the user for their historical baseline first; their own baseline beats any industry table. Vertical-specific ranges live in `references/funnel-benchmarks.md`.

## The diagnostic script

Run through these questions in order. Do not skip ahead.

### Step 1 — Get the numbers

Ask the user for the last 30-90 days:
1. Spend, clicks, average CPC
2. Conversions (form fills / leads), landing page CVR
3. Calls scheduled and calls held (show rate)
4. Calls held → opportunities → closed deals
5. Of the raw leads, what % did sales mark as qualified?

If they don't know any of these, **that is the diagnosis** — they have a tracking problem, not a media problem. Skill output: "Fix tracking before scaling spend. See `/ads-audit` Section A."

### Step 2 — Compare each stage to baseline

For each stage, compute the delta from the user's own historical baseline (preferred) or industry benchmark (fallback). Flag the stage with the largest negative delta.

### Step 3 — Localize the bottleneck

Apply this decision tree:

- **CPC up >30% with same CVR downstream** → keyword/match-type issue or auction pressure. Run `/ads-audit` keyword section.
- **CPC normal, LP CVR collapsed** → landing page or offer problem. Audit form length, page speed, headline-to-keyword match, social proof.
- **LP CVR normal, show rate collapsed** → lead quality or scheduling friction. Check (a) is the conversion action upper-funnel? (b) is the booking flow broken? (c) are inbound texts/emails getting through?
- **Show rate normal, close rate collapsed** → ICP mismatch (the wrong people are showing up) OR a sales process issue. Pull the loss reasons from the CRM. If reasons skew "not a fit" / "no budget" → marketing problem (targeting). If reasons skew "went with competitor" / "timing" → sales problem.
- **Close rate normal, qualified-lead rate low** → upper-funnel conversion is too loose. Move the primary conversion action down-funnel and retrain the algorithm.
- **All stages within range, but CAC still high** → it's a unit-economics problem, not a funnel problem. Move to LTV/payback work, not optimization.

### Step 4 — Output the diagnosis

Always produce **exactly this** structure. No preamble.

---

**Where it's breaking:** [Stage name + the metric, e.g. "Stage 3: Lead → Call held. Show rate is 22% vs 55% historical."]

**Why it's breaking:** [Single root cause, max two sentences. No hedging.]

**The fix:** [Numbered, specific, executable. Each step has an owner and an expected outcome.]
1. ...
2. ...
3. ...

**Expected impact:** [Quantified from the user's own numbers. e.g. "Show rate 22% → 50% recovers ~28 calls/mo at current lead volume, which is ~7 closed deals at 25% close rate."]

**What to monitor next:** [The leading indicator that tells you the fix is working before lagging revenue arrives — usually a daily metric, not weekly.]

---

## Example run

**User's numbers (last 60 days, B2B services, $40K/mo):**
- 6,100 clicks at $6.55 CPC (historical: ~$6.20 — fine)
- 305 leads → LP CVR 5.0% (historical: 5.2% — fine)
- 210 calls scheduled, 48 held → **show rate 23%** (historical: 55%)
- 14 closed from 48 calls → close rate 29% (historical: 27% — fine)

**Diagnosis output:**

**Where it's breaking:** Stage 3: Lead → Call held. Show rate is 23% vs 55% historical.

**Why it's breaking:** Booking confirmations are landing in spam since the domain migration in April; leads book and never receive the calendar invite.

**The fix:**
1. Re-authenticate sending domain (SPF/DKIM/DMARC) — owner: ops; invites land in inbox again.
2. Add SMS confirmation + 1-hour reminder — owner: ops; catches leads email misses.
3. Re-contact the last 60 days of no-shows with a rebooking link — owner: SDR; recovers booked-but-ghosted pipeline.

**Expected impact:** Show rate 23% → 50%+ recovers ~57 held calls/mo at current lead volume — ~15 closed deals at the intact 29% close rate, roughly doubling closes with zero extra ad spend.

**What to monitor next:** Daily show rate on rebooked cohort; confirmation-email open rate.

Notice what the skill did *not* do: touch the ads. CPC and CVR were healthy — spending more or "optimizing" the account would have paid for more no-shows.

## Hard rules

- Never recommend "increase budget" if any downstream stage is broken. Spending more on a leaky funnel just makes the leak louder.
- If the user can't answer any stage, stop the diagnostic and run `/ads-audit` Section A first.
- Never name more than one bottleneck. The whole point is to force focus. If two stages tie, pick the one closest to the top of the funnel — fixing earlier stages compounds.
- Quote numbers, not adjectives. "Show rate is 22%" not "show rate is low".
- If the user is sub-$10K/mo spend, statistical noise dominates and stage-level diagnostics are unreliable. Tell them so and recommend hitting $25K/mo before re-running.

## Common founder traps to call out

- **"CPCs are too high"** — usually not the real problem. Trace forward to LP CVR before agreeing.
- **"We need more leads"** — usually false at small/mid scale. Trace down to close rate first; doubling close rate is cheaper than doubling leads.
- **"The agency is bad"** — sometimes true, but verify by stage. If LP CVR is the bottleneck, no media buyer can fix it.
- **"Let's switch channels"** — channel-switching without a stage diagnosis usually rebuilds the same funnel with the same break.

## Related skills

- **`/ads-audit`** — When Stage 1-2 (or missing data) points at the account itself, the 34-point audit localizes what's broken inside Google Ads.
- **`/search-term-scorer`** — When the CPC/keyword layer is the bottleneck, score the search terms and cut the waste.

## Tone

Diagnostic, surgical, operator-to-operator. No empathy padding. The user is paying for a verdict.
