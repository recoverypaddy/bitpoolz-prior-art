# Disclosure 18: Multi-Currency Pool Architecture — Any Fungible Asset as Entry Unit

**Published by:** Patrick Harrington Maloy / BitPoolz  
**Date:** May 30, 2026  
**Field:** Financial Technology / Multi-Asset Systems / Probabilistic Pool Architecture

---

## Technical Field

A prize pool architecture wherein the entry unit, prize denomination, and custodial balance unit are decoupled — allowing pools to be denominated in any fungible asset (fiat currency cents, stablecoin units, loyalty points, tokenised assets) while retaining the same sequential ticket assignment, blockchain-verified draw, and internal settlement architecture.

---

## Background

The BitPoolz core architecture (Provisional App #64/077,231) was implemented in Bitcoin satoshis. The architectural principles — sequential non-overlapping ticket ranges, blockchain-verified draws, internal custodial settlement — are asset-agnostic. This disclosure establishes prior art for implementation of the same architecture with any fungible unit of value, preventing any third party from patenting the application of these principles to non-Bitcoin assets.

---

## Detailed Description

**1. Asset-Agnostic Entry Unit**

The core ticket assignment algorithm operates on any positive integer unit of any fungible asset:

```
ticket_range_start = previous_running_total + 1
ticket_range_end = previous_running_total + entry_units
running_total = previous_running_total + entry_units
```

Where `entry_units` can be:
- Satoshis (Bitcoin)
- US dollar cents ($1.00 = 100 units)
- Euro cents
- USDC microdollars (1 USDC = 1,000,000 units)
- Airline miles (1 mile = 1 unit)
- Loyalty points (1 point = 1 unit)
- Any divisible digital asset where 1 unit = 1 ticket

**2. Custodial Balance Denomination**

The internal custodial balance (Drip Wallet) denominates in whatever asset the pool operates in. A fiat-denominated variant:
- Balance displayed in USD cents
- Top-up via bank ACH, card, or stablecoin conversion
- Prize credited in USD cents to balance
- Withdrawal via ACH, wire, or stablecoin

**3. Cross-Asset Prize Pools**

A pool where entries are denominated in one asset but prizes paid in another:
- Enter in USD cents → win in Bitcoin sats (converted at draw time using oracle price)
- Enter in loyalty points → win in USD credits
- Enter in stablecoin → win in Bitcoin

Cross-asset conversion uses a price oracle at draw time. Winner receives the converted amount. Exchange rate used is recorded in the draw record for auditability.

**4. Blockchain Randomness — Asset Independent**

The randomness source (Bitcoin block hash) is independent of the asset used for entries. A pool denominated in USD cents still uses a Bitcoin block hash for winner selection — providing the same cryptographic fairness guarantees regardless of asset denomination.

Alternative randomness sources for regulated environments:
- Ethereum block hash (for Ethereum-native pools)
- Publicly verifiable beacon (NIST Randomness Beacon, Drand)
- Any publicly auditable unpredictable source

**5. Regulatory Adaptations by Asset Type**

Different assets trigger different regulatory frameworks:
- Bitcoin/crypto: sweepstakes model (current BitPoolz)
- Fiat USD: money transmitter licence required in most US states
- Loyalty points: generally unregulated (no monetary value)
- Stablecoins: evolving regulation, likely money transmitter

The core architecture is identical across all asset types. Regulatory wrapper varies. This disclosure establishes prior art for the architecture itself, independent of regulatory classification.

**6. Prize-Linked Savings Account (PLSA) Variant**

A specific application: fiat-denominated pools where:
- Participants deposit USD cents into custodial balance
- Interest/yield accrues on the aggregate balance
- Yield funds the prize pool
- Principal is segregated and returned to non-winners
- Winner receives accumulated yield as prize
- No participant loses principal

This is the PLSA architecture implemented via the BitPoolz ticket system. Every depositor holds a ticket range proportional to their deposit. Yield accumulates as the prize. Bitcoin block hash picks the winner. This is directly applicable to bank savings products.

---

## Key Claims

- Sequential non-overlapping ticket assignment algorithm operable with any positive integer unit of any fungible asset
- Internal custodial balance (Drip Wallet) denominatable in any fungible asset
- Cross-asset pool: entry in one asset, prize in another, converted via price oracle at draw time
- Bitcoin block hash randomness source independent of pool entry asset denomination
- Alternative publicly auditable randomness sources (Ethereum block hash, NIST beacon, Drand)
- PLSA variant: yield-funded prize with principal segregation, implemented via ticket assignment architecture
- Same draw verification and audit trail architecture regardless of entry asset
- Regulatory framework independence: architecture unchanged across asset regulatory classifications

---

*Published to establish prior art. BitPoolz retains implementation rights.*  
*Patrick Harrington Maloy — May 30, 2026*
