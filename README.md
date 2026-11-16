# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-11-17

- [arXiv 独立报告](reports/2026-11-17/arxiv.md)
- [GitHub Trending 独立报告](reports/2026-11-17/github-trending.md)
- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-17

## 日期与证据口径

检索截至北京时间 2026-11-17 06:00。最新相关 v1 为 **2026-11-13 UTC**；以下六篇为该批新选、并与 11 月 10—16 日归档去重后的论文，**不是 11 月 17 日投稿**。作者、时间、机制与数字来自 arXiv 元数据及摘要；机构未可靠核验时不作推断。

## 自动驾驶／移动自治

### 1. [Disturbance-Aware Informative Planning in Spatiotemporal Environments](https://arxiv.org/abs/2611.18505)
- **作者／提交：** Kaleb Ben Naveed、Haejoon Lee、Anouck Girard、Dimitra Panagou；v1，2026-11-13 18:22 UTC。
- **问题—机制：** 忽略空间变化扰动会错估移动监测路径和信息量；方法先以路径上扰动不确定性下降安排测量，再以扰动 belief 优化轨迹。
- **实验／价值／局限：** 四个仿真场景将学习时间降 **25.0%–52.3%**；连接“测哪里”与“走哪里”，但需验证时变扰动、在线成本、传感噪声与真机收益。

### 2. [PoliMop: Policy-in-the-Loop Motion Planning in 3D Spaces for Mobile Robots](https://arxiv.org/abs/2611.18110)
- **作者／提交：** Yael Fassbind、Valentin N. Hartmann、Huang Su、Yijiang Huang、Stelian Coros；v1，2026-11-13 12:35 UTC。
- **问题—机制：** 几何通路不等于机器人及其策略可走；kinodynamic RRT 以物理仿真的 policy rollout 扩展节点、以质点预规划引导采样，并纳入环境改动。
- **实验／价值／局限：** 四足、人形、轮式仿真最多省 **63%** 规划时间；把能力写入可达性，仍须测 rollout 成本、策略失配、动态障碍和真机回退。

## 机器人／具身智能

### 3. [Training Reasoning Models in Simulation to Natively Use Real Robots](https://arxiv.org/abs/2611.18562)
- **作者／提交：** Jiaming Tang、Zhuoyang Zhang、Junxian Guo 等 11 位作者；v1，2026-11-13 18:59 UTC。
- **问题—机制：** PEAR 以纯仿真、无示范 robot-use RL 后训练 27B 推理模型，直接输出末端位姿，并检验跨硬件与真实迁移。
- **实验／价值／局限：** LIBERO **1.6%→74.4%**；真实双臂 **60%**、基础模型 0；LIBERO-Pro 新任务 **57.4%**、π0.5 为 **0.75%**。需要真实样本、失败后果、安全护栏与权限审计。

### 4. [Objectives as Policies: Vision-Language Model Cost Programs for Contact-Rich Manipulation](https://arxiv.org/abs/2611.18298)
- **作者／提交：** Zihao Lu、Trong Gia Hung Nguyen、Fuquan Wang、Yifan Zhu；v1，2026-11-13 15:22 UTC。
- **问题—机制：** OaP 将 VLM 指令编译为包含运行／终端代价和阶段条件的可编辑 objective program，在 real-to-sim 数字孪生中以 MPC rollout 修订后再部署。
- **实验／价值／局限：** 作者报告四个真实桌面任务和仿真胜过基线但摘要无具体分数；语言意图可被物理 rollout 反驳，仍需程序错误、sim-to-real、时延与恢复数据。

### 5. [PROOF: Perceptive Robustness via Out-of-Distribution Fallback for Legged Locomotion](https://arxiv.org/abs/2611.18305)
- **作者／提交：** Siyuan Wang、Dongjie Zhu、Jinxuan Lu、Wenjun Xu、Jiankun Wang；v1，2026-11-13 15:26 UTC。
- **问题—机制：** teacher 同时学习视觉与本体 fallback，student 预测外感不确定性，在 OOD 输入下抑制不可靠视觉。
- **实验／价值／局限：** Unitree Go2 + RealSense D435 在遮挡、强光下仍报告稳定运动；回退时机显式化，需 OOD ROC、误退化代价和跨天气验证。

### 6. [Modeling the Frictional Contact of Continuum Robots with Environments through Linear Complementarity Problem](https://arxiv.org/abs/2611.18546)
- **作者／提交：** Jia Shen、Junhyoung Ha、Yue Chen；v1，2026-11-13 18:51 UTC。
- **问题—机制：** 以线性互补约束建模环境静/滑摩擦、滞回和连续体形变。
- **实验／价值／局限：** **287.9 mm** 腱驱机器人最大误差 **45.4 mm→5.85 mm**；接触物理成为可诊断层，仍须测非库仑材料、接触切换、实时上界和真实任务。

