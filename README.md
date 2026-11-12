# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪最新 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-11-13

- [arXiv 独立报告](reports/2026-11-13/arxiv.md)

- [GitHub Trending 独立报告](reports/2026-11-13/github-trending.md)

- [分类趋势总结](CATEGORY_SUMMARY.md)

## 内容标准

每期 arXiv 报告按方向精选并说明问题、创新、机制、实验、价值和局限；GitHub 报告区分可核验元数据与编辑推断。归档位于 [`reports/`](reports/)。


# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-13

## 日期与证据口径

检索截至北京时间 2026-11-13 06:00。arXiv API 在 `cs.RO`、`cs.CV`、`cs.AI` 及关键词检索中最新可得相关 **v1** 批次仍为 **2026-11-10 UTC**；本期因此回溯该批、并与 11 月 10—12 日归档逐篇去重。下列六篇均为 11 月 10 日的新投稿，**不是 11 月 13 日的新稿**。作者、提交时间、方法和出现的数值来自 arXiv 元数据及摘要；元数据未给出可可靠核验的机构时不推断机构，摘要中的结果也不等于真实开放环境的安全保证。

## 自动驾驶／移动自治

### 1. [SIGMO: Sigmoid Gated Interaction-Aware Motion Planning](https://arxiv.org/abs/2611.14414)

- **作者／机构／提交：** Avinash Singh、Manish Saroya、Fatemeh Cheraghi Pouria、Faizan Tariq、Jovin D'sa、David Isele、Yosuke Sakamoto、Sangjae Bae；arXiv 元数据未列可核验机构；v1，2026-11-10 17:53 UTC。
- **问题与创新：** 窄路、多车并线和无信号路口需要判断谁让行；端到端策略往往难解释，规则又难随其他参与者行为变化。SIGMO 将周边体的让行倾向写成由物理交互特征驱动的多项式 sigmoid，而不是黑箱的单一社交评分。
- **机制／结构：** 解析式 yield score 捕捉速度、相对位置等驾驶直觉，再被置入 receding-horizon planner；规划器可接收任意轨迹预测，因此将交互评分与预测器解耦。
- **实验与关键结果：** 作者在高交互仿真和硬件实验中验证其能在主动与防御间平衡，且计算开销较轻；摘要未给出统一成功率、碰撞率、实时延迟或与各基线的完整数表。
- **关注价值：** 显式的让行接口便于诊断“冻结”或过度激进，适合作为端到端候选打分之外的可解释安全层。
- **局限／跟进：** 解析特征的跨城市、异质交通参与者和预测失配鲁棒性尚未量化；应报告最坏时延、误判让行的伤害代价和真实交通长尾案例。

### 2. [RiSE-Drive: Risk-Sensitive Long-Horizon Candidate Evaluation for End-to-End Autonomous Driving](https://arxiv.org/abs/2611.13790)

- **作者／机构／提交：** Yu Zhao、Hongyi Duan、Ming Yin、Hongyuan Zhang、Fan Yang、Hongzhi Wang、Xiubo Liang；arXiv 元数据未列可核验机构；v1，2026-11-10 09:22 UTC。
- **问题与创新：** 多轨迹系统的瓶颈逐渐从“生成候选”转为“在不确定未来下评价候选”；点分数会掩盖迟发失败和尾部风险。RiSE-Drive 将候选评价改为候选条件的长时 latent rollout 上的结果分布评估。
- **机制／结构：** 对每个候选生成未来表征 rollout，估计长时结果分布而非单标量，并按 tail-risk-aware、扰动鲁棒的准则排序，从名义最优转向对安全关键偏差更稳的选择。
- **实验与关键结果：** 摘要称其在 NAVSIM-v1、NAVSIM-v2 和闭环 HUGSIM 上达到 SOTA，并显著提高候选选择鲁棒性；未披露可在摘要中复核的分数、置信区间或安全事件绝对数。
- **关注价值：** 与生成式规划兼容，直接瞄准候选覆盖已足够后仍会“选错”的长时风险问题。
- **局限／跟进：** rollout 分布质量决定排序上限；需检验稀有交互、感知退化、模型失校准时的尾险估计，以及采样预算和车端延迟。

## 机器人／具身智能

