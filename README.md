# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪最新 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-11-15

- [arXiv 独立报告](reports/2026-11-15/arxiv.md)

- [GitHub Trending 独立报告](reports/2026-11-15/github-trending.md)

- [分类趋势总结](CATEGORY_SUMMARY.md)

## 内容标准

每期 arXiv 报告按方向精选并说明问题、创新、机制、实验、价值和局限；GitHub 报告区分可核验元数据与编辑推断。归档位于 [`reports/`](reports/)。

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-15

## 日期与证据口径

检索截至北京时间 2026-11-15 06:00。arXiv `cs.RO`、`cs.CV`、`cs.AI` 中最新相关 v1 批次仍为 **2026-11-12 UTC**；周末无更晚常规批次，本期从该批回溯，并与 11 月 10—14 日归档去重。因此以下七篇均为 **11 月 12 日投稿，不是 11 月 15 日新稿**。作者、时间、方法和数值均据 arXiv 元数据及摘要；未能可靠核验的机构不作推断。

## 自动驾驶／移动自治

### 1. [Evaluating Video LLMs' Understanding of Corner Cases in Autonomous Driving](https://arxiv.org/abs/2611.16767)

- **作者／机构／提交：** Gabriel Manalu 等 9 位作者；arXiv 未列可核验机构；v1，2026-11-12 13:15 UTC。
- **问题与创新：** 常见驾驶 VLM 基准偏向常规交通，难以检验安全关键长尾。DashBench 收录 1,709 条碰撞及非碰撞 corner case 视频，测试 25 个 Video LLM 的开放式问答和解释。
- **机制／结构：** 以精筛驾驶视频、提示词组和诊断工具组成评测，而非训练一个新驾驶策略；重点检查危险主体、事件和动作解释是否一致。
- **实验与关键结果：** 作者称全部受测模型均远低于安全关键应用所需水平，常漏判危险或虚构不存在的主体／动作；摘要未给出统一分数阈值。
- **关注价值：** 为“可解释驾驶 VLM”补上反例和幻觉审计，提醒自然语言理由不能直接当作决策证据。
- **局限／跟进：** 视频和问答分布仍不能代替闭环车辆测试；需公开类别覆盖、标注一致性、校准、时延及解释错误是否真的改变控制风险。

### 2. [From Foundation VLM to Versatile Driving VLM: A Triplet Incremental Training Approach](https://arxiv.org/abs/2611.16727)

- **作者／机构／提交：** Shengtao Wu 等 7 位作者；arXiv 未列可核验机构；v1，2026-11-12 12:39 UTC。
- **问题与创新：** 通用 VLM 迁移驾驶常被认为需重做结构和 3D 先验。该工作把缺口聚焦到 metric depth，以图像—深度—问答 triplet 进行非侵入式增量训练。
- **机制／结构：** 可训练主 VLM 接受驾驶适配；辅助深度流以显式几何约束视觉骨干；冻结 twin VLM 用 logit KL 保留通用语义。辅助分支部署时移除，作者称不增加推理开销。
- **实验与关键结果：** 摘要称在 3D 感知、驾驶语言推理、端到端规划和通用多模态四类基准超过既有驾驶 VLM，3D 表现接近专用模型；未披露绝对分数与闭环安全结果。
- **关注价值：** 将几何适配、通用能力保留和部署预算分开，适合检验驾驶 foundation-model 改造是否真有增益。
- **局限／跟进：** 深度传感／基础模型误差及天气域偏移可能传入主干；需做真实道路、尾延迟、指令冲突和失效降级评测。

## 机器人／具身智能

### 3. [ACE-CaP-0: Real-World Code-as-Policies in the Era of Experience](https://arxiv.org/abs/2611.16872)

- **作者／机构／提交：** ACE-CaP Team、Changxu Wei 等 28 位作者；arXiv 未列可核验机构；v1，2026-11-12 14:38 UTC。
- **问题与创新：** 反复调用大模型控制真机既慢又难复用。ACE-CaP-0 把人类演示按需请求、仿真按需验证和策略代码修订组合为获得可冻结物理技能的流程。
- **机制／结构：** agent 在采集经验时修订 Code-as-Policies；部署阶段用运行时感知与控制执行固定程序，无需人或 coding agent 持续在环。
- **实验与关键结果：** 八项真机操作（对齐、多物体、双臂）共 240 次试验中成功 221 次，即 **92.1%**；平均每任务 0.97—2.27 分钟。
- **关注价值：** 把一次性昂贵推理沉淀为可审阅、可版本化的程序，明确分离开发成本与重复执行成本。
- **局限／跟进：** 八项任务与程序化接口的覆盖有限；应报告修改历史、仿真筛选漏检、异常恢复、权限边界及跨硬件迁移。

