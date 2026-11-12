# GitHub 开源趋势晨报｜2026-11-13

## 时间与证据口径

检索于北京时间 2026-11-13 06:00。`+N/日` 和排名来自第三方镜像保存的 **2026-11-12 UTC 日榜**（采集于 2026-11-12 21:07 UTC），是其记录的 GitHub Trending `gained`，并非本次总 star 的相减值；当前 star、主语言、许可证和项目自述以 GitHub Repository API 于 2026-11-12 22:03 UTC 前后的复核为准。镜像非 GitHub 官方服务。用途为仓库自述可确认信息；走红原因和趋势结论均为编辑推断，star 不证明质量、安全或生产采用。

## 精选项目

### 1. [GoogleChrome/modern-web-guidance-src](https://github.com/GoogleChrome/modern-web-guidance-src)

- **数据：** API 当前 **2,767 stars**；日榜第 1、**+799/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/GoogleChrome/modern-web-guidance-src)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** 仓库自述为“让 coding agent 保持最新 Web 最佳实践”的指导源码。
- **走红原因（推断）：** Agent 写前端时，团队更愿意把规范作为可版本化上下文，而不是依赖一次性提示词。
- **适合人群：** 维护前端工程规范或 Agent 上下文的团队；须按版本审阅内容、兼容性和许可，不能把组织归属当作质量保证。

### 2. [openai/codex-security](https://github.com/openai/codex-security)

- **数据：** API 当前 **12,349 stars**；日榜第 2、**+663/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/openai/codex-security)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** 用于发现、验证和修复安全漏洞的 Codex Security CLI 与 TypeScript SDK。
- **走红原因（推断）：** 当 Agent 能产生和修改代码时，扫描、验证、修复的闭环成为把自动化接入工程流程的必要配套。
- **适合人群：** 工程和安全团队；先在隔离仓库以只读扫描验证误报、数据边界和自动修复审批。

### 3. [QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)

- **数据：** API 当前 **29,754 stars**；日榜第 6、**+151/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/QwenLM/qwen-code)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** 项目自述为运行在终端中的开源 AI coding agent。
- **走红原因（推断）：** 终端仍是最贴近仓库、测试和版本控制的 Agent 入口；开源可部署性对希望保留模型/凭据选择权的开发者有吸引力。
- **适合人群：** 已有测试、审阅和最小权限沙箱的开发者；不要把工作区写权限、shell 命令或密钥暴露给未审阅任务。

### 4. [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)

- **数据：** API 当前 **116,617 stars**；日榜第 9、**+812/日**；JavaScript；MIT。证据：[Repository API](https://api.github.com/repos/addyosmani/agent-skills)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** 面向 AI coding agent 的 production-grade engineering skills 集合。
- **走红原因（推断）：** 热度延续表明团队在把设计、审阅与交付约束沉淀成版本化技能资产，而非仅扩展模型提示。
- **适合人群：** 想标准化 Agent 工作流的平台与应用工程师；每个 Skill 都应视作依赖，逐项审阅脚本、网络访问、数据输入和许可证。

### 5. [meta/astryx](https://github.com/meta/astryx)

- **数据：** API 当前 **26,413 stars**；日榜第 10、**+1,789/日**；TypeScript；MIT。证据：[Repository API](https://api.github.com/repos/meta/astryx)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** 可高度定制、面向 Agent 的开源 design system。
- **走红原因（推断）：** UI Agent 的关注点正从“生成一个页面”转向可编辑、受 design token 约束并能回到团队组件体系的工件。
- **适合人群：** 已有设计系统的前端团队；先验证无障碍、主题、组件版本迁移和生成代码的审阅流程。

### 6. [CopilotKit/OpenBot](https://github.com/CopilotKit/OpenBot)

- **数据：** API 当前 **11,522 stars**；日榜第 11、**+291/日**；TypeScript；MIT。证据：[Repository API](https://api.github.com/repos/CopilotKit/OpenBot)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** 提供带浏览器、文件和工具的开源 AI coworkers；自述称每项行动会在执行前决定、执行后记录，并可接入 AG-UI agent。
- **走红原因（推断）：** “可执行 Agent”开始把行动前计划与行动后记录作为产品面的一部分，回应可观察性和责任追踪诉求。
- **适合人群：** 构建内部任务自动化的团队；应隔离会话与凭据、设置工具 allowlist，并对发布、支付、删除等不可逆动作加确认。

### 7. [ggml-org/llama.cpp](https://github.com/ggml-org/llama.cpp)

- **数据：** API 当前 **134,501 stars**；日榜第 13、**+287/日**；C++；MIT。证据：[Repository API](https://api.github.com/repos/ggml-org/llama.cpp)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** C/C++ 实现的大模型推理项目。
- **走红原因（推断）：** 与 Agent 应用层的增长并列出现，说明本地/可控推理仍是成本、隐私和离线部署的底层需求。
- **适合人群：** 需要自托管或边缘推理的开发者；按目标硬件、量化质量、吞吐/延迟和模型许可证做基准，避免仅以 star 选择运行时。

## 技术趋势与社区偏好

本期热点从上到下形成一条可部署 Agent 链：Modern Web Guidance 与 Skills 提供版本化约束，Qwen Code 和 OpenBot 提供终端/工具执行，Astryx 固化可编辑 UI 工件，Codex Security 补上验证，llama.cpp 保留本地推理选择。社区偏好已不只是“会调用模型”，而是规范、执行权限、可观测记录和可控运行时的组合；安装或接入前仍应优先审计供应链、写权限、凭据、数据留存和许可证。

## 证据链接

- [GitHub Trending 2026-11-12 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-12.json)：排名、快照总 star 与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：镜像采集和统计口径。
- 各项目当前元数据以上述 Repository API 为准；走红原因均为编辑推断。
