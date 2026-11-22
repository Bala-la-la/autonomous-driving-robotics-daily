# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-11-23

- [arXiv 独立报告](reports/2026-11-23/arxiv.md)
- [GitHub Trending 独立报告](reports/2026-11-23/github-trending.md)
- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-23

## 日期与证据口径

检索截至北京时间 2026-11-23 06:00。11 月 21—23 日为周末，arXiv 没有常规新公告；本期明确回溯至 **2026-11-19 UTC（11 月 20 日公告）v1**，精选 **6** 篇未在 11 月 21—22 日入选的论文，并不将其表述为当日新稿。题目、作者、提交时间、摘要中的方法和数字来自 arXiv API 与论文摘要页；机构未在可核验元数据中完整披露时标作“未完整披露”，不作推测。所有指标均为作者报告，未独立复现。

## 自动驾驶／移动自治

### 1. [ZeroVLN: Learning to Navigate without Supervised Fine-Tuning of the VLM Brain](https://arxiv.org/abs/2611.26414)

- **作者／机构／提交：** Zixuan Huang、Yang Zhou、Guli Zhang 等；机构未完整披露；v1，2026-11-19 17:01 UTC。
- **问题：** 连续视觉语言导航（VLN-CE）常把 VLM 主干微调到输出几何目标，可能损伤通用视觉能力，也让高层语义判断与低层连续控制耦合在同一模型里。
- **创新：** 以零导航域 SFT 保留 VLM “大脑”，改用自然语言语义 tool-call 接口连接慢速决策与快速动作专家，再用闭环 RL 联合磨合两层。
- **机制／结构：** VLM 只产生诸如移动意图的语义调用；动作专家先学习将调用落为连续控制。随后慢层的调用决策和快层执行在相同导航 episode 上共同 RL 优化，避免让大脑直接回归几何 waypoint。
- **实验与关键结果：** 作者报告在标准 VLN-CE 基准上优于代表性、经 SFT 的分层方法，同时 VLM 权重变化很小、通用能力大体保留；摘要未给出逐基准绝对成功率，需以正文表格核验。
- **关注价值：** 为车端/移动机器人提供“语义计划—连续控制”的可替换接口：高层模型可升级或换供应商，动作层仍能单独验证与训练。
- **局限／跟进：** 语义调用的歧义、动作专家的跨场景泛化及极端安全约束尚未量化；没有导航域 SFT 不等于不依赖导航数据（仍使用 episode 做 RL）。

### 2. [Planning to Stop: Factored Certification and Terminal Repair for Noncircular Robots](https://arxiv.org/abs/2611.26167)

- **作者／机构／提交：** Runtian Zheng、Congpeng Zhang、Ying Liu；机构未完整披露；v1，2026-11-19 14:19 UTC。
- **问题：** 狭窄空间导航不仅要找到无碰路径，还要在不确定性下让非圆形车体完整停入目标区域；“存在路径”与“可证明到达并停住”是不同问题。
- **创新：** 提出 GeoDiff，把原目标的 stopped-set 包含、见证（witness）引导的终端修补与可复用的分解证明编译结合，显式把终点可停性纳入规划验收。
- **机制／结构：** 用精确的可行平移表征定位终端修补，按请求局部复用证明工作；编译层将路径及终端条件转换为可检验证书，并分别统计发射器节省与求解器覆盖度。
- **实验与关键结果：** 在 11,440 个平面图派生任务中，5 cm 容差、15 秒预算下认证 **61/139**，高于 stopped-set 基线的 **44/139**；BARN 派生 Jackal 任务中为 **202/270**，对比 portal 基线 **3/270**。外部证书适配器只认证 13/139，显示路线可得与认证能力并不等价。
- **关注价值：** 适用于配送车、轮式巡检与泊车式移动操作：把“能到”升级为可审计的“能安全停住”。
- **局限／跟进：** 认证覆盖率仍非全量，且重点是几何/终端证明；动态人群、感知误差的在线置信界和实车紧急制动模型需要并入。

## 机器人／具身智能

### 3. [One Prior, Two Dynamics: Repurposing Video Diffusion Transformers for Self-Supervised Latent Action Learning](https://arxiv.org/abs/2611.26617)

