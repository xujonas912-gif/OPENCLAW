# ecom-assistant 结构映射与缺口清单（基于 Claude Code 设计启发）

目的：把 Claude Code 提炼出的设计点，映射到当前 `ecom-assistant/` 目录结构，明确：
- 现在已有什么
- 现在缺什么
- 后续优先补什么

本文件偏落地，不偏概念。

---

## 1. 当前已有结构（已有基础是好的）

当前目录已经有这些层：

### 1.1 角色层
- `role.md`
- `agents/` 下的多个 agent 说明文件

说明：
已经具备“角色拆分”雏形，这一点很好，后续适合继续往协调器 + 专职 worker 方向发展。

### 1.2 规则/边界层
- `rules/escalation-policy.md`

说明：
已经有风险与升级策略入口，但当前还不够细，后续需要细化为动作级别和任务级别边界。

### 1.3 SOP 层
- `sops/daily-ops.md`

说明：
已有流程入口，但目前更像运营清单，后续应建立“已验证流程”和“待验证流程”的区分。

### 1.4 模板层
- `templates/customer-reply-draft.md`
- `templates/daily-report.md`
- `templates/product-brief.md`

说明：
模板层已经存在，说明后续很适合做“专项任务协议”。

### 1.5 知识层
- `knowledge/customer-service.md`
- `knowledge/policies.md`
- `knowledge/products.md`

说明：
已有知识库基础，但当前更像资料仓，后续要逐步靠近“按任务可调用”的结构。

### 1.6 参考层
- `references/claude-code-analysis-notes.md`
- `references/claude-code-design-points-for-ecom-agent.md`

说明：
已有外部方法论参考入口，这是好的，但下一步重点应该从“继续读参考”切到“改本库结构”。

---

## 2. 当前最大的缺口，不是内容少，而是“运行层”还不够清晰

换句话说：
当前库已经有“角色、知识、模板、SOP”的雏形，
但还缺把这些东西连成运行系统的那一层。

最主要缺口如下：

---

## 3. 缺口一：缺少模块级规则层

### 当前问题
虽然有 `rules/escalation-policy.md`，但它更像总则。
还缺少任务模块自己的规则文件。

### 建议补充目录
建议后续增加：
- `rules/inspection.md`
- `rules/customer-service.md`
- `rules/product-check.md`
- `rules/automation.md`

### 作用
这些文件负责定义：
- 模块适用场景
- 输入/输出
- 分级规则
- 风险边界
- 与其他模块的联动

### 优先级
高

---

## 4. 缺口二：缺少任务运行层 / runbooks

### 当前问题
已有 `sops/`，但 SOP 容易被理解成运营汇报流程。
更适合增加一层“任务运行说明”或“runbooks”。

### 建议补充目录
建议后续增加：
- `runbooks/daily-inspection.md`
- `runbooks/customer-draft.md`
- `runbooks/product-check.md`
- `runbooks/1688-distribute-chain.md`

### 作用
只写：
- 何时触发
- 输入是什么
- 先后顺序
- 中断条件
- 输出什么
- 交给谁

### 优先级
高，但应该建立在已验证链路之上。

---

## 5. 缺口三：缺少任务状态 / 工作记忆层

### 当前问题
现在有知识层，但没有一个明确的位置记录“当前正在做什么、最近验证到了哪一步”。

### 建议补充目录
建议后续增加：
- `state/current-focus.md`
- `state/active-tests.md`
- `state/recent-findings.md`

### 作用
用于保存：
- 当前重点方向
- 当前在测哪些链路
- 哪些已验证 / 半验证 / 未验证
- 当前卡点

### 优先级
高

### 说明
这是把长期知识和当前工作状态分开，避免所有内容混在一起。

---

## 6. 缺口四：缺少专项模板协议化

### 当前问题
已有模板，但还偏“文档模板”，不够像“任务协议模板”。

### 建议补充方向
模板后续可细化为：
- 巡检输出模板
- 客服草稿输出模板
- 商品问题单模板
- 待确认动作模板
- 链路测试记录模板

