arXiv 自动驾驶与机器人晨报｜2026-06-24

说明：本报优先覆盖 2026-06-23 UTC 出现在 arXiv cs.RO 新列表的高相关论文；每条同时给出 arXiv 原始提交/最近更新时间。机构信息以摘要页可得为准，本批多数未公开机构署名。

【自动驾驶】
1. MAGNIFIED: RL Fine-tuning of Multimodal Large Language Models for Motion Planning
链接：https://arxiv.org/abs/2606.20641
作者：Letian Chen, Yiren Lu, Justin Fu, Yichen Xie, Runsheng Xu, Jyh-Jing Hwang, Ben Sapp, Drago Anguelov
时间：2026-06-23 出现在 cs.RO 新列表；arXiv 原始提交/更新 2026-06-02
要解决的问题：把多模态大模型直接用于驾驶规划时，传统 next-token 训练目标只是在模仿文本坐标，不真正优化安全、舒适、礼让等规划目标，容易出现“字面预测对、驾驶意图错”。
核心创新点：作者把“文本 token 轨迹”重新解释为“可执行规划轨迹”，再做 token-level RL fine-tuning，让奖励直接对应 overlap、off-road 等规划指标，而不是只看 token 预测准确率。
方法机制/结构：先用 SFT 建立一个从栅格化 BEV 到 X-Y 文本轨迹的基础 MLLM 规划器；再把输出 token 序列映射回车辆轨迹，用规划奖励做 RLFT；重点是把语言建模目标改造成真正面向闭环规划后果的优化。
实验与结果：Waymo Open Motion Dataset 上，RLFT 相对 SFT 基线带来超过 10.5% 的 overlap rate 降低、38.9% 的 off-road rate 降低。
为什么值得关注：这篇工作代表一个很实用的转向，即不急着替换大模型规划器，而是先纠正其训练目标，把“会说轨迹”推进到“会为驾驶目标负责”。
可能局限/后续点：结果仍主要来自开放环规划评测；真实闭环和稀有长尾交互能否同样受益，还要看后续更强仿真和道路验证。

2. Scaling Self-Play for End-to-End Driving
链接：https://arxiv.org/abs/2606.19641
作者：Luke Rowe, Roger Girgis, Rodrigue de Schaetzen, Daphne Cornelisse, Alaap Grandhi, Felix Heide, Eugene Vinitsky, Christopher Pal, Liam Paull
时间：2026-06-23 出现在 cs.RO 新列表；arXiv 原始提交 2026-06-17，最近更新 2026-06-19
要解决的问题：端到端自动驾驶长期依赖离线人类演示，状态覆盖不够、没有闭环纠偏、对长尾交互脆弱；而自博弈路线过去又多依赖 BEV/特权输入，难和像素端到端模型接上。
核心创新点：作者把“像素级端到端驾驶”与“大规模自博弈”真正拼到一起，提出 Gigapixel 批量驾驶模拟器和 self-play DAgger，用特权 RL teacher 在线蒸馏像素策略。
方法机制/结构：Gigapixel 不追求昂贵照片级传感器仿真，而是保留关键场景结构的透视渲染边框世界，以 50k agent steps/s 的吞吐做大规模采样；训练中用 on-policy distillation 提升样本效率；最后再做轻量 perception adaptation 完成 sim-to-real 迁移。
实验与结果：在人类轨迹监督缺失的前提下，迁移后的策略在 HUGSIM 与 NAVSIM-v2 上取得有竞争力表现；并且自博弈训练规模扩大时，策略性能继续按比例提升。
为什么值得关注：这篇文章的价值不只是一个 simulator，而是把“闭环覆盖”重新拉回端到端驾驶主线，说明像素策略并不一定只能吃静态离线数据。
可能局限/后续点：简化感知渲染能否充分覆盖真实视觉噪声仍有疑问；如果路线要走向量产，天气、稀疏传感器缺陷和长尾社会博弈还需补齐。

3. OmniV2X: A Generative Foundation Planner for Efficient End-to-End Cooperative Driving
链接：https://arxiv.org/abs/2606.21165
作者：Juntong Peng, Juanwu Lu, Yupeng Zhou, Can Cui, Yaobin Chen, Ziran Wang
时间：2026-06-23 出现在 cs.RO 新列表；arXiv 原始提交/更新 2026-06-19
要解决的问题：协同驾驶往往依赖稠密 3D 感知和重通信表示，不仅训练数据稀缺，而且通信开销大、消息格式不标准，导致 V2X 在真实部署里性价比不高。
核心创新点：作者把 cooperative driving 建成一个“生成式基础规划器”，不是先把多模态输入硬融合成共享张量，而是直接解释独立上下文序列，并用轻量标准兼容 V2X token 注入协同信息。
方法机制/结构：主干是高容量生成式序列规划器，通过 cross-attention 吸收多模态、多智能体上下文；训练时以轨迹生成损失做端到端监督；预训练阶段先吃大规模单车规划数据，再用少量协同场景做高效适配。
实验与结果：DAIR-V2X-Seq 上达到 SOTA；只用不到 10% 的 V2X 微调数据、不到 1% 的通信带宽，就超过已有端到端协同驾驶基线。
为什么值得关注：这条路线的现实意义很强，说明 V2X 未必要靠“更重的三维融合”取胜，标准兼容、低带宽、强迁移反而更像可落地方向。
可能局限/后续点：目前亮点主要在数据效率与通信效率；面对更复杂车路协同、多失步通信、地图误差时，生成式 planner 的鲁棒性还要继续看。

