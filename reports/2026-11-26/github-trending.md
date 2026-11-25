# GitHub 开源趋势晨报｜2026-11-26

## 时间与证据口径

检索于北京时间 2026-11-26 06:00。GitHub 当日 Trending 页面可访问，但高位 Agent／Skills 项目与 11 月 21--25 日已报道项目高度重合；为避免重复，本期从 **GitHub Search API 的 2026-11-19 至 25 新建仓库**中选择 6 项，并用 Repository API 复核当前 stars、forks、语言、许可证、创建时间与描述。下表“增量依据”是**创建至查询时的累计 stars**，绝非官方 `stars today`；走红原因均是编辑推断。

| 项目 | 当前 stars | 增量依据 | 语言／类别 |
| --- | ---: | --- | --- |
| iamajmeena/neonclipping | 2,621 | 11-19 创建至查询 | Python／本地视频生产力 |
| os6/nospeaker | 1,876 | 11-22 创建至查询 | Swift／macOS 无障碍／硬件交互 |
| leanprover-community/riemann-hypothesis | 1,212 | 11-20 创建至查询 | Lean／形式化数学 |
| deterministic-machines/deslop-please | 1,049 | 11-22 创建至查询 | Rust／开发工具 |
| qianyiai/kurocat | 949 | 11-21 创建至查询 | TypeScript／桌面生产力 |
| danielwh2/sprite-stacking | 902 | 11-20 创建至查询 | HTML／Agent Skill／创作工具 |

## 精选项目

### 1. [iamajmeena/neonclipping](https://github.com/iamajmeena/neonclipping)

- **确认信息：** Repository API：**2,621** stars、165 forks，Python、AGPL-3.0，2026-11-19 创建。项目自述为本地开源 clipping engine：输入链接，借助音频、YouTube captions 和本地 LLM 生成带字幕的 9:16 短片。
- **用途：** 将长视频转换为竖版、带字幕的候选片段，适合媒体剪辑工作流原型。
- **走红原因（推断）／适合人群：** 把视频切片、字幕和本地模型放在一个可自托管流程中，正好回应创作团队对成本和素材隐私的需求；适合有明确来源授权的内容团队和开发者。
- **采用提醒：** 必须核对视频／字幕权利、平台条款、模型与 AGPL 网络分发义务；先测误剪、字幕幻觉、GPU 资源和对敏感素材的留存策略。

### 2. [os6/nospeaker](https://github.com/os6/nospeaker)

- **确认信息：** Repository API：**1,876** stars、98 forks，Swift、MIT，2026-11-22 创建。项目让 MacBook trackpad 的 haptic motor 发声。
- **用途：** 探索 macOS 触觉执行器作为音频／反馈输出的交互与无障碍实验。
- **走红原因（推断）／适合人群：** 将现有硬件转成出人意料的系统能力，且 demo 直观、代码体量小，容易吸引系统开发者与交互创作者。
- **采用提醒：** 这不是常规扬声器替代；需验证设备兼容性、功耗／发热、用户舒适性、系统权限和对关键输入设备的干扰。

### 3. [leanprover-community/riemann-hypothesis](https://github.com/leanprover-community/riemann-hypothesis)

- **确认信息：** Repository API：**1,212** stars、486 forks，Lean，许可证字段为 `NOASSERTION`，2026-11-20 创建。仓库自述为对 2026-11-20 Riemann Hypothesis 形式化工作的社区清理。
- **用途：** 用 Lean 组织可机器检查的数学定义、引理和证明工件，供形式化验证研究／社区协作。
- **走红原因（推断）／适合人群：** 重大数学事件与可复查 proof assistant 工件结合，显著降低旁观者进入和复核的门槛；适合 Lean 学习者、形式化数学研究者。
- **采用提醒：** star 与 PR 活跃度不构成定理正确性证明；应以指定 Lean／mathlib 版本完整编译，核实证明边界、依赖信任链与缺失许可证。

