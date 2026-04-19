# 从 Claude Code 提炼：最值得电商运营 Agent 学习的 10 个设计点

用途：总结 Claude Code 分析/源码里最值得迁移到 ecom-assistant 的设计方法。
目标：不是复刻 Claude Code，而是提取能让本地电商 agent 更稳定、更智能、更可扩展的部分。

---

## 1. 把 Agent 当运行时系统，而不是聊天工具

### 设计点
Claude Code 的本质不是 CLI 聊天，而是一个 agent runtime：
- query / tool / permission 内核
- memory 系统
- skills / MCP 扩展
- 多 agent 协作
- session 持久化

### 为什么重要
如果只是聊天式助手，任务一复杂就会散、忘、乱。
运行时系统思维更适合长期任务、反复任务、可扩展任务。

### 对 ecom-assistant 的迁移
后续不要把系统理解成“一个会答问题的 AI”，而要理解成：
- orchestrator
- inspection / ops
- customer support
- listing / product check
- execution guardrail
- memory / references / templates

### 当前可直接应用
在目录和文档层面先按模块拆，不再把知识堆成一坨。

---

## 2. Prompt 分层，而不是一段总提示词

### 设计点
Claude Code 把 prompt 分成：
- 默认 system prompt
- agent prompt
- append prompt
- user context
- system context
- task-specific prompt

### 为什么重要
不同任务需要不同约束。把所有规则塞到一段总提示词里，会越来越乱。

### 对 ecom-assistant 的迁移
至少拆成四层：
- 身份层：角色、目标、基本边界
- 任务层：巡检/客服/商品/执行
- 上下文层：当前店铺、当前任务状态、当前页面信息
- 风控层：禁区、确认机制、敏感动作

### 当前可直接应用
后续新增模块时，统一写清：
- 适用场景
- 输入
- 输出
- 风险边界

---

## 3. Context 按需加载，而不是全量灌入

### 设计点
Claude Code 通过模块化 sections、动态注入和条件技能，避免每次都把全部上下文硬塞进去。

### 为什么重要
上下文越杂，越容易混乱、跑偏、成本高。

### 对 ecom-assistant 的迁移
- 做巡检时，优先加载巡检规则与阈值
- 做客服草稿时，优先加载客服分类与模板
- 做商品检查时，优先加载商品检查规则
- 做执行任务时，额外加载风控边界与确认机制

### 当前可直接应用
后续把规则、模板、参考笔记继续拆开，不做单一超长总文档。

---

## 4. Skills 是能力封装单元，不是普通文档

### 设计点
Claude Code 的 skills 有：
- 发现机制
- 元数据
- 条件触发
- 工具边界
- prompt 生成逻辑

### 为什么重要
这样知识不只是“被看见”，而是“能被调用”。

### 对 ecom-assistant 的迁移
后续逐步把知识沉淀成 skill-like 模块，例如：
- inspection skill
- cs-draft skill
- product-check skill
- execution-guardrail skill
- 1688 distribute-chain skill

### 当前可直接应用
每份规则文件都朝这个结构靠：
- 用途
- 适用场景
- 输入
- 输出
- 规则
- 风险边界

---

## 5. 专项任务协议比通用能力更稳定

### 设计点
Claude Code 对 compact、memory update 等后台任务，不用通用 prompt，而是给专项协议。

### 为什么重要
专项任务：
- 目标单一
- 工具受限
- 输出固定
- 跑偏概率小

### 对 ecom-assistant 的迁移
后续任务都尽量专项化：
- 巡检任务协议
- 客服草稿任务协议
- 商品检查任务协议
- 确认执行任务协议

### 当前可直接应用
每个模块后续都补“固定输出模板”和“允许/禁止动作”。

---

## 6. 权限与确认要放进流程，而不是口头提醒

### 设计点
Claude Code 的 permission 不是附属提示，而是运行时控制的一部分。

### 为什么重要
高风险操作如果只靠“谨慎点”，迟早翻车。

### 对 ecom-assistant 的迁移
动作天然分层：
- 只读
- 草稿准备
- 确认后执行
- 禁止自动

关键动作必须写死边界：
- 改价
- 上下架
- 自动发消息
- 自动评价回复
- 售后/退款处理

### 当前可直接应用
已经落地到：
- `ecommerce-rules-automation.md`
后续继续把它搬进 `ecom-assistant` 目录结构中。

---

## 7. 多 Agent 的重点是角色与协作，不是数量

### 设计点
Claude Code 的 multi-agent 不只是开子任务，而是有：
- subagent
- coordinator
- teammates
- mailbox / task / permission bridge

### 为什么重要
一个大而全 agent 很容易负担过重。
角色化更利于复杂任务拆解。

### 对 ecom-assistant 的迁移
当前最合适的角色拆法：
- orchestrator
- ops / inspection
- cs
- listing / product
- research（后续）
- execution guardrail（后续）

### 当前可直接应用
继续完善 `ecom-assistant/agents/` 结构，让不同 agent 的职责更明确。

---

## 8. Memory 要分层，不要什么都记

### 设计点
Claude Code 有 session memory、transcript、resume、compact 等机制。

### 为什么重要
长期协作场景里，真正重要的不是记住一切，而是记对层次。

### 对 ecom-assistant 的迁移
至少分三层：
- 长期层：规则、模板、知识、边界
- 工作层：当前目标、当前待办、近期结论
- 临时层：当前页面、当前商品、当前消息

### 当前可直接应用
后续把：
- references/
- rules/
- templates/
- runbooks/（或 tasks/）
分工更清晰。

---

## 9. 上下文压缩的核心不是删历史，而是重注入关键状态

### 设计点
Claude Code 在 compact 时，不是简单截断，而是保留关键附件、当前计划、技能、工具声明等状态。

### 为什么重要
真正的长期任务不是怕历史变短，而是怕工作台状态丢失。

### 对 ecom-assistant 的迁移
后续在做长任务时，应该优先保留：
- 当前目标
- 当前待办
- 当前风险边界
- 当前页面/任务状态
- 已确认结论

### 当前可直接应用
做链路测试时，记录方式要偏“当前状态摘要”，而不是堆原始流水。

---

## 10. 先把可迁移的模式学会，不急着复刻复杂实现

### 设计点
Claude Code 很强，但也很复杂。不是所有实现都适合当前阶段照搬。

### 为什么重要
如果一开始就追复杂 runtime / swarm / cache / resume 细节，容易掉进过度工程化。

### 对 ecom-assistant 的迁移
当前优先顺序应是：
1. 模块化能力
2. 规则边界
3. 可行性测试
4. 任务模板
5. 角色拆分
6. 再考虑更复杂的自动化和协作

### 当前可直接应用
继续坚持：
- 先验证真实链路
- 再写最小可用流程
- 再考虑自动化扩展

---

## 总结

对 ecom-assistant 最有价值的，不是 Claude Code 的某一份源码，而是这套方法：

- 模块化能力
- 分层 prompt / context
- Skills 化沉淀
- 专项任务协议
- 流程内建权限边界
- 角色化协作
- 分层 memory
- 长任务状态保留
- 渐进式工程化

一句话：
**学 Claude Code，不是为了变成 Claude Code，而是为了让 ecom-assistant 更像一个稳定、可扩展、有边界的本地 agent 系统。**
