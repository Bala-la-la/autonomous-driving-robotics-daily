arXiv 自动驾驶与机器人晨报｜2026-06-29

说明：按 2026-06-29 北京时间抓取。联网检索后，当前能检索到的最新高相关 arXiv 提交/更新主要集中在 2026-06-25 UTC，少量补充到 2026-06-24 UTC；因此本期明确按这两天的最新一批论文整理。作者信息来自 arXiv 条目；机构若 arXiv 摘要页未明确列出，则注明“未在 arXiv 摘要页明确给出”。

【自动驾驶】
1. Proposal-Conditioned Latent Diffusion for Closed-Loop Traffic Scenario Generation
链接：https://arxiv.org/abs/2606.27123
作者/机构：Shubham Vaijanath Phoolari, Aleyna Kara, Christoph Lauer, Steven Peters；机构未在 arXiv 摘要页明确给出
时间：2026-06-25 提交/更新
要解决的问题/痛点：闭环交通仿真不仅要“生成像样的轨迹”，还要在 rollout 过程中持续维持多车交互的一致性、可控性与安全性。已有 diffusion 场景生成方法虽然真实感强，但采样成本高，难放进自动驾驶规划或重规划环路中反复调用。
核心创新点：作者把扩散式场景生成做成 proposal-conditioned latent diffusion。它不从纯噪声慢慢采，而是引入 multimodal proposal priors 作为更接近可行解的初始化，再结合 instance-centric scene context 保证场景级一致性；需要时还能在测试时追加 guidance，定向塑造更安全或更具挑战性的行为。
方法机制或模型结构：一方面用 compact action-latent representation 压缩生成空间，减少每步去噪成本；另一方面用 proposal-based initialization 提高采样效率，并保留 test-time guidance 入口，在不重新训练模型的情况下调节 realism、safety、controllability 之间的权衡。
实验设置和关键结果：实验基于 Waymo Open Motion Dataset，关注多车互动场景下的 realism、安全性与可控性平衡。摘要没有给出单个统一分数，但明确指出该方法在 diverse interactive scenarios 中实现了更好的综合平衡，并且 test-time guidance 可以系统性地调节多个目标之间的 trade-off。
为什么值得关注：这篇工作很贴近自动驾驶仿真的真实使用方式。它不是单纯追求“更会生成”，而是把生成器朝可插入规划闭环、可在推理时定向调参的工程组件推进。
可能局限或后续可跟进点：摘要未披露绝对时延、与现有 closed-loop simulator 的集成成本，以及 guidance 加入后是否会牺牲多样性；后续值得关注其在更长时域和更极端交互场景中的稳定性。

2. PlanRL: A Trajectory Planning Architecture for Reinforcement Learning-based Driving Experts
链接：https://arxiv.org/abs/2606.26858
作者/机构：Joonhee Lim, Yongjae Lee, Jangho Shin, Dongsuk Kum；机构未在 arXiv 摘要页明确给出
时间：2026-06-25 提交/更新
要解决的问题/痛点：很多 RL 驾驶专家直接输出油门和转向，虽然端到端，但可解释性差、学习道路几何的空间复杂度高，而且与当前主流 planning-first 的自动驾驶架构兼容性弱。
核心创新点：PlanRL 把 RL policy 从“直接控制器”重构成“轨迹规划器的一部分”。作者用 Frenet 坐标系给策略引入结构化道路先验，再把多项式轨迹规划和运动学可行性检查接在策略后面，使 RL 负责高层决策，而不是直接在原始控制空间硬学所有几何与动力学约束。
方法机制或模型结构：前端 policy 在 Frenet-frame curvilinear space 里输出更容易学习的轨迹相关决策；后端 polynomial-based trajectory planner 生成平滑轨迹，并用 kinematic feasibility check 保证结果不超出车辆物理极限，从而抑制 planning-based system 中常见的累计跟踪误差。
实验设置和关键结果：在 CARLA Offline Leaderboard v1 与 NoCrash benchmark 上评测。摘要给出的结果是：相对已有 SOTA control-based RL experts，driving score 分别提升 5% 和 11%，success rate 分别提升 8% 和 19%。
为什么值得关注：这是一条“RL 向工程可用形态靠拢”的路线。它没有否定强化学习，而是通过结构化 planner 接口把 RL 更好地嵌入自动驾驶技术栈。
可能局限或后续可跟进点：当前结果主要来自 CARLA；后续要看它在更复杂交通参与者博弈、真实噪声传感输入与大规模闭环评测中的表现，以及轨迹规划模块会不会限制策略上限。

