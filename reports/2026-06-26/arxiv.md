arXiv 自动驾驶与机器人晨报｜2026-06-26

说明：本期按 2026-06-26 北京时间抓取；arXiv 最新可见高相关提交/更新主要落在 2026-06-24 UTC 与 2026-06-23 UTC。以下作者信息来自 arXiv 条目；机构若未在摘要页明确列出，则不强行推断。

【自动驾驶】
1. G2DP: Diffusion Planning with Spatio-Temporal Grid Guidance
链接：https://arxiv.org/abs/2606.26017
作者：Hang Yu, Ye Jin, Alessandro Canevaro, Julian Schmidt, Julian Jordan, Peizheng Li, Marc Kaufeld, Silvan Lindner, Johannes Betz, Wilhelm Stork
时间：2026-06-24 提交/更新
问题：扩散式规划在密集交互交通里能生成多样轨迹，但去噪过程天然带随机性；如果缺少强约束，闭环执行时容易在安全性和路线遵循上掉链子。现有 guidance 多依赖稀疏几何查询或事后修正，场景感知不够密。
创新：把 guidance 从“看几个关键体素/目标体”升级为“直接看一整块可微时空代价场”。作者提出 G2DP，用未来 occupancy 分布和 route-progress map 生成 differentiable spatio-temporal cost volume，在采样时就把安全梯度灌进 denoising loop。
机制：核心是把 cost volume 写成连续 safety energy functional。这样每一步去噪都能收到来自密集环境约束的梯度，而不是到最后再做碰撞修补；本质上是在扩散采样里做环境级、而非对象级的引导。
实验：闭环评测覆盖 nuPlan，并做 zero-shot 转移到 interPlan 和 DeepScenario。摘要给出的关键结果是：相对最强 imitation learning 基线，nuPlan reactive score 提升 +7.2；在 interPlan 上，相比无 guidance 的版本，collision avoidance 提升 +10.15，并保持各 benchmark 顶尖成绩。
为什么值得关注：自动驾驶规划的一个核心趋势，是从“会生成 plausible 轨迹”转向“闭环下可控且可约束”。G2DP 的价值在于把 dense cost map 重新拉回扩散规划主循环，比只靠 sparse query 更像真正面向量产系统的思路。
局限/跟进：摘要没有披露推理时延、不同地图质量下的敏感性，以及面对极端博弈场景时 guidance 是否会让轨迹过保守；后续值得跟进算力成本和真实车闭环表现。

2. FAR-LIO: Enabling High-Speed Autonomy through Fast, Accurate, and Robust LiDAR-Inertial Odometry
链接：https://arxiv.org/abs/2606.26010
作者：Maximilian Leitenstern, Marcel Weinmann, Patrick Haft, Tobias Lasser, Dominik Kulmer, Markus Lienkamp
时间：2026-06-24 提交/更新
问题：高速自动驾驶尤其是无人赛车场景里，里程计不仅要准，还要低延迟；动态运动剧烈、传感器噪声高、地图更新频繁时，传统 LIO 很容易在精度和时延之间顾此失彼。
创新：FAR-LIO 把“快、准、稳”一起作为目标，不是简单堆后端优化，而是从底层数据结构开始 CUDA 化。它提出 CUDA-based voxel hashmap，用于并行最近邻搜索和高效 map update，再叠加稀疏感知 GICP 与自适应阈值。
机制：前端利用带 adaptive density 的 voxel hashmap 做高并发匹配；配准层采用 sparsity-aware GICP，减少不必要计算；后端用 EKF 融合高频 IMU，并通过 upsampling 与 delay compensation 输出更平滑的姿态估计。
实验：评测覆盖四种不同传感器设置，既有公开数据集，也有两台最高时速 250 km/h 的自动驾驶赛车实测。摘要给出的关键结果是：在目标硬件上，用同一套参数相比 SOTA 基线平均位置误差降低 6.9%，运行时间降低 38.4%。
为什么值得关注：这篇论文切中的不是“再高 0.几分 benchmark”，而是高速度 autonomy 真正痛的 latency。对于赛车、无人配送车和高速移动机器人，低延迟里程计往往比离线最优精度更关键。
局限/跟进：摘要未细拆不同传感器配置下的收益来源，也未展开极稀疏点云、雨雾干扰或长时漂移下的退化行为；后续要看代码开源后的可复现性和通用性。

