# Disclosure 11: Drip Wallet Custodial Escrow Architecture for Prize Pool Entry and Settlement

**Published by:** Patrick Harrington Maloy / BitPoolz  
**Date:** May 30, 2026  
**Field:** Financial Technology / Custodial Wallet Systems / Prize Pool Architecture

---

## Technical Field

An internal custodial balance system functioning as the sole entry vehicle and prize settlement layer for probabilistic prize pools, wherein participant funds are held in a defined escrow state from entry confirmation through draw resolution, with atomic settlement upon outcome determination.

---

## Background

Existing prize pool and lottery systems require participants to generate a new payment instrument (Lightning invoice, on-chain address, credit card charge) for each individual pool entry. This creates friction, delays, and dependency on external payment infrastructure for payout delivery. No prior system implements a unified internal custodial balance that simultaneously functions as: (a) the entry payment vehicle, (b) an escrow holding layer during the active pool window, and (c) the prize receipt layer — eliminating external payment dependency for both entry and payout.

---

## Detailed Description

An internal custodial balance system (herein "Drip Wallet") wherein:

**1. Balance Lifecycle States**

The custodial balance maintains three discrete accounting states for each participant:

- **Available balance** — sats freely withdrawable at any time
- **Escrow balance** — sats committed to an active pool entry, held from entry confirmation until draw resolution, not withdrawable during escrow period
- **Total balance** — sum of available + escrow, displayed to participant at all times

The transition from available to escrow occurs atomically at entry confirmation. The transition from escrow to available (for non-winners) or from escrow to increased-available (for winners, reflecting prize credit) occurs atomically at draw resolution.

**2. Atomic Entry Transaction**

Pool entry via Drip Wallet executes as a single database transaction:
- Validate available balance ≥ requested entry amount
- Lock participant record (FOR UPDATE) to prevent concurrent spend races
- Lock pool record (FOR UPDATE) to prevent capacity race conditions
- Deduct entry amount from available balance
- Record escrow position: pool ID, ticket range start, ticket range end, sats amount, timestamp
- Insert pool entry record with ticket range assignment
- Commit — all steps succeed or all rollback

**3. Escrow Visibility During Pool Window**

During the period between entry confirmation and draw resolution, participants have full real-time visibility of:
- Their specific ticket range held in escrow (e.g., tickets #14,001–#27,500)
- Current odds: escrow_sats / total_pool_sats × 100%
- Pool fill status and estimated draw timing
- Expected value: prize_pool × win_probability

The escrow state is explicitly labeled in the participant dashboard. Participants understand their sats are committed but not lost — they will either become a prize credit (win) or return to available balance via non-custodial means at draw completion.

**4. Atomic Settlement at Draw Resolution**

Draw resolution executes as a single database transaction:
- Determine winning ticket number via blockchain randomness oracle
- Identify winning entry record (ticket range containing winning number)
- Credit winner's available balance: available += prize_amount (95% of pool total)
- For all entries: escrow balance for this pool → 0 (position closed)
- Non-winners: no balance change (their escrow was already debited at entry; the debit stands as the cost of participation)
- Insert drip_ledger rows: one 'win_credit' row for winner, one 'draw_close' row per entry
- Commit

No external Lightning payment is required to deliver the prize. The winner's balance updates instantly within the same database transaction that resolves the draw.

**5. User-Controlled Withdrawal**

Participants may withdraw their available balance (including any prize credits) to any Lightning-compatible wallet at any time of their choosing:
- No minimum hold period
- No lock-up after winning
- Withdrawal is asynchronous — does not block any platform operation
- Withdrawal creates an outbound Lightning payment to the participant's specified address
- Withdrawal recorded in drip_ledger with outbound transaction hash

**6. Top-Up via Lightning**

Participants fund their Drip Wallet via a single Lightning invoice:
- Invoice created via BTCPay Server for specified sat amount
- Upon invoice settlement, available balance credited immediately
- No recurring invoices required — one deposit funds multiple pool entries
- Top-up recorded in drip_ledger with inbound invoice ID

---

## Key Claims

- Internal custodial balance with three discrete states: available, escrow, total
- Atomic entry transaction with dual row locks (participant + pool) preventing concurrent spend races
- Explicit escrow state from entry confirmation to draw resolution with full participant visibility
- Atomic settlement: prize credit and position closure in single database transaction
- No external payment required for prize delivery — internal balance credit eliminates Lightning routing dependency
- User-controlled withdrawal timing with no lock-up periods
- Single top-up funds unlimited subsequent entries without additional payment instruments
- Real-time odds and expected value display during escrow period
- drip_ledger append-only audit trail of all balance state transitions

---

*Published to establish prior art. BitPoolz retains implementation rights.*  
*Patrick Harrington Maloy — May 30, 2026*
