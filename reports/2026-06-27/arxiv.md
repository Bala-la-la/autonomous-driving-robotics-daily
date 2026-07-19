arXiv 自动驾驶与机器人晨报｜2026-06-27

说明：按 2026-06-27 北京时间抓取。最新高相关新稿主要集中在 2026-06-25 UTC；其中“自动驾驶”纯相关强稿偏少，因此按要求补入 2026-06-24 UTC 的高相关论文，并在条目中明确日期。作者信息来自 arXiv 条目；机构若摘要页未明确列出，则注明“未在摘要页明确给出”。

【自动驾驶】
1. G2DP: Diffusion Planning with Spatio-Temporal Grid Guidance
链接：https://arxiv.org/abs/2606.26017
作者/机构：Hang Yu 等；机构未在摘要页明确给出
时间：2026-06-24 提交，2026-06-25 更新
问题/痛点：扩散式规划能生成多样轨迹，但闭环执行里常因采样随机性出现碰撞、偏航或不跟路，尤其在高交互交通场景里，靠稀疏几何 query 或事后修补的 guidance 往往不够稳。
核心创新点：把 guidance 从“看几个对象/关键点”升级成“直接看整块时空代价场”。作者将未来 occupancy 分布与 route-progress map 融合成可微的 spatio-temporal cost volume，在 denoising 过程中持续注入密集安全梯度。
方法机制/模型结构：核心是把 cost volume 写成连续 safety energy functional，使每一步扩散去噪都被环境级约束直接牵引，轨迹会被推向 collision-free 且 progress-optimal 的区域，而不是先生成再补救。
实验设置和关键结果：闭环评测覆盖 nuPlan，并做 zero-shot 转移到 interPlan 和 DeepScenario。摘要给出的关键结果是：相对最强 imitation learning 基线，nuPlan reactive score 提升 +7.2；在 interPlan 上，相对无 guidance 版本，collision avoidance 提升 +10.15。
为什么值得关注：这条路线代表自动驾驶规划从“能生成像样轨迹”转向“生成过程可控、可约束、适合闭环系统”。对扩散规划真正落地很关键。
可能局限/后续可跟进点：摘要未披露推理时延、算力开销，以及在极端博弈场景下是否会过保守；后续要看真实车部署与更差地图条件下的稳定性。

2. FAR-LIO: Enabling High-Speed Autonomy through Fast, Accurate, and Robust LiDAR-Inertial Odometry
链接：https://arxiv.org/abs/2606.26010
作者/机构：Maximilian Leitenstern 等；机构未在摘要页明确给出
时间：2026-06-24 提交/更新
问题/痛点：高速自治系统，尤其无人赛车，真正痛点不是离线最优精度，而是低延迟、抗动态扰动、还能稳定闭环控制的里程计。传统 LIO 很容易在精度和延迟之间二选一。
核心创新点：提出 CUDA 加速的 FAR-LIO，从底层数据结构开始围绕实时性重写，包括 CUDA voxel hashmap、稀疏感知 GICP 和带 delay compensation 的 EKF 融合。
方法机制/模型结构：前端用 CUDA voxel hashmap 并行做最近邻搜索和地图更新；配准层用 adaptive density + sparsity-aware GICP 压低计算；后端 EKF 用 upsampling 和延迟补偿融合 LiDAR 与高频 IMU。
实验设置和关键结果：在 4 种传感器设置、公开数据集以及两台最高 250 km/h 自动驾驶赛车上评测。摘要给出的结果是：相对 SOTA 基线，平均位置误差降低 6.9%，运行时间降低 38.4%，且同一套参数即可适配多设置。
为什么值得关注：这不是单纯刷 benchmark，而是正面解决高速 autonomy 的 latency bottleneck，对赛事、无人配送车和高速移动平台都很有参考价值。
可能局限/后续可跟进点：摘要没有拆分不同传感器配置下的收益来源，也未展开雨雾、长时间漂移和稀疏点云退化场景；要继续跟进开源代码的可复现性。