### 作用
让不同任务都能稳定输出固定结构，便于后续自动化。

### 优先级
中高

---

## 7. 缺口五：缺少“已验证 / 未验证”区分

### 当前问题
知识、规则、流程如果不区分验证状态，后面很容易把猜想当事实。

### 建议补充机制
可以在文件头或独立清单里标注：
- `status: draft`
- `status: tested`
- `status: partial`
- `status: blocked`

### 适用文件
- runbooks
- rules
- chain notes
- automation docs

### 优先级
高

---

## 8. 缺口六：agent 角色虽然有了，但执行边界还不够具体

### 当前问题
`agents/` 里已经有角色文件，但还可以继续强化：
- 每个 agent 具体看什么输入
- 输出什么结果
- 不能做什么
- 什么时候升级给 orchestrator

### 建议补充方向
后续 agent 文件中逐步明确：
- scope
- allowed decisions
- escalation triggers
- handoff format

### 优先级
中高

---

## 9. 缺口七：缺少“真实链路测试记录区”

### 当前问题
现在很多学习和判断来自对话或零散记录，没有一个专门位置沉淀“链路测试结果”。

### 建议补充目录
建议增加：
- `tests/1688-distribute.md`
- `tests/inspection-data-access.md`
- `tests/cs-draft-evaluation.md`
- `tests/product-check-evaluation.md`

### 作用
记录：
- 测试目标
- 已打通步骤
- 卡点
- 风险
- 结论（可做 / 半可做 / 暂不适合）

### 优先级
很高

---

## 10. 缺口八：缺少真正的“自动化控制面”文档

### 当前问题
虽然已经有升级策略，但还缺一份把“可自动 / 可半自动 / 必须确认 / 禁止自动”统一写清的控制面。

### 建议补充目录
建议增加：
- `rules/automation-control.md`
或直接扩展 `rules/escalation-policy.md`

### 内容应包括
- 只读任务清单
- 草稿任务清单
- 确认后执行任务清单
- 禁止自动任务清单
- 数量限制
- 失败即停
- 白名单

### 优先级
高

---

## 11. 当前最值得优先做的不是“再加更多知识”，而是补这 4 个点

### P1
1. 真实链路测试记录区（`tests/`）
2. 模块级规则层（`rules/*.md`）
3. 任务状态层（`state/`）
4. 自动化控制面（`rules/automation-control.md`）

### P2
5. runbooks / 已验证流程
6. 更细的模板协议化
7. agent 文件的输入输出与边界强化

### P3
8. 更复杂的任务编排、多 agent 协作机制
9. 更系统的 memory / resume 结构

---

## 12. 推荐的后续目录演化方向

建议逐步演化成：

```text
ecom-assistant/
├── role.md
├── business-profile.md
├── agents/
├── knowledge/
├── references/
├── rules/
│   ├── escalation-policy.md
│   ├── inspection.md
│   ├── customer-service.md
│   ├── product-check.md
│   └── automation-control.md
├── templates/
├── tests/
│   ├── 1688-distribute.md
│   ├── inspection-data-access.md
│   ├── cs-draft-evaluation.md
│   └── product-check-evaluation.md
├── state/
│   ├── current-focus.md
│   ├── active-tests.md
│   └── recent-findings.md
└── runbooks/
    ├── daily-inspection.md
    ├── customer-draft.md
    ├── product-check.md
    └── 1688-distribute-chain.md
```

---

## 13. 结论

当前 `ecom-assistant` 的问题不是没有内容，而是：

**缺少把“角色、知识、模板、规则、测试、状态、执行边界”串成运行系统的中间层。**

所以后续最重要的事不是继续囤知识，而是：
- 用 `tests/` 验证真实链路
- 用 `rules/` 固定判断边界
- 用 `state/` 保存当前工作记忆
- 用 `runbooks/` 只沉淀已验证流程

一句话：
**下一步重点是把 ecom-assistant 从“资料库”推进成“会运行的工作台”。**
