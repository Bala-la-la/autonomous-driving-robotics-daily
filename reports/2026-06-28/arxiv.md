arXiv 自动驾驶与机器人晨报｜2026-06-28

说明：按 2026-06-28 北京时间抓取。当前能检索到的最新高相关 arXiv 更新主要集中在 2026-06-25 UTC；其中“自动驾驶”纯相关强稿相对偏少，因此按要求补入 2026-06-24 UTC 的高相关论文，并在条目中明确日期。作者信息来自 arXiv 条目；机构若 arXiv 摘要页未明确列出，则注明“未在 arXiv 摘要页明确给出”。

【自动驾驶】
1. G2DP: Diffusion Planning with Spatio-Temporal Grid Guidance
链接：https://arxiv.org/abs/2606.26017
作者/机构：Hang Yu, Ye Jin, Alessandro Canevaro, Julian Schmidt, Julian Jordan, Peizheng Li, Marc Kaufeld, Silvan Lindner, Johannes Betz, Wilhelm Stork；机构未在 arXiv 摘要页明确给出
时间：2026-06-24 提交，2026-06-25 更新
要解决的问题/痛点：扩散式自动驾驶规划擅长生成多样轨迹，但闭环运行里常因采样随机性导致碰撞、偏航或不跟路线。现有 guidance 多依赖稀疏几何 query 或事后修补，对高交互交通场景的全局态势理解不够强。
核心创新点：把 guidance 从“对象级提示”升级成“整块时空代价场”。作者把未来 occupancy 分布与 route-progress map 融合成可微的 spatio-temporal cost volume，并把它写成连续 safety energy functional，在 denoising 全过程持续施加密集梯度约束。
方法机制或模型结构：G2DP 仍以 diffusion planner 为主干，但不再只在末端做轨迹修补，而是在每一步去噪时直接把轨迹推向 collision-free 且 progress-optimal 的时空区域。关键是把环境约束编码为密集 cost grid，而不是几个对象的点状特征。
实验设置和关键结果：在 nuPlan 做 extensive closed-loop evaluation，并做 zero-shot 转移到 interPlan 和 DeepScenario。摘要给出的关键结果是：相对最强 imitation-learning 基线，nuPlan reactive score 提升 +7.2；在 interPlan 上，相对无 guidance 版本，collision avoidance 提升 +10.15。
为什么值得关注：这条路线体现出自动驾驶规划正在从“会生成”转向“生成过程可控”。如果扩散规划想从论文走向真实系统，推理期可注入的显式安全约束几乎是必修项。
可能局限或后续可跟进点：摘要未披露推理时延、算力开销与极端博弈场景下的保守性代价；后续值得跟进其在更差地图质量、更多长尾交互和真车部署中的稳定性。

2. FAR-LIO: Enabling High-Speed Autonomy through Fast, Accurate, and Robust LiDAR-Inertial Odometry
链接：https://arxiv.org/abs/2606.26010
作者/机构：Maximilian Leitenstern, Marcel Weinmann, Patrick Haft, Tobias Lasser, Dominik Kulmer, Markus Lienkamp；机构未在 arXiv 摘要页明确给出
时间：2026-06-24 提交/更新
要解决的问题/痛点：高速自治系统尤其无人赛车，真正卡脖子的不是离线精度，而是低延迟、抗剧烈运动和噪声、还能支撑稳定闭环控制的里程计。传统 LIO 往往在精度与延迟之间做艰难折中。
核心创新点：提出 CUDA 加速的 FAR-LIO，从数据结构到配准再到滤波后端都围绕实时性重构，包括 novel CUDA voxel hashmap、sparsity-aware GICP、adaptive thresholding，以及带 upsampling 与 delay compensation 的 EKF 融合。
方法机制或模型结构：前端用 CUDA voxel hashmap 做并行最近邻搜索和地图更新；中间层以稀疏感知 GICP 压低高动态场景中的配准开销；后端 EKF 将 LiDAR odometry 与高频 IMU 融合，并通过延迟补偿输出更平滑稳健的轨迹。
实验设置和关键结果：覆盖 4 种传感器设置、公开数据集以及两台最高 250 km/h 的自动驾驶赛车。摘要给出的结果是：相对现有 SOTA 基线，平均位置误差降低 6.9%，运行时间降低 38.4%，而且同一套参数即可适配多传感器配置。
为什么值得关注：这是少见直接对准高速度真实系统瓶颈的工作，不是只在常规 benchmark 上刷分。对自动驾驶、无人机、高速移动机器人都很有系统工程参考价值。
可能局限或后续可跟进点：摘要没有展开不同传感器组合下收益来源，也未说明雨雾、强退化点云、超长时间漂移时的表现；后续需要看开源代码后的可复现性与硬件门槛。

