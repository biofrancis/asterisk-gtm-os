# GTM system: Asterisk Nigeria outbound

Status: v1, 2026-11-14. A text and Mermaid version of the system map. The Mermaid flowchart is the system map; no Miro board (owner decision, 2026-11-19).
Built from: [signal-matrix.md](../icp/signal-matrix.md), [W1 workflow spec](../../output/campaigns/nigeria-hiring-compliance-roles/workflow-spec.md), [icp.md](../icp/icp.md), [facts.md](../messaging/facts.md).

## How it works

### Phase 1: Find and qualify accounts
1. **Context OS** (this repo, Claude Code, GitHub): ICP, personas, positioning, facts, signal matrix.
2. **Account list from registers**: CBN PSP register, CBN IMTO list, CBN MFB list, SEC ARIP circulars, loaded into Clay as the closed list for priority cells A1, B1, C1, D1.
3. **ICP filter**: 50+ employees on LinkedIn; drop card schemes, NIBSS, super-agent-only, ID and compliance vendors, deposit money banks, customers, contacts from the last 90 days.
4. **Signals** (Clay, weekly): W1 is live in spec (compliance role posted in Nigeria in the last 30 days). Planned: W2 new compliance leader, W3 new CBN licence, W4 new IMTO or SEC ARIP licensee, W5 CBN circular, W6 product or market launch, W7 new partner bank, W8 named accounts.

### Phase 2: Route and write
5. **Recipient found?** Head of Compliance / CCO / MLRO, or COO then CEO when the head role is the one being hired. No recipient means no send.
6. **Route** (W1): role cluster (leadership, monitoring, onboarding, general) x open roles (1, 2+) = 8 cells, each with an approved angle.
7. **Context clause**: at most one per email: tool named in the job post, then team growth, then funding.
8. **Copy** (/campaign-copy): only claims in facts.md; anything else stays a `{{placeholder}}`.
9. **QA** (/campaign-qa) before anything is sent. Owner approval required.

### Phase 3: Send, reply, learn
10. **Send**: email from Shahryar Hasnani, Founder & CEO. Sequencer: **{{TBD}}**.
11. **Replies**:
    - Interested: call with the team (the primary CTA).
    - Objection: answer from approved material. **The data residency answer is still pending** (engineering and legal).
    - Not now: 90-day cooldown, re-enters on a new signal.
    - Unsubscribe or wrong person: suppress, or re-route to the right person.
12. **CRM**: **{{TBD}}**. Asterisk's website form already feeds Attio (privacy page), so Attio is the likely candidate. Confirm.
13. **Learn**: weekly review of results in knowledge-base/learnings/, which updates the Context OS, the signal matrix and the tracker.

## Open items
- Sequencer and CRM for outbound: not yet chosen.
- Data residency answer for the objection branch.

## Flowchart

```mermaid
flowchart TD
    %% Phase 1: find and qualify accounts
    subgraph P1["1. Find and qualify accounts"]
        A1["1A Context OS<br/>ICP, personas, facts, signal matrix<br/>(Claude Code, GitHub)"]
        A2["1B Account list from registers<br/>CBN PSP, CBN IMTO, CBN MFB, SEC ARIP<br/>(Clay import)"]
        A3{"1C ICP fit?"}
        A3X["Exclude<br/>under 50 staff, card schemes, NIBSS,<br/>ID and compliance vendors, banks,<br/>customers, contacted in last 90 days"]
        A4["1D Signals, weekly in Clay<br/>W1 compliance role posted, last 30 days<br/>Planned: W2 to W8"]
        A5{"1E Signal fired?"}
        A5X["Wait<br/>re-check next week"]
    end

    %% Phase 2: route and write
    subgraph P2["2. Route and write"]
        B1["2A Find recipient<br/>Head of Compliance, CCO, MLRO<br/>(Clay Find People, email waterfall)"]
        B2{"2B Head role hired?"}
        B2Y["2C Recipient: COO, then CEO"]
        B3{"2D Recipient found?"}
        B3X["No send"]
        B4["2E Route: role cluster x open roles<br/>leadership, monitoring, onboarding, general<br/>x 1 or 2+ = 8 cells with angles"]
        B5["2F Context clause, max one<br/>tool named, then team growth, then funding"]
        B6["2G Copy from facts.md only<br/>(/campaign-copy)"]
        B7{"2H QA and owner OK?"}
        B7X["Fix in spec or copy"]
    end

    %% Phase 3: send, reply, learn
    subgraph P3["3. Send, reply, learn"]
        C1["3A Send email from Shahryar<br/>Founder and CEO<br/>(sequencer TBD)"]
        C2{"3B Reply?"}
        C2a["Interested<br/>call with the team"]
        C2b["Objection<br/>answer from approved material<br/>(data residency answer pending)"]
        C2c["Not now<br/>90-day cooldown"]
        C2d["Unsubscribe or wrong person<br/>suppress or re-route"]
        C2e["No reply<br/>sequence ends, cooldown"]
        C3["3C CRM<br/>(TBD, Attio likely)"]
        C4["3D Weekly review<br/>knowledge-base/learnings"]
    end

    A1 --> A2 --> A3
    A3 -- No --> A3X
    A3 -- Yes --> A4 --> A5
    A5 -- No --> A5X
    A5X --> A4
    A5 -- Yes --> B1 --> B2
    B2 -- Yes --> B2Y --> B3
    B2 -- No --> B3
    B3 -- No --> B3X
    B3 -- Yes --> B4 --> B5 --> B6 --> B7
    B7 -- No --> B7X --> B6
    B7 -- Yes --> C1 --> C2
    C2 --> C2a & C2b & C2c & C2d & C2e
    C2a --> C3
    C2b --> C3
    C2c --> C3
    C2d --> C3
    C2e --> C3
    C3 --> C4
    C4 -. "Weekly loop: results update the Context OS" .-> A1
```
