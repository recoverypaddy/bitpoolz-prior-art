# Disclosure 17: Shareable Winner Proof Page with Social Verification Card

**Published by:** Patrick Harrington Maloy / BitPoolz  
**Date:** May 30, 2026  
**Field:** Financial Technology / Social Proof / Cryptographic Verification

---

## Technical Field

A publicly accessible, cryptographically anchored winner proof page generated automatically for every prize pool draw completion, containing a verifiable summary of draw parameters and outcome, formatted for social media sharing with an Open Graph image card, enabling winners to share proof of their win while enabling any third party to independently verify the claim.

---

## Background

When a prize pool participant wins, they have no portable, verifiable artifact they can share with others that proves the win was legitimate. A screenshot is trivially forgeable. A blockchain transaction hash is opaque to non-technical viewers. No prior system generates a human-readable, socially shareable, cryptographically verifiable win proof that simultaneously serves as a marketing artifact and an audit document.

---

## Detailed Description

**1. Automatic Page Generation**

At draw completion, the system automatically generates a unique public URL:

```
bitpoolz.com/win/[draw-id]
```

This page is immediately accessible — no authentication required to view it.

**2. Winner Proof Page Contents**

The page displays:
- Pool name, tier, and ID
- Draw date and time
- Total pool size (sats)
- Number of entries and unique entrants
- Prize amount (sats + approximate USD at draw time)
- Winner identifier (masked email: re***@gmail.com)
- Winner's ticket range (e.g., tickets #14,001–#27,500)
- Winner's entry amount (sats)
- Winner's win probability at draw time (e.g., "13.5% odds — beat X other entrants")
- Winning ticket number selected
- Bitcoin block height used for randomness
- Bitcoin block hash (with link to block explorer)
- Draw verification formula: sha256(server_seed || block_hash)
- Server seed (revealed post-draw)
- SHA-256 commitment of server seed (published pre-draw — proves seed wasn't changed)
- "Verify this draw yourself" instructions with copy-pasteable Python snippet

**3. Social Share Card (Open Graph)**

The page generates a dynamic Open Graph image containing:
- BitPoolz logo and branding
- "🏆 WINNER" in large text
- Prize amount prominently displayed
- Pool name and odds beaten
- "Verified on Bitcoin block [height]"
- bitpoolz.com URL

This image appears automatically when the URL is shared on Twitter/X, Telegram, iMessage, WhatsApp, etc.

**4. Winner-Specific Share Flow**

Winners receive a notification containing:
- Their personal win proof URL
- Pre-composed share text: "I just won [X] sats on @BitPoolz — anyone can verify the draw: bitpoolz.com/win/[id]"
- One-tap share buttons for major platforms
- Option to display or hide their masked email on the public page (privacy control)

**5. Cryptographic Verification Integration**

The page integrates with the existing verification system:
- "Verify this draw" button runs the SHA-256 computation in the browser (client-side JavaScript)
- User sees: server_seed + block_hash → sha256 → winning_number → range check → winner confirmed
- Computation runs entirely client-side — no server trust required for verification
- Verification result displayed: ✅ "Winner confirmed — computation matches public blockchain data"

**6. Leaderboard Integration**

The winner proof page links to:
- The pool's full provenance board (all entries and their ticket ranges)
- The Hot Tub (winners leaderboard) where this win appears
- The winner's Drip Wallet (if winner opts in to public profile)

**7. Permanent Availability**

Winner proof pages are permanent — they do not expire. Any draw from any point in BitPoolz history is verifiable. This creates an ever-growing archive of verifiable wins that serves as social proof for the platform's legitimacy.

---

## Key Claims

- Automatic winner proof page generation at draw completion (no manual step)
- Public URL format: platform/win/[draw-id] — no authentication required to view
- Full draw parameter display: pool size, entrant count, ticket range, block hash, server seed, commitment hash
- Client-side SHA-256 verification: winner confirmed without trusting any server
- Dynamic Open Graph image generation for social sharing containing prize amount and verification reference
- Winner-controlled privacy setting for masked email display
- Pre-composed share text with platform attribution and verification URL
- Permanent page availability — no expiry
- Integration with pool provenance board and platform winners ledger

---

*Published to establish prior art. BitPoolz retains implementation rights.*  
*Patrick Harrington Maloy — May 30, 2026*
