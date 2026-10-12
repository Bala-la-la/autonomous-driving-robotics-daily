# GitHub 开源趋势晨报｜2026-10-13

## 时间与证据口径

北京时间 2026-10-13，GitHub Trending 页面请求超时，故本期**不声称官方 `stars today` 或 24 小时增量**。改以 [GitHub Search API](https://api.github.com/search/repositories?q=created%3A%3E%3D2026-10-06&sort=stars&order=desc) 和逐仓库 [Repository API](https://docs.github.com/rest/repos/repos#get-a-repository) 核对 2026-10-06 至 10-08 创建项目；“增量”均为**创建至本次查询的当前 stars**，不是日增量。星数、创建时间、语言、许可证和描述为确认信息；走红原因与适合人群为编辑推断。

| 项目 | 当前 stars | 增量依据 | 语言／类别 |
| --- | ---: | --- | --- |
| openai/math | 14,403 | 创建至查询 | Lean／形式化数学 |
| storytold/wordcraft | 8,944 | 创建至查询 | Rust／本地文档编辑 |
| storytold/cadcraft | 3,407 | 创建至查询 | Rust／CAD 工具 |
| zhongerxin/iPhone-use | 3,347 | 创建至查询 | Python／设备自动化 |
| noahdunnagan/fsearch | 1,961 | 创建至查询 | Rust／本地搜索 |
| HelixDB/helix-foundry | 1,331 | 创建至查询 | TypeScript／数据工作台 |
| pingdotgg/ts-rust | 1,120 | 创建至查询 | Rust／开发基础设施 |
| bherbruck/solidcraft | 1,048 | 创建至查询 | Rust／参数化 CAD／MCP |

### 1. openai/math

- **确认信息**：[仓库](https://github.com/openai/math)／[API](https://api.github.com/repos/openai/math)：2026-10-06 创建，14,403 stars，Lean、Apache-2.0。
- **用途**：提供可复现、机器检查的形式化数学工作基础。
- **走红原因（推断）／适合人群**：随着模型推理进入高价值技术流程，社区会偏好可验证的证明工件；适合研究者、形式化方法与 AI 评测开发者。应先确认数据来源、证明审查流程与自身 Lean 工具链兼容性。

### 2. storytold/wordcraft

- **确认信息**：[仓库](https://github.com/storytold/wordcraft)／[API](https://api.github.com/repos/storytold/wordcraft)：2026-10-07 创建，8,944 stars，Rust、Apache-2.0；自述为纯 Rust 的 Microsoft Word clean-room 重实现。
- **用途**：在本地生成、编辑和处理文档工件。
- **走红原因（推断）／适合人群**：Agent 需要能继续编辑、校验和版本管理的文档表面，而不是一次性导出；适合桌面软件、企业文档流和自动化开发者。复杂 DOCX 保真、宏／外链安全和协作模型仍须压测。

### 3. storytold/cadcraft

- **确认信息**：[仓库](https://github.com/storytold/cadcraft)／[API](https://api.github.com/repos/storytold/cadcraft)：2026-10-07 创建，3,407 stars，Rust、Apache-2.0；自述为 AutoCAD 风格的 CAD／制图应用。
- **用途**：为二维制图与 CAD 编辑提供本地开源底座。
- **走红原因（推断）／适合人群**：可编辑的工程工件正从文档扩展到空间设计；适合 maker、CAD 工具开发者及需审计图纸生成链的团队。DWG/DXF 互操作、几何内核正确性与许可证兼容是采用前检查项。

### 4. zhongerxin/iPhone-use

- **确认信息**：[仓库](https://github.com/zhongerxin/iPhone-use)／[API](https://api.github.com/repos/zhongerxin/iPhone-use)：2026-10-06 创建，3,347 stars，Python、MIT；描述为通过 USB 让 Codex 操作真实 iPhone，含引导安装、App 自动化、实时屏幕和截图回退。
- **用途**：把受控的真实移动设备纳入 Agent 自动化与测试循环。
- **走红原因（推断）／适合人群**：computer-use 的价值从浏览器扩展到实际设备；适合移动端测试、个人自动化和研究原型。必须在隔离测试设备运行，审阅 USB 信任、隐私数据、App 权限和误触操作边界。

### 5. noahdunnagan/fsearch

- **确认信息**：[仓库](https://github.com/noahdunnagan/fsearch)／[API](https://api.github.com/repos/noahdunnagan/fsearch)：2026-10-08 创建，1,961 stars，Rust、MIT；自述为 macOS 全盘搜索，支持模糊名称、容错和索引内容 grep，宣称 8M 文件约 1 ms 查询。
- **用途**：为本地资料、代码和文件系统提供低延迟检索入口。
- **走红原因（推断）／适合人群**：个人 Agent 的上下文基础层需要先能可靠定位原始资料；适合研究、工程与资料密集用户。应评估索引范围、敏感目录排除、后台资源占用和删除后索引清理。

### 6. HelixDB/helix-foundry

- **确认信息**：[仓库](https://github.com/HelixDB/helix-foundry)／[API](https://api.github.com/repos/HelixDB/helix-foundry)：2026-10-07 创建，1,331 stars，TypeScript、Apache-2.0；描述为基于 HelixDB 与 DuckDB 的本地优先数据工作台，将公司数据连接为 ontology。
- **用途**：把异构业务数据组织为可查询的本地语义工作区。
- **走红原因（推断）／适合人群**：Agent 落地正从聊天记忆转向可治理的数据语义层；适合数据平台、分析与知识工程团队。需验证连接器权限、血缘、访问控制与本体维护成本。

### 7. pingdotgg/ts-rust

- **确认信息**：[仓库](https://github.com/pingdotgg/ts-rust)／[API](https://api.github.com/repos/pingdotgg/ts-rust)：2026-10-07 创建，1,120 stars，Rust、MIT；描述为 TypeScript 7 编译器（`tsc`）的实验性 Rust 移植。
- **用途**：探索更高效、可并发的 TypeScript 编译基础设施。
- **走红原因（推断）／适合人群**：大型 Agent 代码改动会放大编译与反馈时间，开发者偏好更快的工具链；适合编译器研究、构建系统和大型 TS 项目维护者。实验性质意味着语义兼容、插件生态和生产稳定性不能默认成立。

### 8. bherbruck/solidcraft

- **确认信息**：[仓库](https://github.com/bherbruck/solidcraft)／[API](https://api.github.com/repos/bherbruck/solidcraft)：2026-10-07 创建，1,048 stars，Rust、Apache-2.0；自述为桌面、Web 与 MCP 自动化皆可用的开源参数化 3D CAD。
- **用途**：将参数化建模暴露给人类设计者及 MCP 驱动的自动化流程。
- **走红原因（推断）／适合人群**：与 CadCraft 一起表明 Agent 工件面正在进入几何设计，且开始以 MCP 提供结构化操作入口；适合硬件原型、生成式设计和机器人场景资产团队。应隔离自动生成模型，并校验尺寸、公差、导出格式和物理可制造性。

## 技术趋势与社区偏好

- **“可验证”从代码测试扩展到数学与工程工件**：openai/math、CAD 与文档重实现共同说明，社区正追逐可继续编辑、检查与版本化的高价值成果，而不只是生成文本。
- **本地优先的上下文层继续下沉**：fsearch 提供文件检索，helix-foundry 提供语义数据工作台；敏感数据接入的权限、索引边界和删除传播成为默认评估项。
- **Agent 正触达真实设备和实体设计**：iPhone-use 与 SolidCraft 把执行范围扩到手机、三维模型和 MCP；这提高可交付性，也要求测试设备隔离、动作确认及工程验算。
- **基础设施偏好效率与兼容性并重**：ts-rust 的快速增长反映开发者对构建反馈的持续压力，但实验性项目应先以兼容测试而非 star 数判断可用性。
