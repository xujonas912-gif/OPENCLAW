# Rules

This directory stores task-level and control-level rules for the e-commerce assistant.

Current rule files:
- `escalation-policy.md`: high-level escalation and safety policy
- `inspection.md`: store inspection rules and prioritization
- `customer-service.md`: support message classification, risk, and draft rules
- `product-check.md`: listing / product maintenance and quality checks
- `automation-control.md`: automation classes, confirmation gates, stop conditions, and audit rules

Recommended use order:
1. Start from `escalation-policy.md`
2. Load the module-specific rule file for the current task
3. Apply `automation-control.md` when any action may move beyond read-only or draft-only work
