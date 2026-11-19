# Positioning: Asterisk Nigeria

Status: v1.1, 2026-11-19 (CBN deadline removed; see facts.md).
Sources: [asterisk-raw.md](../docs/research/asterisk-raw.md) (A), [nigeria-market-raw.md](../docs/research/nigeria-market-raw.md) (N).

## Category
**AI compliance team for fintechs.** Asterisk's own words: "The AI compliance team for fintechs", "a proactive AI coworker" [A: section 1].
It is not a KYC data API (Youverify, Dojah, Prembly) and not a rules engine. It's the layer that does the review work on top of those tools.

**Proactive, not reactive** (country lead, 2026-11-13 [S9]). Compliance tools flag and wait. Asterisk sits on the decision layer where human judgment would be needed: it learns the company's existing processes and protocols, notices patterns, monitors transactions, pulls in results from other tools, makes the decision, and cites why and where each decision feeds from. It removes the repetitive manual work analysts do over and over.

## Positioning statement (internal)
For **growth-stage Nigerian fintechs** whose compliance teams are stretched by manual reviews, alert queues and partner bank requests, **Asterisk** is an **AI compliance team** that does the day-to-day reviews, decisions and follow-up like an analyst and spots risks like a compliance officer. **Unlike** compliance software that adds setup and more work, Asterisk plugs into the ID vendor, rules and agents you already run, with no migration, and you pay only for what it does.

## The three ideas we own
1. **It does the work, not more work.** Other tools produce alerts and queues. Asterisk works the queue: clears false matches, chases documents, records decisions with reasons [A: sections 1, 2].
2. **Keep what you built.** Your form, ID vendor, rules and agents stay. Asterisk takes the step your team still does by hand [A: section 3]. This matters in Nigeria, where fintechs built a lot in-house.
3. **Thinks ahead.** It flags risks you didn't ask about, like a new customer type your flow doesn't cover yet [A: section 1].

## Nigeria framing
- **CBN automated AML standards:** issued 10 March 2026 [N]. Deadline dates conflict across sources, so don't name one (facts.md: DO NOT USE). Asterisk is a way to automate the review work without a rip-and-replace. **Do not claim** Asterisk is CBN-certified or "compliant with the baseline standards". That is not established.
- **Partner banks:** "answering your bank" maps to partner bank questionnaires, audits and RFIs, which are common for BaaS-dependent fintechs [N: section 4].
- **Owners:** UBO tracing is now in a CBN payments circular [N]. Asterisk's KYB "traces its owners and screens everyone behind it" [A: section 2].
- Use local terms: partner bank (not sponsor bank), CAC (business register), BVN/NIN, NFIU, STR, CBN.

## Known weak points (handle honestly)
- **No Nigerian proof yet.** Existing customers are outside Nigeria and confidential.
- **Data localisation (1 January 2027)** for payment transaction data [N]. Asterisk's API stores ingested records (see icp.md), so "we don't hold data" is not a usable answer. Needs an engineering and legal answer before transaction monitoring is pitched.
- **CAC:** supported (country lead, 2026-11-13). OK to say Asterisk checks businesses against the CAC register once it's approved in facts.md.
- **USD pricing** [A: section 4] in a naira market.
