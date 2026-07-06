# Funnel Benchmarks by Vertical

Reference ranges for `funnel-bottleneck`. These are guidance, not verdicts — the user's own historical baseline always beats the table. Use these only when no baseline exists, and say so in the output.

## Stage benchmarks by vertical

### B2B SaaS ($50-500K/mo paid)
| Stage | Healthy range |
|---|---|
| LP CVR (cold paid) | 3-8% |
| Show rate (inbound demo) | 50-65% |
| Call → close | 15-30% |
| Qualified-lead rate | 40-60% |

### B2B services / agencies
| Stage | Healthy range |
|---|---|
| LP CVR | 4-10% (audit/consult offers convert higher than "contact us") |
| Show rate (inbound) | 50-70% |
| Call → close | 20-35% |
| Qualified-lead rate | 40-60% |

### Healthcare / treatment (call-heavy)
| Stage | Healthy range |
|---|---|
| LP CVR (form + call combined) | 5-12% |
| Call → qualified (3+ min) | 35-55% |
| Qualified → admit/booked | 15-30% |
| Note | Phone is the funnel — measure call quality by hour, not just volume |

### Local services
| Stage | Healthy range |
|---|---|
| LP CVR | 6-15% |
| Lead → appointment set | 50-75% |
| Appointment → sold | 25-50% |

### E-commerce (no call stage)
| Stage | Healthy range |
|---|---|
| Add-to-cart rate | 4-10% of sessions |
| Cart → checkout | 40-60% |
| Checkout → purchase | 60-80% |
| Note | Stages 3-5 collapse into cart/checkout steps; adapt the script |

## CPC sanity checks

There is no universal "good CPC" — anchor to:
- The user's own trailing 90-day CPC (drift >30% = investigate)
- Competitor median where visible (within 1.5x is normal auction pressure)
- Implied economics: CPC ÷ (LP CVR × qualified rate × close rate) = CAC. If CAC math breaks at *healthy* downstream rates, the CPC layer is genuinely the problem — rare.

## Reading the deltas

- One stage >30% below baseline, others flat → that's the bottleneck. Stop looking.
- Two adjacent stages soft → suspect the upstream one first (it feeds the downstream number).
- Everything 10-15% soft across the board → seasonality or tracking drift, not a stage break. Check measurement before optimizing anything.
- Everything healthy but CAC too high → unit-economics problem (pricing, LTV, payback), not a funnel problem.

## Volume floors for reliable diagnosis

| Monthly spend | Reliability |
|---|---|
| <$10K | Noise dominates — don't stage-diagnose; fix obvious hygiene and grow volume |
| $10-25K | Directional only; use 90-day windows |
| $25K+ | Stage-level diagnosis reliable on 30-60 day windows |
