arXiv 自动驾驶与机器人晨报｜2026-07-12

时间范围说明：北京时间 2026-07-12 早晨检索。优先覆盖 2026-07-09 至 2026-07-10 在 arXiv 可见的最新提交/更新；自动驾驶强相关新稿数量有限，按要求补充到 2026-07-06 至 2026-07-08 的高相关论文，并在条目中标注日期。

一、自动驾驶
1. Shift & Drift: A Zero-Shot Benchmark for Generalizable and Robust Autonomous Driving Motion Planning
链接：https://arxiv.org/abs/2607.07844
作者：Alessandro Canevaro, Hang Yu, Julian Schmidt, Peizheng Li, Silvan Lindner, Wilhelm Stork, Georg Martius, Julian Jordan
提交/更新：2026-07-08 提交并更新
要解决的问题：现有闭环规划器常在 nuPlan 这类同分布基准上表现不错，但面对陌生城市拓扑、行人/骑行者密集场景，以及执行噪声引发的状态漂移时，泛化和恢复能力到底如何，过去缺少系统压力测试。
核心创新点：提出一个双轨 benchmark，把“语义分布偏移”和“状态分布漂移”拆开测。语义轨把 DeepScenario Open 3D 的航拍数据转换进 nuPlan 仿真，构造跨城市零样本评测；漂移轨向 ego 动力学注入随机扰动，专门测执行误差累积后的恢复能力。
方法机制/结构：不是新 planner，而是新评测框架。它把跨域地图/交通参与者分布变化，与控制链路噪声导致的轨迹偏移分开量化，从而比较 imitation learning、RL 等不同规划范式的失效模式。
实验设置和关键结果：覆盖 1,182 个场景，涉及 4 个德国城市和美国旧金山；对多类规划器做系统评测。结果显示 imitation learning 方法在 ID 基准里分数高，但在语义偏移尤其是行人密集场景显著失效，且在时间相关执行噪声下持续漂移；RL 型 planner 退化更平缓，在安全性和进度指标上更稳。
为什么值得关注：行业里很多端到端驾驶模型还在追逐 ID leaderboard，这篇工作把“换城即掉线”和“轻微执行误差就越跑越偏”这两个部署痛点直接暴露出来，对真实上车价值很高。
可能局限/后续点：当前仍是仿真闭环而非真实车队部署；后续可看是否扩展到天气、传感器失真、V2X 缺失等更复杂 shift，以及是否能成为 VLA/WAM 驾驶模型的通用鲁棒性基准。

2. On Exploring Input Resolution Scaling For Anytime LiDAR Object Detection
链接：https://arxiv.org/abs/2607.08391
作者：Ahmet Soyyigit, Shuochao Yao, Heechul Yun
提交/更新：2026-07-09 提交并更新
要解决的问题：自动驾驶感知栈在环境复杂度变化时，LiDAR 3D 检测延迟会抖动；若硬追最高精度，容易超时拖慢规划控制；若统一降配，又会浪费可用算力并损失检测质量。
核心创新点：提出面向 pillar/voxel 点云检测器的“单模型多分辨率 anytime 推理”方案，不需要为不同输入分辨率分别部署多套模型，同时配一个 deadline-aware 调度器，在线选择在当前时限下可跑的最高分辨率。
方法机制/结构：一方面在输入侧做可伸缩分辨率处理，让同一检测器适配不同粒度点云；另一方面做运行时执行时间预测，解决点云稀疏度不规则、传统静态 worst-case 配置过保守的问题。
实验设置和关键结果：在 nuScenes 上，作者称该方法显著优于已有 anytime LiDAR detection 方案；并在模拟自动驾驶系统中验证，能持续维持 collision-free navigation，同时避免因为环境复杂而频繁无谓停顿。
为什么值得关注：这不是单纯再卷 mAP，而是把“算力预算可变、时限可变”的车规现实拉进模型设计，适合边缘算力受限、任务混跑或多传感器竞争 GPU 的量产场景。
可能局限/后续点：摘要未披露更细的类别级增益和最坏情况延迟界；后续值得看在真实车载 SoC、和 tracker/planner 联调后的收益是否还能保持。