### 4. [EgoX: Egocentric Cross-Embodiment Manipulation with Embodiment Dreaming](https://arxiv.org/abs/2611.16728)

- **作者／机构／提交：** Yaru Niu 等 22 位作者；arXiv 未列可核验机构；v1，2026-11-12 12:40 UTC。
- **问题与创新：** 人、不同真机和仿真角色的传感／动作接口不一致，直接混训易损失可控性。EgoX 以语义对应的观测与动作模态组织异构演示。
- **机制／结构：** MXT+ 为每类观测配专属 tokenizer、为每类动作配 expert，而共享 Transformer 主干；仅训练时的 Embodiment Dreaming 预测未来视觉和本体感觉 latent，使共享表征学习各本体动力学。
- **实验与关键结果：** 13 个任务—本体组合、五任务和六本体（五真机、一仿真人形）中，平均归一化任务进展由 0.63 升至 **0.80**；OOD 条件由 0.53 至 **0.77**。
- **关注价值：** 把跨本体扩展从“混更多数据”转成可检查的接口与未来状态一致性。
- **局限／跟进：** 任务进展不等同完成和接触安全；需分解各本体数据贡献、校准漂移、少样本目标机适配和失败动作代价。

### 5. [Inner Product Regularization for Imitation Learning](https://arxiv.org/abs/2611.17159)

- **作者／机构／提交：** Benjamin A. Christie、Tianyu Qiu、Amy H. Choi、David Fridovich-Keil、Dylan P. Losey；arXiv 未列可核验机构；v1，2026-11-12 17:39 UTC。
- **问题与创新：** 传统正则多在单一状态限制策略敏感性，未约束邻近状态对同一扰动的响应是否一致。InneR 用策略 Jacobian 诱导的状态内积学习共享的局部无效扰动子空间。
- **机制／结构：** 聚类内积对齐的状态、平均其几何并最小化最小特征值，可附加于确定性或随机模仿学习管线，而不直接压低策略表达能力。
- **实验与关键结果：** 仿真中对无关维度和 train/test shift 更稳健；三项真机机械臂任务中 diffusion policy 平均成功率由 **18% 提至 57%**，不增加数据。
- **关注价值：** 将鲁棒性从抽象范数变成“何种扰动本应被忽略”的局部结构，适合连接感知噪声和控制泛化。
- **局限／跟进：** 三任务样本较窄；Jacobian 近似、状态聚类与接触突变下的计算／安全边界仍待量化。

### 6. [Rethinking Actions: Continuity-Aware Priors for World-Model Planning](https://arxiv.org/abs/2611.16645)

- **作者／机构／提交：** Shaobo Yang、Zichen Ai、Ziyang Ma、Qian Yang、Bin Fang；arXiv 未列可核验机构；v1，2026-11-12 11:19 UTC。
- **问题与创新：** 世界模型规划通常泛化探索动作，而专家动作有时间连续结构。该工作从示范动作历史学习 continuation prior，而不是施加通用平滑惩罚。
- **机制／结构：** LG-DKGP 结合近期／长程历史的神经 continuation 和时间 GP 残差；以训练得来的探索尺度初始化候选，冻结世界模型评价目标进展。
- **实验与关键结果：** 五个仿真任务的 macro success 为 **87.07%**，对照 INTACT 71.03%、PRISM 61.66%、LeWM 58.66%。
- **关注价值：** 把动作先验与世界模型评价拆开，有助于定位长时规划收益来自搜索还是模拟器偏差。
- **局限／跟进：** 只给仿真结果；应检验示范质量改变、突发障碍、实时重规划开销及真机接触任务是否保留收益。

## 交叉方向：长期自治／记忆

