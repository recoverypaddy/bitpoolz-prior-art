# Disclosure 15: Pool Entry Insurance — Principal Protection Mechanism

**Published by:** Patrick Harrington Maloy / BitPoolz  
**Date:** May 30, 2026  
**Field:** Financial Technology / Insurance Mechanisms / Prize Pool Risk Management

---

## Technical Field

An optional insurance mechanism for prize pool entries wherein a participant pays a small premium (in sats) at entry time to guarantee return of their entry principal to their custodial balance in the event they do not win, converting a zero-sum pool entry into a principal-protected probabilistic position.

---

## Background

Standard prize pool entries are zero-sum for non-winners — entry sats are distributed to the winner and non-winners receive nothing. This risk profile deters risk-averse participants. A principal-protection mechanism funded by a separate insurance premium creates a new participant category: those willing to pay for downside protection while retaining upside exposure. No prior prize pool system implements an on-platform, per-entry insurance mechanism with cryptographically verifiable premium collection and automated principal return.

---

## Detailed Description

**1. Insurance Premium Calculation**

At entry time, participant selects "Insure this entry" option. Insurance premium is calculated:

```
premium = entry_sats × insurance_rate × (1 - win_probability)
```

Where `insurance_rate` is a platform-configured rate (e.g., 8%) and `win_probability` is the participant's current odds at entry time. Higher-odds entries cost more to insure (more principal at risk). Lower-odds entries are cheaper to insure.

Example: 10,000 sat entry at 10% win odds → premium = 10,000 × 0.08 × 0.90 = 720 sats

**2. Premium Funding Sources**

Insurance premiums fund an insurance reserve pool:
- All premiums collected across all insured entries accumulate in the reserve
- Reserve is a separate ledger account — never commingled with prize pool funds
- Reserve balance is publicly visible (transparency)

**3. Entry Execution with Insurance**

Insured entry executes as a single atomic transaction:
- Deduct (entry_sats + premium) from available Drip balance
- Commit entry_sats to pool (ticket range assignment, running total update)
- Commit premium to insurance reserve
- Record insured_entry flag on entry record
- Record premium amount and win_probability at insure time

**4. Settlement Logic**

At draw resolution:
- **If insured entry wins:** winner receives full prize (95% of pool). No principal return — won the prize instead. Premium is forfeit (as with all insurance policies — you don't get a premium refund when the insured event doesn't occur).
- **If insured entry does not win:** entry_sats returned to participant's available Drip balance from insurance reserve. Participant is made whole on principal. They paid the premium; they get the principal back.

**5. Reserve Solvency**

Insurance reserve sustainability relies on the actuarial relationship between premiums collected and principal returns owed. Since win probability determines the premium, the expected value of premiums collected should exceed expected value of principal returns:

```
expected_premium = Σ(entry_sats × rate × (1 - win_prob))
expected_payout = Σ(entry_sats × (1 - win_prob))
```

At `rate = 8%`, the reserve collects 8% of expected principal returns — building a surplus over time. Platform monitors reserve ratio and adjusts rate if solvency threshold is approached.

**6. Transparency and Auditability**

- Reserve balance publicly visible in real time
- Every premium collection recorded in public ledger
- Every principal return recorded in public ledger
- Reserve ratio (reserve / total insured principal at risk) displayed publicly
- Actuarial parameters (insurance rate) publicly disclosed

**7. Insurance Certificate**

Upon entry with insurance, participant receives an Insurance Certificate containing:
- Entry ID, pool name, entry sats, premium paid, win probability at insure time
- Statement: "If this entry does not win, [entry_sats] sats will be returned to your Drip balance within [X minutes] of draw resolution"
- Certificate hash recorded on ledger

---

## Key Claims

- Per-entry optional insurance premium calculated from entry amount × rate × (1 - win probability)
- Separate insurance reserve pool — never commingled with prize pool funds
- Atomic entry + premium deduction in single transaction
- Automatic principal return to Drip balance upon non-winning draw resolution
- Premium forfeiture on winning entries (standard insurance policy mechanics)
- Public reserve balance display and reserve ratio monitoring
- Actuarial sustainability model: premium rate covers expected principal return obligations
- Insurance Certificate generation with on-ledger hash
- Platform-configurable insurance rate with public disclosure

---

*Published to establish prior art. BitPoolz retains implementation rights.*  
*Patrick Harrington Maloy — May 30, 2026*
