# GitHub 开源趋势晨报｜2026-11-28

## 时间与证据口径

检索于北京时间 2026-11-28 06:00。官方 GitHub Trending 页面本次请求超时，因此**不宣称官方 `stars today`**。以下项目均由 GitHub Search 以创建日期 2026-11-21 至 11-25、按 stars 排序发现，再用 Repository API 复核当前 stars、forks、语言、许可证、创建/更新时间和描述；“增量依据”是从创建至本次查询的可确认累积增长（不等于 24 小时增量），走红原因均为编辑推断。

| 项目 | 当前 stars | 增量依据 | 语言／类别 |
| --- | ---: | --- | --- |
| [EL4CTEO/fast-anything](https://github.com/EL4CTEO/fast-anything) | 4,440 | 11-21 创建至查询累计 | Rust／性能优化 Agent |
| [nexu-io/opengame](https://github.com/nexu-io/opengame) | 2,176 | 11-25 创建至查询累计 | TypeScript／Agent 游戏创作 |
| [alesha-pro/llm.asm](https://github.com/alesha-pro/llm.asm) | 2,131 | 11-25 创建至查询累计 | Assembly／端侧推理教育 |
| [qianyiai/KuroCat](https://github.com/qianyiai/KuroCat) | 1,757 | 11-21 创建至查询累计 | TypeScript／桌面生产力 |
| [sybil-solutions/skill-distill](https://github.com/sybil-solutions/skill-distill) | 997 | 11-21 创建至查询累计 | Python／Skills 工程 |
| [xikhar/papercraft](https://github.com/xikhar/papercraft) | 930 | 11-21 创建至查询累计 | JavaScript／创作 Skill |

## 精选项目

### 1. [EL4CTEO/fast-anything](https://github.com/EL4CTEO/fast-anything)

- **确认信息：** Repository API：**4,440** stars、318 forks，Rust、MIT；2026-11-21 创建，11-27 更新。项目主张只将 profile 发现的热点 5% 迁到 Rust，并让 coding agent 证明新旧实现行为相同，覆盖 Python、JS/TS、Java、Go 等。
- **用途：** 为既有应用选择性做性能剖析、热点重写和等价性验证，而不是全量重写。
- **走红原因（推断）／适合人群：** 它把 Agent 编码从“产出更多代码”转为有性能边界和验证要求的改造流程；适合维护多语言遗留系统、愿意先建立 benchmark 的工程团队。
- **采用提醒：** 自动迁移不能保证语义、并发、FFI 和异常行为等价；应锁定基准/测试、保留人工 code review 与可回滚变更。

### 2. [nexu-io/opengame](https://github.com/nexu-io/opengame)

- **确认信息：** **2,176** stars、355 forks，TypeScript、Apache-2.0；2026-11-25 创建。自述为面向 AI agent 的 Unity/Unreal 式游戏创作平台，可协调 20+ coding agent 并发布 3D/小游戏至多个平台。
- **用途：** 将代码 Agent、游戏模板、构建和多渠道发布连接成创作流水线。
- **走红原因（推断）／适合人群：** “Agent 直接交付可玩的工件”传播性强，且把多 Agent 协作落到具体媒介；适合 game jam、教育和原型团队。
- **采用提醒：** 多平台发布涉及账号、素材版权、未成年人内容和构建供应链；先隔离凭据、审查发布审批和第三方资源许可。

### 3. [alesha-pro/llm.asm](https://github.com/alesha-pro/llm.asm)

- **确认信息：** **2,131** stars、324 forks，Assembly、MIT；2026-11-25 创建。项目包含 12 KB Qwen3-0.6B inference、22 KB 可启动 bare-metal OS 与 32 KB Mini-GPT trainer，均为 x86-64 NASM、无 C/libc/依赖。
- **用途：** 用极小、可读的底层实现学习推理运行时、启动链与训练的资源约束。
- **走红原因（推断）／适合人群：** 在大模型栈日益复杂时，极简实现能帮助开发者理解真正的内存/指令成本；适合系统研究、教育和实验性端侧开发。
- **采用提醒：** 小体积 demo 不代表通用模型性能或安全；裸机代码应在隔离虚拟机/专用硬件上测试，且不要把实验模型用于敏感推理。

### 4. [qianyiai/KuroCat](https://github.com/qianyiai/KuroCat)

- **确认信息：** **1,757** stars、248 forks，TypeScript、MIT；2026-11-21 创建。自述为跨 Win/macOS/Linux/Android 的 3D/2D desktop typing cat 与 AI coding companion，采用 Tauri v2、Rust、MCP，可接 Claude/Codex/DeepSeek/OBS。
- **用途：** 提供可视化桌面陪伴/状态展示，并连接 coding-agent 与 OBS 等本地工具。
- **走红原因（推断）／适合人群：** 它把抽象的 Agent 运行状态变成可见、可分享的桌面交互，覆盖创作者与开发者的轻量生产力场景。
- **采用提醒：** MCP 和桌面集成可能触及本地文件、窗口和 token；需检查每个 server 的权限、网络出口和会话保存策略。

### 5. [sybil-solutions/skill-distill](https://github.com/sybil-solutions/skill-distill)

- **确认信息：** **997** stars、85 forks，Python、MIT；2026-11-21 创建。项目目标是把高质量 Claude Code/Codex 会话蒸馏为开放权重模型可复现任务的 skill。
- **用途：** 将一次性 agent 操作整理为可复用技能资产，服务后续模型或团队工作流。
- **走红原因（推断）／适合人群：** Skill 从提示词转向可积累操作知识是当前 Agent 工程热点；适合有重复工程流程、希望降低昂贵模型调用的团队。
- **采用提醒：** 会话可能含 secrets、私人代码和错误操作；蒸馏前应脱敏、固定输入/工具版本、添加评测与人工审批，避免把偶然成功固化为规范。

### 6. [xikhar/papercraft](https://github.com/xikhar/papercraft)

- **确认信息：** **930** stars、102 forks，JavaScript、MIT；2026-11-21 创建。它是一个用于制作 pop-up papercraft 风格游戏、交互场景、网页和动画的 Agent skill。
- **用途：** 为网页/互动内容提供可重复调用的视觉风格和实现约束。
- **走红原因（推断）／适合人群：** 社区正偏好能直接产生区别化、可见成品的 Skills；适合创意编码、教学和原型演示。
- **采用提醒：** 风格 skill 不等于无版权风险或无障碍合格；需审查素材来源、bundle 体积、移动端性能与生成代码的安全性。

## 技术趋势与社区偏好

- **Agent 工程转向“可验证的改造”。** fast-anything 的性能/等价性约束与 skill-distill 的经验复用，都要求把一次运行变成可测试资产，而非只追求自动化产出。
- **可交付工件仍是强驱动力。** opengame、KuroCat、papercraft 将 Agent 能力落到游戏、桌面交互和网页视觉，社区更愿意传播可直接体验的产物。
- **本地可控与底层透明度回潮。** llm.asm 的热度显示，在云端 Agent 扩张之外，开发者仍关注资源上限、可解释实现和离线实验；这不免除权限、发布和供应链审计。

## 证据链接

- [GitHub Trending 日榜](https://github.com/trending?since=daily)：本次页面连接超时，未用其数值。
- [GitHub Search API](https://docs.github.com/rest/search/search#search-repositories) 与 [Repository API](https://docs.github.com/rest/repos/repos#get-a-repository)：用于发现和复核本期当前 metadata；创建至查询累计 stars 仅作近期增长下界。
