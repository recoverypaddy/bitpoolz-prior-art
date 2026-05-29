# Disclosure 16: Time-Weighted Early Entry Bonus Odds System

**Published by:** Patrick Harrington Maloy / BitPoolz  
**Date:** May 30, 2026  
**Field:** Financial Technology / Incentive Mechanisms / Prize Pool Economics

---

## Technical Field

A time-weighted entry bonus system wherein participants who enter a prize pool during an early window receive a proportional bonus to their effective ticket count — incentivising early pool participation and accelerating pool fill velocity — without altering the fundamental 1-sat-1-ticket pricing architecture.

---

## Background

Prize pools fill faster when early entries create social proof and momentum. However, early entrants face higher uncertainty (pool may not fill) and lower current odds (fewer total sats at time of entry, meaning odds improve as pool fills — creating a paradox where early entry is riskier but not proportionally rewarded). A time-weighted bonus resolves this by giving early entrants a small ticket count bonus that compensates for early-entry risk without compromising the proportional fairness architecture.

---

## Detailed Description

**1. Early Entry Window Definition**

The early entry bonus applies to entries made during the first X% of the pool's expected fill time (operator-configurable, e.g., first 20% of expected duration). For a Quick Shot pool with 1-hour expected fill time, the early window = first 12 minutes.

**2. Bonus Calculation**

Bonus ticket multiplier decays linearly across the early window:

```
bonus_multiplier = 1 + (max_bonus × (1 - entry_time_pct / early_window_pct))
```

Where:
- `max_bonus` = maximum bonus at pool open (e.g., 0.05 = 5% bonus tickets)
- `entry_time_pct` = what percentage through the early window the entry occurred
- Entry at pool open: 5% bonus. Entry at end of early window: 0% bonus. Entry after window: no bonus.

Example: 10,000 sat entry at pool open with 5% max bonus → 10,500 effective tickets. Entry at 50% through early window → 10,250 effective tickets.

**3. Ticket Record Architecture**

The bonus is implemented as additional effective tickets without changing the underlying sats amount:
- `entry.sats` = actual sats paid (e.g., 10,000) — unchanged
- `entry.tickets` = effective tickets including bonus (e.g., 10,500)
- `entry.bonus_tickets` = bonus amount (e.g., 500)
- `entry.early_entry_bonus_pct` = bonus percentage applied (e.g., 5.0%)
- Running total for pool fill calculation uses `entry.sats` (actual payment) — not tickets
- Draw uses `entry.tickets` for winner selection — bonus tickets increase win probability

**4. Display and Transparency**

On entry confirmation, participant sees:
- "You paid 10,000 sats → received 10,500 tickets (5% early entry bonus)"
- Odds displayed using effective tickets: 10,500 / pool_total_tickets

On pool leaderboard, all entries display both sats paid and ticket count — making the bonus visible to all participants.

**5. Fairness Architecture**

- The bonus is announced at pool creation (participants know it exists before entering)
- Bonus parameters are immutable after pool creation
- All bonus ticket assignments are recorded in the public ledger
- Draw verification: verifier uses ticket counts (including bonuses) from the public ledger — fully reproducible
- The bonus does not change the prize pool size (funded from sats paid, not tickets)

**6. Economic Impact**

The bonus creates a small but real incentive to enter early. This:
- Reduces pool fill time (early social proof attracts subsequent entries)
- Rewards early-entry risk with proportional compensation
- Does not create a significant fairness disadvantage for later entrants (bonus is capped and decays)
- Creates a novel economic dynamic absent from all prior prize pool systems

---

## Key Claims

- Time-weighted bonus ticket allocation decaying linearly across early entry window
- Separate tracking: sats_paid vs. effective_tickets including bonus
- Pool fill calculation uses sats (actual payment); draw uses tickets (including bonus)
- Bonus parameters immutable after pool creation
- Public ledger records bonus amount per entry for verifier reproducibility
- Linear decay formula: multiplier = 1 + (max_bonus × (1 - entry_time_pct / window_pct))
- Transparency: all participants see bonus terms before entry and bonus applied to each entry on leaderboard
- Operator-configurable max_bonus and early_window_pct at pool creation

---

*Published to establish prior art. BitPoolz retains implementation rights.*  
*Patrick Harrington Maloy — May 30, 2026*
