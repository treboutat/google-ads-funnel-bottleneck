# Test — Edge case: two stages look broken + low spend noise

**Scenario:** Two stages are soft at once, and the account is small enough that noise matters. The skill must pick ONE bottleneck (the more upstream one) and flag the volume caveat.

## Input

"$12K/mo spend, last 30 days: LP CVR dropped from 6% to 3.8%, and close rate dropped from 25% to 15%. Which do we fix?"

## Expected behavior

- Picks **one** bottleneck: Stage 2 (LP CVR) — the more upstream of the two, because upstream fixes compound and the downstream drop is partly fed by it (a looser lead mix closing worse is expected when CVR/lead quality shifts).
- Explicitly explains the tie-break rule rather than silently choosing.
- Flags the volume caveat: at $12K/mo and 30 days, close-rate math is running on a handful of deals — the 25%→15% "collapse" may be 2-3 deals of noise. Recommends a 90-day window for the close-rate read.
- Fix list targets the LP (form, speed, message match), with close rate as the *monitor* metric, not a second simultaneous fix.

## Pass criteria
- Exactly one bottleneck named, with the upstream tie-break stated.
- The small-sample warning appears (sub-$25K/mo → longer windows).
- No dual-front fix plan; the second stage becomes a monitoring item.
