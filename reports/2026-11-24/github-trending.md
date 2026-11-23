# GitHub 开源趋势晨报｜2026-11-24

## 时间与证据口径

检索于北京时间 2026-11-24 06:00。日榜排名与 `+N/日` 来自 [githubtrending.today](https://githubtrending.today/api/archive/2026-11-23.json) 保存的 **2026-11-23 UTC** 日榜（`collectedAt` 2026-11-23 21:07 UTC）；这是采集窗口内的增星，并非本地轮询差值。当前 stars、forks、语言、许可证、创建／更新时间与项目描述来自本次 [GitHub Repository API](https://docs.github.com/rest/repos/repos#get-a-repository) 复核。排除了过去数期已选和明显面向漏洞利用/红队操作的高热项目；“走红原因”为编辑推断。

| 项目 | 当前 stars | 榜单增量依据 | 语言／类别 |
| --- | ---: | --- | --- |
| HKUDS/CLI-Anything | 63,532 | 日榜第 3，+783/日 | Python／软件 CLI 化与 Agent 执行 |
| firecrawl/firecrawl | 207,822 | 日榜第 6，+920/日 | TypeScript／网页数据与 Agent 检索基础设施 |
| openvinotoolkit/openvino | 12,268 | 日榜第 8，+183/日 | C++／边缘 AI 推理 |
| cathrynlavery/diagram-design | 70,899 | 日榜第 9，+624/日 | HTML／设计工件 Skill |
| Tracer-Cloud/opensre | 14,784 | 日榜第 13，+438/日 | Python／CI/CD SRE Agent |
| toeverything/AFFiNE | 77,336 | 日榜第 14，+593/日 | TypeScript／本地优先知识工作 |

## 精选项目

### 1. [HKUDS/CLI-Anything](https://github.com/HKUDS/CLI-Anything)

- **确认信息：** Repository API：**63,532** stars、5,772 forks，Python、Apache-2.0，创建于 2026-03-08；11 月 23 日日榜第 **3**、**+783/日**。项目目标是将图形软件转为 Agent 可调用的 CLI，并链接 CLI-Hub。
- **用途：** 为 Agent 把原本依赖 GUI 的软件能力暴露为脚本化、可编排命令接口。
- **走红原因（推断）／适合人群：** Agent 从代码生成扩展到操控现有软件时，CLI 是最易记录、测试和串联的执行面；适合构建本地工作流、桌面自动化与可复现设计/媒体流水线的开发者。
- **采用提醒：** GUI 软件的副作用仍需文件隔离、dry-run、命令 allowlist 和产物校验；“能调用”不代表默认安全或幂等。

### 2. [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)

- **确认信息：** Repository API：**207,822** stars、10,861 forks，TypeScript、AGPL-3.0，创建于 2024-04-15；日榜第 **6**、**+920/日**。仓库自述为 Agent 数据基础设施，提供搜索、抓取及 550+ 数据提供方的统一 API。
- **用途：** 为 RAG、研究 Agent 和数据采集工作流提供网页获取、清洗与访问层。
- **走红原因（推断）／适合人群：** 真实业务 Agent 的瓶颈常是新鲜、可引用的外部数据，而不是再换一个模型；适合需要网页检索/抽取管线的产品与数据平台团队。
- **采用提醒：** AGPL-3.0 对服务化集成有合规影响；同时需处理站点 robots/条款、速率限制、个人数据、提示注入与抓取结果溯源。

### 3. [openvinotoolkit/openvino](https://github.com/openvinotoolkit/openvino)

- **确认信息：** Repository API：**12,268** stars、3,678 forks，C++、Apache-2.0，创建于 2018-10-15；日榜第 **8**、**+183/日**。OpenVINO 是优化并部署 AI 推理的开源工具包。
- **用途：** 在 Intel CPU、GPU、NPU 等硬件上做模型转换、图优化和部署，服务视觉、语音与边缘 Agent。
- **走红原因（推断）／适合人群：** 随着多模态与本地 Agent 落地，成本、隐私和尾延迟促使团队重新关注推理部署底座；适合边缘 AI、机器人和平台工程团队。
- **采用提醒：** 性能需按目标芯片、模型版本和真实 batch/上下文长度实测，不能由单一吞吐 benchmark 外推；也应准备驱动和算子回退路径。

### 4. [cathrynlavery/diagram-design](https://github.com/cathrynlavery/diagram-design)

- **确认信息：** Repository API：**70,899** stars、4,745 forks，HTML、MIT，创建于 2026-04-16；日榜第 **9**、**+624/日**。自述提供面向 Claude Code、Codex、Copilot、Cursor 等的编辑式图表设计，覆盖 **52** 种图表类型，输出自包含 HTML + SVG。
- **用途：** 让编码 Agent 产出可继续编辑、可嵌入文档或网站的架构图、流程图和叙事图形。
- **走红原因（推断）／适合人群：** 社区正在偏好“可交付工件”而非一段提示词：结构化 SVG/HTML 更便于版本控制、审阅和品牌化；适合产品、解决方案和技术写作团队。
- **采用提醒：** 生成图应经过事实、可访问性（文字替代、色彩对比）与品牌规范审阅；不要把视觉整洁误认为架构正确。

### 5. [Tracer-Cloud/opensre](https://github.com/Tracer-Cloud/opensre)

- **确认信息：** Repository API：**14,784** stars、1,987 forks，Python、Apache-2.0，创建于 2026-01-13；日榜第 **13**、**+438/日**。仓库定位为开源 CI/CD 可靠性 Agent。
- **用途：** 辅助排查构建、测试和部署流程故障，并把运维诊断接入交付流水线。
- **走红原因（推断）／适合人群：** 代码生成提速后，CI 失败、发布回滚与环境差异成为团队新瓶颈；能读取日志并参与排障的 Agent 贴近实际交付价值。
- **采用提醒：** CI/CD 是高权限执行面：应强制只读诊断优先、生产变更审批、短期凭据、命令审计和网络/密钥隔离，不能把自动建议直接升级为自动发布。

### 6. [toeverything/AFFiNE](https://github.com/toeverything/AFFiNE)

- **确认信息：** Repository API：**77,336** stars、5,662 forks，TypeScript，许可证字段为 `NOASSERTION`，创建于 2022-07-31；日榜第 **14**、**+593/日**。项目自述是隐私优先、可定制的开源知识库，融合规划、整理与创作。
- **用途：** 提供本地优先的文档、白板与知识组织环境，可作为个人或团队知识工作基座。
- **走红原因（推断）／适合人群：** 生成式工作流促使用户希望把资料、画布与计划放在可导出、可控的空间中；适合重视本地数据控制与可定制知识管理的个人/团队。
- **采用提醒：** API 的 `NOASSERTION` 不可当作已确认开源许可，部署/二次分发前需核对仓库实际许可文本、同步/备份设置和团队数据 ACL。

## 技术趋势与社区偏好

- **Agent 栈由“会调用”走向受约束执行：** CLI-Anything、OpenSRE 与 Firecrawl 分别占据软件操作、发布可靠性和外部数据入口；社区兴趣已经覆盖完整执行链，但高权限命令、网页不可信内容和生产变更必须有最小权限与可回放证据。
- **可编辑工件和本地部署同时升温：** diagram-design 将图形变为版本化 HTML/SVG，AFFiNE 提供可控知识空间，OpenVINO 指向端侧推理。热度反映对可交付、可迁移、可控制资产的偏好，不能替代许可证、硬件兼容性和数据治理核验。

## 证据链接

- [GitHub Trending 2026-11-23 日榜归档](https://githubtrending.today/api/archive/2026-11-23.json)：排名、快照总 star 与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：第三方快照口径。
- 各项目的当前 metadata 以上述项目链接对应的 GitHub Repository API 为准；走红原因和趋势为编辑推断。