【机器人 / 具身智能】
4. TACT-ful: Multi-Channel Terrain Affordance and Compliance Training for Payload-Robust Perceptive Humanoid Locomotion
链接：https://arxiv.org/abs/2606.20645
作者：Thanh Ly, Truong-Duy Dang, Chien Le, Tan-Dzung Do, Phuong Tuan Dat, Cuc T. Trinh, Vien Anh Ngo, An T. Le
时间：2026-06-23 出现在 cs.RO 新列表；arXiv 原始提交/更新 2026-06-06
要解决的问题：人形机器人在台阶、棱边、结构化地形上行走时，单一高度图不足以决定可落脚区域；一旦再叠加载荷搬运，刚性步态很容易被外力矩击穿。
核心创新点：作者把“地形可供性建模”和“带载顺应训练”一起做，而不是单独优化落脚点或单独做扰动恢复；重点是多通道 terrain cost 与下肢 compliance targets 的联合训练。
方法机制/结构：平整度、坡度、速度相关高度可达性共同构成 terrain cost，并同时服务 GPU 并行 DCM 落脚规划器和 PPO 稠密奖励；摆腿轨迹采用带自适应 apex bias 的 Bézier 曲线，兼顾脚底姿态；负载训练中在随机载荷附着点注入虚拟 wrench，以无力传感方式学会顺应。
实验与结果：仿真中可在最高 0.20m riser 的楼梯上达到 1.0 m/s；对约 15kg 居中载荷和以手腕力矩为主的载荷，鲁棒性明显提升；并给出结构化地形上的硬件演示。
为什么值得关注：这类工作比“平地跑得更快”更接近真实人形价值，因为它把看地形、踩台阶、搬东西三个原本常分开的能力合在一起训练。
可能局限/后续点：摘要里的真实机验证仍偏定性；长时间耐久、不同足底接触材质、严重感知噪声下的稳定性还需要更系统报告。

5. MemoryVAM: Integrating Memory into Video Action Model for Robot Manipulation
链接：https://arxiv.org/abs/2606.20679
作者：Yuxin Jiang, Chang Yu, Yunuo Chen, Xiang Feng, Yin Yang, Nishank Gite, Chenfanfu Jiang
时间：2026-06-23 出现在 cs.RO 新列表；arXiv 原始提交/更新 2026-06-13
要解决的问题：视频世界模型类操控策略通常只看一个短窗口，因此一旦任务需要记住“之前数过几个物体”“前一次尝试发生了什么”，策略就会失忆，长程操作退化明显。
核心创新点：引入 episodic memory，不额外依赖逐帧进度标签，而是让策略从历史视觉与动作语境中自监督学到“任务已进行到哪一步”的压缩记忆。
方法机制/结构：Recap-Cue 模块先用基于 Perceiver 的 Recap Compressor 把逐帧 CLIP 表征压成 memory tokens，再由 Cue Gate 结合记忆与语言估计任务完成度；这些 token 同时注入视频骨干和动作解码器，并辅以 delta reconstruction 与 episode-boundary 监督。
实验与结果：LIBERO-Mem 平均成功率从 5% 提升到 42.5%；真实机器人上，计数任务成功率 78.3%，空间回忆 80.0%，顺序跟踪 75.0%。
为什么值得关注：很多 VLA/世界模型论文仍默认“更多上下文窗口”就够了，这篇明确把 memory 作为独立模块补回体系，对长程具身任务更有现实意义。
可能局限/后续点：当前记忆机制仍偏任务内 episode 记忆；跨任务迁移、错误记忆累积以及更复杂多实体交互下的压缩损失值得继续追。

6. Vesta: A Generalist Embodied Reasoning Model
链接：https://arxiv.org/abs/2606.20905
作者：Johan Bjorck, Zhiqi Li, Yunze Man 等
时间：2026-06-23 出现在 cs.RO 新列表；arXiv 原始提交/更新 2026-06-18
要解决的问题：定位、空间推理、导航、长程规划往往各自有专门模型，串起来成本高且误差会级联放大；具身系统越来越需要一个单模型统一处理。
核心创新点：作者提出 generalist embodied reasoning model，把空间 grounding 大语料与一个简单但有效的多模态记忆 harness 结合起来，试图用单模型覆盖多类具身任务。
方法机制/结构：核心不是复杂系统编排，而是构造能诱导空间 grounding 的大规模异构训练语料，并让记忆机制支持长程时序推理；因此模型能够在单体架构中处理 localization、navigation、planning 等任务。
实验与结果：在多种 benchmark 上，平均比单任务 SOTA 强 20% 以上，比“每类任务选最优专家再拼装”的集成基线也高 10% 以上；真实机器人需记忆和推理的任务上，成功率提升超过 35%。
为什么值得关注：具身智能正在从“多模型 pipeline”转向“单模型统一体”，这篇给了较强实证，说明 generalist 不只是概念宣传，确实可能在整体系统上优于专家拼接。
可能局限/后续点：统一模型的训练成本和数据构成非常关键；如果某些子能力退化，排障会比模块化系统更困难。

