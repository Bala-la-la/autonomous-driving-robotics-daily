# arXiv 自动驾驶与机器人晨报｜2026-08-17

说明：截至北京时间 2026-08-17 06:00，最新可用常规批次为 2026-08-13 UTC；周末没有更新批次，以下 7 篇均为该批次中未列入 8 月 15—16 日报告的明确回溯，不冒充当日提交。作者、日期与结果来自 arXiv 摘要页。

## 自动驾驶

### 1. BrainWAM: Action-Space Coordination of Semantic Priors and Predictive Dynamics for Autonomous Driving
- 链接：https://arxiv.org/abs/2608.12854
- 作者／机构：Bing Zhan、Shuyao Shang、Jiahao Gu、Shuo Lu 等；机构未完整披露；提交：2026-08-13。
- 问题：VLA 的语义先验与 WAM 的未来动力学若直接共享 token 注意力，语义捷径会挤压预测信息。
- 创新与机制：将两类能力拆成语义与预测两个动作通路，在紧凑 action 表示层协调；异步 rectified-flow 将视频与动作去噪解耦。
- 实验与关键结果：NAVSIM v1 达 89.5 PDMS、v2 达 89.6 EPDMS，优于 VLA-only 与 WAM-only。
- 关注价值：把“理解”和“想象”从 token 竞争改成可检查的动作接口，并直接针对延迟优化。
- 局限／跟进：NAVSIM 仍是离线评测；需验证真实闭环、极端交通和异步流水线的时序误差。

## 机器人／具身智能

### 2. Temporal GRPO: Beyond Trajectory-Level Credit in Vision-Language-Action Reinforcement Learning
- 链接：https://arxiv.org/abs/2608.13026
- 作者／机构：Yao Zhou、Hang Gao、Fengge Wu、Changwen Zheng、Wenwen Qiang；提交：2026-08-13。
- 问题：整条轨迹一个 advantage 会惩罚已经完成正确前置步骤的动作，产生 trajectory-level credit aliasing。
- 创新与机制：检测任务阶段，将 rollout 对齐到阶段区间，只比较进入同一阶段的轨迹，并把 stage advantage 施加到对应动作段。
- 实验与关键结果：RoboTwin 2.0 上成功率和样本效率一致提升；LIBERO-Long 的更新集中在首次分歧阶段。
- 关注价值：将稀疏成功反馈变成阶段级 credit，适合长时操作和可诊断 RL。
- 局限／跟进：阶段检测错误会把 credit 错配；需要研究无明显阶段边界和并行子任务。

### 3. S2-HWM: Sparse Event-Structured Hierarchical World Model for Long-Horizon Surgical Robot Manipulation
- 链接：https://arxiv.org/abs/2608.13103
- 作者／机构：Shuzhe Zhang、Xin Zhu、Yinling Qian、Qiong Wang；提交：2026-08-13。
- 问题：手术操作的有效交互是稀疏且持续时间不定，逐 primitive 想象既浪费算力又隐藏任务进度。
- 创新与机制：从 latent 轨迹学习稀疏 event evidence，驱动事件级 manager 更新目标；Event Transition Model 预测下一边界状态、时长和累计回报，worker 保留 primitive actor-critic。
- 实验与关键结果：SurRoL PegTransfer 成功率 98.7%，比 flat GAS DreamerV3 高 22.7 个百分点。
- 关注价值：把可变时长事件直接纳入世界模型，连接长时规划与低层控制。
- 局限／跟进：当前任务与仿真较单一；需验证真实手术噪声、事件漏检和安全约束。

