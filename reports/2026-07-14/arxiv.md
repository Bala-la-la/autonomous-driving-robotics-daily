arXiv 自动驾驶与机器人晨报｜2026-07-14

说明：截至 2026-07-14 检索，自动驾驶/机器人方向高相关最新 arXiv 提交主要集中在 2026-07-08 至 2026-07-10；7 月 11 日至 14 日暂未见更强相关新稿，因此本报补充最近 3-5 天论文。

【自动驾驶】
1. OpenLongTail: Generative Scaling of Long-Tail Driving Data
链接：https://arxiv.org/abs/2607.09655
作者：Lulin Liu, Nuo Chen, Yan Wang, Bangya Liu, Wenyan Cong, Hezhen Hu, Boris Ivanovic, Hao Wang, Ziyao Zeng, Xinyu Gong, Yang Zhou, Zixiang Xiong, Dilin Wang, Zhangyang Wang, Weisong Shi, Ruohan Zhang, Marco Pavone, Zhiwen Fan（机构未在 API 摘要中显式给出）
时间：2026-07-10 提交/更新
问题：闭环驾驶最缺的是稀有危险场景，但互联网和车端采集到的长尾视频往往只有单目 dashcam 或缺少多视角，无法直接拿来训练策略。
创新点：把“异构长尾视频 -> 可训练多视角驾驶资产”做成开源生成引擎；重点不是单纯做视频生成，而是补齐策略学习真正需要的视角覆盖、跨视角一致性和时间对齐。
方法：先做 pose-informed extrapolative view synthesis 补缺失视角，再把 Plucker ray 几何注入生成过程，增强新视角之间的一致性、时序同步和 ego 轨迹恢复。
实验/结果：摘要确认对长尾事件下的闭环驾驶鲁棒性有显著提升，并在外推视角质量、跨视角一致性和位姿恢复指标上验证有效，但未披露具体百分比。
为什么值得关注：这条路线把“野生视频数据”从不可用素材变成可扩展的驾驶训练燃料，直接对准长尾泛化瓶颈。
局限/跟进：效果会受位姿估计、生成视角真实性和 domain gap 影响；后续要看开源后在真实长尾事故库上的收益是否稳定。

2. 4DR360: State Reasoning for Joint 3D Detection and Occupancy Prediction in 4D Radar-Camera Full-Scene Perception
链接：https://arxiv.org/abs/2607.09629
作者：Xiaokai Bai, Lianqing Zheng, Runwei Guan, Songkai Wang, Siyuan Cao, Hui-liang Shen
时间：2026-07-10 提交/更新
问题：4D 毫米波雷达抗天气强、成本相对友好，但点云太稀疏；现有雷达-相机融合多只盯 3D 检测，box 与 occupancy 两任务之间互动不足。
创新点：把 occupancy 从“最终输出头”提升为“持续演化的场景状态”，让检测与占据预测共享同一套状态推理过程。
方法：采用 cross-modal state reasoning；用 State-guided BEV Enhancement 强化单帧 BEV 表征，再用 Doppler-guided Temporal Fusion 把状态证据沿时间传播，兼顾 360 度全景感知与时序稳定性。
实验/结果：作者还扩展了 ManTruckScenes 的卫星图 occupancy 标签，并和 OmniHD-Scenes 组成统一评测协议；摘要称覆盖准确率、鲁棒性、效率和消融，代码与标签计划开源，但未公开关键数值。
为什么值得关注：自动驾驶感知正在从“检测一个物体”转向“维持一个可推理的世界状态”；4D 雷达也从辅助传感器走向主角。
局限/跟进：目前强结果仍依赖新标注协议；跨数据集泛化、极端稀疏回波和实时部署成本还需要公开数字支撑。

