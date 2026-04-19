# Recent Findings

## Purpose
Store short, durable summaries of what has actually been learned from tests and system design work.

## Findings

### 2026-04-05
- Claude Code analysis is useful as a systems-design reference, especially for runtime design, prompt/context layering, skills, permissions, and multi-agent role structure.
- For this e-commerce assistant, the most important next step is not more theory but building a working structure: tests, state, module rules, and automation boundaries.
- SOPs should come after feasibility is tested, not before.
- The 1688 distribute chain has advanced from entry validation to partial workflow validation.
- The `channel=thyny` distribute settings page body can now be read stably.
- The earlier “blank / unreadable page” problem has been narrowed down to nested iframes and fixed action-bar targeting.
- Real in-frame settings controls can be located and interacted with.
- The remaining hard point is stable selector/ref access to the fixed bottom action bar (`保存配置`, `保存并同步到其他店铺`, `取消修改`).
- The most effective next technical path is likely direct Chrome CDP / Playwright / DevTools frame-level targeting instead of whole-page snapshot reliance.