- **作者／机构／提交：** Yuxin Jiang、Wenqiang Sun、Jiaqi Li 等；机构未完整披露；v1，2026-11-19 18:58 UTC。
- **问题：** 无动作标签视频能提供状态变化，却难揭示引起变化的控制；从头学习逆动力学和前向动力学又浪费已有视频生成模型的世界先验。
- **创新：** O²LaF 将同一个预训练 Video DiT 分别适配成逆动力学编码器和因果、动作条件的视频生成器，在紧凑动作瓶颈上端到端对齐两种动力学。
- **机制／结构：** 逆模型为前馈转移编码器，使用可学习 action queries 从相邻视觉状态抽取潜动作；前向模型仅访问过去，生成动作条件的未来视频。信息可见性约束阻止前向泄漏，再以联合优化让离散/潜在动作同时解释变化与预测后果。
- **实验与关键结果：** 作者称其在导航与操作的少样本 action probing 上达到新 SOTA，并增强跨视觉环境、跨形态的零样本动作迁移；还将先验替换为 V-JEPA2，获得有竞争力表现。摘要未给出具体分数，需查正文协议后横比。
- **关注价值：** 可把互联网视频预训练转化为机器人动作表征，而不必先收齐动作标注；同时把“会辨动作”和“会预测后果”绑定，利于世界模型落地。
- **局限／跟进：** 潜动作未必与真实可执行控制一一对应；视频的相机运动、遮挡及不可观测接触力会造成错误因果归因。

### 4. [Mind2Act World: A Diagnostic Benchmark for Embodied Mind, Physical Action, and Mind-Action Composition in Robotic Manipulation](https://arxiv.org/abs/2611.26444)

- **作者／机构／提交：** Yuzhi Huang、Jie Wu、Fanding Huang 等；机构未完整披露；v1，2026-11-19 17:15 UTC。
- **问题：** 单一成功率无法区分机器人是推理、精确执行，还是把两者通过环境反馈组合时失败。
- **创新：** 提供 Mind、Act、Mind2Act 三视角诊断：分别测历史状态决策、及时精确动作和闭环组合，并为失败 episode 归因。
- **机制／结构：** 基准含 **30** 个仿真操作任务、**5** 个应用域，每项有 **3** 级难度与 Clean/Random 两种场景，共 **180** 个配置；诊断 harness 为多模态 Agent、VLA、WAM 输出 Mind/Act/组合失败画像。
- **实验与关键结果：** 最强受测 Agent 在 Mind 为 **52.7%**、Act 为 **39.0%**，但组合后的 Mind2Act 仅 **12.0%**。分析显示 Agent 较能保留任务状态却难维持接触，端到端策略则反过来。
- **关注价值：** 让“模型分数不错但真机长程失败”有可定位的测试语言，特别适合选择要补记忆、接触控制还是闭环编排的团队。
- **局限／跟进：** 仍是仿真且任务构造会影响归因；与真机延迟、柔性物体和传感噪声的一致性需进一步验证。

### 5. [HumanCOIN: A 12,500-Hour Dataset for Human Intent in Egocentric Manipulation](https://arxiv.org/abs/2611.26434)

- **作者／机构／提交：** Shihan Wu、You Liu、Chunyu He 等；机构未完整披露；v1，2026-11-19 17:09 UTC。
- **问题：** 常见第一视角数据将“观测—动作”当作最小单元，意图如何形成、何时转成动作不可见，难学习早期预测和可解释协作。
- **创新：** 构建以意图通路为中心的 **12,500 小时**数据集，将注视、肌电与脑电作为由注意到用力再到认知准备的分层 proxy。
- **机制／结构：** L1 由头戴相机推断注视（**10,000 h**），L2 加入表面 EMG（**2,000 h**），L3 加入 EEG（**500 h**）；三层逐级继承低层信号，并提供多视角 RGB、深度、点云、头腕 6DoF、步骤级动作/物体标注与时钟/标定信息。
- **实验与关键结果：** 覆盖 **38** 类场景和超过三个采集层级；其核心结果是数据规模与同步标注能力，而非已报告的单一策略胜率。作者提供项目页供后续基准使用。
- **关注价值：** 为预测“手还没动之前的下一意图”、共享控制和人类演示预训练提供比纯视频更早的监督信号。
- **局限／跟进：** 部分注视为视频推断而非全量眼动真值，EMG/EEG 设备佩戴可能改变自然行为；跨人群、跨文化任务的偏差及隐私治理应被单独审查。

## 交叉方向：无人机采集与三维重建

### 6. [AGE-Capture: Autonomous, General, and Efficient UAV Capture for High-Fidelity Scene Reconstruction](https://arxiv.org/abs/2611.26048)

