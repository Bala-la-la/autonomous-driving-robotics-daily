arXiv 自动驾驶与机器人晨报｜2026-06-10

说明：今天是 2026-06-10。按 2026-06-10 检索，arXiv recent 最新可见高相关批次主要包括 2026-06-09 列表中新出现、摘要页时间为 2026-06-08 的机器人/具身论文，以及 2026-06-05 提交、近 4-5 天内最值得跟进的自动驾驶论文。因此本期明确混合“最新一批 + 最近 3-5 天高相关补充”，并在每篇里标注日期。

一、自动驾驶

1. Planning-aligned Token Compression for Long-Context Autonomous Driving
链接：https://arxiv.org/abs/2606.07464
作者/机构：Zhixuan Liang, Yuxiao Chen, Yurong You, Peter Karkus, Wenhao Ding, Boyi Li, Alexander Popov, Yan Wang, Maximilian Igl, Yiming Li, Danfei Xu, Nikolai Smolyanskiy, Boris Ivanovic, Ping Luo, Marco Pavone；摘要页未直接列机构
提交时间：2026-06-05
要解决的问题/痛点：端到端驾驶模型一旦引入长历史上下文，token 和显存会迅速爆炸；而简单的时间衰减或启发式压缩，往往把真正决定 stop / yield / proceed 的关键历史一起压掉。
核心创新点：提出 COMPACT-VA，把“压缩什么记忆”直接和规划目标绑定，不再把 token compression 当成独立预处理。模型学习保留对后续行为最关键的历史，而不是保留平均意义上最完整的信息。
方法机制/模型结构：核心是 conditional VQ-VAE working memory。posterior encoder 在训练时从未来轨迹蒸馏 planning intent；prior encoder 用压缩后的观测去预测该隐变量；压缩记忆与预测到的规划意图一起送入 policy 端端优化。
实验设置和关键结果：作者专门挑了高动态、强依赖历史的驾驶场景做评估，并设计行为指标。在相近 token 预算下，成功率提升超过 6%，达到 68.3%；闭环驾驶性能保持稳定，同时实现 3.3 倍加速和 2.7 倍显存下降。
为什么值得关注：这不是单纯追求更大 backbone，而是直击“长上下文驾驶跑不起来”的部署瓶颈。若泛化稳定，COMPACT-VA 更像一个可插拔 memory 压缩层，能直接服务已有 driving foundation model。
可能局限或后续点：摘要没有展开极端遮挡、交通规则冲突、多车博弈下的信息保真度，也值得继续跟它在不同 backbone、不同 memory budget 下的收益边界。

2. Test-Time Trajectory Optimization for Autonomous Driving
链接：https://arxiv.org/abs/2606.07170
作者/机构：Yihong Xu, Eloi Zablocki, Yuan Yin, Elias Ramzi, Ellington Kirby, Alexandre Boulch, Matthieu Cord；摘要页未直接列机构
提交时间：2026-06-05
要解决的问题/痛点：很多端到端 planner 都是“先提候选轨迹，再做 scorer 排序”。问题是 scorer 只能选优，不能把候选本身变好；如果候选池不行，后端再聪明也无能为力。
核心创新点：提出 TOAD，把 learned scorer 从 reranker 升级为测试时可优化轨迹的 reward function。
方法机制/模型结构：推理阶段直接在基础 planner 提供的候选上 warm-start，使用 Cross-Entropy Method 做 test-time trajectory search；因此无需重训底层 planner，也不绑定特定架构，属于 plug-and-play 优化层。
实验设置和关键结果：在 6 个 base planner 上验证。摘要给出 NAVSIM-v1 达到 94.7 PDMS，NAVSIM-v2 达到 56.3 EPDMS，并且在闭环 HUGSIM 上也持续带来提升。
为什么值得关注：它代表一种很务实的方向，不再一味重训更大的 planner，而是把已有 scorer 真正转成“会修轨迹”的优化器。对工业系统来说，这种增量改造通常比重构整栈更现实。
可能局限或后续点：CEM 会引入额外时延，真实车端预算下是否仍稳健值得继续看；另一个风险是 test-time search 可能过拟合 scorer 偏好，而非真实安全性。

