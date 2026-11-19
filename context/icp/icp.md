# ICP: Asterisk Nigeria

Status: v1.1, 2026-11-13. Segment and stage direction confirmed by the Nigeria country lead from market conversations [S9]: "growth to higher level companies usually work best". Smaller companies may have the need but lack the budget, and some lack the volume to feel the problem.
Scope: **Nigeria only.**
Sources: [asterisk-raw.md](../docs/research/asterisk-raw.md) (A), [nigeria-market-raw.md](../docs/research/nigeria-market-raw.md) (N). Lines marked *Assumption* are working targeting choices, not facts.

## One-line ICP
Growth-stage Nigerian fintechs that move money under a CBN licence or a partner bank's licence, onboard businesses or high volumes of customers, and still do compliance reviews, alert work and partner-bank requests largely by hand.

## Why now (Nigeria timing)
1. **CBN Baseline Standards for Automated AML Solutions** (issued 10 March 2026). Fintechs, PSPs and MMOs must be fully compliant by 10 March 2028. Roadmaps were due around June 2026, so most fintechs are now deciding how to automate. [N: section 1]
2. **CBN UBO disclosure circular** (15 June 2026). Ownership tracing is now a payments-system requirement, which is KYB work. [N: section 1]
3. **Enforcement memory.** The 2024 onboarding bans and reported fines over KYC failures make KYC quality a board-level issue. [N: section 1]
4. **Partner bank pressure.** After the July 2026 revocation of 46 MFB licences, banks and fintechs are both doing more diligence on each other, which means more questionnaires. [N: section 4]

## Firmographics

| Criterion | Include | Notes |
|---|---|---|
| Geography | HQ or main operating licence in Nigeria | Pan-African fintechs with a Nigerian entity qualify |
| Licence / model | PSSP, switching, PTSP, MMO, super agent; national or state MFB with digital operations; fintechs running on a partner bank's licence (BaaS) | Licence types from CBN circular addressees [N10] |
| Stage | Growth-stage and larger (confirmed [S9]) | Has the **budget** and the **volume** to feel the problem. *Assumption on proxies:* Series A or later, or profitable and scaling; roughly 50+ staff. Smaller and low-volume fintechs are out (no budget, or not enough volume to feel the pain) |
| Compliance team | Exists but is small | *Assumption:* 1 to 10 people in compliance, risk and ops. Big enough to feel the work, too small to absorb it |
| Customer type | Onboards **businesses** (KYB) or high customer volumes | KYB is Asterisk's deepest workflow (registers, owners, screening) [A: section 2] |
| Stack | Already uses an ID/KYC vendor and some rules or monitoring | Asterisk works on top of these: "Your vendor stays" [A: section 2] |

## Priority segments (v1)

| Tier | Segment | Why it fits | Lead workflow |
|---|---|---|---|
| 1 | **B2B payments and merchant acquiring** (PSSPs, PTSPs, payment gateways, collections) | Heavy KYB on merchants, UBO tracing now a CBN focus, acquiring monitoring | KYB review, RFIs |
| 1 | **BaaS-dependent fintechs** (business accounts, cards, payouts on a partner bank) | Partner bank questionnaires and audits; KYB and alert evidence on demand | RFIs and correspondence, KYB |
| 1 | **Cross-border, remittance and stablecoin-adjacent fintechs** | Higher-risk flows, foreign correspondents ask hard questions; API supports wallets and Chainalysis [A: section 3]; matches Karsa's history | Alert review, TM, RFIs |
| 2 | **Digital MFBs and MMOs** (consumer-heavy) | High KYC exception volume and alerts, but larger in-house teams | KYC review, alert review |
| 1 | **Scaled fintechs, named accounts** (e.g. national-licence holders such as OPay, Moniepoint, PalmPay, Kuda, Paga [N6]) | "Exactly the type we're going for" (country lead, 2026-11-13 [S9]). Highest volume and budget. Larger teams and longer sales cycles, so work them account by account | Account-specific; start with one workflow |
| 3 | Digital lenders, investment and savings apps | Lighter AML scope or a different regulator (SEC, FCCPC) | Later |

## Exclusions
- Deposit money banks (tier-1 banks). Long procurement and a different buying motion. Out for v1.
- Pre-launch or pre-licence startups with no live volume.
- Early-stage or low-volume fintechs: they lack the budget or don't feel the problem yet [S9].
- ID and compliance vendors (Youverify, Dojah, Prembly, Smile ID, Smartcomply). These are competitors or integration partners, not buyers.
- Asterisk's existing customers (non-Nigerian; names confidential).

## Disqualifiers and risks to check per account
- **Data localisation:** payment transaction data generated in Nigeria must be stored in Nigeria by 1 January 2027 [N: section 1]. Asterisk is a US company [A: section 6], and its API docs say it stores ingested records ("Bytes are stored immediately", "appends a complete immutable transaction snapshot", "retaining the bounded native response for audit") [A: section 3, sources/docs-useasterisk-llms.txt]. **"Asterisk doesn't hold data" is not a safe answer.** Needs an engineering answer (hosting region, what's retained, retention period, in-country option) and a legal read (circular plus NDPA cross-border transfer rules). Until then, lead with KYB and RFIs rather than transaction monitoring.
- No Nigerian proof yet (existing customers are not Nigerian) [A: section 6].

## Confirmed capabilities [S9]
- CAC business register checks: supported (confirmed by the country lead, 2026-11-13).

## Open questions for the country lead
1. Data localisation answer (above): hosting region, retention, in-country option, legal read.
2. Does any Nigerian design partner or pilot exist or is one in progress?
3. Are naira pricing or local billing available, or USD only?
4. Which licence types have you seen the strongest interest from so far?