3. FAR-LIO: Enabling High-Speed Autonomy through Fast, Accurate, and Robust LiDAR-Inertial Odometry
链接：https://arxiv.org/abs/2606.26010
作者/机构：Maximilian Leitenstern, Marcel Weinmann, Patrick Haft, Tobias Lasser, Dominik Kulmer, Markus Lienkamp；机构未在 arXiv 摘要页明确给出
时间：2026-06-24 提交/更新
要解决的问题/痛点：高速自治系统尤其无人赛车，真正的瓶颈常常不是单纯精度，而是定位延迟、剧烈运动下的稳健性，以及能否给闭环控制持续提供平滑可信的位姿估计。传统 LIO 方法常在延迟和鲁棒性之间被迫取舍。
核心创新点：FAR-LIO 围绕“Fast, Accurate, Robust”三件事同时优化，把 CUDA voxel hashmap、sparsity-aware GICP、adaptive thresholding，以及带 upsampling 和 delay compensation 的 EKF 融合到同一套实时 LIO 框架里。
方法机制或模型结构：前端借助 novel CUDA-based voxel hashmap 做并行最近邻搜索和高效地图更新；中间层采用稀疏感知 GICP 在保持精度的同时控制延迟；后端 EKF 把 LiDAR 里程计与高频 IMU 融合，并通过延迟补偿输出更稳定的实时轨迹。
实验设置和关键结果：覆盖 4 种传感器设置、公开数据集，以及两台最高 250 km/h 的自动驾驶赛车。摘要给出的结果是：相对 SOTA 基线，平均位置误差降低 6.9%，运行时间降低 38.4%，且同一参数集能适配不同传感器配置。
为什么值得关注：这不是停留在常规 benchmark 刷指标的 LIO 论文，而是直接对准“高速真实系统能不能跑起来”的工程底盘问题。对自动驾驶、无人机与高速移动机器人都很有借鉴意义。
可能局限或后续可跟进点：摘要未展开在雨雾、点云稀疏、长时间漂移和极端退化环境中的表现；后续需要关注开源代码后的复现门槛与硬件依赖。

【机器人 / 具身智能】
4. Scalable Behavior Cloning with Open Data, Training, and Evaluation
链接：https://arxiv.org/abs/2606.27375
作者/机构：Arthur Allshire, Himanshu Gaurav Singh, Ritvik Singh, Adam Rashid, Hongsuk Choi, David McAllister, Justin Yu, Yiyuan Chen, Huang Huang, Pieter Abbeel, Xi Chen, Rocky Duan, Phillip Isola, Jitendra Malik, Fred Shentu, Guanya Shi, Philipp Wu, Angjoo Kanazawa；机构未在 arXiv 摘要页明确给出
时间：2026-06-25 提交/更新
要解决的问题/痛点：具身操作长期缺少真正可复现的大规模开放底座。很多工作只开放模型、只开放数据、或者只开放局部硬件，导致数据采集、训练、仿真代理评测和真实部署彼此割裂，研究者很难公平比较方法。
核心创新点：作者提出 ABC 全开源行为克隆栈。核心数据集 ABC-130K 含 3500 小时、13 万+ episodes、195 个任务；同时开放硬件搭建、训练基础设施、仿真管线和 400 小时 sim-teleop 数据，并给出 sim/real 共训 recipe，让仿真评测更像真实评测的可靠代理。
方法机制或模型结构：重点不只是“大数据”，而是把 teleop 数据采集、训练基础设施、simulation proxy evaluation 和真实验证串成完整闭环。作者还系统比较 DiT 与 VLA 等常见架构及训练 recipe，而不是只报一个最好模型。
实验设置和关键结果：摘要指出，基于这套开放栈训练出的策略已能完成 box folding、从钱包中抽取信用卡等灵巧任务，证明其不只是数据展示工程，而是真能支撑复杂 manipulation policy 的公共基线。
为什么值得关注：如果社区接受 ABC，它的影响可能比单篇模型论文更持久。它在尝试把机器人行为克隆从“闭门炼丹”变成可复刻、可对比、可持续迭代的公共基础设施。
可能局限或后续可跟进点：摘要没有给出与闭源超大数据栈的差距，也没细分数据质量和任务难度的贡献；后续应关注硬件复刻成本、长尾失败案例以及 sim-to-real proxy 的相关性是否稳定。

