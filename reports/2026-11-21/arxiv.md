# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-21

## 日期与证据口径

检索截至北京时间 2026-11-21 06:00。以下六篇为 **2026-11-19 UTC 的 v1 新稿**；`Accord` 为 2026-11-18 UTC 的补充，已明确标注。作者、时间、方法与数字来自 arXiv 元数据和摘要；机构未能稳定核验时不作推断，所有指标均为作者报告、未独立复现。

## 自动驾驶／移动自治

### 1. [SpecFlow: Flow Matching in the Acceleration Spectrum for Multi-Agent Trajectory Forecasting](https://arxiv.org/abs/2611.26390)

- **作者／提交：** Ziyang Xu、Peng Han、Hai Zhou；v1，2026-11-19 16:44 UTC。
- **问题、创新与机制：** 多主体预测直接生成逐帧坐标，速度与加速度关系没有被显式约束，易损害动力学一致性。SpecFlow 把未来加速度的 DCT 系数作为 flow-matching 生成状态，固定解析积分恢复速度和位置；由只看历史的终点预测器给候选目标，交替注意力建模轨迹假设与主体间互动。
- **实验与关键结果：** best-of-20 下，ETH/UCY 平均 minADE/minFDE 为 **0.15/0.22**，NBA 四秒为 **0.69/0.86**，SDD 为 **7.38/11.57**；作者称 ETH/UCY 五个场景均达 SOTA，NBA 四秒 ADE 最低、FDE 并列最佳。
- **关注价值／局限与跟进：** 以加速度谱作生成接口，适合把交通交互预测接到可行性/舒适性约束；但行人、篮球和户外数据不等同车辆闭环，需在车规采样率、地图约束、罕见急刹和不确定性校准下报告碰撞风险收益。

### 2. [AnyVIO: Feed-Forward Streaming Visual-Inertial Odometry Across Platforms](https://arxiv.org/abs/2611.26625)

- **作者／提交：** Omoruyi Atekha、Marcus Greiff、Ray Zhang、Luca Carlone 等；v1，2026-11-19 18:59 UTC。
- **问题、创新与机制：** 单目几何基础模型缺失可观测的尺度，滤波/因子图融合 IMU 又会引入手工调参和随轨迹增长的优化。AnyVIO 将 streaming GFM 与惯性基础模型并行预测相邻帧度量运动，用轻量学习融合头估计两路可靠性，单次前向输出位姿。
- **实验与关键结果：** 覆盖汽车、腿足/轮式机器人、手持与头戴设备的 **9** 个数据集；相对纯视觉模型，度量位置误差降 **36%**，图像到位姿发布时间 **70 ms**；在两辆实车、最高 **140 km/h**、弱光和扬尘条件部署。
- **关注价值／局限与跟进：** 给 SLAM/长期自治提供不依赖长轨优化的实时度量接口；仍需给漂移随时长的曲线、IMU 标定偏差、异常振动/丢帧、算力功耗和地图闭环后的整体误差，摘要的跨平台结果不能自动保证极端 ODD 安全。

## 机器人／具身智能

### 3. [AgentRoboCritic: Understanding the Capability of Frontier Agents on Direct Robot Control](https://arxiv.org/abs/2611.26613)

- **作者／提交：** Yiyang Du、Yuxuan Kuang、Qitao Zhao、Yixuan Wang、Zhanqiu Guo、Yi Xu 等；v1，2026-11-19 18:57 UTC。
- **问题、创新与机制：** 回合成功率看不到直接输出低层数值动作的多模态 Agent 如何失败。AgentRoboCritic 要策略在每步给出局部意图，critic 对照意图评估动作结果与失败类型，把审计粒度降到 action level。
- **实验与关键结果：** 覆盖 **12** 个操作基准；发布 **12,844** 个动作标注和 **400** 动作人工标注验证集。微调的开源 Muse-Glimmer-30B 失败类型准确率由 **32.58%** 升至 **74.24%**。作者观察到零样本语义 grounding 与局部恢复能力，但抓取/对齐和不同失败模式的恢复不均衡。
- **关注价值／局限与跟进：** 为“Agent 直接控机器人”补上可审计的失败标签和触发恢复入口；critic 的意图文本可能事后合理化，且仿真/基准动作不覆盖力、延迟和不可逆风险，应检验 critic 误放行是否导致真实损伤。

### 4. [PGX: Physically Grounded Execution for Long-Horizon Humanoid Loco-Manipulation](https://arxiv.org/abs/2611.26596)

