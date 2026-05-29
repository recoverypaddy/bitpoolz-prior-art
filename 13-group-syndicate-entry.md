# Disclosure 13: Group/Syndicate Pool Entry with Shared Position Ownership

**Published by:** Patrick Harrington Maloy / BitPoolz  
**Date:** May 30, 2026  
**Field:** Financial Technology / Shared Ownership / Prize Pool Architecture

---

## Technical Field

A group pool entry mechanism wherein multiple participants collectively fund a single pool entry, with prize winnings distributed proportionally among group members based on each member's contribution, executed via a shared custodial position with atomic multi-party settlement.

---

## Background

Traditional lottery syndicates are managed manually — a group organiser collects funds, buys tickets, and distributes winnings informally. This introduces trust dependency on the organiser and provides no cryptographic proof of each member's share. No prior system implements an on-platform group entry where: (a) each member's contribution is individually recorded, (b) prize distribution is automatic and proportional, (c) all group members can independently verify their share before and after the draw.

---

## Detailed Description

**1. Group Creation**

A participant (group creator) initiates a group entry specifying:
- Target pool (pool ID, tier)
- Total entry amount target (sats)
- Maximum group size (number of members)
- Minimum contribution per member (sats)
- Contribution deadline (time window before pool closes)
- Group name (display only)

**2. Member Invitation and Contribution**

- Creator shares an invite link (unique group ID)
- Invited participants view group details: target pool, total target, current funded amount, member list with contribution amounts (email masked), deadline
- Each member commits their contribution from their Drip balance (available balance only, not escrow)
- Contribution is held in a group escrow state — distinct from individual pool escrow — until the group reaches its target or deadline expires

**3. Entry Execution Trigger**

When group reaches its total target:
- All member contributions atomically transfer from group escrow to pool entry
- Single pool entry record created for the full combined amount
- Ticket range assigned for the full amount (e.g., 50,000 sats → tickets #45,001–#95,000)
- Each member's contribution and proportional share (%) recorded in group_members table
- All members receive entry confirmation: group entry confirmed, their share percentage, their ticket sub-range

**4. Proportional Prize Distribution**

If the group entry wins:
- Total prize amount = pool total × 95%
- Each member receives: prize_amount × (member_contribution / total_group_entry)
- All distributions execute atomically — all members credited before any single member can withdraw
- Each credit appears in individual member's drip_ledger as 'group_win_credit'
- Distribution completes regardless of member account status (no manual claim required)

**5. Deadline Expiry Handling**

If group does not reach target by deadline:
- All contributions return to individual member available balances
- No pool entry is made
- Members notified: "Group entry cancelled — your X sats returned to Drip balance"
- Refunds are atomic: all members refunded in single transaction or none

**6. Partial Fill Option**

Optional creator setting: enter with whatever amount is funded at deadline (minimum threshold required):
- Minimum threshold (e.g., 50% of target) must be reached
- Entry executes at deadline with available amount
- Proportional shares recalculated based on actual funded amount
- Members who contributed receive proportional share of actual entry amount

**7. Auditability**

Full group entry history recorded:
- Group creation record with all parameters
- Each member contribution record with timestamp
- Entry execution record linking group to pool entry
- Prize distribution records per member
- All records in public ledger (member emails masked)

---

## Key Claims

- Multi-party group pool entry with proportional contribution tracking
- Two-stage escrow: group escrow (pre-entry) → pool escrow (post-entry)
- Atomic entry execution when group target reached
- Proportional prize distribution in single atomic transaction
- All members credited before any can withdraw (no first-mover advantage)
- Deadline expiry with atomic full refund to all members
- Partial fill option with minimum threshold
- Sub-range display: each member sees their specific ticket numbers within the group range
- Public ledger audit trail with masked member identification

---

*Published to establish prior art. BitPoolz retains implementation rights.*  
*Patrick Harrington Maloy — May 30, 2026*