【机器人 / 具身智能】
3. Scalable Behavior Cloning with Open Data, Training, and Evaluation
链接：https://arxiv.org/abs/2606.27375
作者/机构：Arthur Allshire 等 18 位作者；机构未在摘要页明确给出
时间：2026-06-25 提交/更新
问题/痛点：具身操作领域长期缺的是“可复现的大规模开放栈”而不只是单篇模型。数据、硬件、训练流程、sim-to-real 对齐都碎片化，导致很多方法难以公平比较。
核心创新点：提出 ABC 全开源行为克隆栈，核心是 ABC-130K 数据集：3500 小时、13 万+ episode、195 个任务，并同时开源硬件配置、训练基础设施、仿真管线和 400 小时 sim-teleop 数据。
方法机制/模型结构：作者不只发数据，而是提供 real/sim 共训 recipe，让仿真评测与真实世界结果形成更可信的相关性，用于低成本消融 DiT 与 VLA 等模型设计决策。
实验设置和关键结果：比较多种训练 recipe 和常见 DiT/VLA 架构，并落到真实世界操作。摘要点名展示的任务包括折盒子、从钱包中取信用卡等灵巧操作，证明开放栈不只停留在离线数据整理层。
为什么值得关注：如果这个栈被社区真正复用，它对机器人领域的意义可能不只是“又一个数据集”，而是推动行为克隆实验从不可比、难复现，转向可扩展的开放基线。
可能局限/后续可跟进点：摘要没给出与闭源或更大私有数据栈的绝对差距；后续应关注数据质量分布、任务难度分层，以及开放硬件方案的门槛是否真的足够低。

4. VibeAct: Vibration to Actions for Contact-Rich Reactive Robot Dexterity
链接：https://arxiv.org/abs/2606.27344
作者/机构：Yuemin Mao 等；机构未在摘要页明确给出
时间：2026-06-25 提交/更新
问题/痛点：接触型灵巧操作里，关键事件往往发生得快、局部且视觉遮挡严重。只靠视觉或点云，机器人很难及时知道什么时候发生了接触、打滑或插入失败。
核心创新点：提出 VibeAct，用压电麦克风采集 vibro-acoustic 信号，再通过共享的 contact/slip 表征把真实触觉与仿真强化学习桥接起来，避免直接模拟原始音频。
方法机制/模型结构：真实系统中，作者把麦克风嵌入灵巧手，遥操作采集振动数据；再在 calibrated digital clone 中回放，自动标注每根手指的 contact/slip。随后训练 tactile estimator 从真实波形预测接触与打滑，策略则在仿真里基于同一表征训练。
实验设置和关键结果：在 5 个接触密集任务上评测，覆盖 regrasp、手内重定向、插入等；摘要称其稳定优于 proprioception+point-cloud 基线，且在需要持续反应控制的任务上收益最大，最终能迁移到真实手臂平台并提升成功率。
为什么值得关注：具身学习正在从“看懂动作”转向“看懂接触”。VibeAct 的价值在于给低成本高带宽触觉学习提供了现实路径。
可能局限/后续可跟进点：麦克风信号对安装方式、环境噪声和材料差异可能敏感；后续要看跨任务、跨手型以及更复杂装配任务中的泛化。

5. SSI-Policy: Learning Structured Scene Interfaces for Vision-Language Robotic Manipulation
链接：https://arxiv.org/abs/2606.26800
作者/机构：Kaijun Wang 等；机构未在摘要页明确给出
时间：2026-06-25 提交/更新
问题/痛点：低数据操作学习里，很多方法要么依赖大规模预训练，要么牺牲几何结构；视频式接口容易几何漂移，3D 方法又常要求深度传感器，不利于轻量落地。
核心创新点：提出 Structured Scene Interface，把单目深度特征、语言对齐的对象布局、以及指令条件下的 2D 运动轨迹统一到一个 RGB-only 中间表示里，并与下游控制解耦。
方法机制/模型结构：SSI 是 robot-agnostic 的中间接口，可从无动作标注视频训练；这意味着感知模块能先学出可复用结构，而控制策略只需用少量 demonstration 学决策。
实验设置和关键结果：在 LIBERO 上，每任务只用 10 条 demonstration 时，相对最强已有方法提升接近 15%；同时还能接近那些使用 50 条 demo 且依赖大规模外部预训练的方法，并在 13 个真实任务上验证了空间推理、跨本体迁移和接触操作能力。
为什么值得关注：这类“先把场景结构抽出来，再学控制”的路线，可能比一味增大端到端 VLA 更适合低数据真实机器人。
可能局限/后续可跟进点：摘要没说明在强遮挡、复杂光照和长时序多阶段任务下的退化情况；还需要看 SSI 是否会限制某些更自由的操作策略。

