# GitHub 开源趋势晨报｜2026-11-16

## 时间与证据口径

检索于北京时间 2026-11-16 06:00。排名与 `+N/日` 来自第三方镜像保存的 **2026-11-15 UTC GitHub Trending 日榜**（`collectedAt` 为 2026-11-15 21:07 UTC）；它是镜像的 `gained` 字段，并非本次总 star 相减。当前 star、主语言、许可证和仓库自述由 GitHub Repository API 本次复核。镜像不是 GitHub 官方服务；走红原因及趋势结论均为编辑推断，star 不证明质量、安全或生产采用。为避免重复，排除了 11 月 14—15 日已选项目。

## 精选项目

### 1. [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills)

- **数据：** API 当前 **9,244 stars**；日榜第 3、**+248/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/google-labs-code/stitch-skills)、[日榜快照](https://githubtrending.today/api/archive/2026-11-15.json)。
- **确认用途：** 为 Stitch MCP server 提供 Agent Skills 库，仓库自述称其遵循 Agent Skills 开放标准，并面向多种 coding agent 兼容。
- **走红原因（推断）：** Skill 逐渐从单次提示升级为可分发、可版本化的 UI／工作流能力包，降低跨 agent 复用的格式摩擦。
- **适合人群：** 研究或维护设计生成工作流的 agent 平台团队；安装前应检查 Skill 的网络／文件写入、第三方服务条款、版本锁定与产物版权。

### 2. [ggml-org/ggml](https://github.com/ggml-org/ggml)

- **数据：** API 当前 **15,883 stars**；日榜第 8、**+53/日**；C++；MIT。证据：[Repository API](https://api.github.com/repos/ggml-org/ggml)、[日榜快照](https://githubtrending.today/api/archive/2026-11-15.json)。
- **确认用途：** 机器学习 tensor library；是本地／跨硬件推理生态常见的底层计算组件。
- **走红原因（推断）：** 上层 Agent 需要在本地可控地运行模型，社区持续回流到张量、量化和硬件后端等基础设施，而不只关注聊天界面。
- **适合人群：** 评估边缘或本地推理栈的系统工程师；应以目标模型、后端、量化、吞吐、显存、数值一致性和安全更新策略实测。

### 3. [NVIDIA/SkillEvaluator](https://github.com/NVIDIA/SkillEvaluator)

- **数据：** API 当前 **1,598 stars**；日榜第 12、**+205/日**；Python；Apache-2.0。证据：[Repository API](https://api.github.com/repos/NVIDIA/SkillEvaluator)、[日榜快照](https://githubtrending.today/api/archive/2026-11-15.json)。
- **确认用途：** 多层 Agent Skill 评估框架，含质量门、语义重叠检测、合成评测集生成和测量 Skill 对 agent 行为影响的在线评估。
- **走红原因（推断）：** Skills 数量快速增长后，团队开始需要衡量重复、回归与真实行为增益，而不是只积累提示词目录。
- **适合人群：** 运营内部 Skill catalog 的研发／评测团队；应隔离被测工具权限，审计合成数据偏差与 evaluator 偏差，并设定失败 Skill 的下线条件。

### 4. [elementalsouls/Claude-BugHunter](https://github.com/elementalsouls/Claude-BugHunter)

- **数据：** API 当前 **6,323 stars**；日榜第 9、**+221/日**；Python；MIT。证据：[Repository API](https://api.github.com/repos/elementalsouls/Claude-BugHunter)、[日榜快照](https://githubtrending.today/api/archive/2026-11-15.json)。
- **确认用途：** 面向 bug hunting 与外部红队工作的 Claude Code Skill bundle，仓库自述含 82 项 Skills、15 个 slash command 及基于公开披露报告整理的漏洞模式。
- **走红原因（推断）：** 安全团队希望将披露案例转成可重复检查清单和受控 agent 工作流，而不是每次从零提示。
- **适合人群：** 已获授权的应用安全／代码审计人员；仅可在明确授权的资产和隔离环境运行，须审计命令、依赖、凭据、日志保留及漏洞报告流程。

### 5. [GoogleChrome/modern-web-guidance-src](https://github.com/GoogleChrome/modern-web-guidance-src)

- **数据：** API 当前 **7,031 stars**；日榜第 10、**+1,220/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/GoogleChrome/modern-web-guidance-src)、[日榜快照](https://githubtrending.today/api/archive/2026-11-15.json)。
- **确认用途：** 为 coding agent 保持 Web 最佳实践更新的指导源码。
- **走红原因（推断）：** 项目约束若能以源码管理的 guidance 交给 agent，比散落的团队经验更容易审查、更新和复用。
- **适合人群：** 维护 Web 规范或组件库的前端平台团队；应按自身浏览器支持、框架版本和可访问性要求评审，不能把通用 guidance 当作发布验收。

## 技术趋势与社区偏好

11 月 15 日日榜的未重复样本形成“能力资产—质量门—执行底座—安全规范”链：Stitch Skills 负责分发能力，SkillEvaluator 负责测量是否有用，ggml 代表本地执行底座，BugHunter 将安全模式封装成授权审计流程，modern-web-guidance 则把工程规则版本化。社区偏好不再是单纯增加 Agent 数量，而是让它们更可安装、可评估、可约束；采用前仍需分别审计写权限、供应链、数据留存、许可证与人工审批。

## 证据链接

- [GitHub Trending 2026-11-15 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-15.json)：排名、快照总 star 与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：镜像采集和统计口径。
- 各项目当前元数据以上述 Repository API 为准；走红原因均为编辑推断。