3. BeyondSight: Object Permanence for End-to-End Autonomous Driving
链接：https://arxiv.org/abs/2607.09138
作者：Sandro Papais, Letian Wang, Mudit Jain, Behnaz Rezaei, Steven L. Waslander
时间：2026-07-10 提交/更新
问题：端到端驾驶系统在遮挡下容易“看不见就当不存在”，长时间遮挡会让关键交通参与者直接从预测和规划链路里消失。
创新点：把发展心理学里的 object permanence 明确引入自动驾驶，让 actor 的“存在性”与“当前是否可观测”解耦。
方法：通过持久 actor queries 在时间上持续传播假设，再根据新观测更新证据，使感知、预测、规划能够继续对暂时不可见目标进行推理；同时提出 nuScenes-Permanence 数据扩展和 observability-conditioned 评测。
实验/结果：对不可观测目标的检测从 0 提升到 0.249 mAP，规划误差从 0.61 降到 0.54 L2avg，是摘要里少见给出明确增益数字的论文。
为什么值得关注：这不是简单加记忆模块，而是在端到端驾驶里把“持续存在假设”制度化，正对遮挡决策这一痛点。
局限/跟进：当前主要验证的是 nuScenes 体系；是否能迁移到密集交互和更长遮挡时长的闭环平台，需要更多 closed-loop 结果。

4. WCog-VLA: A Dual-Level World-Cognitive Vision-Language-Action Model for End-to-End Autonomous Driving
链接：https://arxiv.org/abs/2607.08375
作者：Xuerun Yan, Zhexi Lian, Nuoheng Zhang, Shiyu Fang, Haoran Wang, Chen Lv, Jia Hu, Binyang Song
时间：2026-07-09 提交/更新
问题：现有 VLA 驾驶模型更偏“看见后反应”，世界理解和前瞻推演仍然碎片化，难以形成主动驾驶。
创新点：提出双层 world-cognitive VLA，把语义级世界认知/推理与生成级世界演化放进同一框架；并引入 Game-theoretic CoT，把博弈式多车交互显式化。
方法：语义层融合 3D 空间感知和 agent tokens 建模动态世界；生成层用 Aligned Decoupled Diffusion Transformer 生成物理可行的联合多车轨迹，并通过表示对齐减少 diffusion 去噪步数；另构建 85k 条 Game-CoT 标注。
实验/结果：摘要称在 NAVSIM 上取得 92.9 的 SOTA PDMS 分数。
为什么值得关注：端到端驾驶近期明显从“模仿驾驶动作”转向“先建模世界，再生成策略”；这篇把 reasoning 与 world model 结合得很彻底。
局限/跟进：Game-CoT 标注质量和扩展性是核心变量；多阶段系统的真实时延、可解释性与失败模式还需更多公开分析。

【机器人 / 具身智能】
5. TACTIC: Tactile and Vision Conditioned Contact-Centric Control for Whole-Arm Manipulation
链接：https://arxiv.org/abs/2607.09218
作者：Rishabh Madan, Angchen Xie, Samantha Saak, Andres Blanco, Dohyeok Lee, Sarah Grace Brown, Yunting Yan, Mark Zolotas, Jose Barreiros, Tapomayukh Bhattacharjee
时间：2026-07-10 提交/更新
问题：whole-arm manipulation 需要多链路接触、滑移和受力调节，纯视觉或纯学习 rollout 很容易在遮挡、分布偏移和多接触稀疏样本下失真。
创新点：把 tactile sensing、RGB-D、接触雅可比和采样式 MPC 组合成 contact-centric 控制框架，不再把接触当副作用，而当成主状态变量来规划。
方法：TACTIC 用 action-conditioned latent dynamics 预测未来接触配置和交互力，再通过 contact Jacobian 引导动作采样，让规划器主动搜索“能调力、能推进任务”的动作序列。
实验/结果：摘要称在仿真中持续优于现有 model-based 与 model-free 方法，并在真实机器人上完成翻转/重定位人体模型、3D 动态迷宫到达等多接触任务。
为什么值得关注：具身操控开始从“抓住物体”走向“用整条手臂与环境协同接触”，TACTIC 代表了这一更接近真实家务/护理/辅助场景的方向。
局限/跟进：需要分布式触觉硬件，系统复杂度较高；泛化到更快动态接触和更少传感器配置仍待验证。