3. Causality-Based Parametric Control Barrier Function for Safe Multi-Vehicle Interaction
链接：https://arxiv.org/abs/2606.25134
作者：Yiwei Lyu, Caleb Chang, John M. Dolan
时间：2026-06-23 提交/更新（摘要注明 accepted ICRA 2026）
问题：多车交互安全控制里，一个老问题是周边车辆到底“为什么这么动”。如果只做 worst-case 分析，ego 车会过度保守；如果直接从观测拟合邻车控制器，又会被多车相互影响搅乱因果，难判断谁影响了谁。
创新：作者把此前 Parametric-CBF 扩展到多车场景，并显式加入 causality inference，形成 Causality-based Parametric-CBF。重点不是只学一个邻车模型，而是识别交互中的因果影响，再据此做 adaptive safety-critical control。
机制：系统从观测数据学习邻车潜在控制行为，同时在建模阶段嵌入因果推断，区分多车交互中的相互作用；随后由 learned Parametric-CBF 驱动 ego 车控制器，在保障安全的前提下利用多车运动灵活性减少保守性。
实验：摘要没有列出具体 benchmark 名称和绝对数值，但明确声称在多种 interaction-intensive 场景中，借助对多车因果关系的建模，任务效率能显著提升，同时保持安全约束。
为什么值得关注：当前自动驾驶安全控制的一条重要新线索，是从“统一假设别人都守规矩”转向“在线估计他人控制策略并自适应应对”。这篇工作把因果结构引进 CBF，比纯经验式行为预测更接近可验证安全控制。
局限/跟进：摘要没有给出量化提升、场景复杂度和计算开销；后续最值得看的是在更密集交通、非规则驾驶员和感知误差存在时，因果推断是否足够稳。

【机器人 / 具身智能】
4. Learning Action Priors for Cross-embodiment Robot Manipulation
链接：https://arxiv.org/abs/2606.26095
作者：Dong Jing, Tianqi Zhang, Jiaqi Liu, Jinman Zhao, Zelong Sun, Li Erran Li, Zhiwu Lu, Mingyu Ding
时间：2026-06-24 提交/更新
问题：多数 VLA 做法直接把 action head 挂到 VLM 上联合训练，视觉和语言先验很强，但动作模块几乎从零学“物理怎么动”。在跨本体场景下，这会让模型一开始同时处理动作时序结构与跨模态对齐，优化非常别扭。
创新：作者不是继续扩大 VLA，而是先给动作模块预训练 motion prior，再去做视觉-语言-动作对齐。整个框架分成两阶段：先学跨本体 temporal motion structure，再把这个先验转移到 VLA 训练。
机制：Stage 1 用轻量 flow-matching encoder-decoder action module，只吃无条件 action trajectory，不处理图像或文本，从而专注学习动作时序结构。Stage 2 通过 decoder reuse 和 early-stage latent distillation，把已学到的动作先验迁入 VLA，对齐 visual-language feature 与 action embedding space。额外地，训练后的 encoder 还能把 state-action history 压成一个 temporal context token，几乎不增加成本。
实验：覆盖 13 个跨本体任务，包含仿真与真实平台。摘要给出的结果方向很明确：比不带 action prior 的 VLA 收敛更快、成功率更高，尤其在真实世界少数据任务上提升更明显；而且 Stage 1 若吃到更大动作数据，后续下游 VLA 性能还能继续抬升。
为什么值得关注：这篇工作抓住了 VLA 当前一个被低估的问题：语义先验很强，不等于动作先验足够。若想走向跨机器人通用操作，先把“怎么动”抽成可迁移先验，可能比继续堆视觉语言参数更有效。
局限/跟进：摘要没有公开各任务绝对增益，也未说明当动作分布差异极大时先验是否会负迁移；后续要看在灵巧手、双臂和长时序装配任务上的表现。

5. ForceBand: Learning Forceful Manipulation with sEMG
链接：https://arxiv.org/abs/2606.26093
作者：Botao He, Zhi Wang, Linna Kuang, Ishaan Ghosh, Jitendra Malik, Cornelia Fermuller, Tingfan Wu, Jiayuan Mao, Ruoshi Liu, Haozhi Qi, Yiannis Aloimonos
时间：2026-06-24 提交/更新
问题：人类示教是操作学习最可扩展的数据源之一，但无论 mocap 轨迹还是互联网视频，通常都只有运动和外观，没有关键的接触力信息；而很多挤压、抓握、按压任务，失败恰恰就发生在力控制上。
创新：提出 ForceBand，一个低成本腕带式 sEMG 系统，把肌电和 IMU 变成 force-enriched demonstration。它不是给人手直接贴昂贵力传感器，而是先学从肌电到手指受力的映射，再给普通视频示教自动打上力标签。
机制：作者先采集 10 小时多模态数据，包含第一视角视频、sEMG、IMU 和指尖力测量；据此预训练 EMG2Force 模型，预测 per-finger force。之后只需少量 user-specific calibration，用户就能只戴 ForceBand 加视频采示教，系统再回填每根手指的力轨迹。
实验：摘要给出的关键结果是：相较视觉基线，ForceBand 的力预测误差降低超过 50%；在需要根据物体形状、大小、重量调节施力的 pick / squeeze / place 任务上，机器人成功率达到 87%。
为什么值得关注：具身学习正从“看懂动作”走向“看懂接触”。ForceBand 的意义在于它把力示教成本往下打了一大截，为大规模真实世界接触数据采集打开了更现实的路径。
局限/跟进：肌电信号天然有个体差异和漂移问题，跨人泛化、长时间佩戴稳定性、强动态场景抗噪性都需要继续验证；此外，腕部肌电能否稳定重建更细粒度手指力分布，还值得看更大规模实验。

