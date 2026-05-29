# Disclosure 12: Auto-Entry Subscription System for Recurring Pool Participation

**Published by:** Patrick Harrington Maloy / BitPoolz  
**Date:** May 30, 2026  
**Field:** Financial Technology / Subscription Systems / Prize Pool Automation

---

## Technical Field

An automated recurring pool entry system wherein a participant pre-authorises a fixed sat amount to be automatically entered into each newly opened pool of a specified tier, funded from their custodial balance, without requiring any per-entry action.

---

## Background

Current prize pool systems require participants to manually enter each pool individually. Power users who wish to participate in every pool of a given tier must monitor pool openings and manually submit entries. No prior system implements a pre-authorised recurring entry mechanism tied to an internal custodial balance, where entries fire automatically upon pool creation and the participant retains full cancel/pause control.

---

## Detailed Description

**1. Subscription Configuration**

A participant configures an auto-entry subscription specifying:
- Target tier (e.g., Quick Shot, Main Event, Grand Prize)
- Entry amount per pool (in sats, subject to min/max limits)
- Maximum simultaneous active positions (cap on concurrent entries)
- Minimum available balance required before auto-entry fires (safety floor)
- Active/paused status (participant can pause without deleting)

**2. Trigger Mechanism**

When a new pool opens for a subscribed tier:
- The Smart Queue Engine™ emits a pool-open event
- The auto-entry service queries all active subscriptions for that tier
- For each subscription: validate available balance ≥ entry amount + minimum floor
- If valid: execute Drip Wallet atomic entry transaction (identical to manual entry)
- If insufficient balance: skip entry, emit low-balance notification to participant

**3. Entry Execution**

Auto-entries are indistinguishable from manual entries at the data layer:
- Same ticket range assignment algorithm
- Same entry record structure
- Same fee deduction
- Entry record flagged: auto_entry = true for analytics purposes only
- Participant receives entry confirmation notification

**4. Balance Safety Controls**

- Auto-entry never executes if available balance < (entry amount + minimum floor)
- Minimum floor is participant-configurable (default: 2× entry amount)
- System never borrows against escrow balance for auto-entry
- If a participant pauses their subscription mid-pool, existing entries remain active; future pools are skipped

**5. Notification System**

Participant receives notifications for:
- Each successful auto-entry (pool name, sat amount, ticket range, current odds)
- Skipped auto-entry due to insufficient balance (with top-up prompt and amount needed)
- Subscription paused/resumed confirmations

**6. Cancellation and Portability**

- Subscription cancels immediately; no entries fire after cancellation
- Existing entries from prior auto-entries remain active until draw
- Subscription history retained for participant reference
- Export: participant can download full auto-entry history as CSV

---

## Key Claims

- Pre-authorised recurring pool entry tied to internal custodial balance
- Tier-specific subscription with configurable entry amount
- Trigger on pool-open event from Smart Queue Engine™
- Balance floor safety check before every auto-entry execution
- Auto-entry indistinguishable from manual entry at data layer (same ticket assignment)
- Participant-configurable minimum balance floor
- Low-balance notification with top-up prompt
- Immediate cancellation with preservation of existing active entries
- Auto-entry flag for analytics without affecting pool mechanics

---

*Published to establish prior art. BitPoolz retains implementation rights.*  
*Patrick Harrington Maloy — May 30, 2026*
