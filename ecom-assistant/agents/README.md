# Agent Map

This folder defines a simple multi-agent operating model for the e-commerce assistant.

Agents:
- `orchestrator.md`: owner-facing control tower
- `ops-agent.md`: operations analysis
- `cs-agent.md`: customer support and after-sales
- `listing-agent.md`: product content and listing quality
- `ads-agent.md`: advertising analysis
- `research-agent.md`: competitor and market research

Recommended rollout:
1. Start with `orchestrator`, `ops-agent`, and `cs-agent`.
2. Add `listing-agent` after product knowledge is populated.
3. Add `ads-agent` when campaign exports are available.
4. Add `research-agent` once web research workflows are stable.