【机器人 / 具身智能】
3. Scalable Behavior Cloning with Open Data, Training, and Evaluation
链接：https://arxiv.org/abs/2606.27375
作者/机构：Arthur Allshire, Himanshu Gaurav Singh, Ritvik Singh, Adam Rashid, Hongsuk Choi, David McAllister, Justin Yu, Yiyuan Chen, Huang Huang, Pieter Abbeel, Xi Chen, Rocky Duan, Phillip Isola, Jitendra Malik, Fred Shentu, Guanya Shi, Philipp Wu, Angjoo Kanazawa；机构未在 arXiv 摘要页明确给出
时间：2026-06-25 提交/更新
要解决的问题/痛点：操作领域长期缺少真正可复现的大规模开放栈。很多工作只开放模型或局部数据，硬件、训练流水线、仿真与真实评测割裂，导致方法很难公平比较，也很难低成本做消融。
核心创新点：提出 ABC 全开源行为克隆栈。核心数据集 ABC-130K 含 3500 小时、13 万+ episode、195 个任务；同时开放硬件方案、训练基础设施、仿真管线，以及额外 400 小时 sim-teleop 数据，并给出 sim/real 协同训练 recipe。
方法机制或模型结构：作者并非只发布数据，而是搭建一个从 teleop 数据采集、模型训练、simulation proxy evaluation 到真实世界验证的完整基线环境，用它系统比较 DiT 与 VLA 等常见架构和训练 recipe。
实验设置和关键结果：实验覆盖多种模型设计与训练策略，并落到真实世界操作验证。摘要点名展示的真实任务包括 box folding、从钱包中取信用卡等灵巧操作，证明该开放栈不只是“数据仓库”，而是能支撑较复杂 manipulation policy 的真实执行。
为什么值得关注：如果社区接受这套开放栈，它的价值会超过“又一个数据集”。它可能成为具身操作版的标准底座，让行为克隆从不可比、难复现，转向可持续迭代的公共基线。
可能局限或后续可跟进点：摘要没有给出与闭源超大数据栈的绝对差距，也没细拆数据质量分布和任务难度分层；后续应关注硬件复刻成本、开放数据长尾质量和 sim-to-real 相关性的稳定性。

4. VibeAct: Vibration to Actions for Contact-Rich Reactive Robot Dexterity
链接：https://arxiv.org/abs/2606.27344
作者/机构：Yuemin Mao, Uksang Yoo, Jean Oh, Jonathan Francis, Jeffrey Ichnowski；机构未在 arXiv 摘要页明确给出
时间：2026-06-25 提交/更新
要解决的问题/痛点：接触型灵巧操作的关键事件通常发生得很快、很局部，而且常被遮挡。视觉和点云往往来不及感知接触、打滑、插入失败等瞬态信号，导致策略难以做出反应式控制。
核心创新点：提出 VibeAct，用 piezoelectric microphones 采集 vibro-acoustic 信号，再通过共享的 contact/slip 物理表征把真实触觉与仿真强化学习桥接起来，避免直接模拟难以精确复刻的原始音频。
方法机制或模型结构：在真实灵巧手上嵌入麦克风，通过遥操作采集振动波形；再把记录在 calibrated digital clone 中回放，自动标注每根手指的 contact/slip。随后训练 tactile estimator 从真实波形预测接触与打滑，策略则在仿真里基于同一表征学习。
实验设置和关键结果：覆盖 5 个接触密集任务，包括 regrasping、in-hand reorientation 和 insertion。摘要明确指出：VibeAct 在仿真中持续优于 proprioception + point-cloud 基线，且在需要持续反应控制的任务中收益最大，其中 continuous slip-magnitude channel 最有信息量；训练出的策略还能迁移到真实手-臂平台并提升部署成功率。
为什么值得关注：具身学习过去过于依赖视觉，VibeAct 代表“廉价高带宽触觉”开始进入主舞台。它不依赖昂贵专用触觉阵列，却能把接触反应能力补回来。
可能局限或后续可跟进点：麦克风对安装方式、材料和环境噪声可能敏感；后续值得看跨手型、跨任务、跨材质装配以及更复杂接触序列下的泛化。

5. RouterVLA: Turning Smoke Tests into Supervision for Heterogeneous VLA Selection
链接：https://arxiv.org/abs/2606.27355
作者/机构：Xingyu Ren, Chugang Yi, Ge Ma, Youran Sun；机构未在 arXiv 摘要页明确给出
时间：2026-06-25 提交/更新
要解决的问题/痛点：现实机器人团队常常拥有多套 frozen VLA policy，不同任务上各有强弱，但工程上最后常被压缩成“选一个全局赢家”。这样会浪费预部署 smoke tests 中已经暴露出来的 expert 差异。
核心创新点：提出 RouterVLA，把 pre-deployment evaluation rollouts 重新利用为 policy selection supervision。重点不是再训一个更大的通用策略，而是建立一个 commissioning-aware 的异构策略路由层。
方法机制或模型结构：作者采用 outcome-disjoint cross-fitting，先用已记录的 probe rollouts 为每个 frozen expert 建 profile，再用独立 trial 评估选中的 expert，避免把同一试验既拿来建模又拿来验证，造成虚高收益。
实验设置和关键结果：在 34,752 条 LIBERO-Plus rollout records 上，透明的 probe-success routing rule 将 held-out success 从 0.4686 提升到 0.6149，增益为 +14.64 个百分点。作者还指出，如果复用同一 scored trial，测得收益会被夸大到 1.87 倍。
为什么值得关注：这篇论文的价值不在“又做了一个 VLA”，而在提醒社区：系统级收益往往来自策略组合与选择机制，而不是盲目继续堆单模型。对于多机器人、多任务部署尤其现实。
可能局限或后续可跟进点：当前摘要强调的是 scalar-only profile 场景；后续要看更丰富上下文、在线路由成本、实时约束和真实机器人 smoke test 噪声下是否仍然稳定。

