---
name: funnel-bottleneck
description: Diagnose where a paid acquisition funnel is losing customers or money. Use when a user says "ads aren't working", "CAC is too high", "leads are bad", "find the bottleneck", "why isn't this scaling", or describes vague performance pain. Walks the funnel stage by stage (click cost, click to lead, lead to call held, call to close, lead quality) on mature cohorts, compares each stage with the account's own comparable history and the business's acceptable cost per customer, and names the constraint the evidence supports, or the observation that would separate competing explanations.
---

# Funnel Bottleneck Diagnostic

The question that separates operators who scale from operators who guess: **"Where is performance breaking?"** Strong answers point at a stage, with evidence. Weak answers cite a symptom ("CPCs are too high"). This skill forces the stage-level question before anyone touches the ad account.

## How to use

When a user raises a paid acquisition problem, don't solve at the symptom layer. Build the funnel on comparable, mature cohorts, get a number for each stage, compare it with the account's own history and the business's economics, then name the constraint the evidence supports.

## The stages

| # | Stage | Metrics |
|---|---|---|
| 1 | Click acquisition | CPC, clicks |
| 2 | Click → lead | Landing page conversion rate |
| 3 | Lead → call held | Booking rate (scheduled ÷ leads), show rate (held ÷ scheduled) |
| 4 | Call → close | Close rate (closed ÷ held) |
| 5 | Lead quality | Share of leads sales accepts as qualified, and the definition used |

For each stage record: the actual number and how many events sit behind it, the comparison, the change, a status (**healthy**, **soft**, **broken**, **insufficient evidence**) and your confidence. "Broken" means a concrete, material change or defect you can point to. "Soft" means it moved, but noise, seasonality or mix could explain it.

For e-commerce, call-heavy healthcare and local services, the stage shapes differ; see `references/stage-evidence.md`.

This skill doesn't judge stages against industry benchmark tables. Offer, price, traffic mix and stage definitions vary too much for someone else's range to call your stage broken. The tests are the account's own comparable history and what the acceptable cost per customer requires.

## The diagnostic script

Work through these in order.

### Step 1: Get the numbers on mature cohorts

Ask for the last 30-90 days, grouped by lead date (or click date):

1. Spend, clicks, average CPC
2. Leads, what the conversion counts, and landing page CVR
3. Calls scheduled and calls held
4. Calls held → opportunities → closed deals
5. Share of leads sales marked qualified, and how "qualified" is defined
6. Normal time from lead to close, and the acceptable cost per customer
7. What changed and when: campaigns, bids, pages, offer, sales process, staffing, tracking, season

Build each stage on the cohort that produced it. Deals closed this month may come from last month's leads, so dividing this month's closes by this month's calls misstates close rate. Leave out cohorts younger than the normal close cycle, or label them immature.

If the user can't supply a stage, that stage is **insufficient evidence**. Say which system holds the number (ad account, scheduler, CRM) and what it takes to get it. Missing numbers don't prove tracking is broken, and they don't prove the ads are fine. If leads can't be tied back to their source at all, that measurement gap is worth fixing, and `/ads-audit` conversion tracking covers it.

### Step 2: Compare each stage

Compare with the account's own comparable history: same stage definitions, similar season, mature cohorts. Say how many events sit behind each rate. A close rate on 12 calls moves 8 points on a single deal.

If there's no comparable history, don't borrow an industry range. Instead:

- Compute cost per customer from the stages and compare it with the acceptable limit: CAC = CPC ÷ (LP CVR × booking rate × show rate × close rate), which should match spend ÷ customers. Work out what a stage would need to be for CAC to meet the limit.
- Check each stage for an observable defect: a broken form, booking-flow errors, confirmations not arriving, slow follow-up, a qualification rule that changed.
- Name the comparison that would locate the break: a prior period, a cohort, a source split, a controlled test.

### Step 3: Localize the constraint

These are starting hypotheses. Each needs its own evidence.

- **CPC up materially, downstream rates steady** → auction or targeting change. Check auction insights, match types and AI Max settings, bid targets, new competitors and query mix. Inside the account, route to the `/ads-audit` targeting and bidding keys.
- **CPC steady, landing page CVR down** → page or offer. Check the page loads and works on mobile, the form actually submits into the CRM, the message still fits the searches and ads, and what changed on the site.
- **LP CVR steady, booking or show rate down** → scheduling friction or a lead-mix shift. Is the booking flow working? Are confirmations and reminders arriving? Did the lead mix change (and did what the conversion action counts change)?
- **Show rate steady, close rate down** → fit or sales process. Pull loss reasons from the CRM. "Not a fit" or "no budget" points at targeting and qualification; "went with competitor" or "timing" points at the sales process or offer. Check sales staffing and process changes too.
- **Close rate steady, qualification rate low** → the conversion event may reward loose leads. Check whether a more predictive intermediate stage would give timely feedback before changing what bidding optimizes toward.
- **Every stage steady, CAC still too high** → unit economics (price, value, payback), or the stage math never worked at this price. That's a business model question, not an optimization one.

