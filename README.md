# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-11-18

- [arXiv 独立报告](reports/2026-11-18/arxiv.md)
- [GitHub Trending 独立报告](reports/2026-11-18/github-trending.md)
- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-18

## 日期与证据口径

检索截至北京时间 2026-11-18 06:00。最新相关 v1 为 **2026-11-16 UTC**；以下七篇均为该批新稿，**不是 11 月 18 日投稿**。作者、提交时间、方法和数字来自 arXiv 元数据及摘要；机构未在元数据中可靠逐一核验时不作推断，实验数字均为作者报告、未独立复现。

## 自动驾驶／移动自治

### 1. [FlowRow: Learning Navigation Behaviors in Agricultural Environments with Long-Horizon Goal-Conditioned Flow Matching Policies](https://arxiv.org/abs/2611.21035)

- **作者／提交：** Utkarsh Bajpai、Cédric Pradalier、Stéphanie Aravecchia；v1，2026-11-16。
- **问题、创新与机制：** 果园和葡萄园机器人可沿行驶，但跨行、转弯常依赖预先标定的田块几何与手调动作。FlowRow 将远期目标写为机器人坐标系中的相对目标，以深度观测和目标条件化 flow-matching 生成 SE(2) 局部路径；同时给出包含葡萄、柠檬、苹果园共 900 个 episode 的 RowNavBench。
- **实验与关键结果：** 在该基准上报告 **87%** 成功率，按相同演示重训的最强生成式行为克隆为 **44%**。
- **关注价值／局限与跟进：** 将“田间任务目标”而非固定行间模板作为规划接口，适合长周期巡检与作业；但仿真作物几何、深度失效、泥泞/打滑、人员车辆混行及真实机车的恢复代价尚未覆盖。

### 2. [Polygraph: Large-Scale Multi-Session Trajectory Optimization using Pose Graphs](https://arxiv.org/abs/2611.21163)

- **作者／提交：** Petar Lukovic、Tian Yi Lim、Marc Pollefeys、Pablo Speciale、Hermann Blum、Zuria Bauer；v1，2026-11-16。
- **问题、创新与机制：** 重复通行的车、机器人或穿戴设备各自产生局部准确但坐标系不一致的轨迹；离线全局融合既需要所有 session 到齐，也易吸收错误回环。Polygraph 不建完整 3D 图，逐关键帧/局部簇在线处理；以图像检索提出跨 session 候选，再用稀疏匹配、单目米制深度与鲁棒位姿估计验证，并以双层共识门和增量图优化接纳约束、周期性批优化剔除外点。
- **实验与关键结果：** 覆盖立体户外驾驶、HoloLens/iPad 室内、Spot 足式行走及户外手持路线；作者报告在同 GPU 对照的既有结果上更快、接纳更少回环边且精度持平或更好，摘要未给统一绝对误差表。
- **关注价值／局限与跟进：** 适合把长期定位的“何时相信跨日重访”变成可审计图边；应补充跨季节外观变化、检索漏召回、时间戳/尺度漂移、在线内存上界和错误边误接入后的闭环导航风险。

## 机器人／具身智能

### 3. [ScaleVLA: Scaling Vision-Language-Action Models to 552 Billion Parameters](https://arxiv.org/abs/2611.21607)

- **作者／提交：** Ruixi Yu、Dairu Liu、Xuchuan Chen、Zekun Qi、Zekai Li 等（含 He Wang、Li Yi）；v1，2026-11-16。
- **问题、创新与机制：** 大型视觉语言模型的广泛知识常未被充分转为机器人动作能力。ScaleVLA 把 **552B DeepSeek-V4.1-Flash** 视觉语言骨干接入可训练 action DiT，并在 2B–552B 统一训练设置下拆测样本效率、泛化与精细接触操作。
- **实验与关键结果：** 仅 **10** 条演示即超过 2B 骨干用 50 条演示的结果（**87.8% vs. 85.6%**）；LIBERO-PRO **45.1%**、小模型最高 **31.3%**；真实充电器插入 **9/10**、基线 **4/10**；每 action chunk 中位延迟 **216 ms**。
- **关注价值／局限与跟进：** 说明超大预训练表示可能以较少演示改善接触对齐；但单一延迟统计未涵盖尾延迟、云/本地部署成本、故障回退、任务分布偏差及大模型在真实场景的安全审计。

### 4. [Lazy-MOSAIC: Accelerating Skill-Centric Manipulation Planning with Learned Skill-Effect World Models](https://arxiv.org/abs/2611.21517)

- **作者／提交：** Itamar Mishani、Mukund Krishnakumar、Oren Salzman、Maxim Likhachev；v1，2026-11-16。
- **问题、创新与机制：** 长程操作的技能序列和参数空间很大，逐候选跑高保真物理仿真代价高。Lazy-MOSAIC 先用毫秒级 learned skill-effect world model 预测技能可行性与结果状态，在假设结果上搜索；仅对有希望的候选调用昂贵仿真，假设被推翻时只修补受影响的搜索部分，最终计划仍逐技能经仿真验证。
- **实验与关键结果：** 杂乱货架取物难度阶梯和一台真机演示中，作者报告相较基线规划显著更快、仿真查询更少，且各设置成功率持平或更高；摘要未列逐任务数值。
- **关注价值／局限与跟进：** 把学习模型限定为“筛选/提出假设”，保留高保真验证作为提交门；需测 learned effect 的校准、假阴性导致的解空间漏失、现实接触与仿真错配，以及重规划尾时延。

