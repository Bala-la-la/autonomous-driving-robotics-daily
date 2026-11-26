# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-11-27

- [arXiv 独立报告](reports/2026-11-27/arxiv.md)
- [GitHub Trending 独立报告](reports/2026-11-27/github-trending.md)
- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-27

## 日期与证据口径

检索截至北京时间 2026-11-27 06:00。本期精选 **2026-11-25 UTC v1** 的 7 篇投稿；它们不是 11 月 27 日当日投稿，且未出现在 11 月 25--26 日报告。题目、作者、提交时间、方法与数值来自 arXiv 摘要/API；未能由元数据完整核验机构时不臆测。性能均为作者报告，尚未独立复现。

## 自动驾驶／移动自治

### 1. [FeaXDrive2: Body-Scene Spatial Grounding for Feasibility-Aware Generative Driving](https://arxiv.org/abs/2611.34658)

- **作者／机构／提交：** Bo Leng、Baoyun Wang、Wenxin Wen 等；机构未完整披露；v1，2026-11-25 16:30 UTC。
- **问题：** 生成式驾驶规划器常只看参考点，忽略整车车身扫掠，导致中心线看似可行而车角擦碰场景约束。
- **创新与机制：** **FeaXDrive2** 从车身角点发起空间 query，并随 Flow-DiT 的轨迹估计更新视觉取样位置；RC-F 用高风险轨迹监督同时保留参考行为，再做 planning-supervised VLM--Action 对齐。其反事实分析固定轨迹、改变车身几何来检验安全差异。
- **实验与关键结果：** NAVSIM 上相对 base planner at-fault collision 降 **36.5%**、PDMS **87.0→88.8**；NAVSIM v2 EPDMS **86.5→88.3**。
- **关注价值：** 把“车能否通过”从轨迹点提升为可审计的车体--场景接口，适合接入安全壳、不同车型和窄路 ODD。
- **局限／跟进：** 仿真车体 clearance 不等于真实制动、定位延迟和动态体预测风险；应报告候选遗漏、不同轴距/外廓、p95 延迟及实车近失事件。

## 机器人／具身智能

### 2. [Cairn: Object-Centric 3D Trajectory Priors for Steering Frozen VLAs](https://arxiv.org/abs/2611.34914)

- **作者／机构／提交：** Agelos Kratimenos、Kostas Daniilidis、Evangelos Chatzipantazis；机构未完整披露；v1，2026-11-25 18:57 UTC。
- **问题：** 冻结 VLA 会把物体送往训练布局中的位置；障碍或物体移位时，逐任务微调既昂贵又可能遗忘旧技能。
- **创新与机制：** 小型 prior 读取点云、持物姿态和指令，采样至释放点的 SE(3) 物体轨迹；它与冻结 VLA 双向耦合：VLA 意图选择/重塑轨迹，轨迹再拉动去噪动作向下一 waypoint 靠近。
- **实验与关键结果：** 1,941 个留出 LIBERO 场景中，冻结 π0.5 成功率 **24.5→95.1%**；LIBERO-PRO **27.3→38.0%**，被 steering 的 episode 为 **54.4→81.1%**；纯仿真 prior 在 Franka 真机障碍绕行展示可行性。
- **关注价值：** 将通用低层 VLA 与可检查的物体轨迹接口解耦，可更直接审计碰撞、可达性和任务布局改变。
- **局限／跟进：** 点云质量、抓取变换和轨迹采样失败会传递给策略；还需统计真实接触、感知遮挡、错误 waypoint 的回退及在线计算。

### 3. [DexLink: Synthesizing Dexterous Behaviors from Chained Hand-object Poses](https://arxiv.org/abs/2611.34936)

- **作者／机构／提交：** Meenal Parakh、Deep Patel、Beining Han、Jia Deng；机构未完整披露；v1，2026-11-25 18:59 UTC。
- **问题：** 灵巧操作依赖难规模化的人类示范；通用奖励又难精细指定抓型、时序和手--物接触。
- **创新与机制：** 将稀疏、可复用 hand-object interaction template 优化重定向到目标物，保持空间关系；把重定向姿态链为近似参考轨迹，再由 residual RL 在仿真中细化成闭环策略。
- **实验与关键结果：** 覆盖单手、双手、关节物和动态任务；作者称不需物体特定演示即可匹配 dense reference-tracking，并展示跨尺度/实例/类别模板迁移及 sim-only zero-shot 部署潜力；摘要未给统一绝对成功率。
- **关注价值：** 用“可编辑接触模板”替代端到端示范，可将人类意图、优化器与策略学习的责任边界分开审查。
- **局限／跟进：** 近似参考可能隐藏不安全手指接触；需披露优化失败率、接触力/滑落、模板库覆盖度及真机跨手型结果。

