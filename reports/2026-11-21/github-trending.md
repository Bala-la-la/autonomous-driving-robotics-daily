# GitHub 开源趋势晨报｜2026-11-21

## 时间与证据口径

检索于北京时间 2026-11-21 06:00。排名与 `+N/日` 来自第三方镜像保存的 **2026-11-20 UTC GitHub Trending 日榜**（`collectedAt` 2026-11-20 21:07 UTC）；`gained` 是镜像读取的当日增星，并非本次抓取的 star 差值。当前 star、主语言、许可证、创建时间和自述经 GitHub Repository API 复核。镜像不是 GitHub 官方服务；走红原因和趋势判断均为编辑推断。排除攻击/漏洞利用导向和疑似异常项目。

| 项目 | 当前 stars | 日榜依据 | 语言／类别 |
| --- | ---: | ---: | --- |
| obra/superpowers | 322,788 | 第 2，+888/日 | Shell／Agent Skills 与工程方法 |
| HKUDS/CLI-Anything | 61,322 | 第 3，+774/日 | Python／Agent 原生 CLI |
| cursor/plugins | 17,814 | 第 5，+292/日 | TypeScript／IDE 插件规范 |
| firecrawl/firecrawl | 205,168 | 第 6，+1,226/日 | TypeScript／网页知识基础设施 |
| openvinotoolkit/openvino | 11,766 | 第 8，+219/日 | C++／边缘推理 |
| cathrynlavery/diagram-design | 69,236 | 第 9，+634/日 | HTML／可编辑设计 Skills |
| Tracer-Cloud/opensre | 13,564 | 第 13，+465/日 | Python／CI/CD 可靠性 Agent |
| toeverything/AFFiNE | 75,737 | 第 14，+686/日 | TypeScript／知识与生产力 |

## 精选项目

### 1. [obra/superpowers](https://github.com/obra/superpowers)

