# Disclosure 14: Real-Time Marketplace Pricing Intelligence Engine

**Published by:** Patrick Harrington Maloy / BitPoolz  
**Date:** May 30, 2026  
**Field:** Financial Technology / Algorithmic Pricing / Secondary Market Systems

---

## Technical Field

A proprietary pricing intelligence system for secondary market trading of probabilistic pool positions, which continuously computes fair market value estimates based on pool fill percentage, time remaining, historical trading data, and position-specific parameters, displaying premium/discount metrics and suggested listing prices to sellers.

---

## Background

No prior secondary market for probabilistic contest positions exists at scale. Consequently, no pricing model or historical dataset for such positions has been developed. When participants in BitPoolz Pipeline Phase™ trading wish to list their position for sale, they have no reference price. This disclosure describes a pricing intelligence engine that generates suggested prices and displays market context — and simultaneously documents the novel dataset this engine generates as prior art.

---

## Detailed Description

**1. Fair Value Model**

The base fair value (FV) of a position at any point in time:

```
FV = (position_sats / pool_total_sats) × prize_pool_sats
```

Where:
- `position_sats` = sats in the position being valued
- `pool_total_sats` = current total sats in the pool
- `prize_pool_sats` = pool_total × 0.95 (after platform fee)

FV represents the expected value of the position — the statistically neutral price.

**2. Time-Adjusted Value**

As draw approaches, time value adjustments apply:

```
time_value_multiplier = 1 + (urgency_factor × time_decay_coefficient)
```

Where urgency_factor reflects how close the draw is relative to the total pipeline window. Positions closer to draw command premium (reduced opportunity for price discovery, committed capital). This multiplier is bounded to prevent extreme values.

**3. Historical Premium/Discount Dataset**

The engine records every completed trade:
- Pool fill percentage at time of trade
- Position size (sats) relative to pool total (%)
- Agreed trade price vs. FV at trade time (premium/discount %)
- Time remaining in pipeline window at trade time
- Pool tier
- Whether position subsequently won or lost

This dataset — accumulated across all trades on the platform — constitutes a proprietary pricing curve library. Over time, it reveals: what premium do large positions command vs. small ones? Do positions in nearly-full pools trade at premium or discount? What is the typical price discovery curve over the pipeline window?

**4. Suggested Listing Price**

When a participant initiates a listing, the system displays:
- Current FV in sats
- Historical median trade price for similar positions (same tier, similar fill %, similar size %)
- Suggested listing range: FV × 0.85 (quick sale) to FV × 1.15 (hold for premium)
- Current active listings in same pool for reference (competitive pricing context)

**5. Premium/Discount Display**

All active marketplace listings display:
- Listed price vs. FV: "+12% premium" or "-8% discount"
- This contextualises every listing for buyers without requiring financial expertise
- Updated in real time as pool fill % changes (FV changes as pool fills)

**6. Liquidity Score**

Each pool in Pipeline Phase™ receives a liquidity score:
- Based on: number of active listings, bid-ask spread (ratio of highest bid to lowest ask if bids exist), historical trade velocity for this tier
- Displayed as: Low / Medium / High liquidity
- Informs both buyers (execution probability) and sellers (likelihood of finding a buyer)

**7. Price History Chart**

For each pool in pipeline, display trade price history:
- X axis: time since pool entered pipeline
- Y axis: trade price as % of FV at trade time
- Shows price discovery curve developing in real time

---

## Key Claims

- Fair value formula: (position_sats / pool_total) × prize_pool as base pricing model
- Time-adjusted value multiplier based on proximity to draw
- Historical trade dataset: fill %, position size, price vs FV, time remaining — accumulated per trade
- Suggested listing price range computed from historical median + FV
- Real-time premium/discount display vs. current FV for all listings
- Liquidity score per pipeline pool
- Price history chart showing trade price as % of FV over pipeline window
- Dataset constitutes proprietary pricing curve library as trade secret/competitive asset
- FV updates continuously as pool fill % changes (live repricing of all listings)

---

*Published to establish prior art. BitPoolz retains implementation rights.*  
*Patrick Harrington Maloy — May 30, 2026*
