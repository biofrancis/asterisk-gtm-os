# W1: Nigerian fintechs hiring compliance roles

**Status:** COPY-APPROVED 2026-11-19 (structure approved 2026-11-14)

Built with /build-workflow-spec from [signal-matrix.md](../../../context/icp/signal-matrix.md) (W1). Every section was approved by the Nigeria country lead. Copy goes to /campaign-copy, which appends below.

---

## 1. Mother Intent (Trigger) [ENGINE]
A licensed Nigerian fintech has posted at least one compliance role based in Nigeria (AML, KYC/KYB, transaction monitoring, financial crime, compliance officer, MLRO) in the last 30 days.
Catalog: ⭐ Hiring specific roles. Expensive to fake: a compliance hire is real budget going into compliance work now.

## 2. Inclusion / Exclusion [ICP]

### Include
- **Account list:** signal-matrix cells A1 (CBN switching, PSSP and PTSP licensees doing merchant or business payments), B1 (MFBs and PSSPs in business banking), C1 (IMTO licensees, cross-border PSSPs, SEC ARIP firms), D1 (MMOs and national-licence MFBs).
- **Size:** 50+ employees on LinkedIn (growth-stage-and-larger proxy, approved).
- **Trigger titles** (job title, or the first 300 characters of the job post): compliance officer, compliance analyst, compliance associate, compliance manager, AML, anti-money laundering, KYC, KYB, customer due diligence, transaction monitoring, financial crime, MLRO, sanctions, onboarding analyst, risk and compliance.
- **Job location:** Nigeria, Lagos, Abuja, or remote with Nigeria named.
- **Recipient:** Head of Compliance / CCO / MLRO. When the posted role is itself the head (S2 = leadership), the recipient is the **COO, then the CEO**.