- **作者／机构／提交：** Xiaofeng Jin、Ningbo Bu、Matteo Frosi 等；机构未完整披露；v1，2026-11-19 12:55 UTC。
- **问题：** UAV 高保真重建不能只挑“看起来有价值”的视点，还需在传感器不同、飞行资源有限时判断何时采够、如何减少等待和重复拍摄。
- **创新：** AGE-Capture 用轻量在线状态把重建可渲染性、任务进度、视点效用和传感器自适应统一，并在真实飞行闭环中验证。
- **机制／结构：** 通过统一 camera-ray 接口解耦几何探索和重建观测，使 RGB 与不同测距传感器共用管线；reconstruction-frontier 估计剩余价值与自主终止，动力学感知分层规划配合异步事件驱动采集削减跨区移动和计划等待。
- **实验与关键结果：** 在 **10** 个室内外仿真场景，作者报告相对在线基线 PSNR 高 **3.30–3.53 dB**，只用平均 **58.2%** 的共同任务时间预算，峰值 GPU 内存低 **91.0–93.3%**；并在 **9** 个真实场景完成机载闭环飞行。
- **关注价值：** 将主动感知从“选点算法”扩展到可停止、可换传感器、能受飞行学约束的完整采集运行时，对测绘、巡检和灾后建模直接相关。
- **局限／跟进：** 真实场景数量有限，极端风、GNSS 拒止、动态目标和安全禁飞边界下的鲁棒性/失效恢复尚未给出。

## 趋势总结

- **“中间接口”正替代端到端硬耦合：** ZeroVLN 的语义 tool-call、O²LaF 的潜动作瓶颈、Mind2Act 的诊断分层，都把推理、执行和环境反馈拆成可替换、可测量的部件。
- **移动自主从找路线走向可验证的终态与任务完成：** GeoDiff 把停住的证明写入规划，AGE-Capture 把采够的判断写入主动重建；工程验收正在关心停止条件、证书覆盖与资源预算，而非单纯轨迹存在性。
- **数据和基准开始追问动作之前与动作之后：** HumanCOIN 将意图形成过程显式化，Mind2Act 则揭示单项能力不能自动组合为闭环能力；下一阶段的 VLA 训练将更需要过程态监督和组合故障诊断。

# GitHub 开源趋势晨报｜2026-11-23

## 时间与证据口径

