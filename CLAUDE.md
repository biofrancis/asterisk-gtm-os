# Asterisk GTM Context OS

## Company
Asterisk (useasterisk.com): "The AI compliance team for fintechs", a proactive AI coworker that runs KYB/KYC reviews, transaction monitoring, alert reviews and bank RFIs, plugged into a fintech's existing tools and agents. A product of Serai, Inc. (New York), which also makes Karsa; Asterisk is the pivot from Karsa (about Sept 2026). Source: context/docs/research/asterisk-raw.md.
This build covers Nigeria only (owner: Nigeria country lead).
Target ICP (starting point, refine in context/icp/icp.md): growth-stage Nigerian fintechs that process payments or move money, operate under regulatory obligations or regulated partners, are expanding, and run recurring manual compliance, risk or ops processes.

## How this folder works
- `context/icp/`: ICP, personas, signal matrix. Read before any targeting, campaign or copy work.
- `context/positioning/`: positioning, value proposition, competitors. Read before writing anything customer-facing.
- `context/messaging/`: messaging and facts.md (approved claims, proof, banned words). Read before writing copy.
- `context/brand-kit/`: tone of voice and key phrases. Read before writing copy.
- `context/docs/`: research/ (raw sourced facts), case studies, GTM system map. Read research only when building or checking context docs.
- `knowledge-base/playbooks/`: method docs the skills read. Read when a skill or task points to them.
- `knowledge-base/learnings/`: what worked and what didn't. Read before planning a new campaign.
- `meetings/`: meeting notes. Read when a task references a meeting.
- `output/campaigns/`: campaign strategy and one folder per workflow. Read when working on a campaign.
- `tools/`: CLIs, scripts and install guides. Read when using a tool.
- `weekly-priorities/`: one file per ISO week. Read at the start of every session.
- `work-log/`: one file per ISO week, timestamped entries. Read at the start of a session to pick up where we stopped.
- `.claude/skills/`: Claude Code skills.

## Rules
- Cite a source for every company fact.
- Never invent numbers.
- No em dashes in any copy.
- Ask before sending or publishing anything.
- Log every change in this week's work log (work-log/YYYY-Www.md).

## Skills (.claude/skills, from the GTM Starter Kit)
- Strategy and context: /signal-matrix, /campaign-strategy, /build-workflow-spec, /campaign-copy, /prompt-builder.
- Clay build and QA: /clay-build-plan, /campaign-contract, /design-clay-table-json, /import-clay-table, /build-clay, /save-clay-schema, /campaign-qa.
- Clay costs and data: /calculate-costs, /workspace-cost-audit, /export-tables.
- Research and diagrams: /crawl4ai, /agent-browser, /miro-gtm-flowchart.
- Deliverability: /inbox-placement-test.

## Tools
- rex (tools/rex): unofficial Clay client used by the Clay skills. Not installed yet; see tools/rex/GETTING_STARTED.md.
- crawl4ai, agent-browser (tools/): install guides only, not installed yet.
- treg (CLI, paid data lookups): run `tools/treg-venv/bin/treg` with `TREG_CONFIG` set to `.treg/config.json` in this folder (set in .claude/settings.local.json). Find with `treg catalog search "<task>"`, check the price with `treg catalog get <id>` before every call.
