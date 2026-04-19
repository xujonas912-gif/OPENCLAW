# Claude Code Analysis 仓库参考笔记

来源：<https://github.com/liuup/claude-code-analysis>
用途：作为后续建设电商运营 agent / 本地 OpenClaw 助手时的参考资料，不是照搬对象。

---

## 1. 这个仓库是什么

这是一个对 Claude Code 泄露源码做的中文静态分析文档集。

它不是 Claude Code 本体，也不是教程项目，而是把 Claude Code 的核心机制拆开讲：
- 架构
- 安全
- memory
- skills
- tool call
- MCP
- sandbox
- context
- prompt
- multi-agent
- session storage / resume

它的价值不在“功能罗列”，而在于：
**把一个成熟 agent 平台是怎么搭起来的讲明白了。**

---

## 2. 仓库里主要有什么

### 2.1 README.md
总索引。说明整个仓库的分析范围和目录结构。

### 2.2 analysis/
核心分析文档目录，价值最高。

主要包含：
- 架构总览
- 安全分析
- memory 机制
- skills 实现
- tool call 机制
- MCP 实现
- sandbox 实现
- context 管理
- prompt 管理
- multi-agent 实现
- session storage / transcript / resume
- 程序亮点与同类产品对比
- 隐藏功能与额外发现
- 最终总结

### 2.3 src/
用于分析引用的源码材料。

### 2.4 src.zip
源码压缩包。

---

## 3. 这个仓库最核心在讲什么

如果不看目录名，只看实质，它主要在回答这些问题：

1. Claude Code 到底是什么架构
2. 它怎么做长期上下文和记忆
3. 它怎么扩展能力（skills / tools / MCP）
4. 它怎么控风险（sandbox / permission）
5. 它怎么支持复杂协作（subagent / coordinator / swarm）
6. 它怎么做 prompt / context 工程

一句话：
**Claude Code 不是一个命令行聊天工具，而是一套本地 agent runtime。**

---

## 4. 最值得看的几篇

### 第一梯队（最适合学方法）
- `analysis/04c-skills-implementation.md`
- `analysis/04f-context-management.md`
- `analysis/04g-prompt-management.md`
- `analysis/04h-multi-agent.md`
- `analysis/09-final-summary.md`

### 第二梯队（适合理解系统深层能力）
- `analysis/04-agent-memory.md`
- `analysis/04b-tool-call-implementation.md`
- `analysis/04d-mcp-implementation.md`
- `analysis/04e-sandbox-implementation.md`
- `analysis/04i-session-storage-resume.md`

### 第三梯队（补全全貌用）
- 架构总览
- 组件拆解
- 同类产品对比
- 隐藏功能

---

## 5. 对我们最有用的启发

## 5.1 把 agent 当运行时系统，不当聊天壳子
Claude Code 最值得学的不是某个功能，而是：
- query / tool / permission 内核
- memory 系统
- skills / MCP 扩展
- 多 agent 协作
- session 持久化

迁移到电商运营方向：
我们后续做的，不应该只是“一个会回答问题的 AI”，而应该是：
- 巡检模块
- 客服草稿模块
- 商品检查模块
- 执行模块
- 规则库
- 日志审计
- 记忆与知识沉淀

即：
**做运营 runtime，而不是做散装助手。**

---

## 5.2 分层 prompt / context，不要把所有东西塞进一段大提示词
Claude Code 把：
- 默认 system prompt
- agent prompt
- append prompt
- user context
- system context
- task-specific prompts
分层管理。

迁移到我们这里：
后续电商 agent 也应该分层：
- 主身份层
- 当前任务上下文层
- 模块任务层（巡检/客服/商品/执行）
- 风控附加层

不要靠一个总提示词硬扛所有任务。

---

## 5.3 Skills 不是文档，而是能力注入机制
Claude Code 的 skills 值得学的是：
- 可发现
- 有元数据
- 可按场景触发
- 有工具边界
- 是能力封装单元

迁移到我们这里：
后续知识沉淀最好做成“模块能力”，而不只是普通笔记。
例如：
- 店铺巡检 skill
- 客服草稿 skill
- 商品检查 skill
- 后台确认执行 skill
- 1688 铺货链路 skill

每个 skill / 模块都应明确：
- 什么时候用
- 输入是什么
- 输出是什么
- 风险边界是什么
- 可调用哪些工具
- 失败如何处理

