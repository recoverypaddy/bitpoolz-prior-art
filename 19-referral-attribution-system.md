# Disclosure 19: Referral Attribution System with On-Ledger Provable Credit Distribution

**Published by:** Patrick Harrington Maloy / BitPoolz  
**Date:** May 30, 2026  
**Field:** Financial Technology / Referral Systems / Provably Fair Attribution

---

## Technical Field

A referral attribution system for prize pool platforms wherein referral credits are paid from a verifiable on-ledger source, referral chains are publicly auditable, rewards are bounded by confirmed referee pool participation, and all attribution records are permanently immutable — eliminating the trust dependency inherent in traditional opaque referral systems.

---

## Detailed Description

**1. Referral Link Generation**

Each registered participant receives a unique referral identifier (UUID). Their referral URL: `platform/ref/[uuid]`. When a new user registers via this link, the referring participant's ID is recorded on the new user's account permanently.

**2. Participation-Gated Reward**

Referral credit fires only when the referred participant completes their first confirmed pool entry — not at registration. This prevents spam referrals and ensures the referrer is rewarded for genuine platform growth.

Reward amount: configurable (e.g., 100 sats credited to referrer's Drip balance per confirmed referee entry).

**3. On-Ledger Attribution**

Every referral credit is recorded in the drip_ledger as type `referral_credit` with:
- Referrer user ID
- Referee user ID (hashed for privacy)
- Pool entry ID that triggered the credit
- Credit amount in sats
- Timestamp

This makes the entire referral economy publicly auditable — total referral credits paid, credit velocity, attribution chain — without revealing individual identities.

**4. Multi-Tier Attribution (Optional)**

A two-tier variant: referee's referee also credits the original referrer at a lower rate (e.g., 50 sats for second-degree referrals). Maximum two tiers — no infinite chain structures. Both tiers recorded in ledger with tier depth indicated.

**5. Referral Pool Contribution**

A configurable percentage of each referred user's entry fees (e.g., 0.25%) is credited to the referrer's Drip balance for the lifetime of the referred user's platform activity. This converts referral from a one-time reward to an ongoing economic relationship — referrers are incentivised to refer high-engagement users.

**6. Anti-Gaming Controls**

- Self-referral detection: referrer and referee must have distinct email domains and IP addresses at registration
- Velocity cap: maximum X referral credits per 24-hour period per referrer
- Minimum referee activity: referee must complete entry within 30 days of registration for credit to fire
- All controls logged — referral attempts that fail controls are recorded (not silently dropped)

## Key Claims

- Participation-gated referral credit (fires on first entry, not registration)
- On-ledger referral credit records with full attribution metadata
- Optional two-tier referral with maximum depth cap
- Lifetime percentage-of-entry-fee referral credit stream
- Anti-gaming controls with logged rejection records
- Public auditability of aggregate referral economy without individual identity disclosure

---

*Published to establish prior art. BitPoolz retains implementation rights.*  
*Patrick Harrington Maloy — May 30, 2026*
