---
title: Prediction Market for Pool Fill Probability
author: Patrick Harrington Maloy
date: 2026-05-28
copyright_case: 1-15173171741
patent_status: Provisional filed, 75 claims
purpose: Defensive prior art publication
---

# DISCLOSURE 8: Prediction Market for Pool Fill Probability

## Technical Field
Binary outcome prediction market contracts for sweepstakes pool fill probability, integrated with position trading marketplace.

## Background
Users with information advantages (monitoring fill velocity, time of day patterns) may wish to trade on their prediction of whether a pool will fill, separate from holding positions in the pool.

## Detailed Description
A binary outcome prediction market integrated with the position marketplace allowing users to trade contracts on the question: "Will Pool [X] fill completely by [timestamp]?" Contract mechanics: YES contracts pay 1,000 sats if pool fills by deadline, 0 sats if not. NO contracts pay 1,000 sats if pool does not fill, 0 sats if it does. Contracts are priced by the platform using a logarithmic market scoring rule (LMSR) or automated market maker. The fill probability oracle: a real-time probability estimate calculated from current fill percentage, fill velocity (sats per hour over last 2 hours), historical fill rates for this tier at this time of day, and remaining time window. This probability estimate is displayed on pool cards and updates every 60 seconds. Contract settlement: at pool window close, if pool filled → YES contracts pay out; if not → NO contracts pay out. Settlement is automatic and atomic. Hedging use case: a position holder can buy NO contracts as insurance — if the pool doesn't fill and their position is refunded, the NO contracts offset the opportunity cost.

## Key Claims
- Binary fill-probability prediction contracts
- LMSR or AMM pricing mechanism
- Real-time fill probability oracle (velocity + historical + time-of-day)
- Automatic settlement based on actual pool fill outcome
- Hedging use case for position holders
- Integration with existing position marketplace
- 60-second probability oracle update frequency

---

*Published May 28, 2026 by Patrick Harrington Maloy / BitPoolz. US Copyright Case #1-15173171741.*