### 4. [RoboEvo²: Recursive Robot Self-Improvement via Harness-Policy Co-Evolution](https://arxiv.org/abs/2611.34675)

- **作者／机构／提交：** Chenzhi Liu、Jiehong Lin、Wei Huang 等；机构未完整披露；v1，2026-11-25 16:39 UTC。
- **问题：** VLA 遇到新场景常需人工示范；代码 Agent 虽可试错，却反复推理和修复成本高。
- **创新与机制：** P2H 根据 policy failure 让 coding agent 搜索 Code／Code+ICL／Code+Policy 路径，固化验证过的 skill、路由和 memory；H2P 将验证轨迹用于监督训练，并以同起点成功修正对失败的反事实偏好蒸馏更新 policy。
- **实验与关键结果：** LIBERO-PRO standalone **11.0→84.1%**、hybrid **30.4→90.5%**；Unitree G1-D hybrid **95.0%**，作者称 RoboTwin C2R 也有相近增益和更低 agent 成本。
- **关注价值：** 明确把“探索 harness”和“执行 policy”作为互相改进但可分别评测的资产，适合研究具身技能如何累积。
- **局限／跟进：** 高分来自何种试错预算、筛选器和安全约束尚不清楚；应开放失败轨迹、权限/动作 allowlist、真机损伤与跨任务遗忘曲线。

### 5. [DemoFoundry: Toward Scalable Photorealistic Robot Data with Coding Agents and Generative Rendering](https://arxiv.org/abs/2611.34671)

- **作者／机构／提交：** Ruixiang Wang、Xinyue Yao、Xuanning Zhou 等；机构未完整披露；v1，2026-11-25 16:37 UTC。
- **问题：** 仿真数据缺真实视觉，生成视频又往往没有物理一致动作标签；为每个新场景手工建模不可扩展。
- **创新与机制：** coding agent 从已有 robot episode 构造真实--proxy 配对训练视频 renderer，并按场景/指令重建关键几何、写可执行交互程序；物理仿真产出对齐 state/action，渲染器转为场景一致的 photorealistic observation，任务检查筛出成功轨迹。
- **实验与关键结果：** 作者报告生成数据提升视觉质量和 action--video 一致性；训练策略优于 raw simulation，并接近等量真实示范训练，摘要未列统一成功率/样本量。
- **关注价值：** 将生成外观、物理执行和 action supervision 留在同一可追溯流水线，避免只看“视频像不像”。
- **局限／跟进：** renderer 可能掩盖接触/遮挡错误；需审计生成资产许可、程序沙箱、sim exploit、real-to-sim 偏差及真机验证成本。

## 交叉方向：SLAM／长期空间智能

### 6. [MERLoc: Robust Robot Localization in Dynamic Environments with Pose-Based Retrieval over 3D Gaussian Splatting References](https://arxiv.org/abs/2611.34932)

- **作者／机构／提交：** Michael Baumgartner、Dario Mylonopoulos、Sammy Christen、Markus Gross、Moritz Bacher；机构未完整披露；v1，2026-11-25 18:59 UTC。
- **问题：** 动态空间中按外观检索少量 reference image 易被人群、物体重排和重复纹理误导。
- **创新与机制：** 从一次 metric 3D Gaussian Splatting scan 离线渲染与机器人形态/传感器匹配的稠密 Functional Reference Memory，并预编码 localizer；有先验时按空间邻近与朝向而非外观选 reference。
- **实验与关键结果：** 在真实动态数据的 10 个 backend/split 组合中 9 个 position RMSE 降 **15--60%**；Jetson Orin NX 以 **5 Hz** 运行，并完成有人流/重排走廊导航。
- **关注价值：** 将“地图存什么、何时检索”从被动图像缓存变成与机器人可达姿态相关的长期状态设计。
- **局限／跟进：** 依赖可用位姿先验和一次高质量扫描；应报告跨日变化、全局重定位失败、3DGS 内存增长、先验错位和隐私数据保留。

### 7. [Memory Is Not Ground Truth: Revising Navigation Authority under Unreliable VLM Evidence for Persistent Semantic Navigation](https://arxiv.org/abs/2611.34915)

- **作者／机构／提交：** Sumukh Shrote、Shenbagaraj Kannapiran、Eric Eaton、Camillo Jose Taylor；机构未完整披露；v1，2026-11-25 18:57 UTC。
- **问题：** VLM 多次“未看到”目标并不能证明目标已消失；将持久记忆直接作为导航目标会让机器人追逐过期对象。
- **创新与机制：** 在 Spot 四相机与持续时空 visual memory 上量化负验证的相关性；提出 dependence-aware、可逆 memory update：不重复计数相关 miss，证据不足时撤销记忆的导航权威但不宣称目标不存在，后续正证据可恢复。
- **实验与关键结果：** 三个匹配真机决策场景中，episode-local baseline 每次都选择 stale memory；该方法三次均改选 semantic frontier；补充试验在运动中重新验证目标并恢复 fresh memory。
- **关注价值：** 它把“记忆真假”与“记忆能否驱动动作”分开，是长期自治中避免错误状态直接进入控制的关键契约。
- **局限／跟进：** 三个决策上下文样本很小；须扩展到更多目标/楼层/照明，公开误撤销成本、相关性模型校准、p95 感知延迟及人机接管策略。

