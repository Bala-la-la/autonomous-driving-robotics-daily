# GitHub 开源趋势晨报｜2026-11-23

## 时间与证据口径

检索于北京时间 2026-11-23 06:00。GitHub Trending 的官方页面是动态页面，日榜 `+N` 采用 [githubtrending.today](https://githubtrending.today/methodology/) 保存的 **2026-11-16—22 UTC** 日榜归档；这些是各快照采集周期的增星，不能等同于本地两次轮询差值。当前总 star、语言、许可证、创建时间和仓库自述均以本次 GitHub Repository API 查询为准。为避免重复，排除了最近多期已选的 Superpowers、CLI-Anything、Cursor plugins、Firecrawl、OpenVINO、Stitch Skills、FFmpeg Skill 等，以及带明显红队/漏洞利用定位的高热条目。文中严格区分确认信息与编辑推断。

| 项目 | 当前 stars | 增量依据 | 语言／类别 |
| --- | ---: | --- | --- |
| dream-num/univer | 31,246 | 11-16 日榜第 3，+1,878/日 | TypeScript／AI Office SDK |
| NVIDIA/SkillEvaluator | 4,389 | 11-16 日榜第 10，+953/日 | Python／Agent Skill 评测与 CI |
| DeanChensj/jiangshan-map | 8,783 | 11-16 日榜第 7，+285/日 | JavaScript／交互式时序地图 |
| XiaoYouChR/Ghost-Downloader-3 | 15,066 | 11-22 日榜第 15，+690/日 | Python／下载与生产力工具 |
| punkpeye/awesome-mcp-servers | 98,393 | 11-18 日榜第 20，+52/日 | 清单／MCP 服务生态 |

## 精选项目

### 1. [dream-num/univer](https://github.com/dream-num/univer)

- **确认信息：** Repository API 显示当前 **31,246** stars、TypeScript、Apache-2.0，创建于 2022-09-29；项目定位为可嵌入编辑、计算、协作和文件处理的开源 Office SDK，并面向人类与 AI Agent。11 月 16 日 Trending 快照为第 **3**、**+1,878/日**。
- **用途：** 在产品中构建文档、表格、演示式协作与 Agent 可操作的办公对象层。
- **走红原因（推断）：** Agent 开始需要实际读写企业文档，开发者倾向选择可自托管、可二次集成的“办公运行时”，而非只调用闭源编辑器。
- **适合人群：** 构建 AI office、知识工作流、文档自动化或协作 SaaS 的全栈团队。

### 2. [NVIDIA/SkillEvaluator](https://github.com/NVIDIA/SkillEvaluator)

- **确认信息：** 当前 **4,389** stars、Python、Apache-2.0，创建于 2026-06-24。项目提供多层 Agent Skill／插件质量门：安全扫描、harness 兼容性、语义重叠检测、合成评测集与衡量 Skill 对 Agent 行为影响的在线评测，并提供可复用 CI 模板。11 月 16 日榜第 **10**、**+953/日**。
- **用途：** 将 Skill 发布前的结构、兼容性、安全与行为效果纳入 CI，而非只检查能否安装。
- **走红原因（推断）：** Skills 数量快速增长后，组织的痛点从“怎么写”转为“是否安全、是否重复、是否真的提升任务成功率”。
- **适合人群：** 维护内部 Agent 插件市场、开源 Skill 库或要求可审计交付的 AI 平台团队。

### 3. [DeanChensj/jiangshan-map](https://github.com/DeanChensj/jiangshan-map)

- **确认信息：** 当前 **8,783** stars、JavaScript、GPL-3.0，创建于 2026-07-23；自述为覆盖公元前 403 年至今、**18** 个朝代、**198** 个疆域快照的中国历史交互地图，包含古今地名谱系与诗歌路线。11 月 16 日榜第 **7**、**+285/日**。
- **用途：** 以时间轴和可交互空间界面呈现历史地理、地名演化与叙事路线。
- **走红原因（推断）：** 具象、可探索的本地化数据产品很适合展示 Web 地图、知识图谱与叙事可视化的结合，降低公众理解复杂时空数据的门槛。
- **适合人群：** 数字人文、教育可视化、GIS 前端以及需要时空叙事交互的产品团队。

### 4. [XiaoYouChR/Ghost-Downloader-3](https://github.com/XiaoYouChR/Ghost-Downloader-3)

- **确认信息：** 当前 **15,066** stars、Python、GPL-3.0，创建于 2023-08-16；仓库自述为通用下载器。11 月 22 日榜第 **15**、**+690/日**。
- **用途：** 为个人或桌面端工作流提供多来源下载任务管理能力。
- **走红原因（推断）：** 在媒体与资料生产链条中，“可靠拿到本地文件”的确定性体验仍是高频需求；该项目的日榜增量反映生产力工具仍能与 Agent 项目并列获得关注，不代表其对所有站点或来源均合规可用。
- **适合人群：** 需要管理合法可下载资料、课程/素材归档和离线工作流的个人用户；使用前应核对来源条款与版权。

### 5. [punkpeye/awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers)

- **确认信息：** 当前 **98,393** stars、MIT，创建于 2024-11-30；这是 MCP servers 的精选清单。11 月 18 日榜第 **20**、**+52/日**，增长窗口早于本期但仍在最近 7 天内。
- **用途：** 按类别发现 MCP 服务，并作为选型和生态盘点入口，而非生产依赖的安全背书。
- **走红原因（推断）：** MCP 服务供给持续扩张，开发者需要先有一份可搜索的生态地图，再决定连接哪些数据源与工具。
- **适合人群：** 做 Agent 工具选型、搭建内部服务目录、或研究 MCP 互操作性的开发者；应逐项审核维护状态、权限与数据流。

## 技术趋势与社区偏好

- **Agent 生态的重心转向“可治理的能力单元”：** SkillEvaluator 的质量门与 Awesome MCP Servers 的发现入口分别覆盖上线前评测和接入前选型，社区更关心能力是否可验证、可兼容、可审计。
- **生产力基础设施从聊天框走进原生对象：** Univer 代表 Agent 直接操作文档、表格和协作对象的需求；下载器的高增长则提醒本地文件获取与归档仍是端到端工作流的一环。
- **有明确数据模型的体验产品依旧受欢迎：** Jiangshan Map 的热度说明，时空数据、知识谱系和交互叙事在 AI/Agent 热潮之外仍具强吸引力。上述“走红原因”均为编辑推断，确认信息以各归档快照和 Repository API 为准。

## 证据链接

- [GitHub Trending 2026-11-16 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-16.json)：Univer、SkillEvaluator、Jiangshan Map 的排名与 `gained`。
- [GitHub Trending 2026-11-18 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-18.json)：Awesome MCP Servers 的排名与 `gained`。
- [GitHub Trending 2026-11-22 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-22.json)：Ghost Downloader 的排名与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：第三方镜像的采集与统计口径。