【交叉方向】
6. Hallucination in World Models is Predictable and Preventable
链接：https://arxiv.org/abs/2606.27326
作者/机构：Nicklas Hansen, Xiaolong Wang；机构未在摘要页明确给出
时间：2026-06-25 提交/更新
问题/痛点：生成式 world model 经常“看起来合理、实际动力学已漂移”，这是机器人和具身规划走向长期 rollout 时最危险的隐患之一。
核心创新点：作者把 hallucination 明确定义为数据覆盖问题，而不是纯模型容量问题；同时提出 MMBench2 数据集与一套轻量预测信号，既能提前检测幻觉，也能指导有针对性的补数据。
方法机制/模型结构：基于 427 小时、210 个任务、带真值 action/reward/live simulator 的数据训练 3.5 亿参数 world model，并识别出 perceptual、action-marginalized、scene-diverging 三类幻觉模式；再用 coverage-aware sampling 和 curiosity 式 targeted collection 做训练期与在线期修复。
实验设置和关键结果：摘要给出的关键点是，模型可在完全未见环境中，仅用 50 条真实轨迹就完成数据高效微调，显著缓解 hallucination 问题。
为什么值得关注：这篇工作很像给“world model 为何不可靠”这件事加了可操作诊断框架，对机器人控制、具身规划乃至驾驶仿真都重要。
可能局限/后续可跟进点：摘要没有给出各类信号的误报/漏报代价，也未说明更大模型下结论是否保持；后续值得看其在更长时域和部分可观测场景的稳定性。

7. OctoSense: Self-Supervised Learning for Multimodal Robot Perception
链接：https://arxiv.org/abs/2606.27317
作者/机构：Anthony Bisulco, Jeremy Wang, Kostas Daniilidis, Randall Balestriero, Pratik Chaudhari；机构未在摘要页明确给出
时间：2026-06-25 提交/更新
问题/痛点：真实机器人与自动驾驶系统面临的不是“有没有传感器”，而是多模态传感器频率、延迟、噪声、表征都不同，夜间和退化环境更会放大这些问题。
核心创新点：提出 OctoSense 开源传感平台与 59 小时同步数据集，覆盖立体 RGB、事件相机、LiDAR、热成像、IMU、RTK-GPS，以及汽车 CAN/四足本体信息；同时提出 late-fusion masked autoencoder 做自监督表示学习。
方法机制/模型结构：模型采用 modality-specific tokenizer 适配不同传感器的时空特性，并在推理时缓存各模态 token，以便新观测一到就快速更新表示，兼顾异步多模态与实时性。
实验设置和关键结果：数据含多环境、多时段驾驶数据，并特别覆盖夜间与传感退化条件。摘要结果显示：在光流、深度、语义分割、ego-motion（平移/旋转/转向角）等任务上优于 image-only foundation model；表征计算速度为 NVIDIA 5090 上 6.68 ms、Orin NX 上 112 ms。
为什么值得关注：这篇工作把“自动驾驶式多传感器感知”和“机器人式自监督表示学习”真正接到了一起，兼具数据价值和系统价值。
可能局限/后续可跟进点：摘要暂未给出跨平台泛化和更长时间部署结果；后续值得跟进其对缺失模态、标定误差和更极端天气条件的鲁棒性。

【趋势总结】
1. 这批论文的共同信号是：研究重点正在从“把模型做大”转向“把结构和训练信号做对”。G2DP 用稠密代价场约束扩散规划，SSI-Policy 用结构化中间表示解耦感知与控制，VibeAct 和 OctoSense则是在补足现实机器人真正缺失的触觉与多模态感知信号。
2. 自动驾驶方向的新意在于更强调闭环约束和系统时延，而不是只做离线感知打分。G2DP 和 FAR-LIO 分别代表规划侧与定位侧都在往“真系统可用”推进。
3. 机器人方向的明显趋势是开放栈、低数据高效率和 test-time/online 可适应性。ABC 想解决复现与基线问题，Hallucination in World Models 直指 world model 可靠性，说明社区开始补基础设施与可靠性短板。
4. 与过去偏“视觉语言语义先行”的路线相比，最近更有新意的是：动作先验、接触力/滑移、多传感器异步融合、结构化场景接口这些更贴近物理执行面的要素，正在重新成为一等公民。
