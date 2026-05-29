# Disclosure 20: Fiat-Denominated Prize-Linked Savings Pool with Blockchain-Verified Draw

**Published by:** Patrick Harrington Maloy / BitPoolz  
**Date:** May 30, 2026  
**Field:** Financial Technology / Prize-Linked Savings / Banking Products

---

## Technical Field

A prize-linked savings account (PLSA) product implemented via the sequential ticket assignment and blockchain-verified draw architecture, wherein deposited fiat principal is segregated and fully returned to all non-winning participants, while accumulated yield (interest, routing fees, or platform-generated returns) constitutes the prize pool — combining the safety of a savings account with the excitement of a prize draw.

---

## Detailed Description

**1. Core Architecture**

Participants deposit fiat currency (USD, EUR, GBP, etc.) into a custodial account. Each dollar/cent deposited is assigned a ticket range identically to the Bitcoin implementation:

```
ticket_range_start = previous_total + 1
ticket_range_end = previous_total + deposit_cents
```

A 100-person pool with $50 average deposit = 5,000 total tickets. $50 depositor holds tickets #1–#5,000. $100 depositor holds tickets #5,001–#15,000.

**2. Yield Accumulation as Prize**

The aggregate deposited principal generates yield via:
- Bank deposit interest (if held in FDIC-insured account)
- Money market returns
- T-bill yield
- Platform float revenue

Yield accumulates as the prize pool. Draw triggers when yield reaches a minimum threshold (e.g., $500 accumulated) or on a fixed schedule (monthly).

**3. Principal Segregation**

Principal is held in a segregated reserve account — never used as prize. At draw completion:
- Winner receives the full accumulated yield as prize
- All participants (including winner) retain their full principal in their account
- No participant loses any deposited amount

This is the defining characteristic of a PLSA: zero-loss participation. Prize is funded entirely from yield.

**4. Blockchain-Verified Draw**

Despite being fiat-denominated, the draw uses a Bitcoin block hash as the randomness source:
- Provides the same cryptographic fairness guarantees as the Bitcoin implementation
- Any participant can verify the draw outcome using only public blockchain data
- No trust in the platform operator is required for draw fairness

This combination — fiat PLSA with blockchain-verified draws — is novel. Existing PLSAs (Premium Bonds UK, SaverLife US) use proprietary opaque draw systems.

**5. Regulatory Framework**

Fiat PLSAs are regulated as savings products in most jurisdictions:
- US: requires state banking licence or partnership with FDIC-insured bank
- UK: FCA authorisation (Premium Bonds model)
- EU: varies by member state

The technical architecture is jurisdiction-agnostic. Regulatory wrapper varies.

**6. Ticket Tradeability (Optional)**

In jurisdictions where permitted, deposited positions may be tradeable during the draw window — applying the full Pipeline Phase™ and SplitStake™ architecture to fiat PLSA positions. This creates a secondary market for savings account positions — entirely novel.

## Key Claims

- Sequential ticket assignment applied to fiat currency cents as entry unit
- Yield-funded prize pool with principal segregation (zero-loss for all participants)
- Bitcoin block hash as randomness source for fiat-denominated draw (novel combination)
- Draw trigger: yield threshold or fixed schedule
- Principal held in segregated reserve — never at risk
- Optional tradeable positions during draw window (Pipeline Phase™ for PLSA)
- Full draw verifiability by any third party using public blockchain data
- Application to any yield-bearing fiat instrument (bank deposits, money market, T-bills)

---

*Published to establish prior art. BitPoolz retains implementation rights.*  
*Patrick Harrington Maloy — May 30, 2026*