- **确认信息：** [Repository API](https://api.github.com/repos/obra/superpowers) 当前 **322,788 stars**，Shell、MIT，创建于 2025-10-09；日榜第 2、**+888/日**。自述定位为 Agentic skills framework 与软件开发方法。
- **用途：** 将编码 Agent 的计划、执行、验证等做成可复用技能与工作流。
- **走红原因（推断）／适合人群：** 团队正在寻求把一次性 prompt 变成可审查工程流程；适合使用 coding agent 的开发团队。采用前应固定 skill 版本、审查外部工具权限、明确人工审批点和许可证边界。

### 2. [HKUDS/CLI-Anything](https://github.com/HKUDS/CLI-Anything)

- **确认信息：** API 当前 **61,322 stars**，Python、Apache-2.0，创建于 2026-03-08；日榜第 3、**+774/日**。项目自述为让软件 Agent-native 的 CLI-Hub。
- **用途：** 为图形/传统软件补充可由 Agent 调用的命令行操作面。
- **走红原因（推断）／适合人群：** 可组合 CLI 能降低 Agent 操作桌面软件的脆弱性；适合自动化和工具链团队。需先在隔离环境验证命令副作用、参数校验、版本漂移、文件覆盖及权限最小化。

### 3. [cursor/plugins](https://github.com/cursor/plugins)

- **确认信息：** API 当前 **17,814 stars**，TypeScript，许可证字段为空，创建于 2026-01-23；日榜第 5、**+292/日**。自述为 Cursor plugin specification 与官方插件。
- **用途：** 为编辑器内 Agent 扩展定义和提供插件能力。
- **走红原因（推断）／适合人群：** Agent 扩展从单一提示词转向可发现、可安装的能力包；适合维护 IDE 工作流的团队。应审计插件来源、网络/文件权限、升级兼容性和许可证缺失带来的使用限制。

### 4. [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)

- **确认信息：** API 当前 **205,168 stars**，TypeScript、AGPL-3.0，创建于 2024-04-15；日榜第 6、**+1,226/日**。自述提供搜索、抓取和数百数据提供方的 Agent 知识基础设施。
- **用途：** 将网页检索、抓取和结构化内容输入 Agent/RAG 流程。
- **走红原因（推断）／适合人群：** 高质量、可溯源外部数据仍是 Agent 产品的瓶颈；适合需要网页知识管线的应用团队。生产前须评估 robots/版权、PII、抓取频率、数据保留、供应商出口和 AGPL 合规。

### 5. [openvinotoolkit/openvino](https://github.com/openvinotoolkit/openvino)

- **确认信息：** API 当前 **11,766 stars**，C++、Apache-2.0，创建于 2018-10-15；日榜第 8、**+219/日**。自述为 AI 推理优化和部署开源工具包。
- **用途：** 进行模型转换、优化与硬件侧推理部署。
- **走红原因（推断）／适合人群：** 本地/边缘 Agent 和机器人重视成本、隐私、时延；适合视觉、机器人及端侧平台团队。应实测目标硬件的精度回归、算子覆盖、冷启动、p95 延迟和驱动兼容性。

### 6. [cathrynlavery/diagram-design](https://github.com/cathrynlavery/diagram-design)

- **确认信息：** API 当前 **69,236 stars**，HTML、MIT，创建于 2026-04-16；日榜第 9、**+634/日**。自述为适用于多种 coding agent 的 **45** 种图表设计，产物是自包含 HTML+SVG。
- **用途：** 将架构、流程和汇报图做成可编辑、可发布的代码化工件。
- **走红原因（推断）／适合人群：** Agent 的价值越来越依赖可交付而非纯文本；适合产品、技术写作和方案团队。应人工复核图中事实、可访问性、品牌规范与 SVG/HTML 的嵌入安全。

### 7. [Tracer-Cloud/opensre](https://github.com/Tracer-Cloud/opensre)

- **确认信息：** API 当前 **13,564 stars**，Python、Apache-2.0，创建于 2026-01-13；日榜第 13、**+465/日**。项目自述为 CI/CD reliability 的开源 Agent。
- **用途：** 辅助诊断和处理持续集成、发布流水线的可靠性问题。
- **走红原因（推断）／适合人群：** Agent 正进入具有明确日志与回滚边界的运维场景；适合平台/SRE 团队。需从只读诊断起步，配置变更必须审批，并保留审计日志、密钥隔离和回滚演练。

### 8. [toeverything/AFFiNE](https://github.com/toeverything/AFFiNE)

- **确认信息：** API 当前 **75,737 stars**，TypeScript，许可证 API 标为 `NOASSERTION`，创建于 2022-07-31；日榜第 14、**+686/日**。自述为强调隐私、可定制的知识库，结合规划、整理与创作。
- **用途：** 承载个人/团队笔记、白板和知识工作流。
- **走红原因（推断）／适合人群：** Agent 输出需要进入人可编辑、可组织的长期工作空间；适合重视本地控制的知识工作团队。导入前审查许可、同步/备份、访问控制、数据导出与第三方 AI 连接范围。

## 技术趋势与社区偏好

本日日榜串起一条更完整的 Agent 交付链：Superpowers、Cursor plugins 和 CLI-Anything 提供可安装的能力与操作面，Firecrawl 提供外部知识，OpenVINO 将推理落到边缘，OpenSRE 管理交付可靠性，diagram-design 和 AFFiNE 承接人可审阅的产物与知识。社区偏好不再只是“更会生成”的模型包装，而是可执行、可验证、可编辑的运行面；但高日增星不能证明安全或生产成熟度，插件/CLI 权限、抓取数据权利、CI 写入审批、依赖固定和许可证应作为共同准入门。

## 证据链接

- [GitHub Trending 2026-11-20 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-20.json)：排名、快照总 star 与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：镜像采集和统计口径。
- 各项目当前元数据以上述 Repository API 为准；走红原因均为编辑推断。
