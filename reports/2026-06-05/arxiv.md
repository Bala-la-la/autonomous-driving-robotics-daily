arXiv 自动驾驶与机器人晨报｜2026-06-05

时间范围说明：优先覆盖 2026-06-01 至 2026-06-04 的最新 arXiv；由于 2026-06-04 当天纯自动驾驶高相关新稿不算多，补充了 6 月 1-2 日的强相关论文，并在条目中标明日期。

一、自动驾驶
1. Bridging Predictive Uncertainty and Safe Action: Sample-Conditioned Differentiable Planning for Autonomous Driving
链接：https://arxiv.org/abs/2606.03296
作者：Chengzhen Meng, Pei Liu, Zhiyu Huang, Chen Lv, Jun Ma（alphaXiv 检索显示含香港科技大学合作作者）
提交时间：2026-06-02
问题/痛点：驾驶场景的不确定性建模越来越强，但预测模块输出的多模态分布，往往很难被下游规划器以“可解释、可优化、可控风险”的方式真正消化；很多方法不是把未来压成单一路径，就是直接端到端黑箱回归。
核心创新：把“扩散式多未来预测”直接接到“可微规划”里，不再只做 prediction for prediction，而是让规划器在样本级别感知风险；同时用经验 CVaR 尾部风险约束专门处理小概率但高代价的危险交互。
方法机制：先用 conditional diffusion 生成多组 plausible futures；再把这些未来样本喂给 differentiable planner，在优化目标中显式加入 tail-risk constraint；场景上下文用 directed graph 表达，兼顾交互结构和计算效率。
实验与结果：在 Waymo Open Motion 和 Argoverse 2 上做 open-loop + closed-loop 验证；摘要给出的结论是，安全性、效率和乘坐舒适性都显著优于 SOTA 基线。
为什么值得关注：这条路线代表“生成式预测”和“优化式规划”开始真正耦合，不再是两个串接但彼此弱监督的模块；对自动驾驶里越来越重要的 risk-sensitive planning 很有参考价值。
局限/跟进：摘要未给出具体数值提升；真实部署中扩散采样成本、CVaR 超参数稳定性、以及在更密集长尾交互中的实时性，都是后续要看点。

2. Unified Driving Tokens: Representation- and Geometry-Guided Discrete Tokenizer for Driving World Models and Planning
链接：https://arxiv.org/abs/2606.01935
作者：Ziyang Yao, Zeyu Zhu, YunCheng Jiang, Zibin Guo, Huijing Zhao
提交时间：2026-06-01
问题/痛点：很多 driving world model 直接沿用图像生成 tokenizer，但“重建像素容易”不等于“对驾驶决策有用”；token 容易只保留纹理，不保留几何和状态信息。
核心创新：提出 representation-guided + geometry-enhanced 的离散 token 学习框架，让 token 同时服务 world model 生成和 planning readout，而不是只服务视觉重建。
方法机制：离散瓶颈一边对齐 frozen DINO feature space，一边做 RGB/perceptual/adversarial reconstruction；再加上相邻帧深度、相对位姿监督，把几何状态压进 token；用 multi-codebook quantization 稳定多目标训练。
实验与结果：在 NAVSIM 上同时测试 reconstruction、representation consistency、轻量 planning readout 和 GPT-style next-token world model；摘要结论是，在保持固定解码器条件下有竞争力的 planning 性能，且生成质量更好。
为什么值得关注：这不是再造一个更大的 world model，而是在“接口层”动刀。未来很多自动驾驶 VLA/world model 的上限，可能首先受制于 token 是否真的承载驾驶可用信息。
局限/跟进：目前主要在 NAVSIM 验证；跨数据集泛化、长时 rollout 稳定性、以及对闭环控制的直接收益，还需要更强证据。

