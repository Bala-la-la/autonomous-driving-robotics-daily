# GitHub 开源趋势晨报｜2026-11-17

## 时间与证据口径

检索于北京时间 2026-11-17 06:00。排名与 `+N/日` 来自第三方镜像保存的 **2026-11-16 UTC GitHub Trending 日榜**（`collectedAt` 为 2026-11-16 21:07 UTC），是镜像 `gained` 字段，并非本次总 star 相减。当前 star、主语言、许可证和自述经 GitHub Repository API 复核。镜像不是 GitHub 官方服务；走红原因与趋势均为编辑推断，star 不证明质量、安全或生产采用。为避免近期重复，排除 11 月 14—16 日已选项目。

## 精选项目

### 1. [backnotprop/plannotator](https://github.com/backnotprop/plannotator)

- **数据：** API 当前 **12,489 stars**；日榜第 2、**+689/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/backnotprop/plannotator)、[日榜快照](https://githubtrending.today/api/archive/2026-11-16.json)。
- **确认用途：** 面向人留在 agent loop 中的工作区，可塑形、决策、计划、标注、审代码、共享反馈并一键交给 agent。
- **走红原因（推断）：** coding agent 普及后，计划和 review 需要成为可见、可批注的工件，而不是隐藏在聊天记录中。
- **适合人群：** 需要人工审批的工程团队；上线前审计代码/反馈外发、身份边界、仓库权限和审计留存。

### 2. [alibaba/open-code-review](https://github.com/alibaba/open-code-review)

- **数据：** API 当前 **52,880 stars**；日榜第 11、**+946/日**；Go；Apache-2.0。证据：[Repository API](https://api.github.com/repos/alibaba/open-code-review)、[日榜快照](https://githubtrending.today/api/archive/2026-11-16.json)。
- **确认用途：** 混合确定性流水线与 LLM Agent 的代码审阅工具，内置多语言规则（如 NPE、线程安全、XSS、SQL 注入），兼容 OpenAI 与 Anthropic 接口。
- **走红原因（推断）：** 团队更需要把模型解释置于稳定规则和行级反馈之后，而非完全依赖一次性 Agent 判断。
- **适合人群：** 想为 CI 加入 AI 辅助 review 的平台团队；需先做误报/漏报、敏感代码外传、提示注入、模型保留与规则更新评测。

### 3. [google-research/paper-orchestra](https://github.com/google-research/paper-orchestra)

- **数据：** API 当前 **1,391 stars**；日榜第 12、**+306/日**；Python；Apache-2.0。证据：[Repository API](https://api.github.com/repos/google-research/paper-orchestra)、[日榜快照](https://githubtrending.today/api/archive/2026-11-16.json)。
- **确认用途：** 用多 agent 自动化 AI 研究论文写作的框架。
- **走红原因（推断）：** 社区正试验把检索、论证、写作与批评分拆为角色，但也因此更需要可追溯证据和作者责任界面。
- **适合人群：** 研究工作流原型团队；不得将生成文本当作可靠文献结论，应复核引用、实验、贡献归属和发表政策。

### 4. [ChromeDevTools/chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp)

- **数据：** API 当前 **57,633 stars**；日榜第 13、**+837/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/ChromeDevTools/chrome-devtools-mcp)、[日榜快照](https://githubtrending.today/api/archive/2026-11-16.json)。
- **确认用途：** 为 coding agent 提供 Chrome DevTools 接入。
- **走红原因（推断）：** agent 若能检查真实浏览器的 DOM、网络和运行时状态，前端修复可从猜测转向可观测证据。
- **适合人群：** Web 开发与测试团队；应隔离登录会话、限制可访问域名、清理网络日志中的 token，并保留工具调用审计。

### 5. [getarcaneapp/arcane](https://github.com/getarcaneapp/arcane)

- **数据：** API 当前 **8,650 stars**；日榜第 6、**+31/日**；Go；BSD-3-Clause。证据：[Repository API](https://api.github.com/repos/getarcaneapp/arcane)、[日榜快照](https://githubtrending.today/api/archive/2026-11-16.json)。
- **确认用途：** 自述为面向普通用户的现代 Docker 管理工具。
- **走红原因（推断）：** Agent/AI 服务落地仍依赖容器、卷、镜像和运行状态；更易用的运维界面能降低试验环境门槛。
- **适合人群：** 自托管开发者和小型平台团队；Docker socket 等同高权限，应检查认证、网络暴露、密钥、备份和升级回滚。

### 6. [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)

- **数据：** API 当前 **68,066 stars**；日榜第 9、**+122/日**；Python；MIT。证据：[Repository API](https://api.github.com/repos/mvanhorn/last30days-skill)、[日榜快照](https://githubtrending.today/api/archive/2026-11-16.json)。
- **确认用途：** agent Skill，可跨 Reddit、X、YouTube、HN、Polymarket 和 Web 检索后汇总带依据的摘要。
- **走红原因（推断）：** 时效型研究需求推动 agent 把多源检索流程封装为可安装资产，而不只是请求“一份总结”。
- **适合人群：** 做探索性情报与研究辅助的用户；须逐条复核原始来源、平台访问规则、时间窗、排名偏差、个人数据和事实引用。

## 技术趋势与社区偏好

11 月 16 日日榜的未重复样本呈现“人类决策—受控执行—可观测环境—交付研究”的链条：Plannotator 保留人类计划/批注，Open Code Review 用规则与 agent 混合审查，Chrome DevTools MCP 将浏览器状态引入执行反馈，Arcane 管理部署底座，PaperOrchestra 与 last30days-skill 将研究生产和时效检索资产化。社区偏好仍是让 agent 接入真实工作流；相应的权限最小化、证据可追溯、数据保留与许可证审计必须先于采纳。

## 证据链接

- [GitHub Trending 2026-11-16 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-16.json)：排名、快照总 star 与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：镜像采集和统计口径。
- 各项目当前元数据以上述 Repository API 为准；走红原因均为编辑推断。