### 3. [From Video Frames to Robot Meta-Frames: A Unified Latent Interface for World Action Models](https://arxiv.org/abs/2611.14365)

- **作者／机构／提交：** Guoqiang Liang、Yiqi Lin、Yanzhe Chen、Kevin Yuchen Ma、Mike Zheng Shou；arXiv 元数据未列可核验机构；v1，2026-11-10 17:21 UTC。
- **问题与创新：** 预训练视频扩散模型的 latent 先验主要来自自然视频；把动作、本体感觉和值函数逐项塞进额外 frame 或编码器会产生分布失配。MetaWAM 用冻结去噪器的相对重建误差诊断此失配，并提出单一 meta-frame 接口。
- **机制／结构：** 每一种机器人信号占用不相交的频域通道，经逆 DCT 提升为空间 latent；固定 band layout 和 slot-aware routing 令同一 frame 同时服务 policy、world model 与 value 预测，无新增模块。
- **实验与关键结果：** 摘要报告 RoboCasa 成功率 68.9%，相对逐信号 frame 的方案将推理时延降低 39%；三个真实 Franka 任务为 85.0% 成功率。代码和模型链接由作者提供。
- **关注价值：** 将多模态条件注入从“格式选择”变成可测的预训练分布对齐问题，为复用视频模型提供轻量工程路径。
- **局限／跟进：** 频带划分可能限制变量数、动态范围与跨机器人泛化；真机仅三任务，需报告任务数、重复次数、故障恢复和视觉干扰下的收益。

### 4. [From Prediction to Action: Learning Physical Context for Deformable Linear Object Manipulation](https://arxiv.org/abs/2611.14274)

- **作者／机构／提交：** Chengxiao Dong、Alessio Caporali、Hongyu Lan、Gianluca Palli；arXiv 元数据未列可核验机构；v1，2026-11-10 16:17 UTC。
- **问题与创新：** 能更准预测绳索等可变形线状物响应的表示，不一定更利于选动作。论文把 predictive utility 与 decision utility 分开检验，并给出 Geometry-Pointer-Flow（GPF）这一抓取点选择和抓后运动生成分离的骨干。
- **机制／结构：** 在统一 GPF 上比较真实物理参数、估计参数和交互历史；前者服务下一步形状预测，后者作为动作条件上下文。训练全部在仿真完成，直接零样本迁移真机。
- **实验与关键结果：** geometry-only GPF 相对 DLO diffusion policy 将一步执行形状误差降 32.8%，参数少 18.7 倍、推理约快 193 倍；470 对仿真试验中，交互历史再降执行误差 9.9%，而估计物理参数虽更利于预测却未带来可检测的控制增益。作者称闭环和零样本硬件也以历史表示最佳。
- **关注价值：** 给 world model/物理表示一个更严格的评估原则：不要只看预测误差，要看它是否改善实际决策。
- **局限／跟进：** 平面单抓取和仿真训练限制较强；需扩展到多接触、遮挡、材料突变和更复杂的真实操作，并公布硬件成功率与方差。

## 交叉方向：SLAM／长期自治

### 5. [GEMOR-GS: Global Extrinsic-calibration-refined Mapping and Online Relocalization for 3D Gaussian-Splatting SLAM](https://arxiv.org/abs/2611.13528)

- **作者／机构／提交：** Yuchen Yang、Ming Ding、Xinyu Wu、Hesheng Wang；arXiv 元数据未列可核验机构；v1，2026-11-10 03:51 UTC。
- **问题与创新：** LiDAR—惯性—视觉 SLAM 要同时保证可渲染地图的度量一致性和跟踪丢失后的可重入。GEMOR-GS 将离线外参校准、全局 Gaussian 重建和在线重定位串成一个生命周期。
- **机制／结构：** 先在专用标定段直接对齐估计 LiDAR—相机外参；随后交替优化关键帧位姿与 Gaussian 参数，目标结合门控可微渲染和 LiDAR 投影；失跟后经 XFeat bypass map、RANSAC-PnP 粗定位及 Gaussian RGB-D warp refinement 返回地图。
- **实验与关键结果：** 一条自采和五条公开序列上，离线图在配对关键帧比在线图高 14.3–19.9 dB，较 Gaussian-LIC2 的 PSNR 约高 9 dB；留出重定位成功率 86–100%，且与外参质量相关。
- **关注价值：** 不只追求 3DGS 的视觉质量，也把“离开后重回地图”作为长期自治的明确能力指标。
- **局限／跟进：** 离线标定段是部署前提，指标可能受数据与渲染条件影响；应测试外参随时间漂移、动态场景、夜间天气和端侧显存/回环延迟。

