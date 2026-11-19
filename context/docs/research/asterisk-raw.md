# Asterisk: raw research

Captured 2026-11-13. Every fact has a source. Quotes are verbatim. Anything not stated by a source is under **Inferences** and is marked as such.

Raw captures in [sources/](sources/):
- [useasterisk-site-copy.md](sources/useasterisk-site-copy.md): every string on the homepage
- [useasterisk-legal.md](sources/useasterisk-legal.md): privacy policy and website terms
- [docs-useasterisk-llms.txt](sources/docs-useasterisk-llms.txt): developer docs index

Source keys used below:
- **[S1]** https://useasterisk.com/ (homepage; text in the JS bundle /assets/main-DtbWtK9L.js)
- **[S2]** https://useasterisk.com/privacy.html and /terms.html
- **[S3]** https://docs.useasterisk.com/ (llms.txt, /platform/overview, /openapi/ingestion.openapi.yaml)
- **[S4]** WHOIS and DNS for useasterisk.com
- **[S5]** https://gokarsa.com/
- **[S6]** https://www.ycombinator.com/companies/karsa
- **[S7]** https://www.ycombinator.com/launches/MgV-karsa-the-global-dollar-account
- **[S8]** https://news.ycombinator.com/item?id=42879661 (Launch HN, 2025-01-30)
- **[S9]** Internal: Karsa's country lead (owner of this Context OS), stated 2026-11-13. Use it for internal context. Don't cite it publicly without approval.

---

## 1. What Asterisk is

- Title: "Asterisk — The AI compliance team for fintechs" [S1]
- Meta description: "Asterisk is a proactive AI coworker that handles compliance for fintechs. It runs customer reviews and monitoring, spots risks your team hasn't found, and plugs into the tools and agents you already have." [S1]
- Hero headline (from og:image alt text): "A new kind of compliance team, for you and your agents" [S1]
- Positioning paragraph: "Asterisk is a thoughtful colleague. It thinks ahead like a compliance officer, spotting risks and what's coming, and it handles the reviews, decisions and follow-up like an analyst." [S1]
- Origin story: "The compliance team we always wanted. We were frustrated that compliance products were tools that gave us more work and more setup. None of them took on the heavy day-to-day work, or helped us catch the risks we hadn't even thought of." [S1]

## 2. Product: workflows ("What you can do with Asterisk") [S1]

| Workflow | Site description | Inputs shown |
|---|---|---|
| KYB review | "Checks the business at its source, traces its owners and screens everyone behind it." | Registers, Ownership, Websites |
| KYC review | "Works the failed and flagged checks from your ID vendor against what's on file." | Your ID vendor, Failed checks, Evidence on file |
| Transaction alert review | "Works each alert with the customer's history and records the decision with reasons." | Customer history, Declared activity, Decisions |
| Transaction monitoring | "Runs the scenarios you choose on your transactions and works what they find." | Structuring, Velocity, Flow of funds |
| RFIs and correspondence | "Answers your sponsor bank and partners from evidence already on file." | Questionnaires, Evidence, Policy gaps |
| And more, or build your own | Listed: Limit increase reviews, Keeping files current, Relationship and network review, Control coverage, Review quality, Regulatory change, Licence maintenance, Policy updates, Filing preparation | |

Example monitoring scenarios shown: "Split under the cash reporting line", "Salary paid into a business account", "Micro-deposit testing", "Many senders, one customer". [S1]

Example bank questionnaire items: "Who approves high-risk customers?", "How do you verify beneficial owners?", "Who reviews dormant accounts?" [S1]

## 3. How it fits in (integration and deployment)