二、机器人 / 具身智能
3. AirDreamer: Generalist Drone Navigation with World Models
链接：https://arxiv.org/abs/2606.03252
作者：Zian Liu, Andong Yang, Chunkai Yang, Ruidong An, Chao Gao, Guyue Zhou
提交时间：2026-06-02
问题/痛点：无人机在未知拥挤环境中导航，很容易依赖手工感知链路、人工规则和固定环境先验，跨环境泛化差，遇到局部最优和姿态控制问题尤其脆弱。
核心创新：把世界模型式环境理解和 RL 策略叠起来，用更“动物式”的预判机制替代大量手工管线；同时设计 sparse reward，避免靠 reward shaping 堆技巧。
方法机制：高层由 world-model-like 环境理解建模空间结构和可达性，低层用 RL policy 决策；奖励函数刻意稀疏，但显式鼓励 yaw control 行为，从而减少陷入局部陷阱。
实验与结果：仿真和真实无人机都做了；在 challenging maps 上成功率比最强基线高 5.3%，且无需部署期调参即可实现 sim-to-real transfer。
为什么值得关注：近几个月空中机器人最明显的趋势之一，就是从“纯 VLA 指令跟飞”转向“预测驱动的闭环决策”；这篇是相对工程可落地的一支。
局限/跟进：摘要里没有展开 world model 的具体结构，也没给出不同障碍密度/观测噪声下的分解结果；后续要看它到底是 world model 贡献更大，还是 RL 奖励设计贡献更大。

4. EaDex: A Cross-Embodiment Dexterous Manipulation Framework from Low-Cost Demonstrations
链接：https://arxiv.org/abs/2606.03268
作者：Qian Zhao, Xin Tong, Chengdong Wu, Yang Yang, Yingtian Li
提交时间：2026-06-02
问题/痛点：灵巧手学习长期受限于两件事：高质量 demonstration 成本太高，纯 RL 探索又太慢；不同手型/不同本体之间还存在迁移困难。
核心创新：一方面把 demonstration 成本压到“单 RGB-D 相机采集人手动作”的级别，另一方面提出 contact-reward-based dynamic demonstration annealing，让策略从“依赖示范”平滑过渡到“自主优化”。
方法机制：数据侧用 MANO 手模型、数据归一化和 motion retargeting，把低成本人手观测变成结构化示范；学习侧根据接触奖励动态衰减 demonstration 依赖，逐步释放探索。
实验与结果：在 3 种 dexterous hands、3 类 articulated object opening 任务、共 9 个 cross-embodiment 设定上验证；相对“不做 demonstration annealing”的基线，取得 55.3% 的相对提升。
为什么值得关注：这篇不靠更大 VLA，而是正面解决“便宜数据怎么变成有效 manipulation supervision”；对实验室和创业团队都很实际。
局限/跟进：目前任务集中在开门/开盖类 articulated object；更复杂接触动力学、双手协作和长时任务是否同样受益，还不清楚。

5. Generalization of World Models under Environmental Variability for Vision-based Quadrotor Navigation
链接：https://arxiv.org/abs/2606.05015
作者：Luca Zanatta, Grzegorz Malczyk, Kostas Alexis
提交时间：2026-06-03
问题/痛点：大家都在讲 world model 能提升样本效率，但“环境变化一大时它还能不能真泛化”，证据其实不足；仿真里表现好，不代表真实飞行就稳。
核心创新：不是再提一个新模型，而是做系统性变量研究：改变环境随机性，分别考察 SSL 预训练和 RL 微调阶段的泛化，并把 cross-environment validation 和真实无人机部署挂钩。
方法机制：以 DreamerV3 系世界模型为底座，在不同随机性等级环境中训练/交叉验证；再把学到的模型和导航策略上真实四旋翼，甚至做“仅给 2.5 秒真实感知，随后完全凭 imagination 飞行 12 米”的开放回路测试。
实验与结果：能在真实环境中穿过最窄 0.67m 的缝；结论很强：SSL 阶段对环境变化泛化好的模型，真实部署就更可靠；反过来，仿真策略评测最强的模型反而可能在真实平台失败。作者还指出离散 latent size 和训练序列长度是主导因素。
为什么值得关注：它把最近很热的“世界模型有效吗”问题，从单次 SOTA 对比拉回到“哪些训练信号真决定 sim2real 成败”，这对后续研究路线很关键。
局限/跟进：这更像高质量诊断论文，不是新架构论文；能否把这些发现转成通用训练 recipe，仍待后续工作。