### 7. [AstroMemBench: A Benchmark for Memory Systems in Embodied Spacecraft Agents](https://arxiv.org/abs/2611.16590)

- **作者／机构／提交：** You Wu、Guhong Zhang、Hongwei Li、Xinyue Hong、Yuan Jia；arXiv 未列可核验机构；v1，2026-11-12 10:23 UTC。
- **问题与创新：** 长时自治需要在通信延迟、资源约束和物理操作下使用历史，现有 memory 评测难以分辨真正状态利用。AstroMemBench 将这些要求映射为可执行挑战。
- **机制／结构：** 覆盖 16 个记忆子挑战、140 个模板、2,240 个实例和九类任务；确定性环境按完成度、状态变化、安全和资源使用评分，并含 session restart 条件。
- **实验与关键结果：** Mem0、Chain-of-Memory、LightMem、RAG 都提升同 session 分数，三种 memory 未明显超过 RAG；重启后 Mem0 比 RAG 高 **12.25 分**，收益偏向指令保留／结果复用而非持续状态与能量预留。
- **关注价值：** 明确 memory 何时有效、何时只是检索替代品，适用于所有断续运行的机器人系统。
- **局限／跟进：** 航天仿真不等价于实物故障与通信链路；需检查状态陈旧、错误记忆、资源模型真实性与跨任务迁移。

## 趋势总结

本期共同主题是把“可靠性”拆成可测接口：驾驶 VLM 需要以长尾视频反例和显式几何检验，而不是依赖流畅解释；具身策略则把可复用代码、跨本体模块、扰动不变结构和动作连续先验分别显式化；长期自治进一步要求把记忆的会话重启、状态保持和资源后果单独评测。下一步最值得追踪的是这些接口能否在真机／闭环、时延、接触失败和错误历史下保持收益。
# GitHub 开源趋势晨报｜2026-11-15

## 时间与证据口径

检索于北京时间 2026-11-15 06:00。排名与 `+N/日` 来自第三方镜像保存的 **2026-11-14 UTC GitHub Trending 日榜**（`collectedAt` 为 2026-11-14 21:07 UTC）；它是镜像的 `gained` 字段，不是本次总 star 相减。当前 star、主语言、许可证和用途由 GitHub Repository API 本次复核。镜像并非 GitHub 官方服务；走红原因和趋势结论均为编辑推断，star 不证明质量、安全或生产采用。

## 精选项目

### 1. [tradermonty/claude-trading-skills](https://github.com/tradermonty/claude-trading-skills)