### 4. [deterministic-machines/deslop-please](https://github.com/deterministic-machines/deslop-please)

- **确认信息：** Repository API：**1,049** stars、49 forks，Rust、MIT，2026-11-22 创建；简介为“Bring (back) sanity to your code”。
- **用途：** 面向代码质量／可维护性问题的 Rust 工具项目；具体规则与执行模型应以仓库文档和版本化配置为准。
- **走红原因（推断）／适合人群：** 在 AI 辅助编码扩张后，开发者愈发需要将风格、复杂度和可读性拉回可执行规则；适合愿意在 CI 中试验严格检查的团队。
- **采用提醒：** 简短定位不足以说明误报率或自动修复安全性；先在只报告模式跑基线，固定版本，并审阅对生成代码、monorepo 和 CI 时延的影响。

### 5. [qianyiai/kurocat](https://github.com/qianyiai/kurocat)

- **确认信息：** Repository API：**949** stars、146 forks，TypeScript、MIT，2026-11-21 创建。Tauri v2 + Rust + MCP 的跨平台透明置顶打字宠物／OBS overlay，项目列出 Win、Mac、Linux、Android 等目标。
- **用途：** 为直播、桌面陪伴或输入可视化提供轻量的本地 overlay，也展示了 MCP 接入桌面小应用的模式。
- **走红原因（推断）／适合人群：** 可见的互动产物、跨平台交付与 AI 定制入口结合，契合独立开发与创作者对低门槛桌面体验的偏好。
- **采用提醒：** overlay、输入监测和 MCP 都可能触及键盘数据及系统权限；应核查输入过滤、秘密遮蔽、插件来源、网络访问和 OBS 场景隔离。

### 6. [danielwh2/sprite-stacking](https://github.com/danielwh2/sprite-stacking)

- **确认信息：** Repository API：**902** stars、73 forks，HTML、MIT，2026-11-20 创建。项目将四个像素画视图生成可旋转的伪 3D sprite，并声明支持 Claude Code、Codex、Cursor、OpenCode、Gemini CLI 与 Pi。
- **用途：** 把特定像素艺术制作规范封装为 Agent 可调用 Skill，用于游戏、交互页面和动画资产生成。
- **走红原因（推断）／适合人群：** 结果视觉化、输入约束明确，正是小而专的 Skill 易被复制、改造和嵌入创作流水线的类型；适合独立游戏开发者与前端创作者。
- **采用提醒：** 生成资产仍需检查原创性、许可证、风格一致性、透明通道／分辨率和无障碍替代文本；不要将一个 Skill 的演示效果外推为通用视觉生产能力。

## 技术趋势与社区偏好

- **“可交付的本地工件”比抽象 Agent 框架更醒目。** 本地剪辑、桌面 overlay、像素资产和代码约束都直接产出可见或可合入的结果；这也是近期 Trending 中 Skills／生产力项目反复出现的原因之一。
- **可验证性正在横跨不同层次。** Lean 形式化追求机器检查，代码工具追求可执行约束，创作工具则需要来源和构建可追溯；热度不能替代复现、权限或许可证审计。
- **近期样本不代表日榜增量。** 本期以创建至查询的累计 stars 作为确认增长证据，并刻意不把它写成 `stars today`；官方 Trending 的当日排序可证明可见度，但不能倒推出上述仓库的精确日增长。

## 证据链接

- [GitHub Search API：近 7 天创建且 stars 大于 20](https://api.github.com/search/repositories?q=created%3A%3E2026-11-18%20stars%3A%3E20&sort=stars&order=desc&per_page=50)：候选发现和创建窗口。
- [GitHub Trending 日榜](https://github.com/trending?since=daily)：当日可见度背景；本期未将其排序当作项目日增量。
- 每项当前 metadata 以对应项目的 [GitHub Repository API](https://docs.github.com/rest/repos/repos#get-a-repository) 复核为准。