- **作者／提交：** Kai Lu、Chenyang Ma、Ioannis Havoutis；v1，2026-11-19 18:52 UTC。
- **问题、创新与机制：** 单体 VLA 很难同时处理长程阶段、行走—操作协同和接触精度。PGX 将执行拆成谓词状态机（阶段门、恢复、导航/等待协调）、活动阶段内的 VLA skill，以及以站位、物体相对位置、接触目标维持空间一致性的 world-coordinate locking；其中状态机和锁定模块不需训练。
- **实验与关键结果：** 在 **3** 个仿真任务与 Unitree G1 的 **1** 个真机长程 loco-manipulation 任务上，作者报告阶段推进和任务成功率提升；摘要未给绝对成功率。
- **关注价值／局限与跟进：** 把慢推理、任务进度和几何约束分层，是人形落地更清晰的故障隔离方式；需公开谓词误判、站位漂移、恢复次数、阶段转换延迟与跌倒/接触失败代价，不能只以最终成功率判断。

### 5. [Risk-Controlled Test-Time Adaptation for Vision-Language-Action Models](https://arxiv.org/abs/2611.26438)

- **作者／提交：** Zixuan Liu、Hashem Haghbayan、Zizhan Zheng、Siavash Khajavi；v1，2026-11-19 17:12 UTC。
- **问题、创新与机制：** 检索示范虽能让 VLA 免更新适配，但模型未必会用到正确示范。R2-VLA 用不确定性预测器决定自主执行还是请求专家，并校准阈值以满足用户指定的任务失败风险；专家修正持续写入检索记忆。
- **实验与关键结果：** 在 **3** 种 VLA backbone、**4** 个 LIBERO suite 上，平均任务成功率提高 **9.2–11.2 个百分点**，并以更少专家请求达成设定目标。
- **关注价值／局限与跟进：** 将“是否求助”变成有任务级风险口径的运行时接口；基准中的校准不保证分布外接触任务仍有效，部署还需报告置信度漂移、拒绝率、专家响应延迟和错误记忆的可撤销性。

### 6. [Awaken-HI: Scaling Humanoid Intelligence with Whole-Body Human Experience](https://arxiv.org/abs/2611.26420)

- **作者／提交：** EngineAI；v1，2026-11-19 17:03 UTC。
- **问题、创新与机制：** 第一视角视频通常没有同步全身运动，难为人形 loco-manipulation 提供可转移动作监督。Awaken-Human 配对约 **50,000 小时**第一视角双目视频与全身人体运动、覆盖逾 **100** skills；Awaken-HI 以共享动作 expert 同时预测人类运动和重定向的机器人动作。
- **实验与关键结果：** 随人类预训练数据增加，留出机器人动作误差呈经验 scaling law 下降；全量预训并适配 T800 后，**8** 个真机单任务平均成功率 **93.75%**，作者称超过 GR00T N1.7 与 $π_{0.5}$，并测试未见物体及新物体—目标配对。
- **关注价值／局限与跟进：** 同步全身数据可能缓解人形数据瓶颈；需进一步审计人—机运动重定向误差、稀有接触/跌倒、标注许可与隐私、长程任务的置信区间，单一机型比较不能代表跨本体泛化。

## 交叉方向：长期空间状态

### 7. [Accord: Universal Online Metric Localization and Dense Mapping from one Camera and an IMU](https://arxiv.org/abs/2611.25279)（2026-11-18 UTC 补充）

- **作者／提交：** Jaafar Mahmoud、Arthur Movsesyan、Cuong Huynh、Mikhail Iumanov、Sergey Zagoruyko、Sergey Kolyubin；v1，2026-11-18 23:16 UTC。
- **问题、创新与机制：** 单目 IMU-VIO 有度量运动却几何稀疏，深度基础模型有稠密结构却缺尺度一致性。Accord 用 VIO 位姿产生度量锚点，将短 keyframe window 的深度以双向共视一致性校正逐图尺度，再用因子图融合子图；不按相机/数据集单独调参。
- **实验与关键结果：** 在 **5** 种公开 camera-IMU 设置和新的 Phone-rig/GoPro 数据上，作者报告每个平台 5 cm mean F-score 均为最佳或次佳；开源代码与 phone-rig 数据。
- **关注价值／局限与跟进：** 把基础模型的稠密预测接回可核对的多视几何，可服务手机、车载和机器人建图；仍应报告动态场景、回环、长程尺度漂移、设备同步误差和端侧吞吐，5 cm F-score 不是导航安全证据。

## 趋势总结

- **具身系统正将“何时相信策略”显式化：** R2-VLA 的风险阈值、AgentRoboCritic 的动作级意图审计、PGX 的物理谓词共同把求助、恢复与阶段切换从隐含行为变为接口；下一步应统一报告误触发、漏触发、p95 延迟和真实损伤代价。
- **规模数据与结构化执行互补而非替代：** Awaken-HI 用大规模同步人体运动扩展人形监督，PGX 用几何锁定和状态机收紧部署。数据 scaling 不等于接触可靠性，转换误差和回退策略必须独立评测。
- **长期自治需要“度量且可更新”的状态：** AnyVIO 与 Accord 均让学习式几何接受 IMU/多视约束，SpecFlow 将未来动作的动力学结构前置。跨设备、跨时间和动态物体下的状态来源、更新与失效条件比单帧指标更重要。