### 6. [Persistent Metric-Semantic Maritime Scene Memory from Open-Vocabulary 3D Scene Graphs](https://arxiv.org/abs/2611.13903)

- **作者／机构／提交：** Kim Alexander Christensen、Dina Zimmermann、Martin Steinert、Eleni Kelasidi；arXiv 元数据未列可核验机构；v1，2026-11-10 10:59 UTC。
- **问题与创新：** 开放词汇 3D 场景图主要在室内/陆地验证；海上重复航行时，物理实体碎片化和“地点/海域”抽象不足。该工作研究迁移失败，并在保留底层 mapper 的前提下补上持续场景记忆。
- **机制／结构：** 先汇总证据作 metric-semantic consolidation，再用几何支撑的多视图 VLM 把残余碎片对齐为实体、将观测归并为局部地点；并利用地图先验、水面和结构观测构造宏观海域，再关联地点。
- **实验与关键结果：** 作者称零样本户外 3DSG 对其数据中大多数有几何证据的物体与标注一致；后处理比基线及仅 consolidation 都更少实体碎片，能跨重复航行对应固定地点，并提升所审阅查询的上下文检索。摘要未提供具体百分比。
- **关注价值：** 将长期记忆的对象身份、地点重识别和大尺度空间层次拆开处理，对港口、海上机器人等稀疏视觉环境有参考价值。
- **局限／跟进：** VLM 聚合可能引入幻觉，海况与季节变化的稳定性未量化；需开放更大规模标注、测量错误合并/拆分代价和实时资源消耗。

## 趋势总结

这批回溯论文共同强调“预测不是终点，而是接口选择”。SIGMO 和 RiSE-Drive 将交互/风险写入候选决策；MetaWAM 让视频先验能容纳机器人信号；GPF 证明最准物理预测未必最利于控制；GEMOR-GS 与海事情景记忆则把长期自治拆成可校准、可重定位、可维持实体身份的状态。后续应特别看这些显式接口在传感错误、时延和环境变化下是否仍能改善真实闭环决策。


## 时间与证据口径

# GitHub 开源趋势晨报｜2026-11-13

## 时间与证据口径

检索于北京时间 2026-11-13 06:00。`+N/日` 和排名来自第三方镜像保存的 **2026-11-12 UTC 日榜**（采集于 2026-11-12 21:07 UTC），是其记录的 GitHub Trending `gained`，并非本次总 star 的相减值；当前 star、主语言、许可证和项目自述以 GitHub Repository API 于 2026-11-12 22:03 UTC 前后的复核为准。镜像非 GitHub 官方服务。用途为仓库自述可确认信息；走红原因和趋势结论均为编辑推断，star 不证明质量、安全或生产采用。

## 精选项目

### 1. [GoogleChrome/modern-web-guidance-src](https://github.com/GoogleChrome/modern-web-guidance-src)

- **数据：** API 当前 **2,767 stars**；日榜第 1、**+799/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/GoogleChrome/modern-web-guidance-src)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** 仓库自述为“让 coding agent 保持最新 Web 最佳实践”的指导源码。
- **走红原因（推断）：** Agent 写前端时，团队更愿意把规范作为可版本化上下文，而不是依赖一次性提示词。
- **适合人群：** 维护前端工程规范或 Agent 上下文的团队；须按版本审阅内容、兼容性和许可，不能把组织归属当作质量保证。

### 2. [openai/codex-security](https://github.com/openai/codex-security)

- **数据：** API 当前 **12,349 stars**；日榜第 2、**+663/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/openai/codex-security)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** 用于发现、验证和修复安全漏洞的 Codex Security CLI 与 TypeScript SDK。
- **走红原因（推断）：** 当 Agent 能产生和修改代码时，扫描、验证、修复的闭环成为把自动化接入工程流程的必要配套。
- **适合人群：** 工程和安全团队；先在隔离仓库以只读扫描验证误报、数据边界和自动修复审批。

