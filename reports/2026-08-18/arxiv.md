# arXiv 自动驾驶与机器人晨报｜2026-08-18

说明：截至北京时间 2026-08-18 06:00，arXiv 最新可用常规批次为 2026-08-14 UTC；以下论文均为该批次中未列入 8 月 15—17 日报告的明确回溯，不冒充当日提交。作者、日期与结果来自 arXiv 摘要页。

## 自动驾驶

### 1. Control-Informed Constraint Adaptation in Minimum-Time Trajectory Planning for Autonomous Racing
- 链接：https://arxiv.org/abs/2608.14448
- 作者／机构：Ann-Kathrin Schwehn、Alexander Langmann、Mattia Piccinini、Johannes Betz；提交：2026-08-14。
- 问题：规划器通常假设完美跟踪，只能保守缩小赛道可行域，无法利用系统性控制误差。
- 创新与机制：在线测量跟踪偏差，动态调整空间约束并迭代扩展自由空间；规划仍以最短时间为目标。
- 实验与关键结果：高保真闭环仿真中单圈时间减少 1.8 秒，中位运行时 25 ms，未增加计算负担。
- 关注价值：把执行误差反馈给规划层，展示模块化架构也能持续释放赛道边界性能。
- 局限／跟进：目前主要是仿真赛车；需验证轮胎变化、真实噪声与安全边界校准。

### 2. CORAL: Curriculum-Optimized Reward Adaptation for LiDAR-Based Goal-Directed Urban Driving
- 链接：https://arxiv.org/abs/2608.14332
- 作者／机构：Anisa Saleem、Duksu Kim；提交：2026-08-14。
- 问题：长程城市驾驶同时要求到达目标、跟线、避障、信号遵守，固定奖励没有合理学习顺序。
- 创新与机制：五阶段课程逐步拉长路线、收紧约束，并同步重排进度、跟线、安全、平滑和规则奖励权重；PPO 输入 99 维 LiDAR/遥测/路线状态。
- 实验与关键结果：CARLA 最长路线 20/20 到达，而两基线仅 5% 与 10%；零样本迁移到七个城镇成功率 68%—98%，横向偏差低于 0.35 m。
- 关注价值：说明奖励调度与课程设计可比换大感知骨干更直接地改善长程闭环。
- 局限／跟进：单城训练、短路线迁移；需测试复杂交通参与者与真实传感器。

## 机器人／具身智能

### 3. Reflex: Enabling Fast and Predictive Vision-Language-Action Models for Reaction-Critical Manipulation
- 链接：https://arxiv.org/abs/2608.14379
- 作者／机构：Yuxuan Chen、Wanruo Zhang、Xiao Li；提交：2026-08-14。
- 问题：静态操作 benchmark 掩盖了动态交互中的延迟与反应失败。
- 创新与机制：发布支持异步推理和可配置延迟的 ReflexBench；ReflexVLA 用潜在未来预测、多帧融合、批量视觉编码和 CUDA Graph 降低闭环延迟。
- 实验与关键结果：六项动态任务上持续优于对照，同时保持静态任务竞争力，并在真实机器人验证。
- 关注价值：把控制频率、推理延迟和动态任务纳入 VLA 一等评价指标。
- 局限／跟进：摘要未给出统一绝对提升；需公开硬件、延迟分布和更多本体结果。

### 4. Expected Free Energy-based Informative Path Planning for Robotic Mars Exploration
- 链接：https://arxiv.org/abs/2608.14466
- 作者／机构：Ajith Anil Meera、Pablo Lanillos、Wouter Kouw；提交：2026-08-14。
- 问题：探索机器人既要提高信息地图质量，又要找到高价值区域并控制行驶和测量预算。
- 创新与机制：以主动推断的 Expected Free Energy 统一信息增益与目标价值；用高斯过程维护信息场，在硬路径长度约束下规划连续轨迹。
- 实验与关键结果：多种场景中同时获得更准确后验地图和高价值区域定位，优于同预算信息论基线。
- 关注价值：为行星探索提供可解释、易调参与资源受限的主动感知目标。
- 局限／跟进：仍是仿真与高斯过程设定；需评估非平稳地形、通信中断和真实能耗。

### 5. A Temporal Barrier Framework for Collision Avoidance in Multi-Agent Autonomous Aerial Vehicles
- 链接：https://arxiv.org/abs/2608.14239
- 作者／机构：Benedikt Barthel Sorensen、Mitchell Black、Erfaun Noorani、Themistoklis Sapsis；提交：2026-08-14。
- 问题：距离型屏障在近距离编队和对抗意图下反应滞后，过度保守又损害任务进度。
- 创新与机制：定义对抗时间到碰撞 aTTC，在控制屏障函数中直接约束时间风险；神经网络可微代理实时嵌入 QP 控制器。
- 实验与关键结果：独立追逐与编队仿真中，相比高阶距离 CBF，航点进度最高翻倍、碰撞率降至一半。
- 关注价值：把“还有多久会撞”变成安全控制量，适合密集多机协作。
- 局限／跟进：对抗意图模型决定证书质量；需硬件飞行、通信延迟和感知误差验证。

## 交叉方向：导航、定位与长期自治

### 6. OccPlanner: Goal-Aware Occupancy-Conditioned Diffusion Planner for Pixel-Goal Navigation
- 链接：https://arxiv.org/abs/2608.14160
- 作者／机构：Binling Huang、Nianjin Ye、Xi Yang、Liang Hu、Zhou Huang 等；提交：2026-08-14。
- 问题：像素目标没有深度和可通行性，难以落到连续、无碰撞的三维规划。
- 创新与机制：扩散规划器把时间视觉上下文、局部 3D occupancy 与像素目标逐级条件化；L3ROcc 从单目视频重建机器人坐标占据监督。
- 实验与关键结果：5—8 m 闭环场景平均成功率由 NavDP 的 20.81% 提升至 71.55%；Go2 实机开放环实验显示迁移迹象。
- 关注价值：把像素级指令直接连接到几何占据和动作生成，减少文本化 3D 中间层损失。
- 局限／跟进：真实闭环结果仍有限；需长程、动态障碍和传感器退化测试。

### 7. Sensor-Driven Mission Synthesis for UAV/UGV Swarms
- 链接：https://arxiv.org/abs/2608.14306
- 作者／机构：Uwe M. Borghoff、Paolo Bottoni、Remo Pareschi；提交：2026-08-14。
- 问题：异构群体在不完整、受攻击或通信中断的传感证据下，既要形成任务又要保证执行安全。
- 创新与机制：TB-CSPN 编排雷达、RF、声学和视觉 token；顾问代理解释，监督代理授权，独立模拟安全包络在执行端钳制或否决危险动作。
- 实验与关键结果：海岸监视案例展示有界时证据融合、可审计转换和硬件级安全闸门；摘要未给出统一成功率。
- 关注价值：将 Agent 协同与不可绕过的物理安全边界分层，回应群体系统治理问题。
- 局限／跟进：案例研究为主；需实机规模化、故障注入与通信攻击量化。

## 趋势总结
1. 自动驾驶规划开始把执行误差、课程奖励和安全证书纳入闭环，而不是把控制当作理想黑盒。
2. 机器人 VLA 的竞争轴转向反应延迟、阶段性风险和资源预算；动态任务比静态成功率更能暴露部署差距。
3. 导航与群体自治共同走向“几何证据 + 主动决策 + 可审计安全闸门”，文本接口逐步让位于 occupancy、时间风险和授权状态。
