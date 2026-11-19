# Signal matrix: Asterisk Nigeria

Status: WORK IN PROGRESS v1, 2026-11-13. Built with /signal-matrix. Axes, priority cells and the Matrix 2 signal set were confirmed by the Nigeria country lead. Validate signals on the first Clay runs.
Reads with: [icp.md](icp.md), [personas.md](personas.md), [positioning](../positioning/), [nigeria-market-raw.md](../docs/research/nigeria-market-raw.md).

## Market reality
Nigeria is a narrow market. Each cell holds **tens of companies, not hundreds**: the CBN register lists 17 mobile money operators, 19 switching and processing licensees, 100+ payment solution service providers (PSSPs) and 47 payment terminal service providers (PTSPs) [CBN PSP register, fetched 2026-11-13]. So:
- Build the **full account list** for each cell once, from the registers below.
- Use signals for **timing** (who to contact this month and with what angle), not for discovering volume.
- The partner-licence column can only be found by elimination ("not on any register"), so it isn't prioritised for v1.

### Registers (backbone data sources)
| Register | URL | Status |
|---|---|---|
| CBN licensed PSPs (MMO, switching, PSSP, PTSP, super agent, PSHC) | https://www.cbn.gov.ng/PaymentsSystem/PSPs.html | VERIFIED: fetched and parsed 2026-11-13 (static HTML, Clay HTTP or scraper) |
| CBN licensed IMTOs | https://www.cbn.gov.ng/PaymentsSystem/InternationalMoneyTransferOperators.html | VERIFIED exists (search); not yet fetched |
| CBN microfinance banks | https://www.cbn.gov.ng/Supervision/Inst-MF.html | PARTIAL: page shell loads, list appears to load separately; find the file link |
| SEC Nigeria ARIP admissions | https://sec.gov.ng/for-investors/keep-track-of-circulars/ | VERIFIED exists (July 2, 2026 circular); notices only, no consolidated list |
| CBN circulars | https://www.cbn.gov.ng/Documents/circulars.html | VERIFIED link exists (CBN homepage) |

---

## Matrix 1: Segments (business model x licence)

Filter on every cell: growth-stage and larger, with the volume and budget to feel the problem [icp.md].