三、交叉方向（导航 / 世界模型 / 数据合成）
6. ImagineUAV: Aerial Vision-Language Navigation via World-Action Modeling and Kinodynamic Planning
链接：https://arxiv.org/abs/2606.01205
作者：Xuchen Liu, Jiawei Huang, Shihao Xia, Bingxi Liu, Jinqiang Cui, Jiankun Yang
提交时间：2026-05-31（纳入近 5 天补充）
问题/痛点：VLA 模型做 UAV VLN 时，语义理解通常够强，但几何一致性和飞行动力学匹配差，导致“会看不会飞”。
核心创新：提出 cascaded world-action modeling，不直接回归动作，而是先“想象”指令条件下未来会看到什么，再从 imagined future 中提取 6-DoF 动作，最后交给 kinodynamic planner 做物理可执行化。
方法机制：latent video diffusion model 负责 instruction-conditioned future observation generation；action extractor 从 imagined observations 反推动作；kinodynamic planner 再做 collision-free refinement；step-distilled inference pipeline 保证实时性。
实验与结果：仅 1.3B 参数，优于已有 VLN/VLA 基线，并完成真实无人机验证。
为什么值得关注：这条路线很像把“视频世界模型 + 控制规划器”做成空中具身版本，比单纯把大模型接到 action head 更可信。
局限/跟进：摘要没有给出具体 benchmark 数字，也没展开在复杂风场/高速机动条件下的表现；真实世界的鲁棒性仍要看更完整实验。

7. RoboDream: Compositional World Models for Scalable Robot Data Synthesis
链接：https://arxiv.org/abs/2606.02577
作者：Junjie Ye, Rong Xue, Basile Van Hoorick, Runhao Li, Harshitha Rajaprakash, Pavel Tokmakov, Muhammad Zubair Irshad, Vitor Guizilini, Yue Wang
提交时间：2026-06-01
问题/痛点：机器人学习仍被 demonstration 成本卡住；纯视频生成虽然能“扩数据”，但往往只会做表层视觉增强，或者直接出现 embodiment hallucination，生成物理上不可执行的动作。
核心创新：提出 embodiment-centric compositional world model，把“机器人运动”与“场景/物体合成”解耦，既保留动作真实性，又能大规模合成新场景、新物体、新视角数据。
方法机制：用 rendered robot motion 作为动作锚点，同时条件化显式场景先验和物体先验；由此解锁两种能力：retrieval and rebirth（把旧轨迹重生到新环境）与 prop-free teleoperation（操作员对着空气操作，模型事后补出目标物体和场景）。
实验与结果：真实机器人实验显示，生成数据能稳定提升下游策略表现，并显著减少真实世界数据需求。
为什么值得关注：这代表数据合成研究从“做更像的视频”转向“做对策略真正有用、且动作不漂的训练数据”，对 manipulation scaling 非常重要。
局限/跟进：摘要未披露任务范围和具体提升幅度；如果场景先验本身偏差较大，合成数据是否会放大偏见，是后续值得盯的点。

四、趋势总结
1. 这批论文的共同主线不是“把模型再堆大”，而是让 world model / future prediction 真正进入决策回路：自动驾驶里是 uncertainty-conditioned planning，空中机器人里是 imagined future + kinodynamic planning，导航与 manipulation 里则是 action-conditioned world modeling。
2. 自动驾驶方向的一个明显新意，是研究者开始把 token 接口、风险度量和规划可微性当作一等公民处理，而不再只追求更强的端到端感知-控制回归。
3. 机器人方向最值得注意的是“低成本数据”和“高保真合成数据”双线并进：EaDex 试图让便宜的人类示范可用，RoboDream 试图让合成 demonstration 真能替代部分真实采集。
4. 空中机器人特别活跃。AirDreamer、ImagineUAV、Quadrotor world model generalization 这几篇一起说明，UAV 正在成为检验世界模型、VLA、闭环规划是否真的成立的高压场景。
5. 相比以往“世界模型=更好视频预测”的路线，新一批工作更强调：几何一致性、动作可执行性、跨环境泛化、以及对真实部署指标的解释力。这是一个相对实用、也更接近落地的转向。
