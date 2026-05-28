---
title: Charitable Prize Pool with Cryptographically Verified Donation
author: Patrick Harrington Maloy
date: 2026-05-28
copyright_case: 1-15173171741
patent_status: Provisional filed, 75 claims
purpose: Defensive prior art publication
---

# DISCLOSURE 5: Charitable Prize Pool with Cryptographically Verified Donation

## Technical Field
Charitable giving mechanism integrated into Bitcoin Lightning prize pool systems with cryptographic proof of donation.

## Background
Combining charitable giving with prize pools creates social good alignment and expands the participant base to users motivated by charitable impact.

## Detailed Description
A prize pool variant wherein a configurable percentage (1%-50%) of the prize pool is automatically distributed to a verified charitable organisation upon draw completion, with the remainder going to the winner. The charity percentage is set at pool creation and is immutable thereafter (preventing post-hoc modification). Verified charity whitelist: charities are pre-verified via Lightning address + charitable registration number. Distribution is automatic and atomic: winner payment and charity payment execute in the same transaction. Cryptographic proof of donation: the charity payment transaction hash is recorded in the public ledger and a Proof of Donation certificate is generated (same format as Proof of Fair Play certificate) containing: charity name, registration number, amount donated in sats, Lightning payment hash, block height of payment, and draw result. This certificate is emailed to all participants as proof their entry contributed to charitable giving.

## Key Claims
- Configurable charity percentage set at pool creation (immutable)
- Verified charity whitelist with Lightning address + registration number
- Atomic winner + charity payment in single transaction
- Cryptographic Proof of Donation certificate generation
- Certificate distribution to all participants
- Tax receipt generation for charitable contributions
- Public ledger recording of charity payments

---

*Published May 28, 2026 by Patrick Harrington Maloy / BitPoolz. US Copyright Case #1-15173171741.*
