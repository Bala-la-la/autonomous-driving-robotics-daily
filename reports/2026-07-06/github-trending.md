GitHub Star 飙升项目速览｜2026-07-06

说明：按 2026-07-06 早晨抓取 GitHub Trending 日榜/周榜与 GitHub API 当前仓库信息。下面每项里，“确认信息”来自 Trending 页的 stars today / stars this week 或 GitHub API 当前 star；“推断原因”是基于仓库定位、发布时间和社区话题做的判断。

1. DeusData / codebase-memory-mcp
链接：https://github.com/DeusData/codebase-memory-mcp
当前 star：26,674
类别/语言：MCP / 代码智能基础设施，C
它做什么：把代码库索引成持久化知识图谱，做高性能代码检索与上下文记忆。
确认信息：GitHub Trending 周榜显示本周 +9,517 stars；GitHub API 当前 star 为 26,674。
为什么最近飙升（推断）：Agent 编程从“能调用工具”快速转向“能长期记住代码库结构”，而这个项目主打毫秒级索引、低 token 消耗、静态单二进制，正好卡在团队把 MCP 真正接入日常研发的时间点。
适合谁关注：做 coding agent、IDE 辅助、代码搜索、知识图谱索引或私有仓库上下文管理的团队。

2. openai / codex-plugin-cc
链接：https://github.com/openai/codex-plugin-cc
当前 star：25,387
类别/语言：Agent 开发工具，JavaScript
它做什么：让 Claude Code 直接调用 Codex 做代码审查与任务委派。
确认信息：GitHub Trending 日榜显示今天 +1,519 stars、周榜显示本周 +1,974 stars；GitHub API 当前 star 为 25,387。
为什么最近飙升（推断）：跨代理协作从概念演示进入真实开发流，这个仓库把“不同 coding agent 互相分工”做成可落地插件，天然带来高讨论度。
适合谁关注：已经在团队内使用 Claude Code、Codex 或多代理编码工作流的开发者与平台工程团队。

3. alibaba / page-agent
链接：https://github.com/alibaba/page-agent
当前 star：23,793
类别/语言：GUI Agent / 浏览器自动化，TypeScript
它做什么：在网页内部直接用自然语言控制 GUI，偏 in-page agent。
确认信息：GitHub Trending 日榜显示今天 +801 stars、周榜显示本周 +2,484 stars；GitHub API 当前 star 为 23,793。
为什么最近飙升（推断）：相比传统 browser automation，这类“页面内原生代理”更容易做稳定的 UI 操作和可视化反馈，社区正把关注点从通用 agent 转向更可控的具体执行层。
适合谁关注：做网页自动化、RPA、浏览器 agent、前端测试基础设施或 AI 运营工具的人。

4. browser-use / video-use
链接：https://github.com/browser-use/video-use
当前 star：15,000
类别/语言：视频编辑 agent，Python
它做什么：让 coding agent 通过代码方式完成视频编辑。
确认信息：GitHub Trending 周榜显示本周 +4,174 stars；GitHub API 当前 star 为 15,000。
为什么最近飙升（推断）：Agent 的落地正从“写代码”外溢到多媒体生产，视频是最直观、最容易展示效果的生产力场景之一，因此社区传播速度很快。
适合谁关注：做内容自动化、创作者工具、AI 媒体处理、工作流编排的团队。

5. Robbyant / lingbot-map
链接：https://github.com/Robbyant/lingbot-map
当前 star：9,880
类别/语言：3D 场景重建 / 机器人感知，Python
它做什么：一个从流式数据重建场景的 feed-forward 3D foundation model。
确认信息：GitHub Trending 周榜显示本周 +2,065 stars；GitHub API 当前 star 为 9,880。
为什么最近飙升（推断）：机器人与具身圈正在重新关注“重建先于推理”，尤其是流式 3D 表征、地图基础模型和实时场景理解，这个仓库正踩在该趋势上。
适合谁关注：做机器人感知、3D 重建、SLAM、空间计算、数字孪生的研究和工程团队。

6. ogulcancelik / herdr
链接：https://github.com/ogulcancelik/herdr
当前 star：12,001
类别/语言：终端 agent 编排，Rust
它做什么：一个住在终端里的 agent multiplexer，用来并行/分流多个代理。
确认信息：GitHub Trending 日榜显示今天 +650 stars、周榜显示本周 +3,506 stars；GitHub API 当前 star 为 12,001。
为什么最近飙升（推断）：开发者已经不满足于单代理串行工作，开始系统化管理多个代理、多个上下文和多个终端会话；herdr 这种“调度层”因此获得关注。
适合谁关注：重度终端用户、AI coding power users、内部 agent 平台和 DevEx 工具开发者。

7. logto-io / logto
链接：https://github.com/logto-io/logto
当前 star：13,816
类别/语言：身份认证基础设施，TypeScript
它做什么：面向 SaaS 与 AI 应用的 OIDC / OAuth 2.1 身份认证与授权平台，支持多租户、SSO、RBAC。
确认信息：GitHub Trending 周榜显示本周 +1,488 stars；GitHub API 当前 star 为 13,816。
为什么最近飙升（推断）：AI 应用从 demo 进入企业化交付后，认证、组织隔离、SSO 和权限系统重新成为刚需，社区对“可自建、对 AI 友好”的 auth infra 兴趣明显上升。
适合谁关注：做 B2B SaaS、企业 AI 应用、平台工程、身份与权限治理的团队。

【简短总结】
1. 最近 GitHub 热门项目的主旋律，不是再追单点模型，而是给 agent 补基础设施：代码记忆、终端编排、网页执行、视频工作流和企业认证都在涨。
2. 社区偏好也在变化：一类是“离真实生产更近”的工具型项目，另一类是能直接嵌入既有开发流的 agent 组件；纯概念性项目热度相对更难持续。
3. 本期增长依据主要来自 GitHub Trending 日榜/周榜与 GitHub API 当前 star；其中“为什么会涨”属于推断，不等同于 GitHub 官方原因说明。

信息来源：
GitHub Trending 日榜：https://github.com/trending?since=daily
GitHub Trending 周榜：https://github.com/trending?since=weekly
GitHub API 仓库页：对应各仓库 https://api.github.com/repos/{owner}/{repo}
