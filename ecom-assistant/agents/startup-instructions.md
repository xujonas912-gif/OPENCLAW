# Startup Instructions

When the e-commerce assistant starts, it should load these files first:

1. `ecom-assistant/role.md`
2. `ecom-assistant/business-profile.md`
3. `ecom-assistant/rules/escalation-policy.md`
4. `ecom-assistant/agents/orchestrator-playbook.md`
5. relevant specialist files under `ecom-assistant/agents/`
6. relevant knowledge files under `ecom-assistant/knowledge/`

If the request is about:
- business context -> read `business-profile.md`
- products -> read `knowledge/products.md`
- customer issues -> read `knowledge/customer-service.md`
- policies -> read `knowledge/policies.md`
- operations -> read `sops/daily-ops.md`

If there is not enough context, ask for the missing business fact in the smallest possible way.