---

## 5.4 条件触发比全量塞上下文更聪明
Claude Code 的条件技能思想很值得学：
只在相关场景加载相关能力，避免认知过载。

迁移到我们这里：
- 做巡检时，不加载全部客服模板
- 做客服草稿时，不加载全部商品检查规则
- 做铺货链路时，不加载全部巡检规则
- 做高风险执行时，额外加载风控边界

即：
**模块化按需注入上下文。**

---

## 5.5 多 agent 的重点不是数量，而是角色与协作协议
Claude Code 的 multi-agent 不是简单“多开实例”，而是：
- subagent
- coordinator -> workers
- swarm teammates

关键点在：
- 有角色
- 有通信
- 有任务平面
- 有权限回流
- 有共享状态

迁移到我们这里：
未来可拆成：
- orchestrator（协调器）
- ops / inspection worker（巡检）
- cs worker（客服）
- listing worker（商品）
- execution worker（执行）

当前阶段不急着做复杂 swarm，但角色拆分思路可以先应用到文档和任务设计里。

---

## 5.6 权限与确认不是提醒语，而是流程的一部分
Claude Code 里权限不是外挂，而是运行时内核的一部分。

迁移到我们这里：
电商 agent 的动作必须天然分成：
- 只读
- 草稿准备
- 确认后执行
- 禁止自动

尤其以下动作必须写入流程边界：
- 改价
- 上下架
- 自动发送消息
- 自动公开回复
- 售后 / 退款处理

重点：
**不要把权限写在一句“谨慎操作”里，要写进流程里。**

---

## 5.7 长任务系统必须管理上下文与记忆
Claude Code 的 context 管理提醒我们：
不能每轮从零开始，也不能把全部历史一直塞进上下文。

迁移到我们这里：
后续至少要区分：
- 长期记忆：规则、模板、风控、SOP
- 会话态记忆：当前待办、今日异常、当前任务状态
- 临时上下文：当前页面、当前商品、当前消息

核心原则：
**压缩低价值历史，重注入关键状态。**

---

## 5.8 专项任务 prompt 比大一统 prompt 更稳定
Claude Code 对 compact / memory 等后台任务，都使用了强约束的专项 prompt。

迁移到我们这里：
电商任务也应拆成专项任务协议，例如：
- 巡检任务 prompt
- 客服草稿任务 prompt
- 商品检查任务 prompt
- 执行确认任务 prompt

每类任务：
- 目标单一
- 工具受限
- 输出格式固定
- 边界明确

---

## 6. 当前最值得直接应用到本库的点

### 6.1 继续模块化沉淀
把已有知识沉淀成：
- 规则文件
- 检查清单
- 可调用模块
- 实测链路记录

### 6.2 给每个模块明确输入 / 输出 / 工具 / 禁区
避免“会一点，但不稳定”。

### 6.3 按场景加载，不要每次全量带知识
保持上下文简洁。

### 6.4 采用协调器 + 工作者思路
哪怕暂时不真的起多 agent，也可以先按角色设计任务与文档结构。

### 6.5 把风控和审计放在一开始
包括：
- 权限边界
- 失败即停
- 数量限制
- 确认机制
- 日志字段

---

## 7. 当前不建议盲学的点

### 7.1 不要过早追复杂 swarm
现阶段先把角色拆清、任务边界拆清、流程拆清。

### 7.2 不要把 prompt 工程玩成复杂系统
当前优先级仍然是：
- 规则库
- 模板库
- 实测链路
- 风险边界

### 7.3 不要过早投入高级 context 优化工程
在真实工作链路没跑通前，复杂 compact / cache 优化优先级不高。

---

## 8. 一句话方法论

从这个仓库里对我们最有价值的结论是：

**把电商运营 agent 做成“模块化能力 + 分层上下文 + 明确权限 + 专项任务协议 + 可持续沉淀”的本地运行系统。**

不是：
- 单一 prompt
- 单一 agent
- 单次问答
- 一堆零散脚本

而是：
- 模块
- 规则
- 协调
- 确认
- 记忆
- 审计

---

## 9. 后续使用建议

后续引用本笔记时，优先把它当作：
- 系统设计参考
- 文档结构参考
- 模块化沉淀参考
- 风控与权限边界参考

不把它当作直接照抄模板。
