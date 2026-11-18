# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-19

## 日期与证据口径

检索截至北京时间 2026-11-19 06:00。以下七篇均为 **2026-11-17 UTC** 的 v1 新稿，故是本期可得的最新批次，**不是 11 月 19 日投稿**。作者、时间、方法与数字来自 arXiv 元数据和摘要；未能可靠核验机构时不作推断，实验数字均为作者报告、未独立复现。

## 自动驾驶／移动自治

### 1. [Multimodal Masked Diffusion Autoencoder for Modeling Impaired Driving](https://arxiv.org/abs/2611.23211)

- **作者／提交：** John Gideon、Anshul Gupta、Megan Applegate-Kenton 等；v1，2026-11-17 18:50 UTC。
- **问题、创新与机制：** 驾驶分心、压力与视觉负荷的标签昂贵，且单独看视频或车辆轨迹会丢掉人—车—场景关系。ID-MAE 将受损状态预测做成 masked token，同时重建被遮蔽的注视与轨迹；并发布含视频、视线、车辆状态的 DIVERT 驾驶模拟数据。
- **实验与关键结果：** DIVERT 含 **103 小时、109 人、10 类诱发状态**；同地点配对的受损识别 AUC 为 **0.706**，去掉重建损失为 **0.590**。
- **关注价值／局限与跟进：** 可为驾驶员监测和条件化辅助系统提供多模态预警，而非将“受损”简化为单帧表情分类；但模拟诱发不等于自然道路行为，公平性、误报后的交互、隐私和跨相机/人群校准须在真实运行中验证。

### 2. [Learned versus Kinematic Trajectory Prediction under Reduced Observation Frequency](https://arxiv.org/abs/2611.23198)

- **作者／提交：** Nukhbala Gadzhiev、Alexander Morochko；v1，2026-11-17 18:38 UTC。
- **问题、创新与机制：** V2X 位置常以 1–10 Hz 到达，运动预测却通常假设固定高频历史。工作在 Argoverse 2 中系统降采样 5 秒历史，比对按频率单训的 LSTM、10 Hz 模型插值和 CV/CA 运动学基线，并预注册假设、以十个随机种子和 bootstrap 报不确定性。
- **实验与关键结果：** 在 **24,984** 个测试场景，频率匹配 RNN 的 ADE 相对 10 Hz 增加：5 Hz **3.1%**、2 Hz **10.1%**、1 Hz **20.3%**；其相对较强运动学模型仍有 **24–30%** 优势。10 Hz 插值模型到 2 Hz 最多差 **1.3%**，1 Hz 差 **11.5%**。
- **关注价值／局限与跟进：** 给出通信频率—预测精度的可部署基线，提醒工程上不必为 2 Hz 立即重训；未包含地图、邻车、丢包延迟与协作控制，不能直接推为闭环安全收益。

### 3. [FIRE-Drive: Feasibility-Informed Risk Evaluation for End-to-End Diffusion Planning](https://arxiv.org/abs/2611.22297)

- **作者／提交：** Qifeng Xie、Kai-Yuan Feng、Wenkang Wan、Yue Wu、Maoguo Gong、Kai Sheng；v1，2026-11-17 06:54 UTC。
- **问题、创新与机制：** 扩散式端到端规划的随机初始化会生成不可行候选，相似轨迹也难按安全和交互风险区分。FIRE-Drive 以动态可行锚点初始化，用候选专属 BEV 风险证据评分，并以紧凑高质量候选监督配合轻量细化，将生成、风险选择和可行性对齐。
- **实验与关键结果：** NAVSIM v1 上报告 PDM Score **91.5**（ResNet-34）；另在 **220** 条 Bench2Drive 闭环路线报告 Driving Score **71.43**、成功率 **42.73%**。
- **关注价值／局限与跟进：** 将风险评分放在候选选择接口，便于审计“为何选这条”；仍须报告碰撞类别、候选覆盖、风险校准、长尾天气和真实道路中的降级策略，不能只以聚合分数判断安全。

## 机器人／具身智能

### 4. [TCP4D: A Unified Tool-Center-Point Tracking and Generation Model for Robot Manipulation](https://arxiv.org/abs/2611.23143)

- **作者／提交：** Haosong Peng、Xiangyang Liu、Zhengshen Zhang、Yunfeng Fan、Tianyu Qi、Xin Xia 等；v1，2026-11-17 17:59 UTC。
- **问题、创新与机制：** RGB 操作视频通常缺少可迁移的动作和夹爪标注。TCP4D 以本体无关的工具中心点（TCP）位姿为动作空间，让共享 4D 场景表征同时追踪观测到的 SE(3) TCP/夹爪状态并生成未来轨迹；其跨本体增强把已恢复动作重定向并合成替代机器人观测。
- **实验与关键结果：** DROID/RoboLab 的绝对轨迹误差为 **7.60/16.07 mm**；新本体只用 **10** 条示范适配。RoboTwin 平均成功率 **69.19%**，源数据加增强数据比只用增强高 **41.5%**。
- **关注价值／局限与跟进：** 把视频数据转成可复用的动作接口，有助于降低采集门槛；单目尺度、遮挡、TCP 定义偏差和合成观测的 sim-to-real 差距会直接传给控制，需分任务报告失败恢复和接触安全。