- **数据：** API 当前 **4,751 stars**；日榜第 3、**+556/日**；Python；MIT。证据：[Repository API](https://api.github.com/repos/tradermonty/claude-trading-skills)、[日榜快照](https://githubtrending.today/api/archive/2026-11-14.json)。
- **确认用途：** 面向权益投资者／交易者的 Claude Code Skills，涵盖市场分析、技术图表、经济日历、筛选与策略开发。
- **走红原因（推断）：** 垂直领域把提示词、数据入口和重复步骤封装成可安装技能，比通用聊天更接近可重复工作流。
- **适合人群：** 想研究 Skill 组织方式的开发者；金融结论须独立复核数据来源、时效、回测偏差和合规性，不能按仓库输出交易。

### 2. [dream-num/univer](https://github.com/dream-num/univer)

- **数据：** API 当前 **24,435 stars**；日榜第 7、**+495/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/dream-num/univer)、[日榜快照](https://githubtrending.today/api/archive/2026-11-14.json)。
- **确认用途：** 可嵌入的 Office SDK，覆盖编辑、计算、协作与文件处理，面向人和 AI agent。
- **走红原因（推断）：** Agent 产品需要的不是只读文件解析，而是可编辑、可协作、可交付的文档／表格工件层。
- **适合人群：** 构建企业文档与表格功能的前端／平台团队；应审计公式兼容、协作冲突、文件转换、访问控制和数据留存。

### 3. [ag-ui-protocol/ag-ui](https://github.com/ag-ui-protocol/ag-ui)

- **数据：** API 当前 **17,325 stars**；日榜第 8、**+9/日**；TypeScript；MIT。证据：[Repository API](https://api.github.com/repos/ag-ui-protocol/ag-ui)、[日榜快照](https://githubtrending.today/api/archive/2026-11-14.json)。
- **确认用途：** 用于把 Agent 接入前端应用的 Agent—User Interaction Protocol。
- **走红原因（推断）：** Agent 从 CLI 走向产品界面后，状态、流式结果、审批和用户交接需要共享协议而非每个应用自行拼接。
- **适合人群：** 制作 agent-native Web 产品的团队；应先定义会话隔离、工具确认、失败重连和前端可见状态，避免协议层泄漏敏感上下文。

### 4. [ashhart/TensorFold](https://github.com/ashhart/TensorFold)

- **数据：** API 当前 **2,147 stars**；日榜第 9、**+53/日**；Zig；Apache-2.0。证据：[Repository API](https://api.github.com/repos/ashhart/TensorFold)、[日榜快照](https://githubtrending.today/api/archive/2026-11-14.json)。
- **确认用途：** 面向 Metal、CUDA 与 Vulkan 的 LLM inference engine。
- **走红原因（推断）：** 多后端、本地运行和推理成本仍是 Agent／AI 应用能否落地的底座，轻量系统实现持续受关注。
- **适合人群：** 评估跨硬件推理栈的系统工程师；要以目标模型、量化、显存、吞吐、尾延迟和数值一致性实测，不从 star 推断性能。

### 5. [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman)

- **数据：** API 当前 **120,017 stars**；日榜第 10、**+227/日**；Go；Apache-2.0。证据：[Repository API](https://api.github.com/repos/JuliusBrussee/caveman)、[日榜快照](https://githubtrending.today/api/archive/2026-11-14.json)。
- **确认用途：** 自述为 coding-agent 的 viral skill 与代理，声称可通过压缩表达减少 token。
- **走红原因（推断）：** 大量 Agent 使用者正在把成本控制从模型选型细化到提示、工具输出和上下文表达。
- **适合人群：** 研究 token 优化权衡的开发者；“65%”属项目自述，须用真实任务比较遗漏、工具调用失败、可读性和总成本。

### 6. [Tencent/LoopForge](https://github.com/Tencent/LoopForge)

- **数据：** API 当前 **861 stars**；日榜第 13、**+101/日**；Go；许可证 API 为 `NOASSERTION`。证据：[Repository API](https://api.github.com/repos/Tencent/LoopForge)、[日榜快照](https://githubtrending.today/api/archive/2026-11-14.json)。
- **确认用途：** 自托管 coding-agent 交付工作流，可编排 CodeBuddy、Codex、Claude Code、脚本和人工审批。
- **走红原因（推断）：** 团队需要把不同 coding harness 的执行、人工关口和交付脚本放到一个可见流程，而不只是替换模型。
- **适合人群：** 已有 CI／审批流程的工程平台团队；上线前要审查命令执行权限、密钥、隔离、审计记录和实际许可文本。

### 7. [we-promise/sure](https://github.com/we-promise/sure)

- **数据：** API 当前 **15,253 stars**；日榜第 12、**+659/日**；Ruby；AGPL-3.0。证据：[Repository API](https://api.github.com/repos/we-promise/sure)、[日榜快照](https://githubtrending.today/api/archive/2026-11-14.json)。
- **确认用途：** 面向个人财务的开源应用。
- **走红原因（推断）：** 个人生产力软件仍受社区欢迎，尤其是可自托管、可查看实现的日常数据工具。
- **适合人群：** 希望探索个人财务开源产品的用户与开发者；财务数据高度敏感，应审查同步方式、备份、部署安全和 AGPL-3.0 的网络服务义务。

## 技术趋势与社区偏好

11 月 14 日日榜把能力资产、交互协议、可编辑办公工件、推理底座和交付编排连成链：Skills 提供领域流程，AG-UI 暴露人机交接，Univer 提供成品工件，TensorFold 和 Caveman 分别面对算力／token 成本，LoopForge 将执行接回审批。社区热度显示 Agent 正从“生成答案”转向可治理的工作流基础设施；仍需逐项检查数据来源、写权限、凭据、许可证和基准复现。

## 证据链接

- [GitHub Trending 2026-11-14 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-14.json)：排名、快照总 star 与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：镜像采集和统计口径。
- 各项目当前元数据以上述 Repository API 为准；走红原因均为编辑推断。