## 趋势总结

- **几何/物理中间接口正成为冻结基础模型的安全阀。** FeaXDrive2 的车角 query、Cairn 的持物轨迹、DexLink 的接触模板，都让策略的空间假设能被逐项检查，而非只看最终 success。
- **自我改进开始强调“什么可写回系统”。** RoboEvo²、DemoFoundry 和记忆权威修订都先筛验证轨迹/证据再复用；下一步需要将数据/程序版本、试错伤害和回滚规则纳入同一报告。
- **长期空间状态从“多存一点”转向“谁有资格驱动行动”。** MERLoc 以姿态检索限制参考，Memory Is Not Ground Truth 可撤销陈旧记忆的行动权；变化场景下的重定位、错误隔离和资源上界仍是缺口。

# GitHub 开源趋势晨报｜2026-11-27

## 时间与证据口径

检索于北京时间 2026-11-27 06:00。GitHub Trending/第三方日榜快照可见，但官方页面只展示“当天增星”且会滚动；本期当前 stars、forks、语言、许可证、创建时间和项目描述均以 Repository API 复核。下表的 **增量依据** 仅为第三方 2026-11-26 日榜/近 7 天可见度，绝不将累计 stars 误写为官方 `stars today`；走红原因均为编辑推断。

| 项目 | 当前 stars | 增量依据 | 语言／类别 |
| --- | ---: | --- | --- |
| [deepseek-ai/dsh-superagent-prototype](https://github.com/deepseek-ai/dsh-superagent-prototype) | 24,663 | 11 月日榜单日峰值 +4,369（第三方快照） | TypeScript／Agent 系统 |
| [pingdotgg/t3code](https://github.com/pingdotgg/t3code) | 80,844 | 11-25 第三方榜单 +1.9k | TypeScript／远程 Agent 控制 |
| [stablyai/orca](https://github.com/stablyai/orca) | 140,269 | 11-25 第三方榜单 +1.9k | TypeScript／Agent fleet |
| [KKKKhazix/agent-autoloop](https://github.com/KKKKhazix/agent-autoloop) | 6,643 | 11 月日榜单日峰值 +1,613（第三方快照） | TypeScript／后台 Agent 编排 |
| [Parcha-ai/agentrun](https://github.com/Parcha-ai/agentrun) | 1,275 | 11-26 日榜可见（第三方快照） | JavaScript／Agent runtime |
| [shinyobjectz/raea](https://github.com/shinyobjectz/raea) | 5,283 | 11-26 日榜可见（第三方快照） | TypeScript／本地创作引擎 |

## 精选项目

### 1. [deepseek-ai/dsh-superagent-prototype](https://github.com/deepseek-ai/dsh-superagent-prototype)

- **确认信息：** Repository API：**24,663** stars、3,103 forks，TypeScript、MIT，2026-10-31 创建；项目简介为“Towards a More Autonomous Agent System”。第三方月度快照记录其 11 月单日峰值 **+4,369**。
- **用途：** 用于研究或原型化更自主的 Agent 系统；具体运行面、权限与部署模型须以版本化文档为准。
- **走红原因（推断）／适合人群：** 以“superagent”叙事切中自主执行热度，且由模型厂商组织发布；适合 Agent 架构研究者和愿意在隔离环境评估的工程团队。
- **采用提醒：** 名称与热度不代表可生产使用；先核验工具调用、持久状态、审批/stop 条件、遥测外发和模型许可。

### 2. [pingdotgg/t3code](https://github.com/pingdotgg/t3code)

- **确认信息：** Repository API：**80,844** stars、14,263 forks，TypeScript、MIT，2026-02-08 创建；自述为从任意电脑或手机控制 Claude Code、Codex 等。第三方 11-25 榜单记录 **+1.9k** 当日增量。
- **用途：** 提供跨设备访问/控制 coding-agent 的工作流入口。
- **走红原因（推断）／适合人群：** 将长运行代码任务从单机终端扩展到移动端和远程控制，契合开发者对随时查看、干预与接管的需求；适合已有可控开发环境的个人/小团队。
- **采用提醒：** 远程控制扩大密钥、代码与命令权限边界；应先审计认证、设备绑定、会话过期、命令确认、日志脱敏和网络暴露。

### 3. [stablyai/orca](https://github.com/stablyai/orca)

- **确认信息：** Repository API：**140,269** stars、8,970 forks，TypeScript、MIT，2026-03-17 创建；项目称可用自有订阅运行 Claude Code、Grok、Agy、Codex 等 bot fleet，并提供桌面、移动与远程 runtime。第三方 11-25 榜单记录 **+1.9k**。
- **用途：** 对多 Agent/多任务进行集中启动、查看和调度。
- **走红原因（推断）／适合人群：** “用已有订阅调度一组 bots”直指成本与并行生产力；适合需管理多个隔离任务的高级用户与平台原型团队。
- **采用提醒：** fleet 把凭据、目录、并发预算和外部写入集中化；必须采用每 agent 最小权限、沙箱、成本上限、审批队列和可回放审计。

### 4. [KKKKhazix/agent-autoloop](https://github.com/KKKKhazix/agent-autoloop)

- **确认信息：** Repository API：**6,643** stars、1,238 forks，TypeScript、MIT，2026-11-03 创建。项目自述让命令行 Agent 在后台接活、跟进到底，仅在拿不准时出卡片请求决策；第三方月度快照记录单日峰值 **+1,613**。
- **用途：** 将任务队列、后台持续执行和人工决策点组合到 CLI Agent 工作流。
- **走红原因（推断）／适合人群：** 它把“不要频繁打断人、但关键处升级”做成明确产品行为，契合异步 coding-agent 的操作习惯；适合愿意定义明确任务边界的开发者。
- **采用提醒：** “自动跟进”最容易越过授权边界；请核查默认写入/网络命令、取消语义、重试上限、队列持久化、提示注入和 secrets 隔离。

### 5. [Parcha-ai/agentrun](https://github.com/Parcha-ai/agentrun)

- **确认信息：** Repository API：**1,275** stars、106 forks，JavaScript、Apache-2.0，2026-09-23 创建；自述为在既有 Agent harness、算力和模型之上提供 self-improvement、durable execution 与 control plane。11-26 第三方日榜可见。
- **用途：** 为现有 Agent 包装持久执行、控制面和改进循环的 runtime。
- **走红原因（推断）／适合人群：** 不强迫替换既有 harness，而把可靠执行/控制层拆出，适合已有原型但缺少运行治理的团队。
- **采用提醒：** durable execution 意味着状态与重试会跨会话存留；部署前应检查幂等键、失败补偿、租户隔离、状态加密、模型/工具版本固定和成本熔断。

### 6. [shinyobjectz/raea](https://github.com/shinyobjectz/raea)

- **确认信息：** Repository API：**5,283** stars、423 forks，TypeScript，许可证字段 `NOASSERTION`，2026-10-18 创建；自述为将 Agent 编写的 React/TypeScript 在自有 GPU 渲染成视频、运动图形、3D 场景或游戏，采用 Rust + Bevy，支持 macOS/Linux/Windows。11-26 第三方日榜可见。
- **用途：** 将生成式代码直接落成可预览的 GPU 视觉工件，面向视频、动态图形和 3D/游戏原型。
- **走红原因（推断）／适合人群：** 把 Agent 代码能力与本地可见产物绑定，demo 可传播性强且避免将渲染完全交给云端；适合创意技术开发者与需要快速原型的团队。
- **采用提醒：** GPU 渲染代码应视为不可信输入；需要进程/文件/网络沙箱、资源配额、依赖锁定与素材版权检查，且 `NOASSERTION` 许可证必须在采用前澄清。

## 技术趋势与社区偏好

- **自主性正在从模型能力转向运行契约。** superagent、后台 loop、durable runtime 和 fleet 关注的是任务如何持续、何时升级人工、怎样停止，而不只是“能否调用模型”。
- **远程/多端控制放大了治理需求。** t3code 与 Orca 的便利性同时扩大凭据、命令和代码资产的攻击面；任何“随处控制”设计都应先落地会话隔离与可撤销授权。
- **Agent 产物继续从文本走向可运行工件。** raea 的本地 GPU 渲染体现社区对直接交付视频、3D、游戏的偏好；但运行不受信任代码、素材权利和许可证确认不能由星增代替。

## 证据链接

- [GitHub Trending 日榜](https://github.com/trending?since=daily)：官方可见度背景，数值随页面滚动。
- [GitTrend 2026-11-25 快照](https://gittrend.io/) 与 [upcurrent 11 月归档](https://upcurrent.dev/github-trending/2026-11/)：第三方增量/日榜依据；非 GitHub 官方计数。
- 当前 metadata 以对应项目的 [GitHub Repository API](https://docs.github.com/rest/repos/repos#get-a-repository) 复核。

## 内容标准与归档

每期 arXiv 按问题、创新、机制、实验、价值和局限选篇；GitHub 区分可核验元数据与编辑推断。历史文件位于 [`reports/`](reports/)，跨期判断见 [分类趋势总结](CATEGORY_SUMMARY.md)。