3. VeriDrive: Verifiable Counterfactual Supervision for Cost-Efficient Vision-Language Planning
链接：https://arxiv.org/abs/2606.07338
作者/机构：Zikai Zhang, Hubert P. H. Shum, Toby P. Breckon；摘要页未直接列机构
提交时间：2026-06-05
要解决的问题/痛点：驾驶 VLM / VLA 越来越依赖 reasoning supervision，但自由文本 rationale 生成贵、难验证，而且“像推理”不等于“真有用监督”。
核心创新点：把驾驶 reasoning 改写成可验证、可反事实修正的结构化监督链，而不是继续堆自由文本 CoT。
方法机制/模型结构：VeriDrive 构造 Perception-Evaluation-Revision 三段式链路。先 grounding 关键交通参与者及未来运动，再用可规则检查的证据评估候选 ego 轨迹风险，最后把高风险意图修正到更接近 expert 的规划目标；数据构建上采用 local generation + validator-guided selective correction，只把难样本升级给更贵模型。
实验设置和关键结果：作者基于 nuScenes 构建 VeriDrive 数据集，并按 Omni-Q protocol 训练。摘要明确指出，在 open-loop 评估中，L2、Collision、Intersection 均优于 OmniDrive，同时显著降低 token 使用、生成耗时和实际付费模型成本。
为什么值得关注：这篇论文把“推理监督”从不可审计的文本泡沫拉回到可检查中间变量和可控标注成本，更贴近真实数据生产流水线。
可能局限或后续点：目前公开结果仍以 open-loop 为主；闭环收益、跨法规域迁移、长尾场景修正质量还需要后续验证。

二、机器人 / 具身智能

4. MemoryVLA++: Temporal Modeling via Memory and Imagination in Vision-Language-Action Models
链接：https://arxiv.org/abs/2606.09827
作者/机构：Hao Shi, Weiye Li, Bin Xie, Yulin Wang, Renping Zhou, Tiancai Wang, Xiangyu Zhang, Ping Luo, Gao Huang；摘要页未直接列机构
提交/更新时间：2026-06-08（2026-06-10 检索时属于最新可见批次）
要解决的问题/痛点：大量 VLA 仍然过度依赖当前帧，长时依赖任务里既记不住过去交互，也不会想象未来状态演化，因此在需要阶段记忆和前瞻的操作任务上很容易掉链子。
核心创新点：把 working memory、episodic memory 和 future imagination 三件事同时塞回 VLA，而不是只做单一历史缓存。
方法机制/模型结构：预训练 VLM 先把当前观测编码为 perceptual / cognitive tokens，构成工作记忆；这些 token 再查询一个 Perceptual-Cognitive Memory Bank，检索并整合历史低层细节与高层语义；随后 world model 在去噪 latent 空间中想象未来状态，再与历史记忆融合，得到完整 temporal-aware tokens，最后条件化 diffusion action expert 生成动作序列。
实验设置和关键结果：覆盖 5 个仿真 benchmark 和 3 类真实机器人任务、3 台机器人，涉及通用操作、长时任务、鲁棒性和泛化。摘要给出的代表性结果是：真实机器人上，general / memory-dependent / imagination-dependent 任务分别提升 9%、26%、28%。
为什么值得关注：很多具身论文只强调“更多视觉、更大语言模型”，MemoryVLA++ 则把时间建模明确拆成记忆与想象两个功能模块，方向上比继续堆当前帧编码更有研究价值。
可能局限或后续点：摘要没有给出推理时延和长期 memory bank 的维护成本；如果内存检索或 future imagination 太重，真实闭环频率可能成为下一步瓶颈。