### 5. [ForceHarness: Turning Force into Action and Physics for Frozen Frontier Models](https://arxiv.org/abs/2611.21099)

- **作者／提交：** Ke Sun、Kevin Yuchen Ma、Yike Zhang、Yanzhe Chen、Mike Zheng Shou；v1，2026-11-16。
- **问题、创新与机制：** 冻结、API 形式的多模态模型看不见接触力，且其决策速率慢于力变化。ForceHarness 先由腕力传感器或关节力矩标定手端力，再以会自终止的力原语在模型下方闭环；物理翻译层把力轨迹转为带不确定性的物理量回传，而非直接喂原始力序列。论文另建含隐藏物理变量的七任务 HiddenPhys。
- **实验与关键结果：** 无腕力传感器真实机械臂上，GPT-6 Astra 零样本成功率 **3.3%→90.0%**；ForceBench +**17.5** 个百分点、HiddenPhys +**34.3** 个百分点，并称后者匹配手写专家控制器。
- **关注价值／局限与跟进：** 为闭源/冻结模型提供“慢推理—快接触”分层接口；力标定、传感器漂移、原语的故障安全、模型产生错误高层意图和 API 时延仍可能造成风险，须报告碰撞/超力尾部事件而非只给成功率。

### 6. [WinDEX: Metric 3D Hand Motion Reconstruction in the Wild for Dexterous Teleoperation and Policy Learning](https://arxiv.org/abs/2611.21143)

- **作者／提交：** Hongyu Ma、Hairong Qu、Shiqi Zhao、Yongsong Yang、Kai Shi 等；v1，2026-11-16。
- **问题、创新与机制：** 野外人手视频难以低成本生成米制、时序连续的灵巧操作监督。WinDEX 将几何—时间优化、双鱼眼校准立体视觉和视觉惯性 SLAM 合并为世界坐标手部标注；以模型辅助标注—再训练形成数据飞轮，并提供离线与因果流式蒸馏模型及 CyberCap 采集装置。
- **实验与关键结果：** WinDEX-Hand 含 **1,000 小时**训练标注；离线 **43.61 FPS**、流式 **171 FPS**；留出集投影误差 **14.5 px**、世界坐标关节误差 **37.29 mm**；以其动作参考训练的 RL 策略任务成功率为 WiLoR/HaWoR 的 **7.6×/3.6×**。
- **关注价值／局限与跟进：** 连接低成本人类动作采集、实时遥操和策略学习；数据授权、相机/IMU 标定漂移、遮挡接触、手—物尺度误差及由重建误差导致的危险控制命令需在真实机器人上单独量化。

## 交叉方向：多智能体安全／实时世界动作模型

### 7. [Distilling Safety Filters for Filter-free Multi-agent RL](https://arxiv.org/abs/2611.19190)

- **作者／提交：** Srikar Babu Gadipudi、Somayeh Sojoudi、Claire J. Tomlin；v1，2026-11-14 06:11 UTC（为补足多智能体安全主题的最近两日回溯，非 11 月 16 日新稿）。
- **问题、创新与机制：** 多机器人 CBF 安全过滤器的集中约束随团队规模二次增长，而过滤器又掩盖了策略本应学习的危险代价。方法用 implicit Q-learning 只学习已执行的安全动作，并在合成近碰撞状态蒸馏过滤器；理论上将蒸馏损失与安全裕度违反、部署碰撞概率相连。
- **实验与关键结果：** 仅局部观测且部署时无过滤器，在 **1,800** 个多智能体测试 episode 无碰撞；三智能体训练零样本迁至二十台、每体计算常数，至八台保持无碰撞；另在最多五台 Crazyflie 同飞测试。
- **关注价值／局限与跟进：** 用可扩展策略替代运行期集中优化，有利于车队/无人机密集协同；覆盖部署状态是理论前提，现实通信丢失、定位误差、非合作参与者和未覆盖近碰撞仍须由运行期独立安全层或保守退化补偿。

## 趋势总结

- **把大模型降到可验证的动作接口：** ScaleVLA 追求表示规模，ForceHarness 将接触闭环放在冻结模型下方，Lazy-MOSAIC 又把世界模型限定为搜索筛选器；后续应一起报告模型错误、验证门覆盖与 p95 决策时延。
- **长期自治依赖可回查状态而非单次感知：** Polygraph 的跨 session 图边和 WinDEX 的世界坐标动作监督均强调来源、尺度和时序；长期运行还需测外观变化、漂移累积与错误状态写入后的恢复。
- **安全扩展要同时降低集中计算与物理风险：** FlowRow、过滤器蒸馏都把特定环境/团队约束编入策略，但仿真高成功率不能替代对未覆盖状态、通信和真实接触异常的保守回退。

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

## 内容标准与归档

每期 arXiv 按问题、创新、机制、实验、价值和局限选篇；GitHub 区分可核验元数据与编辑推断。历史文件位于 [`reports/`](reports/)，跨期判断见 [分类趋势总结](CATEGORY_SUMMARY.md)。