6. GenVid2Robot: From Video Generation to Robot Manipulation via Rigid-Geometric Consistency
链接：https://arxiv.org/abs/2607.09191
作者：Haohui Huang, Xi Yuan, Panpan Liao, Tao Teng, Chenguang Yang, Jing Guo, Yi Guo
时间：2026-07-10 提交/更新
问题：生成视频能提供动作先验，但视觉上“像能做”不代表机器人真的“做得了”；缺少度量几何、抓取约束和执行反馈时，直接回放轨迹很不可靠。
创新点：把生成视频降级为“不确定的视觉运动假设”，只把通过刚体几何一致性验证的那部分运动迁移到机器人上。
方法：从真实首帧 RGB-D 采样语义锚点，跟踪生成视频候选中的 2D 运动，再检查它是否可由首帧稀疏相对 SE(3) 几何解释；通过 mask-constrained grasping 选抓取位姿，并用 bounded depth compensation 修正执行误差。
实验/结果：摘要称真实机器人实验显示，相比直接依赖生成视频先验的方法，该框架在可靠性上明显更强，但未给出统一数值表。
为什么值得关注：这是“视频世界模型 -> 真实操控”之间非常关键的一层物理落地桥梁，避免了把视频生成误当机器人 demonstration。
局限/跟进：目前仍依赖首帧 RGB-D 质量和刚体假设；对可形变物体、多接触任务和在线重规划的支持还不充分。

7. PAC-ACT: Post-training Actor-Critic for Action Chunking Transformers
链接：https://arxiv.org/abs/2607.09590
作者：Yujie Pang, Zudong Li
时间：2026-07-10 提交/更新
问题：工业接触操作更需要低时延、低显存的 action-chunking policy，但纯行为克隆容易在接触扰动和位姿偏差下崩掉。
创新点：把 RL post-training 明确移植到 ACT 这类 chunking policy，而不是一味追求更大 VLA；重点是保留原有低延迟优势的同时补足闭环恢复能力。
方法：在 chunk level 上重写策略优化，构建 ACT-transferred actor-critic，并用 hybrid behavior-prior constraint 在在线微调时约束策略不要偏离预训练动作分布。
实验/结果：工业精密接触基准上，成功率、接触稳定性和力安全性都有提升；Contour 任务里峰值接触力显著下降，超过 60N 的读数比例减少 46 倍。
为什么值得关注：这篇很像机器人版“后训练时代”信号，说明具身控制也开始从纯 BC 转向 RL-based post-training，而且优先落在真实可部署的小模型/低延迟范式上。
局限/跟进：目前主要聚焦工业接触任务；对长时序多阶段任务、跨机器人迁移和样本效率的表现还要继续看。

【交叉方向】
8. What VGGT Knows About Overlap: Probing Geometric Foundation Models for Co-Visibility
链接：https://arxiv.org/abs/2607.09503
作者：Filippo Ziliotto, Luciano Serafini, Lamberto Ballan, Tommaso Campari
时间：2026-07-10 提交/更新
问题：SLAM、SfM 和机器人定位都依赖 co-visibility 判断，但低重叠图像对常常很难做稳。
创新点：作者发现几何基础模型 VGGT 在没有监督 co-visibility 的前提下，内部已经自发学出这一能力；并把不同层当作不同几何专家来用。
方法：冻结 VGGT，只训练一个不足 7.5M 参数的 layer-wise mixture-of-experts 头 Co-VGGT，自适应汇聚各层的几何抽象来判别图像是否共享可见表面。
实验/结果：在 Co-VisiON 上超过人工标注基线，并比既有方法高出 25% 以上 pairwise、10% multiview，且校准误差 ECE=0.030，可直接做可见性图边权。
为什么值得关注：自动驾驶和机器人都在追求“基础模型化几何感知”，这篇提供了一个很强的证据：foundation model 不只会识别语义，也会内化几何可见性结构。
局限/跟进：当前成果集中在 co-visibility 识别；离完整 SLAM/定位系统还差数据关联、回环、地图维护等模块整合。

【趋势总结】
1. 世界状态化：无论是 4DR360 的 occupancy state，还是 BeyondSight 的 actor permanence，最新工作都在把“瞬时观测”升级成“持续维护的世界状态”。
2. 从模仿到后训练：PAC-ACT 和自动驾驶 post-training 综述共同说明，BC-only 路线正在让位给带安全/恢复目标的后训练与闭环优化。
3. 生成模型开始接管数据与规划，但都在补物理约束：OpenLongTail 用生成补数据，WCog-VLA 用生成做世界演化，GenVid2Robot 用几何一致性给生成视频上“物理闸门”。
4. 多模态接触/几何成为关键：机器人侧明显在强化 tactile、force、geometry；自动驾驶侧则强化 radar、occupancy、occlusion memory，而不是只堆更大通用模型。
5. 相比以往只追求单点指标，这一批论文更强调“可闭环部署”的结构性改造：长尾数据引擎、遮挡存在性、低时延 post-training、可校准几何基础模型，都是为真实系统补短板。