- "With Asterisk you pick the work you want, like customer due diligence, transaction monitoring or answering your bank, and add more whenever you like. Whatever you've built internally stays, with no migration. You can change how any of it works in chat, or from your own tools and agents. You only pay for what you use." [S1]
- Against incumbents: "Most compliance products needed sales calls, contracts, endless configuration and full migrations before you could get started." [S1]
- Surfaces: "Asterisk messages you in Slack, emails you, and works straight from your terminal. ... Your own agents can hand Asterisk a review through the API or MCP and get the decision back with its sources." [S1]
- Product demo shows Slack (#compliance), Gmail draft replies with evidence attached, a terminal command (`asterisk · review_business`), and an onboarding agent calling Asterisk. [S1]
- Demo states the onboarding flow it slots into: Your form, ID check (your vendor), Business review (by hand), Risk rules (your team), Open account (your agent). Asterisk takes over "the one step your team still did by hand". [S1]
- API: "Karsa Data Ingestion API", servers `https://api.sandbox.useasterisk.com` and `https://api.useasterisk.com`. Resources: Customers (individual and business, UBOs), KYB dossiers and runs, Accounts (bank, virtual account, wallet), Transactions, Documents, Screening observations, Monitoring controls, historical RFI events, Outcomes, signed webhooks. [S3]
- Named provider integrations in the API: AiPrise (verification), SEON (fraud), Chainalysis (blockchain alerts), plus "other verification, fraud, AML, transaction-monitoring, or blockchain-screening" providers. [S3]
- KYB run statuses: pending, running, needs_review, completed, failed. [S3]

Illustrative demo numbers (the terms say these are "illustrative product examples ... not customer records" [S2], so **do not use as proof**): "Reviewed 14 new businesses", "Cleared 26 screening matches that were different people", "Chased 3 customers for missing documents", "Answers to all 23 questions". [S1]

## 4. Pricing [S1]

"Start small with no minimum, and scale to a plan when you need it." Annual billing: "Save 10%".

| Plan | Who | Monthly | Annual (per month) | Credits |
|---|---|---|---|---|
| Pay as you go | Flexible, selected use | $0 monthly minimum | $0 | $1 per credit |
| Starter | Selected workflows | $500 | $450 | 625 credits / month |
| Team | Regular team usage | $1,000 | $900 | 1,250 credits / month |
| Scale | Higher work volumes | $2,500 | $2,250 | 3,125 credits / month |
| Custom | Larger commitments, agreed scope and terms | Agreed balance and credit rate | | + custom workflow design |

The site doesn't say how many credits one review or task uses. Internal [S9]: credits are used according to the tasks Asterisk performs. No per-task rate was given.

## 5. Go-to-market signals

- CTA: "Get started". Form: "Leave a work email and we'll send you sandbox access." [S1]
- Form submissions go to Attio (CRM) via a webhook. [S1, S2]
- Privacy page mentions demo bookings through Calendly, and Google for email, calendar, meetings and transcripts. [S2]
- No website analytics or tracking pixels: "We do not currently use website analytics, advertising pixels, or tracking cookies on useasterisk.com." [S2]
- No customer logos, testimonials, case studies, security certifications or compliance attestations (e.g. SOC 2) appear on the site. [S1]
- Nav: Product, Workflows, Pricing, Docs. Company: Contact (support@gokarsa.com). Legal: Privacy, Website terms. [S1]

## 6. Company

- Company structure (internal [S9]): Serai, Inc. is the legal entity. Karsa and Asterisk are both products under Serai, Inc.
- Nigeria (internal [S9]): Karsa has a country lead for Nigeria, the owner of this Context OS. The Asterisk ICP for this build is Nigeria only.
- Customers (internal [S9]): "We're already working with fintechs running over $2 billion transaction volumes annually." Names can't be disclosed yet. The customers are **not Nigerian** (confirmed [S9]). Not yet clear: whether $2B is per fintech or combined, and how many fintechs. Don't use this in public copy until it's clarified and approved. **Asterisk has no Nigerian customer yet**, so Nigeria copy can't claim local proof.
- Legal entity: Serai, Inc., 433 Broadway, #222, New York, NY 10013. Terms governed by Delaware law. Legal pages effective October 30, 2026. "We are based in the United States." [S2]
- Contact email: support@gokarsa.com. [S1, S2]
- Domain useasterisk.com registered 2026-09-12 (NameCheap). Hosted on AWS CloudFront. [S4]
- The developer docs and API spec are titled "Karsa Data Ingestion API" and refer to "Karsa" throughout. [S3]

### Karsa (the predecessor company)
- YC W25. "Stablecoin neobank for emerging markets." Founded 2025, team size 2, New York City, status Active, website gokarsa.com. [S6]
- Founders: Shahryar Hasnani, Founder/CEO ("Previously head of BD at Ethereum infrastructure startup"), and Dale Wilson, Founder/CTO ("Previously protocol development lead at a layer 1 AI Blockchain"). [S6]
- Socials: https://www.linkedin.com/company/karsa/ , https://twitter.com/go_karsa [S6]
- Launch: "going live today with sellers in Pakistan, India, Nigeria, Kenya, Paraguay". [S7]
- Launch HN (2025-01-30): peer-to-peer stablecoin buying via escrow smart contract, "We currently take a 1% transaction fee". Founder on AML: "we do KYC, and we discourage / don't present cash as an option." [S8]
- gokarsa.com today: "Karsa | Export your wallet. Access your Karsa wallet and explore our recommended alternatives." [S5]

## 7. Inferences (not stated by any source; check before using)

1. ~~Asterisk is Karsa's pivot.~~ **CONFIRMED 2026-11-13** by the Context OS owner, who is Karsa's country lead (internal source, [S9]): Asterisk is the pivot from Karsa, made around two months ago (about September 2026, consistent with the domain registration on 2026-09-12 [S4]). Serai, Inc. is the legal entity behind both products (confirmed [S9]).
2. **The "compliance team we always wanted" story likely comes from running Karsa.** A fintech handling KYC, screening and partner obligations in emerging markets would have felt this pain. This is plausible but not stated.
3. **The site copy leans US.** "Sponsor bank", "cash reporting line" (sounds like US currency transaction reporting), USD pricing, NY and Delaware. **No Nigeria, Africa or NGN mention appears anywhere** on the site, in the legal pages or in the API spec. Brazil is the only country named ("Brazilian businesses have started applying, but your review flow doesn't check Brazil's company register yet"). The API does support wallets and Chainalysis, which suggests crypto and stablecoin fintechs are in scope.
4. **Implication for our ICP: RESOLVED [S9].** The ICP for this build is Nigeria only, owned by the Nigeria country lead. The public site is written for a global, US-leaning reader, so Nigerian copy has to translate the concepts locally (for example, "sponsor bank" maps to partner banks and licensed partners; US cash reporting has local equivalents). Do that in context/positioning and messaging, from sourced regulatory facts only.
5. **Stage.** Early: domain two months old, sandbox-access form, no public logos or proof. Internally there are already live fintech customers [S9], so the public site is behind on proof, not the business.

## 8. Gaps (still to research)
- Founders' and team's current LinkedIn titles (do they list Asterisk?)
- Asterisk social profiles (LinkedIn, X), launch posts, any YC re-launch
- Funding since the YC seed
- Customers: none public. Internal: live fintechs over $2B annual volume [S9]. Clarify per-fintech vs combined, the count, the country, and what we may say publicly (e.g. anonymised).
- Credits per task type (internal [S9] says usage is task-based; no rates yet)
- Nigerian regulatory context to source for positioning: CBN, NFIU, SCUML, NDPA/NDPC, CBN AML baseline standards (March 2026)
- Security and data handling (no SOC 2 or similar stated)
- Competitors: possible adjacent players from searches, unverified as competitors: Smartcomply, Rulebase, Grace AI Lab, Optimus AI Labs, Norm AI, Sei.

## Method notes
- The web fetcher and the sandbox at first could not resolve useasterisk.com. Once access was allowed, the site was pulled with curl, and copy was extracted from the JS bundle because the page renders client-side.
- Web search had not indexed useasterisk.com as of 2026-11-13.