3. A Reliable Context-Aware and Temporal Planning Framework for Autonomous Driving
链接：https://arxiv.org/abs/2607.04689
作者：Argho Dey, Yunfei Yin, Swachha Ray, Md Minhazul Islam, Zheng Yuan, Sijing Xiong, Hongyu Liu, Zhiqiu Huang
提交/更新：2026-07-06 提交并更新
要解决的问题：城市道路里相机经常受遮挡、模糊、照度变化和噪声干扰。很多 BEV 端到端方法把时间帧一股脑融合，坏帧也会进记忆，最终让检测、预测和规划一起抖动，提升碰撞风险。
核心创新点：提出 RCT-AD，把“这一帧值不值得信”显式建模。它不是盲目累积时序特征，而是先做可靠性评分，再通过 quality-gated FILO memory 只保留可信上下文，用历史可靠帧去重建当前退化观测。
方法机制/结构：整体由 Reliable Context Awareness 模块、质量门控 FILO 记忆、Temporal Trajectory Planner，以及联合 detection/segmentation head 组成。共享 BEV 空间里同时注入语义与运动线索，用于多智能体交互下的长期轨迹规划。
实验设置和关键结果：在 nuScenes 上，RCT-AD 达到 61.5 NDS、52.9 mAP、52.3 mIoU，并且作者强调其 planning robustness 优于近期端到端基线，同时保持接近实时部署的计算效率。
为什么值得关注：相比“更大的 backbone/更多历史帧”，这篇更像是在补自动驾驶端到端栈的一块工程短板：先判断信息可靠性，再谈时序融合。对于雨雾、遮挡、夜间场景尤其重要。
可能局限/后续点：可靠性估计本身若失准，可能把有价值的新信息误判成噪声；后续可继续观察其在极端天气、多模态传感器输入和失效回退机制中的表现。

二、机器人 / 具身智能
4. Native Video-Action Pretraining for Generalizable Robot Control
链接：https://arxiv.org/abs/2607.08639
作者：Qihang Zhang, Lin Li, Luyao Zhang, Shuai Yang, Yiming Luo, Shuaiting Li, Ruilin Wang, Junke Wang, Jiahao Shao 等
提交/更新：2026-07-09 提交并更新
要解决的问题：当前很多 video-action/世界模型路线，本质是在把为数字内容生成而生的视频模型硬改成机器人控制器，但物理世界要求严格因果性、高频推理、动作精度和闭环重接地，这和视频生成需求并不一致。
核心创新点：提出 LingBot-VA 2.0，强调“从一开始按 embodiment 去建 video-action foundation model”，而不是二次改造内容生成模型。亮点是语义视觉-动作 tokenizer、严格因果预训练、稀疏 MoE 主干，以及异步闭环推理。
方法机制/结构：1）semantic visual-action tokenizer 将视觉表示同时对齐语义与动作；2）用 causal pretraining 避免从双向结构迁移时的灾难性遗忘；3）以 sparse MoE 扩容量但兼顾效率；4）通过异步推理并行预测未来 latent，同时用最新观测和 learned forward dynamics 持续 re-ground。
实验设置和关键结果：摘要未给公开 benchmark 数字，但明确报告了 real-world deployment，并强调在复杂操作任务上具备 few-shot generalization 能力。
为什么值得关注：这代表具身模型正从“借视频模型的力”转向“为控制原生设计”。如果这条路线成立，机器人 foundation model 会更接近 action-native world model，而不是视觉模型外挂动作头。
可能局限/后续点：缺少公开摘要级定量指标，不利于直接横比；后续应重点关注其开源程度、跨 embodiment 泛化，以及与 VLA、diffusion policy、world model RL 的统一接口。

5. DexVerse: A Modular Benchmark for Multi-Task, Multi-Embodiment Dexterous Manipulation
链接：https://arxiv.org/abs/2607.08751
作者：Yunchao Yao, Zhuxiu Xu, Tianqi Zhang, Zixian Liu, Sikai Li, Zhenyu Wei, Feng Chen, Dihong Huang, Kechang Wan, Chenyang Ma 等
提交/更新：2026-07-09 提交并更新
要解决的问题：灵巧手研究长期碎片化，很多 benchmark 只测单任务、单手型、单视觉设定，很难真正回答“一个策略能否跨任务、跨手型、跨视觉变化泛化”。
核心创新点：提出大规模模块化基准 DexVerse。覆盖 100 个任务、3 种机械臂、6 种灵巧手，并且系统提供纹理、背景、光照、相机视角等可控视觉变化；同时提供 VR 遥操作接口和多模态演示数据。
方法机制/结构：任务覆盖抓取/搬运、关节物体交互、工具使用、双手协作、非抓持控制、接触丰富行为、多目标执行、长程多阶段任务等；数据侧同步提供 proprioception、RGB、depth、point cloud 和 state。
实验设置和关键结果：提供 3,180 条 demonstrations，并在 19 个任务上 benchmark Diffusion Policy、DP3、OpenVLA、pi_0.5 等代表方法。结果不是“谁 SOTA”，而是揭示现有方法在任务泛化和 visuomotor robustness 上都还有明显缺口。
为什么值得关注：当前具身圈一个大问题不是模型不够大，而是 benchmark 不够像真实世界。DexVerse 这种“跨任务+跨本体+多视觉扰动”的评测设施，可能比再加几万条单任务 demo 更有长期价值。
可能局限/后续点：仍以仿真和数据集构建为主，sim-to-real gap 依旧存在；后续可跟进是否会出现基于该 benchmark 的统一评测榜单和真实机器人转移结果。