5. VibeAct: Vibration to Actions for Contact-Rich Reactive Robot Dexterity
链接：https://arxiv.org/abs/2606.27344
作者/机构：Yuemin Mao, Uksang Yoo, Jean Oh, Jonathan Francis, Jeffrey Ichnowski；机构未在 arXiv 摘要页明确给出
时间：2026-06-25 提交/更新
要解决的问题/痛点：灵巧操作里最关键的接触事件往往极快、局部且被遮挡，视觉和点云经常捕不到“滑了”“碰上了”“插歪了”这类瞬态信号，导致策略难以做反应式控制。
核心创新点：VibeAct 用 piezoelectric microphones 采集高带宽 vibro-acoustic 信号，再把真实触觉和仿真强化学习通过共享的 contact/slip 物理表征连接起来。这样就不需要在仿真里忠实复刻原始音频，也能让策略利用快速接触反馈。
方法机制或模型结构：作者先在真实灵巧手中嵌入麦克风，通过 teleoperation 采集振动波形；再把这些记录回放到 calibrated digital clone 中，自动标注每根手指的 contact/slip。tactile estimator 从真实波形预测接触与滑移，而仿真中的策略则直接在同一表征上训练。
实验设置和关键结果：覆盖 5 个接触密集任务，包括 regrasping、in-hand reorientation、insertion。摘要明确指出：VibeAct 在仿真中持续优于 proprioception + point-cloud 基线，在需要持续反应控制的任务上收益最大，其中 continuous slip-magnitude channel 最有信息量；学到的策略还能迁移到真实手臂平台并提升成功率。
为什么值得关注：这类工作表明具身系统不应再只押注视觉。VibeAct 代表一种成本相对低、带宽却很高的“弱触觉”传感路线，可能会显著提升接触型操作的实用性。
可能局限或后续可跟进点：麦克风方案可能受结构安装、材料和环境噪声影响；后续应看其跨手型、跨材质、跨任务和长期使用下的泛化与耐久性。

6. RouterVLA: Turning Smoke Tests into Supervision for Heterogeneous VLA Selection
链接：https://arxiv.org/abs/2606.27355
作者/机构：Xingyu Ren, Chugang Yi, Ge Ma, Youran Sun；机构未在 arXiv 摘要页明确给出
时间：2026-06-25 提交/更新
要解决的问题/痛点：现实机器人团队往往手里有多套 frozen VLA policy，每个 expert 各有所长，但部署时常被压缩成“全局选一个最好模型”。这样会白白丢掉 smoke tests 中已经显现的策略差异。
核心创新点：RouterVLA 的创新不在训更大模型，而在把 pre-deployment evaluation rollouts 重新变成 policy routing supervision。它把 commissioning 过程本身视为系统能力来源，而不是把所有收益都归因给单个大模型。
方法机制或模型结构：作者采用 outcome-disjoint cross-fitting。已记录 probes 用来给每个 expert 建 profile，独立 trial 再用于评估被选中的 expert，避免把同一试验既用于建模又用于验证，导致收益虚高。摘要还特别强调“透明 probe-success rule”已足够强，额外 scalar scorer capacity 并未显著创造新收益。
实验设置和关键结果：在 34,752 条 LIBERO-Plus rollout records 上，held-out success 从 0.4686 提升到 0.6149，增益为 +14.64 个百分点。若错误复用同一 scored trial，收益会被夸大到 1.87 倍。
为什么值得关注：这篇论文提醒具身领域一个很现实的事实: 系统层收益未必来自“更大的统一 VLA”，而可能来自更好的策略组合与选择机制。对于多任务、多机器人团队尤其重要。
可能局限或后续可跟进点：当前结论主要建立在 scalar-only profiles；后续需要验证更丰富上下文、在线路由延迟以及真实机器人噪声下的稳健性。