If one stage clearly accounts for the change, name it. If two stages moved together, say whether one plausibly drives the other (a looser lead mix closes worse) and name the observation that separates them, such as close rate for leads from unchanged pages or close rate by source. Don't force a single bottleneck the evidence doesn't support.

### Step 4: Output the diagnosis

Use this structure. No preamble.

---

**Where it's breaking:** [Stage and metric vs its comparison, with event counts. e.g. "Stage 3: Lead → call held. Show rate 23% (48 of 210) vs 55% over the prior six months." If two explanations remain, name both and the observation that decides between them.]

**Why it's breaking:** [The supported cause, its evidence and your confidence. Keep observed fact, diagnosis and what still needs testing separate.]

**The fix:** [Numbered, specific, executable. Each step has an owner ("unassigned" if nobody has agreed yet) and what it should change.]
1. ...
2. ...
3. ...

**Expected impact:** [Direction, plus scenario arithmetic on the user's own numbers with the assumption labeled. e.g. "If show rate returns to its 55% history at current booking volume: ~115 held calls instead of 48 over 60 days, ~33 closes instead of 14 at the current close rate. Arithmetic on an assumption, not a forecast."]

**What to monitor next:** [The leading indicator that shows the fix working before revenue catches up, and when to re-read the full funnel on mature cohorts.]

---

## Example run (hypothetical)

**User's numbers:** B2B services. Window: the 60 days ending 10 days ago, so every lead has had a full sales cycle (usually under 10 days). Spend $40K.
- 6,100 clicks at $6.55 CPC (prior six months: ~$6.20)
- 305 leads → LP CVR 5.0% (prior: 5.2%)
- 210 calls scheduled (69% of leads), 48 held → **show rate 23%** (prior: 55%)
- 14 closed from 48 held → close rate 29% (prior: 27%)
- Changes: sending domain migrated April 14; booking confirmations now go out from the new domain.

**Where it's breaking:** Stage 3, Lead → call held. Show rate 23% (48 of 210) vs 55% over the prior six months. CPC, LP CVR and close rate are within their normal movement.

**Why it's breaking:** Booking confirmations stopped reaching inboxes after the April 14 domain migration. The email platform shows confirmations landing in spam since that date, and show rate fell the same week. Confidence: high on timing; confirm with an inbox placement test.

**The fix:**
1. Re-authenticate the sending domain (SPF, DKIM, DMARC). Owner: ops. Should restore inbox delivery of invites.
2. Add an SMS confirmation and a 1-hour reminder. Owner: ops. Covers leads the email misses.
3. Re-contact the last 60 days of no-shows with a rebooking link. Owner: SDR. Recovers booked-but-missed pipeline.

**Expected impact:** If show rate returns to its 55% history at current booking volume, that's ~115 held calls instead of 48 over 60 days, and ~33 closes instead of 14 at the current 29% close rate. That's arithmetic on an assumption, not a forecast; recovered no-shows may close at a different rate.

**What to monitor next:** Daily show rate on newly booked calls and confirmation inbox placement. Re-read the full funnel once the first post-fix cohort has completed a sales cycle.

Notice what the skill did *not* do: touch the ads. CPC and CVR held within their own history, so spending more or "optimizing" the account would have bought more no-shows.

## Hard rules

- **Build stages on mature cohorts from the same leads.** Don't divide this month's closes by this month's calls when the sales cycle crosses months.
- **Compare with the account's own comparable history or the acceptable cost per customer**, not an industry table.
- **Don't recommend more budget while the stage that makes the economics fail is broken.** Adding spend to a leak buys more of the leak. Scaling needs profitable additional demand, reliable measurement and capacity.
- **Missing numbers are insufficient evidence.** Say where they live and how to get them.
- **Name one bottleneck when the evidence supports one.** When it doesn't, name the competing explanations and the observation that separates them.
- **Quote numbers with their counts.** "Show rate is 22% on 48 held calls," not "show rate is low."
- **No invented lift.** Impact is the expected direction plus labeled scenario arithmetic on the user's own numbers.

## Common founder traps to call out

- **"CPCs are too high."** Check what CPC does to CAC after the downstream stages before agreeing.
- **"We need more leads."** Check show and close rates first. More leads through a leaking stage raises CAC.
- **"The agency is bad."** Sometimes true. Verify by stage: if the landing page or the sales process is the constraint, no media buyer can fix it.
- **"Let's switch channels."** Without a stage diagnosis, a new channel can feed the same break.

## Related skills

- **[`ads-audit`](https://github.com/treboutat/google-ads-account-audit):** when stages 1-2 point at the account itself, or the conversion event is suspect.
- **[`search-term-scorer`](https://github.com/treboutat/google-ads-search-term-scorer):** when a shift in query mix explains the CPC or lead-quality change.

## Tone

Diagnostic and direct, operator to operator. The user wants a verdict: give the one the evidence supports, with its confidence, and say what would change it.