5. AHA-WAM: Asynchronous Horizon-Adaptive World-Action Modeling with Observation-Guided Context Routing
链接：https://arxiv.org/abs/2606.09811
作者/机构：Jisong Cai, Long Ling, Shiwei Chu, Zhongshan Liu, Jiayue Kang, Zhixuan Liang, Wenjie Xu, Yinan Mao, Weinan Zhang, Xiaokang Yang, Ru Ying, Ran Zheng, Yao Mu；摘要页未直接列机构
提交/更新时间：2026-06-08（2026-06-10 检索时属于最新可见批次）
要解决的问题/痛点：现有 world-action model 往往把视频世界预测和动作执行绑在同一时间分辨率，导致 world branch 反复建模很多近场冗余帧变化，效率低且浪费容量。
核心创新点：提出“异步世界建模 + 高频动作闭环执行”。世界模型不必和控制器同频刷新，而是作为低频长视野规划器给动作模块持续供上下文。
方法机制/模型结构：整体是 dual Diffusion Transformer。video DiT 作为低频 world planner，滚动维护过去观测的 key-value memory，并输出层级 latent context；action DiT 作为高频执行器，通过 layerwise joint attention 查询这些世界上下文。为支撑异步控制，作者又设计了 horizon-adaptive offset training 与 Observation-Guided Video-Context Routing。
实验设置和关键结果：在 RoboTwin 和真实操作任务上，无需 robot-data pretraining 即达到 SOTA；摘要给出 RoboTwin 平均成功率 92.80%，4 个真实任务平均 78.3%，闭环频率 24.17 Hz，较 Fast-WAM 加速 4.59 倍。
为什么值得关注：AHA-WAM 不是单纯做 world model 更准，而是把“世界预测该低频跑、动作控制该高频跑”这个系统设计讲清楚了，对真实机器人闭环尤其重要。
可能局限或后续点：异步上下文在强接触和突发扰动场景下会不会变旧，是值得继续盯的风险；另外它在更开放任务分布上的泛化仍需看后续结果。

6. ReCoVLA: VLM-Guided Reward Compilation for Failure Recovery in Vision-Language-Action Policies
链接：https://arxiv.org/abs/2606.09630
作者/机构：Haodi Hu, Chung-Ta Huang, Jing Liu, Ye Wang, Kei Suzuki, Matthew Brand, Toshiaki Koike-Akino；摘要页未直接列机构
提交/更新时间：2026-06-08
要解决的问题/痛点：VLA 在标准分布内表现不错，但一旦进入 off-nominal state，往往缺少有针对性的恢复策略；直接微调整个 VLA 又代价高、稳定性差。
核心创新点：提出 failure-conditioned residual recovery，把 VLM 用作“语义奖励编译器”而不是直接动作生成器。
方法机制/模型结构：保持预训练 VLA 冻结，外部 VLM 负责推断失败类型与恢复阶段，并选择任务相关 reward mask 与 descriptor；随后在仿真中训练 residual recovery policy，再做 zero-shot sim-to-real 部署。核心思想是把高层失败理解和低层修正控制解耦。
实验设置和关键结果：覆盖短时、长时和强接触 manipulation。摘要给出：仿真中平均成功率从微调版 pi0.5 baseline 的 36.7% 提升到 66.7%；真实世界 zero-shot sim-to-real 平均成功率达到 61.7%，优于对比方法。
为什么值得关注：具身领域开始越来越重视“失败后怎么办”，而不只是“正常演示里成功率多少”。ReCoVLA 抓的是一个非常工程化、也非常缺少系统解法的问题。
可能局限或后续点：依赖外部 VLM 进行 failure semantics 解析，若视觉描述本身不稳，奖励编译也会偏；不同机器人与任务模板上的迁移值得继续跟。

三、交叉方向