【交叉方向】
7. Hallucination in World Models is Predictable and Preventable
链接：https://arxiv.org/abs/2606.27326
作者/机构：Nicklas Hansen, Xiaolong Wang；机构未在 arXiv 摘要页明确给出
时间：2026-06-25 提交/更新
要解决的问题/痛点：生成式 world model 经常出现“画面看起来像真，动力学其实已经偏了”的 hallucination。对机器人规划、长时 rollout，乃至驾驶仿真而言，这类错误比画面瑕疵更危险，但过去缺少成体系的诊断与修复框架。
核心创新点：作者把 hallucination 归因为 state-action coverage 缺口，而不是笼统地归因给模型太小或训练不够久；同时提出 MMBench2 数据集、三类 hallucination mode 和对应预测信号，把“世界模型哪里会坏”从模糊经验变成可检测对象。
方法机制或模型结构：基于 427 小时、210 个任务、带 ground-truth actions/rewards/live simulators 的数据训练 3.5 亿参数世界模型，区分 perceptual、action-marginalized、scene-diverging 三类失败模式；训练期用 coverage-aware sampling 补 coverage，在线期则把 hallucination predictors 当 curiosity reward 做 targeted data collection。
实验设置和关键结果：摘要给出的关键结果是：在完全未见环境中，只用 50 条真实环境轨迹就能对预训练世界模型做数据高效微调并缓解 hallucination；三种轻量信号也能较准确预测模型会在哪些状态动作区域失败。
为什么值得关注：这篇论文的价值在于把 world model 的“不可托付感”拆成了可诊断、可补救的问题。对机器人控制、具身规划、仿真驱动训练都是基础性进展。
可能局限或后续可跟进点：摘要未展开误报/漏报代价，更没说明在更大模型、部分可观测环境和更长时域下是否仍然成立；真实机器人在线补数成本也需要进一步量化。

8. OctoSense: Self-Supervised Learning for Multimodal Robot Perception
链接：https://arxiv.org/abs/2606.27317
作者/机构：Anthony Bisulco, Jeremy Wang, Kostas Daniilidis, Randall Balestriero, Pratik Chaudhari；机构未在 arXiv 摘要页明确给出
时间：2026-06-25 提交/更新
要解决的问题/痛点：真实机器人和自动驾驶系统并不缺传感器，难点在于多模态之间表示形式、频率、延迟和噪声完全不同，一到夜间或退化环境就更难对齐和稳健融合。
核心创新点：OctoSense 一次性把 stereo RGB、事件相机、LiDAR、热成像、IMU、RTK-GPS 与本体信息整合到开源传感平台和 59 小时同步数据集里，并提出 late-fusion masked autoencoder 做多模态自监督学习。
方法机制或模型结构：模型使用 modality-specific tokenizers 适配不同传感器的时空特性，并在推理阶段缓存各模态 token，随着新测量到来增量更新表示，兼顾异步多模态与部署时延。
实验设置和关键结果：数据覆盖不同环境、不同时间段和传感器退化情形。摘要给出的结果是：在 optical flow、depth、semantic segmentation 与 ego-motion 估计上优于 image-only foundation model；表征计算时间在 NVIDIA 5090 上为 6.68 ms、在 Orin NX 上为 112 ms，且在夜间与传感退化条件下仍保持鲁棒预测。
为什么值得关注：它把自动驾驶式多传感器堆栈与机器人式自监督表征真正结合起来了，不只是新数据集，也是在探索一条更现实的具身感知基础模型路线。
可能局限或后续可跟进点：摘要暂未披露跨平台泛化、缺失模态恢复、标定误差敏感性与极端天气表现；后续值得关注其在更多机器人平台上的迁移能力。

【趋势总结】
1. 最近一批论文最明显的共同点，是研究重点从“把模型做得更大”转向“把系统接口、结构约束和训练信号做对”。Proposal-conditioned scenario diffusion、PlanRL、RouterVLA 和 hallucination diagnosis 都体现了这种偏向。
2. 自动驾驶方向正在明显回到闭环和系统工程现实：场景生成开始强调可控重规划，RL 驾驶专家开始向轨迹规划接口靠拢，定位系统则直接对准高速低延迟闭环控制。
3. 机器人方向出现两条并行趋势：一条是 ABC 这种开放栈，试图把数据、训练、仿真与真实评测连成公共基座；另一条是 VibeAct、OctoSense 这类工作，把触觉、多模态异步融合和弱光退化鲁棒性重新抬到核心位置。
4. 与前一阶段更偏“视觉语言大模型一把梭”的路线相比，这批论文的新意在于更重视物理可行性、组合式系统收益、world model 可靠性诊断，以及真实部署中的时延与传感约束。这种回归现实约束的趋势，值得连续跟踪。