检索于北京时间 2026-11-23 06:00。GitHub Trending 的官方页面是动态页面，日榜 `+N` 采用 [githubtrending.today](https://githubtrending.today/methodology/) 保存的 **2026-11-16—22 UTC** 日榜归档；这些是各快照采集周期的增星，不能等同于本地两次轮询差值。当前总 star、语言、许可证、创建时间和仓库自述均以本次 GitHub Repository API 查询为准。为避免重复，排除了最近多期已选的 Superpowers、CLI-Anything、Cursor plugins、Firecrawl、OpenVINO、Stitch Skills、FFmpeg Skill 等，以及带明显红队/漏洞利用定位的高热条目。文中严格区分确认信息与编辑推断。

| 项目 | 当前 stars | 增量依据 | 语言／类别 |
| --- | ---: | --- | --- |
| dream-num/univer | 31,246 | 11-16 日榜第 3，+1,878/日 | TypeScript／AI Office SDK |
| NVIDIA/SkillEvaluator | 4,389 | 11-16 日榜第 10，+953/日 | Python／Agent Skill 评测与 CI |
| DeanChensj/jiangshan-map | 8,783 | 11-16 日榜第 7，+285/日 | JavaScript／交互式时序地图 |
| XiaoYouChR/Ghost-Downloader-3 | 15,066 | 11-22 日榜第 15，+690/日 | Python／下载与生产力工具 |
| punkpeye/awesome-mcp-servers | 98,393 | 11-18 日榜第 20，+52/日 | 清单／MCP 服务生态 |

## 精选项目

### 1. [dream-num/univer](https://github.com/dream-num/univer)

- **确认信息：** Repository API 显示当前 **31,246** stars、TypeScript、Apache-2.0，创建于 2022-09-29；项目定位为可嵌入编辑、计算、协作和文件处理的开源 Office SDK，并面向人类与 AI Agent。11 月 16 日 Trending 快照为第 **3**、**+1,878/日**。
- **用途：** 在产品中构建文档、表格、演示式协作与 Agent 可操作的办公对象层。
- **走红原因（推断）：** Agent 开始需要实际读写企业文档，开发者倾向选择可自托管、可二次集成的“办公运行时”，而非只调用闭源编辑器。
- **适合人群：** 构建 AI office、知识工作流、文档自动化或协作 SaaS 的全栈团队。

### 2. [NVIDIA/SkillEvaluator](https://github.com/NVIDIA/SkillEvaluator)

- **确认信息：** 当前 **4,389** stars、Python、Apache-2.0，创建于 2026-06-24。项目提供多层 Agent Skill／插件质量门：安全扫描、harness 兼容性、语义重叠检测、合成评测集与衡量 Skill 对 Agent 行为影响的在线评测，并提供可复用 CI 模板。11 月 16 日榜第 **10**、**+953/日**。
- **用途：** 将 Skill 发布前的结构、兼容性、安全与行为效果纳入 CI，而非只检查能否安装。
- **走红原因（推断）：** Skills 数量快速增长后，组织的痛点从“怎么写”转为“是否安全、是否重复、是否真的提升任务成功率”。
- **适合人群：** 维护内部 Agent 插件市场、开源 Skill 库或要求可审计交付的 AI 平台团队。

### 3. [DeanChensj/jiangshan-map](https://github.com/DeanChensj/jiangshan-map)

- **确认信息：** 当前 **8,783** stars、JavaScript、GPL-3.0，创建于 2026-07-23；自述为覆盖公元前 403 年至今、**18** 个朝代、**198** 个疆域快照的中国历史交互地图，包含古今地名谱系与诗歌路线。11 月 16 日榜第 **7**、**+285/日**。
- **用途：** 以时间轴和可交互空间界面呈现历史地理、地名演化与叙事路线。
- **走红原因（推断）：** 具象、可探索的本地化数据产品很适合展示 Web 地图、知识图谱与叙事可视化的结合，降低公众理解复杂时空数据的门槛。
- **适合人群：** 数字人文、教育可视化、GIS 前端以及需要时空叙事交互的产品团队。

### 4. [XiaoYouChR/Ghost-Downloader-3](https://github.com/XiaoYouChR/Ghost-Downloader-3)

- **确认信息：** 当前 **15,066** stars、Python、GPL-3.0，创建于 2023-08-16；仓库自述为通用下载器。11 月 22 日榜第 **15**、**+690/日**。
- **用途：** 为个人或桌面端工作流提供多来源下载任务管理能力。
- **走红原因（推断）：** 在媒体与资料生产链条中，“可靠拿到本地文件”的确定性体验仍是高频需求；该项目的日榜增量反映生产力工具仍能与 Agent 项目并列获得关注，不代表其对所有站点或来源均合规可用。
- **适合人群：** 需要管理合法可下载资料、课程/素材归档和离线工作流的个人用户；使用前应核对来源条款与版权。

### 5. [punkpeye/awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers)

- **确认信息：** 当前 **98,393** stars、MIT，创建于 2024-11-30；这是 MCP servers 的精选清单。11 月 18 日榜第 **20**、**+52/日**，增长窗口早于本期但仍在最近 7 天内。
- **用途：** 按类别发现 MCP 服务，并作为选型和生态盘点入口，而非生产依赖的安全背书。
- **走红原因（推断）：** MCP 服务供给持续扩张，开发者需要先有一份可搜索的生态地图，再决定连接哪些数据源与工具。
- **适合人群：** 做 Agent 工具选型、搭建内部服务目录、或研究 MCP 互操作性的开发者；应逐项审核维护状态、权限与数据流。

## 技术趋势与社区偏好

- **Agent 生态的重心转向“可治理的能力单元”：** SkillEvaluator 的质量门与 Awesome MCP Servers 的发现入口分别覆盖上线前评测和接入前选型，社区更关心能力是否可验证、可兼容、可审计。
- **生产力基础设施从聊天框走进原生对象：** Univer 代表 Agent 直接操作文档、表格和协作对象的需求；下载器的高增长则提醒本地文件获取与归档仍是端到端工作流的一环。
- **有明确数据模型的体验产品依旧受欢迎：** Jiangshan Map 的热度说明，时空数据、知识谱系和交互叙事在 AI/Agent 热潮之外仍具强吸引力。上述“走红原因”均为编辑推断，确认信息以各归档快照和 Repository API 为准。

## 证据链接

- [GitHub Trending 2026-11-16 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-16.json)：Univer、SkillEvaluator、Jiangshan Map 的排名与 `gained`。
- [GitHub Trending 2026-11-18 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-18.json)：Awesome MCP Servers 的排名与 `gained`。
- [GitHub Trending 2026-11-22 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-22.json)：Ghost Downloader 的排名与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：第三方镜像的采集与统计口径。

## 内容标准与归档

每期 arXiv 按问题、创新、机制、实验、价值和局限选篇；GitHub 区分可核验元数据与编辑推断。历史文件位于 [`reports/`](reports/)，跨期判断见 [分类趋势总结](CATEGORY_SUMMARY.md)。