### 5. [SR-VLA: Stall-Reduced VLA Execution via Predicted-Input Lookahead and Selective KV Cache Repair](https://arxiv.org/abs/2611.22356)

- **作者／提交：** Tao Zhang、Yi Zhong、Jinhao Ruan、Yipeng Gao、Linfeng Zhong、Youming Yang；v1，2026-11-17 08:08 UTC。
- **问题、创新与机制：** VLA 推理阻塞下一 action chunk 会造成控制停顿；提前推理又可能基于错误的下一帧。SR-VLA 用轻量动作条件预测器预取视觉/本体状态，投机生成 KV cache 与动作；真实输入到达后按预测—真实差异和任务条件选择接受动作或局部修复 KV，而非全量重算。
- **实验与关键结果：** LIBERO 上对同步 $π_{0.5}$、OpenVLA-OFT 的查询加速分别 **2.67×/1.27×**，成功率保持有竞争力；目标运动扰动下仍有 **1.52–1.93×** 加速。
- **关注价值／局限与跟进：** 直接针对“模型会做但来不及做”的部署瓶颈；摘要没有给错误投机被接受的频率、p95 延迟、真实机械臂碰撞后果及网络/API 推理条件，均应作为上线门。

### 6. [Beyond Episodic Recall: Experience-to-Knowledge Evolution for Lifelong Embodied Navigation](https://arxiv.org/abs/2611.22321)

- **作者／提交：** Weitao An、Chenghao Xu、Xu Yang、Cheng Deng；v1，2026-11-17 07:18 UTC。
- **问题、创新与机制：** 长期导航直接存观测或高维 embedding 会持续膨胀，固定场景图又难把经验演化成环境规律。EvoNav 用稀疏 experience atoms 存语义、空间关系和任务反馈，在线合并重复观察；较慢时间尺度蒸馏物体共现与反馈成环境结构知识，并与当前可通行图联合检索目标。
- **实验与关键结果：** 在单目标、连续多楼层和多模态导航测试中，作者报告以紧凑持久记忆提升路径效率，并展示真机迁移；摘要未给统一绝对数值。
- **关注价值／局限与跟进：** 将“记住过什么”与“提炼出何种可迁移知识”分层，适合长期巡检；过期物体、错误反馈写入、环境重布置和隐私数据删除的回滚机制仍未由摘要量化。

## 交叉方向：协同控制与目标理解

### 7. [Capability Composition in Heterogeneous Teams via Barrier-Guided Diffusion Sampling](https://arxiv.org/abs/2611.23149)

- **作者／提交：** Diana Laura Morales、Ruoyu Lin、Magnus Egerstedt、Fabio Pasqualetti；v1，2026-11-17 18:03 UTC。
- **问题、创新与机制：** 异构机器人未必拥有协作示范，重训团队生成模型昂贵。方法从各个体独立示范训练生成模型，以已知物理能力条件写成轨迹约束，并在 diffusion sampling 时用 barrier-guided 约束合成协作轨迹；理论上刻画可生成的安全团队轨迹，并允许成员加入/离开而不重训。
- **实验与关键结果：** 两类协作数值任务和多机器人实机测试显示可生成满足约束的团队轨迹；摘要未披露成功率、约束违反率或通信条件。
- **关注价值／局限与跟进：** 是把“物理能力先验”用于零协作示范组合的清晰路线，可服务车队、无人机和异构移动机器人；barrier 模型误差、状态估计/通信延迟及约束不可行时的安全停机策略需要单列验证。

## 趋势总结

- **从离线高分到受资源约束的闭环接口：** FIRE-Drive 选择可行候选、SR-VLA 管推理停顿、低频轨迹研究给出通信下限；后续应共同报告校准、候选遗漏、p95 时延和实际控制代价。
- **视频与经验正被压缩为可操作状态：** TCP4D 将视频变为 TCP 轨迹，EvoNav 将观察变为经验原子和知识。它们的价值取决于尺度、时间有效性和错误状态能否隔离/回滚，而非只看数据规模。
- **多主体自主性需要约束能跨成员成立：** barrier-guided 组合说明单体能力并不自动变成协作能力；新成员、感知误差和通信中断应成为比平均仿真成功率更优先的测试轴。