## 趋势总结

扰动 belief、策略 rollout、VLM 代价程序、OOD fallback 与摩擦模型都将可靠性落在可执行中间层；后续应联合报告校准、回退误触发、sim-to-real、尾延迟与物理失败代价。

# GitHub 开源趋势晨报｜2026-11-17

## 时间与证据口径

排名与 `+N/日` 来自第三方镜像保存的 **2026-11-16 UTC** 日榜（`collectedAt` 2026-11-16 21:07 UTC），为镜像 `gained`，非本次总 star 差值。当前元数据经 GitHub Repository API 复核；镜像不是官方服务，走红原因和趋势均为编辑推断，且排除 11 月 14—16 日近期重复项目。

### 1. [backnotprop/plannotator](https://github.com/backnotprop/plannotator)
- **数据：** **12,489 stars**；第 2、**+689/日**；TypeScript；Apache-2.0。[API](https://api.github.com/repos/backnotprop/plannotator)／[日榜](https://githubtrending.today/api/archive/2026-11-16.json)。
- **用途／原因／适合：** 人在 agent loop 中计划、标注、审阅与反馈的工作区；反映审批正成为可见工件。适合工程团队，须审计反馈外发、身份边界、仓库权限与留存。

### 2. [alibaba/open-code-review](https://github.com/alibaba/open-code-review)
- **数据：** **52,880 stars**；第 11、**+946/日**；Go；Apache-2.0。[API](https://api.github.com/repos/alibaba/open-code-review)／[日榜](https://githubtrending.today/api/archive/2026-11-16.json)。
- **用途／原因／适合：** 确定性规则与 LLM Agent 混合的多语言代码 review；说明工程团队需要稳定规则加行级反馈。适合 CI 团队，先测误报/漏报、代码外传、提示注入和保留策略。

### 3. [google-research/paper-orchestra](https://github.com/google-research/paper-orchestra)
- **数据：** **1,391 stars**；第 12、**+306/日**；Python；Apache-2.0。[API](https://api.github.com/repos/google-research/paper-orchestra)／[日榜](https://githubtrending.today/api/archive/2026-11-16.json)。
- **用途／原因／适合：** 多 agent 自动化论文写作框架；研究流程角色化在升温。适合原型研究，必须复核引用、实验、署名和发表政策。

### 4. [ChromeDevTools/chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp)
- **数据：** **57,633 stars**；第 13、**+837/日**；TypeScript；Apache-2.0。[API](https://api.github.com/repos/ChromeDevTools/chrome-devtools-mcp)／[日榜](https://githubtrending.today/api/archive/2026-11-16.json)。
- **用途／原因／适合：** 将 Chrome DevTools 接给 coding agent，使修复基于 DOM、网络和运行时证据。适合 Web 团队；隔离登录态、限制域名、清理日志 token 并审计调用。

### 5. [getarcaneapp/arcane](https://github.com/getarcaneapp/arcane)
- **数据：** **8,650 stars**；第 6、**+31/日**；Go；BSD-3-Clause。[API](https://api.github.com/repos/getarcaneapp/arcane)／[日榜](https://githubtrending.today/api/archive/2026-11-16.json)。
- **用途／原因／适合：** 面向普通用户的 Docker 管理工具，显示 AI 服务仍依赖可理解的容器底座。适合自托管团队；Docker socket 属高权限，先检查认证、密钥、暴露面、备份和回滚。

### 6. [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)
- **数据：** **68,066 stars**；第 9、**+122/日**；Python；MIT。[API](https://api.github.com/repos/mvanhorn/last30days-skill)／[日榜](https://githubtrending.today/api/archive/2026-11-16.json)。
- **用途／原因／适合：** 跨 Reddit、X、YouTube、HN、Polymarket 和 Web 检索、汇总摘要的 agent Skill；时效型检索正被封装为资产。适合研究辅助，须复核原始来源、时间窗、访问规则、偏差和个人数据。

## 技术趋势与社区偏好

人工决策、受控执行、环境观测、部署底座和证据生产已连成 Agent 工作流。热度不等于质量或生产采用；最小权限、来源追溯、日志/凭据治理与许可证审计必须先于采纳。

## 内容标准与归档

每期 arXiv 按问题、创新、机制、实验、价值和局限选篇；GitHub 区分可核验元数据与编辑推断。历史文件位于 [`reports/`](reports/)，跨期判断见 [分类趋势总结](CATEGORY_SUMMARY.md)。