7. Your Model Already Knows: Attention-Guided Safety Filter for Vision-Language-Action Models
链接：https://arxiv.org/abs/2606.09749
作者/机构：Seongbin Park, Fan Zhang, Baharan Mirzasoleiman, Shahriar Talebi, Nader Sehatbakhsh；摘要页未直接列机构
提交/更新时间：2026-06-08
要解决的问题/痛点：VLA policy 虽然能端到端完成操作，但对场景里的无关物体缺少碰撞保证。现有安全过滤器常靠额外 VLM 先识别障碍物，速度太慢，通常只能在 episode 开头调用一次，无法处理动态障碍。
核心创新点：作者发现 VLA 内部少数 attention heads 已经隐式学会定位当前目标物体，于是直接拿这些内部信号做实时安全过滤。
方法机制/模型结构：系统每一步从 VLA attention heads 提取 active target，把其余场景元素视作障碍，再接入 Control Barrier Function 过滤器；配合轻量实时 tracker，就能持续跟踪移动障碍，且整个过程 training-free。
实验设置和关键结果：在扩展后的 SafeLIBERO（含动态障碍）上评估。静态场景中，效果接近使用特权状态的 oracle；动态障碍场景下，平均比这个只在初始化做目标识别的 oracle 高 43%。
为什么值得关注：这篇论文的重要启发是，安全所需的感知信号未必需要额外模型，很多时候已经藏在 VLA 内部表征里。把这些隐式表征提出来，比再堆一个外部 guardian model 更轻更实用。
可能局限或后续点：如果 attention heads 在更复杂场景里失去稳定可解释性，这种安全层可能退化；不同 backbone 是否都存在同样“可提取目标头”仍需继续确认。

8. Efficient Minimal Solvers for Relative Pose Estimation in Autonomous Driving Applications
链接：https://arxiv.org/abs/2606.09569
作者/机构：Tao Li, Liang Liu, Jianli Han, Weimin Lv；摘要页未直接列机构
提交/更新时间：2026-06-08
要解决的问题/痛点：多相机视觉定位和环境感知在自动驾驶、机器人导航里都很基础，但经典相对位姿估计 often 需要较多特征匹配且代数求解复杂，RANSAC 假设生成成本高，实时性受限。
核心创新点：提出统一框架下的三类高效 minimal solver，围绕新 translation parameterization 与一阶 rotation approximation 展开，并分别吃掉 IMU 垂直方向先验、转向轴先验和地面车辆平面运动先验。
方法机制/模型结构：本质上是把自动驾驶场景中天然可得的物理先验显式注入位姿求解，从而减少最小点对应数与多项式复杂度，让 RANSAC 里的 hypothesis generation 更快。
实验设置和关键结果：在合成数据和 KITTI benchmark 上验证。摘要未给具体数值，但明确指出，相比现有 SOTA 方法，速度与精度之间取得了更优平衡，更适合时间敏感的车载系统。
为什么值得关注：在 end-to-end 热潮下，这类“几何求解器级别”的基础论文容易被忽视，但真正上车或上机器人时，鲁棒几何前端仍然决定了很多系统底线。
可能局限或后续点：收益高度依赖先验是否成立，例如非平整路面、剧烈颠簸和非标准相机布置下效果如何，需要看全文实验细节。

趋势总结

1. 最近这批论文的共同点不是继续盲目放大模型，而是把部署中的硬瓶颈拆开解决：自动驾驶在压长上下文、测试时优化、可验证监督、感知误差注入；机器人在时间建模、异步 world model、失败恢复、安全过滤。

2. 自动驾驶与具身智能正在明显共享一套方法论：更重视 memory、test-time adaptation、可验证中间变量、结构化恢复和安全约束，而不是把一切都塞进黑盒 policy。

3. 和上一波“端到端直接吐动作/轨迹”相比，新意在于把规划、监督、恢复、安全、部署重新拆成可审计模块。社区现在开始更认真地同时算两本账：性能账，以及算力/时延/安全/标注成本账。

4. 接下来最值得继续跟踪的是：COMPACT-VA 能否跨 backbone 稳定泛化，TOAD 在严格时延预算下能否保持收益，MemoryVLA++ 与 AHA-WAM 的时间建模是否真能规模化落地，以及 ReCoVLA / Safety Filter 这类“失败恢复 + 安全层”能否成为 VLA 系统标配。
