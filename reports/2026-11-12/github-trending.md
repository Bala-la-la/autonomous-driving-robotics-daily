# GitHub 开源趋势晨报｜2026-11-12

## 时间与证据口径

检索于北京时间 2026-11-12 06:00。Trending 增量取自第三方镜像保存的 **2026-11-11 UTC 日榜**（采集 2026-11-11 21:07 UTC）；`+N/日` 是镜像记录的 GitHub Trending `gained`，不是本次总 star 的相减值。当前 star、语言、许可证和用途以本次 GitHub Repository API 复核为准；镜像不是 GitHub 官方服务。项目“走红原因”及趋势结论均为编辑推断，star 不证明质量、安全或生产采用。

## 精选项目

### 1. [meta/astryx](https://github.com/meta/astryx)

- **数据：** API 当前 **24,810 stars**；11 月 11 日日榜第 1、**+2,842/日**；TypeScript；MIT。证据：[Repository API](https://api.github.com/repos/meta/astryx)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 可高度定制、面向 Agent 的开源 design system。
- **走红原因（推断）：** 团队希望 Agent 产出的 UI 能落回 design token 与组件约束，热度反映“可编辑工件”而非只生成页面的需求延续。
- **适合人群：** 维护前端设计系统的团队；应先检查无障碍、主题、版本迁移与生成输出的审阅流程。

### 2. [GoogleChrome/modern-web-guidance-src](https://github.com/GoogleChrome/modern-web-guidance-src)

- **数据：** API 当前 **1,682 stars**；日榜第 3、**+133/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/GoogleChrome/modern-web-guidance-src)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 仓库自述为空；从仓库名和组织可确认其为 Chrome 团队发布的现代 Web guidance 源码，具体 Agent 集成范围须以 README/版本文档为准。
- **走红原因（推断）：** 面向 Agent 的 Web 开发需要可靠、可版本控制的技术指导来源，官方组织发布降低了资料来源的不确定性。
- **适合人群：** 构建 Web 工程规范或辅助编码上下文的团队；勿把组织归属当作完整兼容性/安全保证，须逐版本核验内容和许可。

### 3. [shadcn/improve](https://github.com/shadcn/improve)

- **数据：** API 当前 **10,784 stars**；日榜第 4、**+333/日**；主要语言未标注；MIT。证据：[Repository API](https://api.github.com/repos/shadcn/improve)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 以能力较强模型审计代码库、产出计划，再让低成本模型执行该计划。
- **走红原因（推断）：** 将昂贵推理聚焦在规划/审阅、将实施分发给更廉价执行模型，直击 coding agent 的成本与稳定性问题。
- **适合人群：** 有成熟 CI 与代码审阅机制的软件团队；计划必须经过人类/自动测试验证，不能让下游模型获得未审阅的写权限。

### 4. [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)

- **数据：** API 当前 **115,870 stars**；日榜第 5、**+788/日**；JavaScript；MIT。证据：[Repository API](https://api.github.com/repos/addyosmani/agent-skills)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 面向 AI coding agent 的 production-grade engineering skills。
- **走红原因（推断）：** 连续多日上榜说明工程团队在把审阅、设计和交付约束沉淀为版本化资产；这是兴趣信号，不是采用率统计。
- **适合人群：** 使用 coding agent 的应用/平台工程师；把每个 Skill 视作可执行依赖，审阅脚本、网络访问、数据输入、许可并在沙箱测试。

### 5. [vercel-labs/agent-browser](https://github.com/vercel-labs/agent-browser)

- **数据：** API 当前 **49,806 stars**；日榜第 6、**+712/日**；Rust；Apache-2.0。证据：[Repository API](https://api.github.com/repos/vercel-labs/agent-browser)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 面向 AI Agent 的浏览器自动化 CLI。
- **走红原因（推断）：** 结合 Skills/计划型工具的同榜表现，浏览器仍是 Agent 获取信息和落地内部流程的通用执行面。
- **适合人群：** 受控网页测试和内部自动化团队；隔离会话与凭据、设置域名 allowlist，并对支付、发布、删除等写操作设置明确确认。

### 6. [homeassistant-ai/ha-mcp](https://github.com/homeassistant-ai/ha-mcp)

- **数据：** API 当前 **7,284 stars**；日榜第 8、**+640/日**；Python；MIT。证据：[Repository API](https://api.github.com/repos/homeassistant-ai/ha-mcp)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 让 Claude、ChatGPT 等助手配置和自动化 Home Assistant。
- **走红原因（推断）：** MCP 将 Agent 接到真实设备控制面，增长显示对可执行连接器的兴趣延续，并不证明默认配置安全。
- **适合人群：** 已部署 Home Assistant 的自动化开发者；从只读/低风险实体开始，最小化 token 权限，并把门锁、警报、能源类动作置于独立审批。

### 7. [openai/codex-security](https://github.com/openai/codex-security)

- **数据：** API 当前 **11,655 stars**；日榜第 9、**+20/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/openai/codex-security)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 用于发现、验证和修复安全漏洞的 Codex Security CLI 与 TypeScript SDK。
- **走红原因（推断）：** 在 Agent 能写代码、操作浏览器和设备的同一榜单中，安全验证工具显示社区开始要求执行链附带审计与修复闭环。
- **适合人群：** 希望把安全检查纳入开发流程的工程/安全团队；先用只读扫描与隔离测试仓库验证误报、范围、数据外传和自动修复审批。

## 技术趋势与社区偏好

本期热点形成“规范—计划—执行—审计”的链条：Modern Web Guidance/Skills 提供可版本化知识，Astryx 提供可编辑 UI 约束，Improve 划分高价规划与低价实施，agent-browser/ha-mcp 打开网页与实体执行面，Codex Security 补上验证。社区偏好显然不止模型能力，而是可复用工作流和可交付产物；相应地，任何安装内容都应先审计供应链、写权限、凭据、数据留存和许可证。

## 证据链接

- [GitHub Trending 2026-11-11 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-11.json)：排名、快照总 star 与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：镜像采集和统计口径。
- 各项目当前元数据以上述 Repository API 为准；走红原因均为编辑推断。
