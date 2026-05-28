---
title: Automated Market Maker (AMM) for Sweepstakes Position Trading
author: Patrick Harrington Maloy
date: 2026-05-28
copyright_case: 1-15173171741
patent_status: Provisional filed, 75 claims
purpose: Defensive prior art publication
---

# DISCLOSURE 2: Automated Market Maker (AMM) for Sweepstakes Position Trading

## Technical Field
Automated market making algorithms applied to fractional sweepstakes position trading markets.

## Background
Current sweepstakes position markets use order books (listed price, buyer accepts). An AMM would provide instant liquidity at all times without requiring a matching counterparty.

## Detailed Description
A constant-product automated market maker (x*y=k formula or variants) applied to sweepstakes ticket-range position trading. Liquidity providers deposit paired assets (position-credit pairs) into liquidity pools. Traders swap positions for platform credits at prices determined algorithmically by the ratio of assets in the liquidity pool. The system tracks: pool depth per sweepstakes pool tier, position unit standardization (normalising different ticket range sizes into tradeable units), slippage calculation based on trade size relative to pool depth, fee distribution to liquidity providers (proportional to their share of pool depth), and impermanent loss calculation specific to sweepstakes positions (accounting for draw-time binary outcome). Position units expire at draw time — AMM liquidity is automatically unwound and returned to LPs at draw completion.

## Key Claims
- Constant-product AMM formula applied to sweepstakes positions
- Standardised position unit creation from ticket ranges
- LP share tracking and fee distribution
- Impermanent loss model for binary-outcome position assets
- Automatic liquidity unwinding at draw completion
- Slippage protection thresholds

---

*Published May 28, 2026 by Patrick Harrington Maloy / BitPoolz. US Copyright Case #1-15173171741.*
