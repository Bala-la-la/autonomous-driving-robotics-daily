# GitHub 开源趋势晨报｜2026-09-18

说明：查询日期为 2026-09-18（Asia/Shanghai）。`stars today` 取 2026-09-18 GitHub Trending 日榜快照；当前 stars、创建日期、语言、许可证和描述由 GitHub Repository API 查询窗口核对。两类数字来自不同采集时点，不能相减推导增长率；走红原因属于编辑推断。攻击、账号自动化、来源不清和明显高风险项目不纳入精选。

## 精选项目

1. [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill)：JavaScript，2026-06-18 创建，API 当前 13,460 stars，MIT；Trending 快照 +3,606。面向 coding agent 的多阶段安全审计 skill，输出可机读、可独立验证的 findings。**推断走红原因**：社区开始要求 Agent 产出可复核的安全证据，而不只给一段自然语言建议；采用前仍应检查其覆盖范围、误报处理和权限边界。

2. [alibaba/open-code-review](https://github.com/alibaba/open-code-review)：Go，2026-05-18 创建，API 当前 36,580 stars，Apache-2.0；Trending 快照 +3,290。用确定性流水线分配审查单元，再由 LLM Agent 输出精确到行的评论，并内置 NPE、线程安全、XSS、SQL 注入等规则。**推断走红原因**：代码审查正在形成“规则负责边界、模型负责判断”的混合架构，适合进入 CI，但需要审计数据集、模型调用和规则覆盖。

3. [Tencent/BrowserSkill](https://github.com/Tencent/BrowserSkill)：TypeScript，2026-06-22 创建，API 当前 5,233 stars，MIT；Trending 快照 +1,350。通过 CLI 加浏览器扩展，让 Agent 复用已登录的真实浏览器，同时在独立窗口执行任务。**推断走红原因**：它直接解决登录态、真实前端和“不要打断用户”三者的冲突；高权限浏览器会话、跨站授权和操作回滚是采用前置条件。

4. [affaan-m/ECC](https://github.com/affaan-m/ECC)：JavaScript，2026-01-18 创建，API 当前 261,982 stars，MIT；Trending 快照 +1,171。面向 Claude Code、Codex、OpenCode、Cursor 等 Agent 的 harness 性能优化系统，覆盖 skills、instincts、memory、security 和 research-first workflow。**推断走红原因**：社区关注点从单次 prompt 转到可复用、可调试、可持续改进的运行时资产；范围较广，实际采用应逐项审查默认指令和外部工具权限。

5. [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)：JavaScript，2026-02-15 创建，API 当前 96,359 stars，MIT；Trending 快照 +680。面向 AI coding agent 的生产级工程 skills 集合。**推断走红原因**：技能正在成为可安装、可版本化的工程资产，成熟度判断不能只看 star，还要看测试、版本锁定、依赖和与不同 Agent 的兼容边界。

6. [Fission-AI/OpenSpec](https://github.com/Fission-AI/OpenSpec)：TypeScript，2025-08-05 创建，API 当前 69,303 stars，MIT；Trending 快照约 +298。为 AI coding assistant 提供 spec-driven development 工作流，把提案、需求、设计、任务和验证组织成可追踪工件。**推断走红原因**：随着 Agent 获得更大写权限，先形成可审查规格再执行的流程比单纯增加工具数量更有价值；需要关注遥测、生成物校验和团队流程摩擦。

7. [alphaXiv/OpenResearch](https://github.com/alphaXiv/OpenResearch)：Rust，2026-06-07 创建，API 当前 5,285 stars，MIT；Trending 快照 +940。把 coding agent 扩展为 research agent，面向检索、实验、分析和论证链组织长任务。**推断走红原因**：研究型 Agent 的竞争点从回答问题转向并行探索、可追踪中间产物和跨模型运行；使用时应核查引用真实性、实验复现和长任务成本。

8. [anthropics/claude-code](https://github.com/anthropics/claude-code)：TypeScript，2025-02-22 创建，API 当前 146,255 stars，许可证未由 API SPDX 字段标出；Trending 快照 +538。运行在终端中的 coding agent，能够理解代码库、执行日常任务并处理 Git 工作流。**推断走红原因**：终端 Agent 已成为其他 skills、harness、审查和规格项目的共同宿主；生产使用的核心问题仍是命令授权、敏感文件访问和可回滚性。

9. [TencentCloud/Octop](https://github.com/TencentCloud/Octop)：Python，2026-07-08 创建，API 当前 3,926 stars，MIT；Trending 快照 +367。可自托管、多用户、多 Agent 的 AI assistant。**推断走红原因**：Agent 正从单聊天窗口进入带记忆、工具、渠道和团队状态的控制平面，适合观察本地部署与多用户隔离如何落地；应先审查插件、MCP、浏览器和 Shell 权限。

10. [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins)：Python，2026-01-23 创建，API 当前 24,854 stars，Apache-2.0；Trending 快照 +287。面向知识工作者的开源插件集合，目标是把常见工作流程封装为可调用能力。**推断走红原因**：Agent 生态正在从通用工具转向领域工作流与角色化插件；组织采用前需要评估数据驻留、产品耦合、权限继承和插件更新策略。

## 数据边界与排除

- `stars today` 是 Trending 日榜在 2026-09-18 的页面快照；API 当前 stars 是另一采集时点的总量，不能当作同一天的增量。
- 本期保留 Agent harness、Skills、浏览器执行、代码审查、规格工作流、研究 Agent 和自托管控制面，排除逆向工程、账号自动化、攻击工具、用途不清和明显灌星风险项目。
- 项目描述、许可证字段和趋势解释分别来自仓库元数据、API 与编辑判断；进入生产前仍需审查代码、依赖、模型／数据来源、网络访问和默认权限。

## 趋势总结

本期 GitHub 信号集中在四层：安全与代码审查的可验证 Agent、可安装的 Skills／规格工作流、复用真实浏览器和终端的高权限执行，以及带记忆和多用户隔离的自托管控制面。社区关注点继续从“模型能否完成一次任务”转向“能力能否版本化、执行能否授权、结果能否复核、状态能否回滚”。
