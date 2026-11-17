# GitHub 开源趋势晨报｜2026-11-18

## 时间与证据口径

检索于北京时间 2026-11-18 06:00。排名与 `+N/日` 来自第三方镜像保存的 **2026-11-17 UTC GitHub Trending 日榜**（`collectedAt` 2026-11-17 21:07 UTC）；`gained` 是镜像从 GitHub Trending 读取的当日增星，不是本次查询的 star 差值。当前 star、主语言、许可证、创建时间和仓库自述经 GitHub Repository API 复核。镜像非 GitHub 官方服务；走红原因和趋势均为编辑推断。为避免与 11 月 14—17 日报告重复，本期排除了已选项目及安全攻击导向项目。

| 项目 | 当前 stars | 日榜依据 | 语言／类别 |
| --- | ---: | ---: | --- |
| Tencent/LoopForge | 3,065 | 第 4，+590/日 | Go／Agent 交付编排 |
| cursor/plugins | 16,864 | 第 8，+196/日 | TypeScript／插件生态 |
| obra/superpowers | 319,255 | 第 9，+598/日 | Shell／Agent 工程方法 |
| ag-ui-protocol/ag-ui | 19,951 | 第 10，+1,444/日 | TypeScript／Agent 前端协议 |
| affaan-m/ECC | 305,414 | 第 13，+902/日 | JavaScript／Agent harness |

## 精选项目

### 1. [Tencent/LoopForge](https://github.com/Tencent/LoopForge)

- **确认信息：** [Repository API](https://api.github.com/repos/Tencent/LoopForge) 当前 **3,065 stars**，Go，许可证 API 为 `NOASSERTION`，创建于 2026-07-28；[日榜](https://githubtrending.today/api/archive/2026-11-17.json) 第 4、**+590/日**。仓库自述为自托管 coding-agent 交付工作流，可编排 CodeBuddy、Codex 与 Claude Code，并带脚本和人工审批门。
- **用途：** 把编码 agent、脚本与人工审批组织成可自托管的交付流程。
- **走红原因（推断）／适合人群：** 从单次聊天走到团队交付后，任务编排、审批和可见状态比另一个模型入口更紧缺；适合已有 CI/变更流程的工程平台团队。采用前应验证审批是否不可绕过、凭据隔离、任务重试幂等、审计日志与未声明许可证的复用边界。

### 2. [cursor/plugins](https://github.com/cursor/plugins)

- **确认信息：** [Repository API](https://api.github.com/repos/cursor/plugins) 当前 **16,864 stars**，TypeScript，许可证 API 为 `NOASSERTION`，创建于 2026-01-23；日榜第 8、**+196/日**。仓库定位为 Cursor 插件规范与官方插件。
- **用途：** 为 IDE 内 agent/工具扩展提供规范和官方实现入口。
- **走红原因（推断）／适合人群：** 工具调用逐步迁入日常编辑器，插件接口与升级兼容性成为生态分发层；适合编辑器平台、内部开发者体验团队。需要逐插件审计网络/文件权限、遥测、供应链固定、版本兼容和没有 SPDX 标识的许可风险。

### 3. [obra/superpowers](https://github.com/obra/superpowers)

- **确认信息：** [Repository API](https://api.github.com/repos/obra/superpowers) 当前 **319,255 stars**，Shell，MIT，创建于 2025-10-09；日榜第 9、**+598/日**。项目自述为 agentic Skills 框架与软件开发方法论。
- **用途：** 将软件工程中的计划、实现、测试等过程封装为可调用的 Skills／工作法。
- **走红原因（推断）／适合人群：** 大量 Agent 项目正在从 prompt 试验转向可复用的流程资产和团队约定；适合希望统一工程操作方式的开发团队。应把每个 Skill 当作可执行依赖审查：输入来源、命令副作用、测试门、版本锁定与组织规范的冲突均需检查。

### 4. [ag-ui-protocol/ag-ui](https://github.com/ag-ui-protocol/ag-ui)

- **确认信息：** [Repository API](https://api.github.com/repos/ag-ui-protocol/ag-ui) 当前 **19,951 stars**，TypeScript，MIT，创建于 2025-05-07；日榜第 10、**+1,444/日**。仓库描述为将 Agent 接入前端应用的 Agent-User Interaction Protocol。
- **用途：** 为前端呈现 agent 状态、交互与事件流提供协议层。
- **走红原因（推断）／适合人群：** Agent 产品需要把执行过程、人工输入和结果以可控 UI 暴露出来，协议层可降低应用间集成摩擦；适合构建 agent 产品前端的平台/全栈团队。需特别审查事件中的隐私数据、会话绑定、用户确认语义、重放攻击和后端授权是否与 UI 状态一致。

### 5. [affaan-m/ECC](https://github.com/affaan-m/ECC)

- **确认信息：** [Repository API](https://api.github.com/repos/affaan-m/ECC) 当前 **305,414 stars**，JavaScript，MIT，创建于 2026-01-18；日榜第 13、**+902/日**。仓库自述为面向 Claude Code、Codex、OpenCode、Cursor 等的 Agent harness 性能优化系统，覆盖 Skills、instincts、memory、security 和 research-first development。
- **用途：** 汇集多种 coding-agent 的上下文、记忆、流程与性能优化资产。
- **走红原因（推断）／适合人群：** 高热度说明开发者正在寻找横跨不同 agent 的运行方法和持续改进框架；适合已有多 Agent 试验、需要比较与统一操作层的高级用户。范围很宽，不能将 star 数视为集成安全证明；应逐文件审阅默认指令、外部检索、记忆留存、写入权限和组织许可要求。

## 技术趋势与社区偏好

这份日榜的新增样本连接成“**工作流编排—扩展分发—工程方法—交互协议—跨 agent 运行时**”：LoopForge 管交付与审批，Cursor plugins 与 Superpowers 管能力资产化，AG-UI 管用户可见的执行面，ECC 管多 harness 的持续调优。社区偏好正由“让 agent 能执行”延伸到“如何接入团队、让用户看见并约束执行”。热度仍不能证明安全、质量或生产适用性；审批不可绕过、最小权限、事件/日志数据治理、供应链和许可证审计是共同前置条件。

## 证据链接

- [GitHub Trending 2026-11-17 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-17.json)：排名、快照总 star 与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：镜像采集和统计口径。
- 各项目当前元数据以上述 Repository API 为准；走红原因均为编辑推断。
