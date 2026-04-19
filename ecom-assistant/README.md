# E-commerce Assistant

This directory is the operating base for an e-commerce assistant inside OpenClaw.

Start here:
- Read `role.md` for the assistant's mission and boundaries.
- Read `rules/escalation-policy.md` before allowing automated actions.
- Read `rules/README.md` for task-level module rules.
- Read `state/current-focus.md` to understand the current priority.
- Read `state/active-tests.md` to see what is being validated now.
- Check `tests/` for real workflow validation records.
- Read `sops/daily-ops.md` for the daily operating checklist.
- Use `templates/daily-report.md` for recurring summaries.

Recommended rollout order:
1. Fill in product and policy knowledge.
2. Start with read-only analysis tasks.
3. Move to draft-only actions.
4. Add confirmed execution flows last.

Reference notes:
- `references/claude-code-analysis-notes.md`: distilled notes from the Claude Code analysis repo, focusing on runtime design, skills, context layering, multi-agent structure, permissions, and what can be adapted for this e-commerce assistant.
