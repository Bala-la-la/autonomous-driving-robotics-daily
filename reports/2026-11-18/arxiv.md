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