6. TouchWorld: A Predictive and Reactive Tactile Foundation Model for Dexterous Manipulation
链接：https://arxiv.org/abs/2607.07287
作者：Jianyi Zhou, Feiyang Hong, Yunhao Li, Yicheng Zhao, Yongjue Cen, Zirui Liu, Jiakang Huang, Zirui Chen, Ruiyang Zhang, Weizhuo Zhu 等
提交/更新：2026-07-08 提交，2026-07-09 更新
要解决的问题：视觉和语言擅长给语义和几何目标，但看不到滑移、接触稳定性、受力失配等隐藏接触状态；而许多触觉策略又把触觉仅当成低频观测，无法既做长程任务规划又做毫秒级纠偏。
核心创新点：提出 TouchWorld，把触觉同时作为“预测性的接触参考”和“反应式高速反馈”。核心不是把 tactile token 塞进一个大模型，而是分层拆解任务规划、触觉世界模型、目标条件动作生成和残差修正。
方法机制/结构：High-Level Planning Layer 负责子任务与触觉子目标；Visuo-Tactile Goal-Conditioned Policy 生成 nominal action chunks；Tactile-Conditioned Refinement Policy 利用近期触觉与 proprio feedback 做在线残差校正。
实验设置和关键结果：在 6 个长程、接触丰富的灵巧操作任务上，TouchWorld 在 clean setting 达到 65.0% 成功率，在人为扰动下达 53.7%，分别比最强基线高 15.7 和 18.5 个百分点。
为什么值得关注：这篇说明“触觉不是附属模态”，而是具身闭环里单独值得被建模成 predictive + reactive 双重机制的核心信号。对插接、拧转、对位等任务尤其关键。
可能局限/后续点：层级式系统通常工程复杂度更高，且对触觉硬件一致性较敏感；后续值得看在低成本触觉阵列和跨手型迁移上的表现。

三、交叉方向（SLAM / 多机器人 / 几何优化）
7. Learning Adaptive Solvers for Distributed Factor Graph Optimization on Matrix Lie Groups
链接：https://arxiv.org/abs/2607.08735
作者：Jaeho Shin, Maani Ghaffari, Yulun Tian
提交/更新：2026-07-09 提交并更新
要解决的问题：多机器人感知、跨 session 建图和大型几何优化，常需要分布式 factor graph 求解；但现有 distributed solver 往往高度依赖手工调参，而且多半只盯着刚体 pose graph，不够泛化。
核心创新点：提出 DeepCORD，把并行加速的黎曼优化器展开成可微迭代过程，再学习一个自监督反馈策略，动态调节 solver 参数，使其能根据优化阶段和通信状态自适应运行。
方法机制/结构：框架支持一般 matrix Lie groups，而不局限于 SE(3)。它同时覆盖同步和异步通信场景，因此更贴近多机器人、分布式 SLAM、子图对齐等实际部署环境。
实验设置和关键结果：在真实世界 SE(3) pose graph optimization 与 SL(4) projective submap alignment 上，作者报告其在大多数 benchmark 和现实通信设定下，都能比已有 distributed baseline 得到更低 objective value。
为什么值得关注：机器人社区这两年一边追 foundation model，一边又在真实系统里被优化器稳定性和通信约束拖后腿。DeepCORD 代表一种很务实的方向：不是替换几何优化，而是让求解器本身“学会自调”。
可能局限/后续点：摘要没有给出收敛速度、通信开销和最坏情况稳定性的细粒度数字；后续要重点看其在大规模多机器人 SLAM、异构传感器图优化中的泛化。

趋势总结
1. 自动驾驶侧的主线，明显从“单一数据集上的端到端分数”转向“分布偏移、可靠性与实时性”三件事一起抓。Shift & Drift、RCT-AD、Anytime LiDAR 都不是再卷单点精度，而是在补部署短板。
2. 机器人/具身侧，越来越多工作不再满足于通用 VLA 口号，而是开始按控制闭环真实需求重做组件：LingBot-VA 2.0 强调因果与异步闭环，TouchWorld 强调触觉的预测/反应双角色，说明具身 foundation model 正向 action-native、contact-aware 演化。
3. benchmark 基础设施在加速升级。DexVerse 这类“跨任务、跨本体、跨视觉扰动”的评测体系，反映社区开始意识到：如果 benchmark 设计仍然过窄，再大的模型也很难证明通用性。
4. 交叉方向上，学习增强的几何/优化模块重新受到重视。DeepCORD 这类方法说明，foundation model 并没有替代 SLAM/图优化，反而在推动“可学习但仍保留结构先验”的混合路线。
5. 相比以往“更大模型 + 更多数据”的线性扩张，本批论文的新意在于：更强调系统约束、闭环鲁棒性、接触反馈、跨分布评测，以及把真实部署痛点直接做成研究问题。

信息来源：arXiv API / arXiv 摘要页，检索时间为北京时间 2026-07-12 早晨。