【交叉方向】
6. Hallucination in World Models is Predictable and Preventable
链接：https://arxiv.org/abs/2606.27326
作者/机构：Nicklas Hansen, Xiaolong Wang；机构未在 arXiv 摘要页明确给出
时间：2026-06-25 提交/更新
要解决的问题/痛点：生成式 world model 往往“画面看着连贯，动力学已经跑偏”。这类 hallucination 对机器人长时 rollout、具身规划，乃至驾驶仿真都很危险，但过去缺少可诊断、可修复的框架。
核心创新点：作者把 hallucination 明确定义为 state-action coverage 问题，而不是单纯模型容量不足；同时提出 MMBench2 数据集与三类预测信号，既用于提前检测失败，也用于指导 targeted data collection。
方法机制或模型结构：基于 427 小时、210 个任务、带 ground-truth actions/rewards/live simulators 的数据训练 3.5 亿参数 world model，并区分 perceptual、action-marginalized、scene-diverging 三类 hallucination。训练期用 coverage-aware sampling 补 coverage，在线期把 hallucination predictor 当 curiosity reward 继续采数修复。
实验设置和关键结果：摘要给出的关键结果是：模型能在完全未见环境中，仅用 50 条真实轨迹完成高数据效率微调，显著缓解 hallucination；同时三种轻量预测信号能较准确地预判模型会在哪里失败。
为什么值得关注：这项工作把“world model 不可靠”从经验抱怨变成了可度量、可操作的问题定义。对机器人控制、具身规划、长期仿真训练都很关键。
可能局限或后续可跟进点：摘要没有展开各检测信号的误报/漏报代价，也未说明更大模型或更长时域下结论是否保持；后续应关注部分可观测场景和真实机器人在线采数成本。

7. OctoSense: Self-Supervised Learning for Multimodal Robot Perception
链接：https://arxiv.org/abs/2606.27317
作者/机构：Anthony Bisulco, Jeremy Wang, Kostas Daniilidis, Randall Balestriero, Pratik Chaudhari；机构未在 arXiv 摘要页明确给出
时间：2026-06-25 提交/更新
要解决的问题/痛点：真实机器人与自动驾驶系统的问题从来不是“缺传感器”，而是多模态传感器之间存在不同表示、频率、延迟与噪声，而且夜间和退化环境会放大这些不一致。
核心创新点：提出 OctoSense 开源传感平台与 59 小时同步数据集，融合 stereo RGB、事件相机、LiDAR、热成像、IMU、RTK-GPS 和本体信息；并设计 late-fusion masked autoencoder 做多模态自监督表征学习。
方法机制或模型结构：模型使用 modality-specific tokenizers 适配不同传感器的时空特性，并在推理时缓存各模态 token，使新观测到来时可以快速更新表示，从而兼顾异步多模态与实时部署需求。
实验设置和关键结果：数据覆盖不同环境、不同时间段以及传感器退化场景。摘要给出的结果是：在 optical flow、depth、semantic segmentation 和 ego-motion（平移、旋转、转向角）估计上优于 image-only foundation model；表征计算时间为 NVIDIA 5090 上 6.68 ms、Orin NX 上 112 ms，并且在夜间或传感退化条件下仍保持鲁棒预测。
为什么值得关注：这篇工作把自动驾驶式多传感器堆栈和机器人式自监督学习真正接起来了，既有数据集价值，也有部署体系价值。
可能局限或后续可跟进点：摘要暂未给出跨平台泛化、长期部署稳定性与缺失模态情形的细节；后续值得跟进其对标定误差、极端天气与不同移动平台的鲁棒性。

【趋势总结】
1. 这批论文最明显的共同点，是研究重点从“盲目把模型做大”转向“把结构、训练信号和系统接口做对”。G2DP 用稠密时空代价场约束扩散规划，RouterVLA 用策略路由替代单模型崇拜，Hallucination in World Models 则直接补 world model 的可靠性短板。
2. 自动驾驶方向的新意在于更强调闭环约束与低时延系统能力，而不是只做离线 perception/planning 指标。G2DP 和 FAR-LIO 分别代表规划侧与定位侧都在往“真实系统可部署”推进。
3. 机器人方向出现两条并行趋势：一条是 ABC 这种开放栈，试图把数据、训练、仿真和真实评测连成公共基座；另一条是 VibeAct、OctoSense 这类工作，把过去被低估的触觉、多模态异步感知重新抬到核心位置。
4. 与前一阶段偏“视觉语言大模型一把梭”的路线相比，最近一批工作更重视结构化中间表示、路由机制、触觉/滑移反馈、world model 诊断、系统工程时延这些更贴近物理执行面的因素，这种回归现实约束的趋势值得持续跟进。