【交叉方向】
7. A scalar per patch from pre-trained ViTs enables fast moving navigation in the real world
链接：https://arxiv.org/abs/2606.21216
作者：Steeven Janny, Leonid Antsfeld, Christian Wolf
时间：2026-06-23 出现在 cs.RO 新列表；arXiv 原始提交/更新 2026-06-19
要解决的问题：真实导航里，大家都知道预训练视觉编码器重要，但究竟哪些视觉表征真正对机器人运动决策有用、是否需要高维特征，一直缺乏大规模真实世界证据。
核心创新点：作者在真实楼宇内做了 966 次导航、总计 24km 的大规模实验，并提出一个很“反直觉”的结论：把预训练 ViT 压到每个 patch 一个 scalar，仍能保留强导航价值，而且会自然浮现可解释 affordance 特征。
方法机制/结构：系统比较多种视觉编码器与多教师蒸馏；对编码器表示做原则性的 spatial bottleneck，观察最低信息量下仍能支持导航的视觉因子；同时比较 RGB-only 与利用特权信息预训练再微调的策略。
实验与结果：摘要未给单一汇总数字，但强调这是大规模真实世界对照实验，并系统展示了多教师蒸馏、表征瓶颈化和特权预训练对导航性能与特征可解释性的作用。
为什么值得关注：这不是又一篇“导航模型更大更强”，而是在问什么视觉信息真正值得给机器人保留，对后续轻量部署、可解释导航和廉价模型设计都很关键。
可能局限/后续点：摘要没有展开各 encoder 间绝对差距；对户外、夜间、极端动态场景能否复现类似结论，仍要后续验证。

8. JPPD: Joint Prediction_Planning Diffusion with Differentiable Safety Guidance for Dynamic Obstacle Avoidance in Intelligent Transportation Systems
链接：https://arxiv.org/abs/2606.20686
作者：Jiahao Wu, Shengwen Yu
时间：2026-06-23 出现在 cs.RO 新列表；arXiv 原始提交/更新 2026-06-14
要解决的问题：共享空间里的低速无人平台常把“他人轨迹预测”和“自身规划”拆成两段，导致信息单向流动，预测不理解机器人自己的动作选择，规划也只能在后处理里硬塞安全约束。
核心创新点：作者把多参与者未来轨迹与机器人规划放进同一个联合扩散采样分布里，再用可微安全势场直接引导联合采样，而不是事后用启发式排斥修修补补。
方法机制/结构：采用带 cross-trajectory attention 的 causal Transformer 统一生成机器人和周边参与者未来；安全部分使用时变 occupancy-probability potential，其梯度直接指导采样；再用 conditional flow matching 减少推理步数并维持多模态轨迹多样性。
实验与结果：评测不再只看 ADE/FDE，而看 near miss、阻塞时间、诱导行人偏移、急刹事件、嵌入式延迟；在场景仿真、自然行人回放、Isaac Sim 和 ROS/Orin 部署上，相比“先预测后规划”基线，尾部安全性与运行效率都更好。
为什么值得关注：它反映了一个更广泛趋势，即自动驾驶/机器人开始把“多智能体未来演化”和“自身决策”联立建模，而不是继续固守流水线。
可能局限/后续点：联合生成模型的稳定性、可解释性与极端拥挤场景下的算力上界，还会是实际部署门槛。

【趋势总结】
1. 从 imitation 到 objective alignment：像 MAGNIFIED 这类工作不再满足于“拟合专家轨迹”，而是直接把规划目标、安全指标或偏好对齐到训练目标里。
2. 从离线数据到闭环生成：Scaling Self-Play、JPPD 都在强调闭环覆盖与多智能体交互建模，说明驾驶研究正在补过去离线模仿路线最弱的一环。
3. 从重感知堆料到高效协同：OmniV2X 代表的不是更重的 V2X 融合，而是更低带宽、更标准兼容、更像真实部署条件下的协同规划。
4. 机器人侧的主旋律是“把缺失的能力补成系统能力”：TACT-ful 补顺应与地形可供性，MemoryVAM 补长期记忆，Vesta 补跨任务统一推理，说明研究重点正从单技能极限分数转向完整能力闭环。
5. 与以往路线相比，这一批论文的新意在于更少“单点模块 SOTA”，更多“把训练目标、记忆、仿真闭环、通信约束、评测指标一起重写”，更接近实际自动驾驶与具身系统的真实瓶颈。
