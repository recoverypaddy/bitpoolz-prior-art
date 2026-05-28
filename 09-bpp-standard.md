---
title: BitPoolz Position Protocol (BPP) — Open Technical Standard
author: Patrick Harrington Maloy
date: 2026-05-28
copyright_case: 1-15173171741
patent_status: Provisional filed, 75 claims
purpose: Defensive prior art publication
---

# DISCLOSURE 9: BitPoolz Position Protocol (BPP) — Open Technical Standard

## Technical Field
Open technical standard for representing, transferring, and verifying fractional sweepstakes position ownership across compatible systems.

## Background
As sweepstakes position trading grows, third-party wallets, exchanges, and portfolio trackers will need a standard way to represent and verify position ownership. A published open standard prevents fragmentation and establishes BitPoolz as the reference implementation.

## Detailed Description
The BitPoolz Position Protocol (BPP) is an open technical standard defining: (1) Position Data Schema — JSON structure containing: position_id (UUID), pool_id, pool_name, pool_tier, ticket_range_start (bigint), ticket_range_end (bigint), sats_value, current_owner_email (hashed), current_owner_lightning_address, acquisition_timestamp, acquisition_price_sats, status (active/listed/in_escrow/won/lost), draw_result (null until draw fires); (2) Ownership Transfer API — REST endpoint specification: POST /positions/transfer accepting signed transfer request with seller signature, buyer address, agreed price, timestamp; (3) Verification Endpoint — GET /positions/{id}/verify returning cryptographic proof of position authenticity signed by platform private key; (4) Signature Format — secp256k1 signature over position data hash, verifiable against platform public key published at well-known URL; (5) Cross-Platform Compatibility — any wallet or exchange implementing BPP can display, transfer, and verify BitPoolz positions; (6) Reference Implementation — open source TypeScript library published to npm as @bitpoolz/bpp.

## Key Claims
- JSON position data schema specification
- Signed ownership transfer API specification
- Cryptographic verification endpoint specification
- secp256k1 signature format for position authenticity
- Cross-platform compatibility requirements
- Reference implementation as open source npm library
- Platform public key publication for third-party verification

---

*Published May 28, 2026 by Patrick Harrington Maloy / BitPoolz. US Copyright Case #1-15173171741.*
