# Delegation Map

Use this map when deciding which specialist should handle a task.

## Task -> Agent

- Store performance summary -> `ops-agent`
- Daily report -> `ops-agent`
- Weekly report -> `ops-agent`
- Order anomaly review -> `ops-agent`
- Inventory risk review -> `ops-agent`
- Customer complaint handling -> `cs-agent`
- Customer reply drafting -> `cs-agent`
- Refund-risk review -> `cs-agent`
- Product title drafting -> `listing-agent`
- FAQ drafting -> `listing-agent`
- Product selling point refinement -> `listing-agent`
- Ad account diagnosis -> `ads-agent`
- Campaign anomaly analysis -> `ads-agent`
- ROAS / CPA interpretation -> `ads-agent`
- Competitor review -> `research-agent`
- Platform rule lookup -> `research-agent`
- External product trend scan -> `research-agent`

## Multi-Agent Cases

Use more than one agent when:

- bad reviews are affecting conversion
  - `cs-agent` for complaint patterns
  - `listing-agent` for copy or FAQ fixes

- ad performance is dropping after listing changes
  - `ads-agent` for traffic and spend diagnosis
  - `listing-agent` for page quality review

- refunds or complaints are increasing
  - `cs-agent` for issue taxonomy
  - `ops-agent` for business impact

- preparing a decision memo for the owner
  - specialist agent for analysis
  - orchestrator for final synthesis