| Business model | Own licence (CBN, IMTO or SEC) | Partner bank's licence |
|---|---|---|
| **A. B2B payments and acquiring** | **A1, PRIORITY 1.** Target: CBN switching, PSSP or PTSP licensees processing merchant or business payments. Examples (all on the CBN register): Paystack Payment Limited, Flutterwave Technology Solutions, Interswitch, Remita Payment Service, Nomba Financial Services, Kora Payments, Payaza Africa, Cellulant Nigeria, Global Accelerex, Hydrogen Payment Services, Coralpay, Xpress Payments, Itex Integrated Services. Angle: KYB on merchants and their owners; CBN automated AML deadline; partner and scheme RFIs. | A2, low. Nigerian payment companies not on the register. Requires Clay research: Nigeria + payments/gateway keywords, minus the register list. Angle: partner bank RFIs. |
| **B. Business banking and finance ops** | **B1, PRIORITY 4.** Target: national or state MFBs and PSSPs serving SMEs and businesses. Examples: Moniepoint (national MFB, plus switching via Teamapt Limited), Paystack MFB (acquired January 2026, per Techeconomy), Duplo Limited, Woven Finance, Onepipe.io Services, Okra Technologies (last four on the PSSP register). Angle: KYB volume; partner and CBN requests. | B2, medium. Fintechs embedded in banks (e.g. Duplo inside Wema's ALAT Business). Requires Clay research. Angle: partner bank RFIs. |
| **C. Cross-border, remittance and stablecoin** | **C1, PRIORITY 3.** Target: IMTO licensees, cross-border PSSPs, SEC ARIP crypto firms. Examples: Grey (IMTO 2026), NALA (IMTO, March 2026), Fincra Technologies, Klasha Technologies, Leadremit, BVNK Services (PSSP register), Busha and Quidax (SEC ARIP approval in principle, 2024), Luno Fintech Nigeria and Bitbarter (ARIP, July 2026). Angle: alert review; correspondent and partner RFIs; Chainalysis-aware. Hold transaction monitoring until data localisation is answered. | C2, medium. OnePurze (says it operates through licensed partners) plus Clay research. Angle: partner RFIs. |
| **D. Consumer digital banks and MMOs** | **D1, PRIORITY 2 (named accounts).** Target: MMOs and national-licence MFBs with consumer scale. Examples: Opay Digital Services, PalmPay, Pagatech (MMO register), Moniepoint, Kuda (national licences, January 2026), FairMoney MFB. Angle: KYC exceptions, screening false positives, alert backlog, CBN exam readiness. Worked account by account. | D2, low. Consumer apps on a partner bank. Requires Clay research. |

## Phase 2: Scores

| Cell | Signal density | Product fit | Penetrability | Priority |
|---|---|---|---|---|
| A1 | High | High | High | 1 |
| D1 | Med-High | High | Med | 2 |
| C1 | Med | High | Med | 3 |
| B1 | Med | Med-High | Med | 4 |
| C2, B2 | Low | High | Low | later |
| A2, D2 | Low | Med | Low | later |

---

## Matrix 2: Signals

Iron Law: "Could I send this to a Clay operator right now with zero ambiguity?" Credits per action are **not stated here**: check the live Clay price for each action (and run /calculate-costs after a test run) before scaling. Volumes are bounded by the cell size above; monthly trigger volume is to be **measured on the first run**, not guessed.

### Universal (one Clay build, swap keywords per cell)

| # | Signal | Data source / Clay action | Key filters | Status |
|---|---|---|---|---|
| U1 | **Hiring compliance roles** | Clay "Find Jobs" on the cell's company list; LinkedIn Jobs via Apify as backup | Location Nigeria/Lagos/Abuja/remote-NG; titles: Compliance Officer, Compliance Analyst, AML Analyst, KYC Analyst, KYB, Transaction Monitoring, Financial Crime, MLRO, Fraud Analyst; posted in last 30 days | VERIFIED |
| U2 | **New compliance leader** (started in last 90 days) | Clay "Find People" at company + job start date | Titles: Chief Compliance Officer, Head of Compliance, MLRO, Head of Risk and Compliance, Head of Financial Crime; start date within 90 days | VERIFIED |
| U3 | **Compliance team growth** | Clay "Find People" count by title at company, monthly snapshot | Same titles as U1; growth of 2+ people or 25%+ in 6 months | VERIFIED (COMPOUND): pair with U1 or U2 |
| U4 | **Recent funding** | Crunchbase via Clay "Find Organization" / funding fields | Nigeria HQ or Nigeria ops; round in last 6 months | VERIFIED (COMPOUND): Nigerian fintech is VC-backed, but round volume is low; use as a secondary enrichment |
| U5 | **Compliance tools named in job posts** | Job description text from U1 | Keywords: Youverify, Smile ID, Dojah, Prembly, Smartcomply, Adhere, ComplyAdvantage, Sumsub, SEON, goAML | VERIFIED (COMPOUND): routing enrichment, angle "sits on top of [tool]" |
| U6 | **Product or market launch** (new customer type, new country, business accounts) | Google News RSS per company via Clay HTTP | Company name + "launches", "expands", "business accounts", "new market" | VERIFIED (PARTIAL): news coverage is uneven; needs known company names (fine, lists are closed) |

### Niche-specific (Nigeria)

| # | Signal | Data source / Clay action | Applies to | Status |
|---|---|---|---|---|
| N1 | **New or changed CBN payments licence** | Monthly scrape and diff of https://www.cbn.gov.ng/PaymentsSystem/PSPs.html (Clay HTTP or scheduled scraper) | A1, B1, D1 | VERIFIED |
| N2 | **New IMTO licence** | Monthly diff of the CBN IMTO page, plus Google News RSS "IMTO licence" | C1 | VERIFIED (PARTIAL): page not yet fetched; news backup |
| N3 | **SEC ARIP admission or VASP licence** | SEC Nigeria circulars page, monitored via Clay HTTP; Google News RSS "SEC ARIP" | C1 | VERIFIED (PARTIAL): notices, no list |
| N4 | **New CBN circular affecting a licence category** | CBN circulars page monitored (Clay HTTP); manual review of relevance | All cells (one campaign per circular to the affected cells) | VERIFIED (PARTIAL): event-driven, needs a human relevance check per circular |
| N5 | **MFB licence upgrade (national/state)** | CBN MFB list (link to be located) + news | B1, D1 | PARTIAL: source link still to find |
| N6 | **New partner bank or bank partnership announced** | Google News RSS: company + "partners with" + bank names | B1, C1 (and B2/C2 later) | VERIFIED (PARTIAL) |

### Killed (and why)
- **Lookalike of existing customers:** customers are confidential and not Nigerian.
- **Technographics (BuiltWith):** compliance and ID tools are back-end and undetectable. Replaced by U5 (job post keywords).
- **CBN enforcement or fines as a trigger:** fear framing is banned in facts.md, and reporting is inconsistent. Use only as internal account research.
- **Website visitors (RB2B):** US only.
- **LinkedIn content engagement:** not yet verified for Nigerian compliance leaders. Revisit if the team sees activity.

### Compounding insight
Of 12 live signals, **6 are universal** (one Clay build across all four priority cells; only title keywords and the angle change) and **6 are niche-specific** (registers and regulator feeds, each built once). The registers double as the account list for every cell.

### Matrix 2 by cell (play + angle)

| Signal | A1 B2B payments | D1 Consumer banks/MMOs | C1 Cross-border | B1 Business banking |
|---|---|---|---|---|
| U1 Hiring compliance | Hiring KYB/onboarding analysts: offer to take the merchant review queue | Hiring KYC/AML analysts: take the KYC exceptions and screening false positives | Hiring TM/AML analysts: work alerts with history and reasons | Hiring KYB analysts: business onboarding |
| U2 New compliance leader | First 90 days: review stack; "keep what you built" | Same, named account | Same | Same |
| N1 / N2 / N3 New licence | New PSSP/switch licence: compliance build-out ahead of CBN AML deadline | Licence upgrade: more scrutiny, more volume | New IMTO / ARIP: correspondent and regulator questions | New licence |
| N4 CBN circular | UBO circular: owner tracing on merchants | AML baseline standards | Circular on IMTO settlement | UBO circular |
| N6 Partner bank news | n/a | n/a | New corridor or partner: RFIs | New bank partnership: bank questionnaires |

All cells pitch the same product (Asterisk). The **lead workflow** changes: A1 KYB review; D1 KYC review and alert review; C1 alert review and RFIs; B1 KYB and RFIs.

---

## Matrix 3: Workflow tracker

| W # | Status | Workflow name | Mother intent | Cells | Persona | Channel | Clay URL | Copy URL | Total leads |
|---|---|---|---|---|---|---|---|---|---|
| W1 | Copy approved | Nigerian fintechs hiring compliance analysts | Hiring specific roles (U1) | A1, D1, C1, B1 | Head of Compliance / CCO | Email | | | |
| W2 | Planned | New compliance leaders at Nigerian fintechs | New leadership (U2) | A1, D1, C1, B1 | New CCO / Head of Compliance | Email | | | |
| W3 | Planned | New CBN payments licence | Niche: register diff (N1) | A1, B1, D1 | CEO/COO + Head of Compliance | Email | | | |
| W4 | Planned | New IMTO and SEC ARIP licensees | Niche: register diff (N2, N3) | C1 | Head of Compliance / MLRO | Email | | | |
| W5 | Planned | CBN circular response | Regulatory change (N4) | Per circular | Head of Compliance | Email | | | |
| W6 | Planned | Product or market launch | New product launches (U6) | A1, B1, C1 | Head of Compliance | Email | | | |
| W7 | Planned | New partner bank | Niche: partnership news (N6) | B1, C1 | Head of Compliance / Partnerships | Email | | | |
| W8 | Planned | Named accounts: consumer banks and MMOs | Niche: account-based | D1 | CCO + CEO/COO | Email + LinkedIn | | | |

Compound enrichments for routing on every workflow: U3 team growth, U4 funding, U5 tools named in job posts.

## Sources
- CBN PSP register (fetched): https://www.cbn.gov.ng/PaymentsSystem/PSPs.html
- CBN IMTO page: https://www.cbn.gov.ng/PaymentsSystem/InternationalMoneyTransferOperators.html
- Grey IMTO: https://thecondia.com/grey-secures-imto-licence-cbn/
- NALA IMTO: https://itweb.africa/article/nala-enters-nigeria-with-imto-license-nibss-integration/wbrpOMg2wYx7DLZn
- Flutterwave banking licence (April 2026): https://www.semafor.com/article/04/03/2026/nigerian-digital-payments-company-flutterwave-granted-banking-license
- SEC ARIP circular (July 2, 2026): https://sec.gov.ng/for-investors/keep-track-of-circulars/sec-clears-seven-new-fintech-firms-for-admission-into-the-accelerated-regulatory-incubation-programme-arip/
- Busha and Quidax ARIP: https://techpoint.africa/insight/sec-clears-vasps-for-arip/
- Duplo and Wema ALAT Business: https://techcabal.com/?p=193289
- Brass into Paystack MFB: https://techeconomy.ng/tag/fintech-nigeria/feed/
- OnePurze partner model: https://thecondia.com/onepurze-cross-border-fintech-regulations/
- National licence upgrades (January 2026): https://nairametrics.com/2026/01/26/cbn-upgrades-opay-moniepoint-other-major-fintechs-mfbs-to-national-status/
