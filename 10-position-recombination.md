---
title: Sweepstakes Position Recombination (Defragmentation) Mechanism
author: Patrick Harrington Maloy
date: 2026-05-28
copyright_case: 1-15173171741
patent_status: Provisional filed, App #64/077,231 — 121 claims, 39 inventions
purpose: Defensive prior art publication
---

# DISCLOSURE 10: Sweepstakes Position Recombination (Defragmentation) Mechanism

## Technical Field
Merging multiple non-contiguous fractional ticket ranges held by the same owner into unified entries without altering pool integrity.

## Background
After multiple fractional trades, a user may accumulate several small non-contiguous ticket ranges in the same pool from different purchases. Managing these separately creates cognitive overhead and operational complexity. Recombination merges them into a clean unified entry.

## Detailed Description
A recombination mechanism allowing a user who holds two or more separate entries (ticket ranges) in the same pool to merge them into a single unified entry. Eligibility criteria: (a) all entries must belong to the same pool; (b) all entries must have the same current owner (same email/account); (c) pool must be in 'open' or 'pipeline' status (not drawing or complete); (d) none of the entries may be listed for sale or in escrow. Merge process (atomic database transaction): (1) validate eligibility of all selected entries; (2) calculate combined ticket count = sum of all entry sats values; (3) assign new unified ticket range — the range is logically consolidated but the specific ticket numbers remain unchanged (the draw cares only about which numbers are owned, not how entries are structured); (4) create new single entry record with combined sats and unified range representation; (5) delete original entries; (6) record recombination event in drip_ledger for audit; (7) update ownership record. Recombination fee: optional small platform fee (e.g. 100 sats) to prevent spam recombinations. The draw system is completely unaffected — ticket numbers don't change, only the ownership record structure changes.

## Key Claims
- Multi-entry merge into single unified entry (same owner, same pool)
- Eligibility validation (status check, escrow check, ownership check)
- Atomic transaction: create new + delete old in single DB transaction
- Ticket numbers unchanged — only record structure changes
- Recombination event recording in audit ledger
- Optional recombination fee mechanism
- Draw system isolation — completely unaffected by recombination

---

*Published May 28, 2026 by Patrick Harrington Maloy / BitPoolz. US Copyright Case #1-15173171741.*