6. In-Context World Modeling for Robotic Control
链接：https://arxiv.org/abs/2606.26025
作者：Siyin Wang, Junhao Shi, Senyu Fei, Zhaoyang Fu, Li Ji, Jingjing Gong, Xipeng Qiu
时间：2026-06-24 提交/更新
问题：标准 VLA 往往只看“当前观测 + 指令”，默认相机视角、机器人形态、系统动力学和训练时差不多。一旦换摄像头角度或换机器人，本来好用的策略常常需要重度 fine-tune。
创新：作者提出 In-Context World Modeling，把 system identification 视为上下文适应问题。关键思想不是用 context 告诉模型“做什么任务”，而是让模型先通过一小段自发、与任务无关的交互，理解“这个系统怎么运作”。
机制：ICWM 在任务执行前先读入短历史交互轨迹，让模型在 context window 中隐式估计当前系统变量和动力学；之后再执行控制，无需参数更新就能适配新配置。也就是说，world model 被拿来做 execution-context inference，而不是只做未来预测。
实验：摘要明确指出，在仿真和真实机器人平台上，ICWM 在 novel camera viewpoints 上显著优于标准 VLA baseline，证明只靠上下文适配就能改善 OOD 配置泛化。
为什么值得关注：这条路线很有代表性，它把“适配新本体/新视角”从昂贵微调问题转成 test-time in-context adaptation。对机器人基础模型来说，这比每换一个 setup 就重新训练更有现实价值。
局限/跟进：摘要目前只明确强调 novel camera viewpoint 场景，尚未给出跨 morphology、控制频率变化或强接触操作上的量化结果；后续要看 world modeling 上下文长度和交互预算对效果的影响。

【交叉方向】
7. RoboAtlas: Contextual Active SLAM
链接：https://arxiv.org/abs/2606.26046
作者：Alexander Schperberg, Shivam K. Panda, Abraham P. Vinod, M. K. Jawed, Stefano Di Cairano
时间：2026-06-24 提交/更新
问题：传统 Active SLAM 通常偏几何探索，foundation model 导航又常偏语义问答；前者不知道“去哪里找更有意义”，后者又缺少可靠的 3D 语义地图支撑，导致探索与任务推理割裂。
创新：RoboAtlas 想做的是 contextual Active SLAM，把几何探索、全局语义地图推理和第一视角 VLM 推理统一起来，并用 contextual multi-armed bandit 动态决定什么时候该继续探、什么时候该朝语义目标走。
机制：底层依赖可扩展 3D semantic mapping 系统 OpenRoboVox；上层结合 frontier exploration、global semantic-map reasoning 和 egocentric VLM reasoning。随着场景理解提升，bandit 机制会逐步把策略从几何探索切向语义引导导航。
实验：作者既做了仿真，也在 Unitree Go2 上验证，真实环境规模超过 1800 平方米、约 3 万个语义实例。结果上，系统实现 100% task success；在 GOAT-Bench Val Unseen 上，用 GPT-4o 时达到 90.6% SR，较此前最强基线提升 17.8 个点；即使用更小的 Qwen2.5-VL-7B，仍有 88.8% SR，甚至超过所有使用 GPT-4o 的基线。
为什么值得关注：这篇论文非常典型地展示了“VLM 不是替代地图，而是应该被大规模 3D 语义地图约束和增强”。它同时踩中机器人和具身导航当前两条主线：主动探索与 foundation model grounding。
局限/跟进：摘要没有给出实时性、token 成本和长期部署稳定性；此外，多臂老虎机式策略切换在更动态、更多人类干扰的环境中能否保持鲁棒，还有待观察。

【趋势总结】
1. 这一批论文最明显的共性，是不再迷信“直接端到端把模型做大”。自动驾驶的 G2DP、Causality-based Parametric-CBF，机器人侧的 action prior、ForceBand、ICWM，都在强调结构化先验、测试时引导或更好的训练信号。
2. 自动驾驶方向的研究重点正在从静态感知堆分数，转向闭环可控性与高速度部署约束。G2DP 代表 dense guidance 进入扩散规划主环，FAR-LIO 代表里程计开始围绕时延和硬件效率深做，CBF 工作则把因果推理拉回交互安全控制。
3. 机器人/具身方向的一个新意，是“世界模型、动作先验、力信号”被重新当作一等公民。相比过去只靠视觉语言语义硬扛，现在更多工作在补足动作结构、系统识别和接触信息这些真正影响落地的要素。
4. 交叉方向上，RoboAtlas 说明地图、语义和 foundation model 的结合正在从离线理解走向可执行系统；它和前几天出现的 contextual mapping、active exploration 类工作一起，显示研究正往“能长期运行的具身系统”收敛。