### Exclude
- Card schemes (Visa, Mastercard, American Express, UnionPay, Verve and others in the register's card/payment schemes category), NIBSS, Interswitch PSHC, super-agent-only licensees.
- ID and compliance vendors: Smile Identity Nigeria, Youverify, Dojah, Prembly, Smartcomply, Blusalt.
- Deposit money banks.
- Asterisk customers and active pipeline: none in Nigeria as of 2026-11-14 (owner). Anyone contacted in the last 90 days.
- Non-financial-compliance posts: titles matching tax, HSE, health and safety, telecom, engineering, intern, NYSC.

## 3. Sources [ENGINE]

| Need | Source |
|---|---|
| Account list | CBN PSP register https://www.cbn.gov.ng/PaymentsSystem/PSPs.html (snapshot: context/docs/research/sources/cbn-psp-register-2026-11-13.md); CBN IMTO list https://www.cbn.gov.ng/PaymentsSystem/InternationalMoneyTransferOperators.html; CBN MFB list (link to locate); SEC ARIP circulars https://sec.gov.ng/for-investors/keep-track-of-circulars/. CSV import to Clay |
| Domain and LinkedIn company match | Clay "Enrich Company" |
| Trigger: open roles | Clay "Find Jobs" on the account list; backup LinkedIn Jobs via Apify; Jobberman to be verified |
| Job post text | Find Jobs / Apify job description |
| Headcount | Clay "Enrich Company" |
| Compliance team growth | Clay "Find People" with compliance titles + current-role start date |
| Funding | Crunchbase via Clay |
| Recipient | Clay "Find People" (recipient titles), then the Clay email waterfall |

## 4. Signals table [ENGINE]

| # | Signal | Role | How it's read | Output |
|---|---|---|---|---|
| S1 | Compliance role posted in Nigeria, last 30 days | trigger | Boolean: title matches trigger regex AND location matches Nigeria/Lagos/Abuja AND posted ≤ 30 days ago AND title does not match exclusion regex | true / false |
| S2 | Role cluster | router | Regex on each S1-true title, checked in this order: **leadership** (head, chief, CCO, MLRO, director, VP), **monitoring** (AML, anti-money laundering, transaction monitoring, financial crime, sanctions), **onboarding** (KYC, KYB, due diligence, CDD, onboarding), **general** (any other trigger match). With several roles, the earliest match in that order wins | enum: leadership / monitoring / onboarding / general |
| S3 | Open compliance roles | router | Count of distinct S1-true posts per company | clusters: **1** = filling one seat; **2+** = building out the team |
| S4 | Segment | context-clause | From the source register: A1 / B1 / C1 / D1 | merchants / business customers / transfers / customers |
| S5 | Compliance tool named in the job post | context-clause | Regex on job description: Youverify, Smile ID, Dojah, Prembly, Smartcomply, Adhere, ComplyAdvantage, Sumsub, SEON, goAML | tool name or empty |
| S6 | Recipient found | gate | Boolean: Find People returns a recipient-title person | true, or no send |
| S7 | Compliance team growth | context-clause | Count of people with compliance titles (S1 regex) whose current-role start date is in the last 6 months | clusters: **0-1** = no clause; **2+** = growing clause |
| S8 | Recent funding | context-clause | Crunchbase: last round date within 12 months | round type + month, or empty |

Context-clause rule: at most one per email. Priority is S5, then S7, then S8 (first present). S4 is always available as the customer word.

## 5. Routing matrix WITH angles [ENGINE]

4 role clusters × 2 count clusters = **8 cells**. Every cell has `{{company_name}}`, `{{role_title}}`, `{{segment_customer_word}}`.

| Cell | Deterministic read | What it tells us (inferred situation) | The angle it earns |
|---|---|---|---|
| 1. Leadership, 1 role | S2 = leadership, S3 = 1 | They are hiring the head of compliance: the seat is empty or being upgraded, and daily reviews still run during the search. Recipient: COO, then CEO. | Keep the review work moving while the seat is filled. Asterisk runs reviews and records each decision with reasons and sources, so the new head inherits an explained file, not a backlog. |
| 2. Leadership, 2+ roles | S2 = leadership, S3 = 2+ | They are building the compliance function from the top: a head plus a team. Recipient: COO, then CEO. | Design the new function with the repetitive review work handled from day one, so the head and team they are hiring go to judgment calls. Set it up before the team arrives. |
| 3. Monitoring, 1 role | S2 = monitoring, S3 = 1 | They are adding an AML or transaction-monitoring seat: alert volume has outgrown the current analysts. | Asterisk works each alert with the customer's history and records the decision with reasons, so the new analyst spends time on escalations and reporting decisions, not routine clears. |
| 4. Monitoring, 2+ roles | S2 = monitoring, S3 = 2+ | They are building an AML and monitoring team: monitoring is scaling as a programme. | Scale alert review without scaling analysts one-for-one, with every decision documented. Fits the CBN's direction on automating AML work (public fact only, never a certification claim). |
| 5. Onboarding, 1 role | S2 = onboarding, S3 = 1 | They are adding a KYC/KYB seat: more `{{segment_customer_word}}` are being onboarded. | Asterisk works the failed and flagged ID checks against what's on file, runs the business checks (CAC, owners, screening) and chases missing documents. The hire takes the edge cases. Their ID vendor stays. |
| 6. Onboarding, 2+ roles | S2 = onboarding, S3 = 2+ | They are building out an onboarding review team: volume is up or a new customer type is coming on. | Take over the review step the team does by hand, without touching the onboarding flow they built, and flag risks the current flow doesn't yet cover. |
| 7. General, 1 role | S2 = general, S3 = 1 | They are adding one generalist compliance officer: a small team where one person covers KYC, monitoring and bank requests. | One coworker that takes the repetitive part of all of it, including answering partner bank questionnaires from evidence already on file. |
| 8. General, 2+ roles | S2 = general, S3 = 2+ | They are growing a general compliance team: load is rising across several workstreams at once. | Start with the workflow that hurts most (partner bank questionnaires, KYB or alerts) and add more later, paying only for what it does. No migration. |

**Branch coverage:**
- `{{open_roles_count}}` exists only in cells 2, 4, 6 and 8.
- Cells 1 and 2 go to the COO/CEO, and their angles don't assume the reader does compliance work day to day.
- `{{tool_named}}`, the team-growth clause and `{{funding_round}}` are optional in every cell, and no angle depends on them.

**Niche-native:** each angle depends on the posted role type and on Nigerian specifics (ID vendors, CAC checks, partner banks, the CBN AML direction).

## 6. Variables contract [ENGINE]

| Variable | Source field | Exists in branches |
|---|---|---|
| `{{first_name}}` | Find People: first name | All |
| `{{company_name}}` | AI column (text only): short brand name cleaned from the register's legal name (e.g. "Nomba Financial Services Limited" → "Nomba") | All |
| `{{role_title}}` | Find Jobs: title of the role that decided S2, title-cased | All |
| `{{role_cluster}}` | S2 enum | All (routing only, never printed) |
| `{{open_roles_count}}` | S3 count | Cells 2, 4, 6, 8 |
| `{{segment_customer_word}}` | S4 | All |
| `{{tool_named}}` | S5 match | Where present |
| `{{compliance_hires_6m}}` | S7 count (2+ only) | Where present |
| `{{funding_round}}`, `{{funding_month}}` | S8 | Where present |
| `{{context_clause_type}}` | First present of S5, then S7, then S8, else none | All (routing only) |
| `{{sender_first_name}}` | "Shahryar" (facts.md) | All |

## 7. Cadence & channel [ENGINE]
- **Periodicity:** always-on. Find Jobs re-runs weekly on the account list. A company enters once per trigger, with a 90-day cooldown.
- **Channel:** email from Shahryar Hasnani, Founder & CEO. The CTA is a call with the team, with no calendar link in email 1. LinkedIn is out of v1.

## Definition of done
- [x] Mother intent: one sentence, signal-led, catalog match
- [x] Inclusion: ICP box + trigger + recipient [ICP]
- [x] Exclusion with reasons
- [x] Sources: trigger + every enrichment
- [x] Signals table: deterministic, roles declared
- [x] Count clusters declared (S3, S7)
- [x] Routing matrix with angles (8 cells)
- [x] Branch coverage
- [x] Variables contract
- [x] Engine/ICP markers
- [x] Cadence & channel

---

## Copy

Written with /campaign-copy. Register: signal play, founder voice (Shahryar's own prospect email as the voice reference). Facts from context/messaging/facts.md only. Sender signature: "Shahryar / Founder, Asterisk". Sequence: 3 emails, waits 3 and 7 days, same thread.

### Email 1 (approved 2026-11-19)

**Subject (static):** `{compliance hiring question|quick compliance question|your compliance roles}`

`{{first_name}},`

**Line 1, dynamic (`{{e1l1}}`), one per cell, exhaustive (no fallback):**
+ CELL 1, leadership, 1 role: My guess is someone is covering the reviews and sign-offs while you hire a {{role_title}}.
+ CELL 2, leadership, 2+: With {{open_roles_count}} compliance roles open, including a {{role_title}}, it sounds like {{company_name}} is building the function from the top.
+ CELL 3, monitoring, 1: Adding a {{role_title}} usually comes when transaction alerts are growing faster than the team.
+ CELL 4, monitoring, 2+: Could be off, but {{open_roles_count}} open compliance roles, including a {{role_title}}, suggests monitoring at {{company_name}} is scaling fast.
+ CELL 5, onboarding, 1: Hiring a {{role_title}} probably means more {{segment_customer_word}} are coming through onboarding, so the review queue is growing.
+ CELL 6, onboarding, 2+: With {{open_roles_count}} compliance roles open, including a {{role_title}}, I'd guess onboarding volume is up or a new type of customer is coming on.
+ CELL 7, general, 1: A single {{role_title}} hire often means one person ends up covering KYC, alerts and partner bank requests.
+ CELL 8, general, 2+: Not 100% sure, but {{open_roles_count}} compliance roles at once usually means the work is growing on several fronts.

**Line 2, dynamic waterfall (`{{e1l2}}`), context clause, priority order:**
+ TOOL NAMED (S5): The job description mentions {{tool_named}}, so I'm assuming that stays in place.
+ TEAM GROWTH (S7, 2+): That would follow {{compliance_hires_6m}} compliance hires in the last six months.
+ FUNDING (S8): Makes sense with the {{funding_round}} in {{funding_month}}.
FALLBACK: line omitted (the email reads complete without it).

**Line 3, static:** `{I'm Shahryar, founder of Asterisk.|I'm Shahryar, I founded Asterisk.} {We build|We've built} a proactive coworker that runs the core compliance work for fintechs.`

**Line 4, dynamic (`{{e1l4}}`), one per cell, exhaustive:**
+ CELL 1: It could keep reviews moving while you hire, and record every decision with its reasons and sources, so your new head inherits an explained file rather than a backlog.
+ CELL 2: Set up before the team arrives, it takes the repetitive reviews from day one, so the people you hire spend their time on judgment calls.
+ CELL 3: It works each alert with the customer's history and records the decision with reasons, so the new hire can focus on escalations and reporting decisions.
+ CELL 4: It scales alert review without adding an analyst for every jump in volume, and documents every decision with its sources.
+ CELL 5: It works the failed and flagged ID checks against what's on file and chases missing documents, with your ID vendor staying exactly where it is.
+ CELL 6: It takes over the review step your team does by hand, without touching the onboarding flow you built, and flags risks that flow doesn't cover yet.
+ CELL 7: It takes the repetitive part of all three, including answering partner bank questionnaires from evidence already on file.
+ CELL 8: You can start with whichever piece is heaviest (partner bank questionnaires, KYB or alerts) and add more later, without migrating anything and paying only for what you use.

**CTA, static:** `{Worth a short call with the team to compare notes?|Open to a short call with our team to compare notes?|Would a short call with the team be worth it?}`

`Shahryar`
`Founder, Asterisk`

### Email 2 (approved 2026-11-19), day 3, same thread (subject "Re: <E1 subject>")

`{{first_name}},`

**Line 1, dynamic by role cluster (`{{e2l1}}`), exhaustive (no fallback).** A hedged lead-in plus three examples; the best-matched example comes first so the email doesn't assume a single pain. (Export note: this is a multi-line block. Keep line breaks in the sequencer field, or split it into `{{e2l1a}}`/`{{e2l1b}}`/`{{e2l1c}}`.)

Lead-in, static: `{Not sure which of these matters most for you, but a few things it handles:|Hard to know which of these fits your team best, so a few examples:}`

Examples:
- (A) Investigating a flagged cross-border payment, assessing the source-of-funds evidence and preparing the case for your banking partner
- (B) Checking a new business against the CAC register, tracing its owners and screening everyone behind them
- (C) Drafting answers to your partner bank's questionnaires from evidence already on file, with the sources attached
- (D) Flagging risks nobody asked about, like a new type of customer your review flow doesn't check yet

+ LEADERSHIP (cells 1, 2): D, C, B
+ MONITORING (cells 3, 4): A, B, C
+ ONBOARDING (cells 5, 6): B, A, C
+ GENERAL (cells 7, 8): C, B, A

**Line 2, static:** `{We work|We're working} with fintechs across several markets, and {teams|their teams} configure it in plain English and use it through Slack, email or their own agents.`

**Line 3, static:** `{If it helps,|If useful,} the team can build a sandbox specifically for {{company_name}} so you can try it.`

**CTA, static:** `{Want us to set one up?|Should we put one together for you?|Worth us setting one up?}`

`Shahryar`
`Founder, Asterisk`

### Email 3 (approved 2026-11-19), day 7 after Email 2, same thread

`{{first_name}},`

**Line 1, static:** `{Last note from me on this.|I'll leave it here after this one.}`

**Line 2, static:** `{You can start|Teams usually start} with a single workflow, with no minimum, and add more only if it earns its place.`

**Line 3, static:** `{I'd love to show you what we've built and hear how you're running compliance.|We'd love to show you what we've built and hear how compliance runs at {{company_name}}.}`

**CTA, static:** `{Worth a look, or is someone else at {{company_name}} the right person for this?|Is this worth a look, or should I be talking to someone else at {{company_name}}?}`

`Shahryar`
`Founder, Asterisk`

---

### Assembled sample (cell 5, onboarding, 1 role; consumer fintech; tool named). Company and person are illustrative.

**Email 1 (day 0)**
> **Subject:** compliance hiring question
>
> Tolu,
>
> Hiring a KYC Analyst probably means more customers are coming through onboarding, so the review queue is growing.
>
> The job description mentions Smile ID, so I'm assuming that stays in place.
>
> I'm Shahryar, founder of Asterisk. We build a proactive coworker that runs the core compliance work for fintechs.
>
> It works the failed and flagged ID checks against what's on file and chases missing documents, with your ID vendor staying exactly where it is.
>
> Worth a short call with the team to compare notes?
>
> Shahryar
> Founder, Asterisk

**Email 2 (day 3, same thread)**
> Tolu,
>
> Not sure which of these matters most for you, but a few things it handles:
>
> - Checking a new business against the CAC register, tracing its owners and screening everyone behind them
> - Investigating a flagged cross-border payment, assessing the source-of-funds evidence and preparing the case for your banking partner
> - Drafting answers to your partner bank's questionnaires from evidence already on file, with the sources attached
>
> We work with fintechs across several markets, and teams configure it in plain English and use it through Slack, email or their own agents.
>
> If it helps, the team can build a sandbox specifically for ExamplePay so you can try it.
>
> Want us to set one up?
>
> Shahryar
> Founder, Asterisk

**Email 3 (day 10, same thread)**
> Tolu,
>
> Last note from me on this.
>
> You can start with a single workflow, with no minimum, and add more only if it earns its place.
>
> I'd love to show you what we've built and hear how you're running compliance.
>
> Worth a look, or is someone else at ExamplePay the right person for this?
>
> Shahryar
> Founder, Asterisk