### 3. [QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)

- **数据：** API 当前 **29,754 stars**；日榜第 6、**+151/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/QwenLM/qwen-code)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** 项目自述为运行在终端中的开源 AI coding agent。
- **走红原因（推断）：** 终端仍是最贴近仓库、测试和版本控制的 Agent 入口；开源可部署性对希望保留模型/凭据选择权的开发者有吸引力。
- **适合人群：** 已有测试、审阅和最小权限沙箱的开发者；不要把工作区写权限、shell 命令或密钥暴露给未审阅任务。

### 4. [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)

- **数据：** API 当前 **116,617 stars**；日榜第 9、**+812/日**；JavaScript；MIT。证据：[Repository API](https://api.github.com/repos/addyosmani/agent-skills)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** 面向 AI coding agent 的 production-grade engineering skills 集合。
- **走红原因（推断）：** 热度延续表明团队在把设计、审阅与交付约束沉淀成版本化技能资产，而非仅扩展模型提示。
- **适合人群：** 想标准化 Agent 工作流的平台与应用工程师；每个 Skill 都应视作依赖，逐项审阅脚本、网络访问、数据输入和许可证。

### 5. [meta/astryx](https://github.com/meta/astryx)

- **数据：** API 当前 **26,413 stars**；日榜第 10、**+1,789/日**；TypeScript；MIT。证据：[Repository API](https://api.github.com/repos/meta/astryx)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** 可高度定制、面向 Agent 的开源 design system。
- **走红原因（推断）：** UI Agent 的关注点正从“生成一个页面”转向可编辑、受 design token 约束并能回到团队组件体系的工件。
- **适合人群：** 已有设计系统的前端团队；先验证无障碍、主题、组件版本迁移和生成代码的审阅流程。

### 6. [CopilotKit/OpenBot](https://github.com/CopilotKit/OpenBot)

- **数据：** API 当前 **11,522 stars**；日榜第 11、**+291/日**；TypeScript；MIT。证据：[Repository API](https://api.github.com/repos/CopilotKit/OpenBot)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** 提供带浏览器、文件和工具的开源 AI coworkers；自述称每项行动会在执行前决定、执行后记录，并可接入 AG-UI agent。
- **走红原因（推断）：** “可执行 Agent”开始把行动前计划与行动后记录作为产品面的一部分，回应可观察性和责任追踪诉求。
- **适合人群：** 构建内部任务自动化的团队；应隔离会话与凭据、设置工具 allowlist，并对发布、支付、删除等不可逆动作加确认。

### 7. [ggml-org/llama.cpp](https://github.com/ggml-org/llama.cpp)

- **数据：** API 当前 **134,501 stars**；日榜第 13、**+287/日**；C++；MIT。证据：[Repository API](https://api.github.com/repos/ggml-org/llama.cpp)、[日榜快照](https://githubtrending.today/api/archive/2026-11-12.json)。
- **确认用途：** C/C++ 实现的大模型推理项目。
- **走红原因（推断）：** 与 Agent 应用层的增长并列出现，说明本地/可控推理仍是成本、隐私和离线部署的底层需求。
- **适合人群：** 需要自托管或边缘推理的开发者；按目标硬件、量化质量、吞吐/延迟和模型许可证做基准，避免仅以 star 选择运行时。

## 技术趋势与社区偏好

本期热点从上到下形成一条可部署 Agent 链：Modern Web Guidance 与 Skills 提供版本化约束，Qwen Code 和 OpenBot 提供终端/工具执行，Astryx 固化可编辑 UI 工件，Codex Security 补上验证，llama.cpp 保留本地推理选择。社区偏好已不只是“会调用模型”，而是规范、执行权限、可观测记录和可控运行时的组合；安装或接入前仍应优先审计供应链、写权限、凭据、数据留存和许可证。

## 证据链接

- [GitHub Trending 2026-11-12 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-12.json)：排名、快照总 star 与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：镜像采集和统计口径。
- 各项目当前元数据以上述 Repository API 为准；走红原因均为编辑推断。
