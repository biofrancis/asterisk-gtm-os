# Personas: Asterisk Nigeria

Status: DRAFT v1, 2026-11-13. Hypotheses built from the product's design (A) and the Nigerian market (N). Validate on first calls.
Sources: [asterisk-raw.md](../docs/research/asterisk-raw.md) (A), [nigeria-market-raw.md](../docs/research/nigeria-market-raw.md) (N).

## Who to contact first
Primary recipient: **Head of Compliance / Chief Compliance Officer / MLRO.** They own the work Asterisk takes over, and the CBN requires a named, accountable compliance officer (job posting evidence in N section 2 searches). Asterisk's pay-as-you-go entry means they can start without a big procurement [A: section 4].

## 1. Head of Compliance / CCO / MLRO (champion and usually the buyer)
- **Titles:** Chief Compliance Officer, Head of Compliance, MLRO, Compliance Lead, Head of Compliance and Risk.
- **Background:** often recruited from a bank (fintechs hire experienced bank staff) [N: section 2].
- **Owns:** KYC/KYB policy, STR filing to NFIU, CBN examinations, partner bank relationships, the AML automation roadmap.
- **Pains (in their words, hypothesised):**
  - "My team spends the day clearing false screening matches and chasing documents."
  - "The bank sent another 40-question questionnaire and I have to pull the evidence from five places."
  - "We need an automated AML plan for the CBN and I don't want a 9-month implementation."
  - "We built onboarding in-house and I can't rip it out."
- **What they care about:** audit trail and reasons for every decision, regulator-readiness, not adding headcount, keeping control over decisions.
- **Asterisk hook:** handles the reviews and follow-up like an analyst, records decisions with sources, works in Slack and email, keeps the existing stack [A: sections 1 to 3].
- **Fears:** an AI making decisions the CBN will question; data leaving Nigeria; another tool to configure.

## 2. Compliance / KYC / AML Analyst or Ops Lead (user, influencer)
- **Titles:** Compliance Analyst, KYC Analyst, AML Analyst, Onboarding Lead, Risk Operations Lead.
- **Owns:** the queue: failed ID checks, screening hits, KYB files, alerts.
- **Pains:** repetitive manual reviews, missing documents, alert backlog.
- **Asterisk hook:** takes the queue work off them and leaves them the judgment calls.
- **Note:** don't frame Asterisk as replacing them. Frame it as taking the repetitive part.

## 3. CEO / COO / Founder (economic buyer at smaller fintechs)
- **Pains:** compliance cost slowing growth (a survey reports 87.5% say compliance cost significantly limits their capacity to innovate [N: section 2]); onboarding delays costing merchants; partner-bank or licence risk.
- **Asterisk hook:** scale compliance work without matching headcount; start pay-as-you-go [A: section 4].

## 4. CTO / Head of Engineering / Head of Product (technical evaluator)
- **Pains:** in-house onboarding flows and rules they don't want to migrate; compliance asks that become engineering tickets.
- **Asterisk hook:** API and MCP; your own agents can hand Asterisk a review and get the decision back with sources; no migration [A: section 3].
- **Will ask about:** data residency (Nigeria localisation, 1 January 2027 [N: section 1]), security, which ID vendors are supported.

## 5. Head of Partnerships / Banking Relations (situational)
- Owns the partner bank relationship at BaaS-dependent fintechs. Feels the RFI and questionnaire load. A good second contact for the RFIs angle.