### 4. EgoPHI: Estimating Contact and Force from Egocentric Vision
- 链接：https://arxiv.org/abs/2608.13014
- 作者／机构：Andela Ilic、Rachel Schuchert、Yijing Jiang、Christian Holz；提交：2026-08-13；ECCV 2026 接收。
- 问题：单目第一视角通常只能定位接触，无法恢复手和物体表面的三维受力。
- 创新与机制：用物理仿真为现有手物数据补充逐顶点力监督，联合预测手／铰接物体网格上的稠密接触图与 3D 力分布。
- 实验与关键结果：在分布内、OOD 和真实数据上优于既有力估计；真实采集覆盖 8 名参与者与多种触摸／抓取。
- 关注价值：为人类视频到机器人策略提供物理接触中间表示，而不止是外观模仿。
- 局限／跟进：仿真材料与真实摩擦仍有差距；需要更多本体、遮挡和动态接触验证。

## 交叉方向：导航、定位与长期自治

### 5. HumanoidVLN: A Physics-Grounded Simulator and Benchmark for Vision-Language Navigation Across Diverse Humanoid Embodiments
- 链接：https://arxiv.org/abs/2608.12860
- 作者／机构：Quan-Dung Pham、Anh Dao、The-Anh Nguyen-Dinh 等；提交：2026-08-13。
- 问题：现有 VLN 多忽略双足动力学、不同身高本体和行走引起的相机扰动。
- 创新与机制：基于 Isaac Sim 接入四种人形、RL 行走策略与 PD/MPC 路径跟踪器；多 Agent 生成—审阅—改写指令，并提供碰撞感知 episode。
- 实验与关键结果：933 个参考 episode；四模型四本体中 JanusVLN 平均成功率 43.55%、nDTW 48.38%；G1 20 次 sim-to-real 误差相关系数 0.935。
- 关注价值：把导航模型、控制器和身体差异放进同一评测契约。
- 局限／跟进：场景与指令仍有限；需公开更多真实长程、跌倒恢复和人群交互结果。

### 6. ASPIRE-VINS: Adaptive Spline-based Visual-inertial Navigation System With Robust 3D Measurement Residuals
- 链接：https://arxiv.org/abs/2608.12840
- 作者／机构：Kwangyik Jung、Eungchang Mason Lee、Taekjun Oh、Hyun Myung；提交：2026-08-13；RA-L 2026。
- 问题：固定时间间隔关键帧难同时表达快速运动和静止区间，任意时刻残差也不易稳定计算。
- 创新与机制：自适应 knot placement 按运动变化分配节点，多分辨率 spline 做局部切向细化，3D measurement residual 让特征与观测光线在三维对齐。
- 实验与关键结果：多种运动与传感条件下轨迹误差达到竞争性或更低水平。
- 关注价值：为长期自治提供连续时间、运动自适应的定位表示，适配异步传感器。
- 局限／跟进：连续优化开销和快速旋转退化需量化；尚需大规模户外与长时间回环测试。

### 7. SAP-Nav: Spatial Semantic Representation Meets Active Perception for Hierarchical Open-Vocabulary Object Navigation
- 链接：https://arxiv.org/abs/2608.12707
- 作者／机构：Xuetong Pei、Jian Liu、Vidura Munasinghe、Bo Miao 等；提交：2026-08-13。
- 问题：开放词汇导航既需要跨位置持久空间证据，又需要看清候选目标的判别视角。
- 创新与机制：在线维护可查询空间—语义表示；Active Viewpoint Verification 在证据不足时主动换位，再按类别与属性核验目标，无需预计算地图或任务训练。
- 实验与关键结果：LangMap、HM3D-OVON 达整体最佳，区域级 SR 比训练方法提升 12.2%，并完成真实机器人验证。
- 关注价值：将主动感知变成导航闭环的一部分，减少“看到了但无法确认”的失败。
- 局限／跟进：主动移动成本、遮挡和地图记忆漂移仍待长时评估；代码尚待公开。

## 趋势总结
1. 驾驶与操作的共同方向是把语义、动力学和 credit 分配对齐到动作／阶段接口，减少 token 竞争与长轨迹误归因。
2. 具身数据正从外观扩展到力、接触和事件边界；世界模型开始以可变时长预测直接服务长时规划。
3. 导航与定位同时走向物理化和主动化：人形身体约束、连续时间 VIO 和主动换位都把“何时观察、如何执行”纳入感知闭环。
