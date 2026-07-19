arXiv 自动驾驶与机器人晨报｜2026-06-12

说明：2026-06-12 当天可见的“自动驾驶/机器人/具身”强相关新条目不算密集，以下补充覆盖 2026-06-07 至 2026-06-10 的最新高相关 arXiv 论文。

【自动驾驶】
1. LUNA-AD: Lightweight Uncertainty-Aware Language Model with Lifelong Learning for Autonomous Driving
链接：https://arxiv.org/abs/2606.08470
作者：Ruoyu Yao, Pei Liu, Ruiguo Zhong, Mingxing Peng, Rui Yang, Jun Ma
提交时间：2026-06-07
要解决的问题：把 LLM/VLM 引入自动驾驶时，常见痛点是推理成本高、决策不稳定、候选行为缺少不确定性表达，而且一旦路况分布变化，模型很难持续改进。
核心创新点：作者把“高质量推理”和“可部署推理”拆成三层。先用多 agent 分析系统做多假设探索，生成带不确定性的决策示范；再蒸馏到轻量双头启发式模型，同时输出决策分布与文字解释；最后加入 reflection-driven lifelong learning，让系统根据闭环反馈持续修正候选决策与理由。
方法机制：本质上是“重 teacher、多样推理、轻 student、在线反思”的闭环。Teacher 负责拉开策略多样性，student 负责低延迟部署，反思模块负责避免模型越学越单一。
实验与结果：论文在 nuPlan 闭环基准上评测 non-reactive 和 reactive 两种模式，摘要称其 success rate 达到同类 knowledge-driven AD 框架中的 SOTA，同时推理延迟显著低于已有方法。
为什么值得关注：这篇不是单纯把大模型塞进 AD，而是认真处理了 safety-critical 场景里最关键的三个问题：不确定性、可解释性、部署开销。它更接近“能上车”的系统设计。
局限与后续：摘要未披露不同 traffic scenario 的细粒度收益，也还没看到对长尾 corner case 的系统失效分析；后续值得跟踪它在真实车端算力预算与数据回流闭环中的表现。

2. AutoMine Solution for AV2 2026 Scenario Mining Challenge
链接：https://arxiv.org/abs/2606.11874
作者：Songliang Cao, Jiele Zhao, Yuru Wang, Hao Li, Daqi Liu, Zehan Zhang, Fangzhen Li, Yu Wang, Yue Zhang, Bing Wang, Guang Chen, Hao Lu, Hangjun Ye
提交时间：2026-06-10
要解决的问题：自动驾驶评测和数据回流越来越依赖“从海量日志里挖出真正高价值、规划相关、风险高的场景”，但纯规则方法脆弱，纯 LLM 方法又容易 prompt 敏感、对感知噪声不稳。
核心创新点：提出一个 self-refining 的 scenario mining 框架，把 LLM/VLM 与鲁棒轨迹原子函数结合起来。它一边用语义保持的 prompt augmentation 降低 prompt 敏感性，一边把 VLM 负责开放世界视觉线索，把轨迹函数负责几何和运动约束，最后再用执行反馈改写生成代码。
方法机制：可以理解为“代码生成式场景挖掘”。模型不是直接输出标签，而是输出可执行的 mining logic，然后在真实日志上跑，失败后再根据 execution feedback 迭代修正。
实验与结果：该方案在 Argoverse 2 Scenario Mining Competition at CVPR 2026 中拿到 HOTA-Temporal 36.38、Timestamp BA 77.21，说明它不仅能找场景，还兼顾时间边界质量。
为什么值得关注：行业现在越来越重视 evaluation data engine，这篇代表了一个很实用的方向，即把大模型当作“规则生成器 + 代码修复器”，而不是直接端到端替代整个挖掘系统。
局限与后续：这更像强工程导向方案，论文摘要里对泛化到其他日志 schema、其他城市和多传感器设置的讨论还不够；后续值得看它是否能沉淀成通用 scenario DSL 或自动化安全回归流水线。

【机器人 / 具身智能】
3. Embodied-R1.5: Evolving Physical Intelligence via Embodied Foundation Models
链接：https://arxiv.org/abs/2606.11324
作者：Yifu Yuan, Yaoting Huang, Xianze Yao, Yutong Li, Shuoheng Zhang, Linqi Han, Pengyi Li, Jiangeng Sun, Wenting Jia, Zhao Zhang, Yuhao Liu, Ruihao Liao, Yucheng Hu, Qiyu Wu, Yuxiao Li, Zibin Dong, Fei Ni, Yan Zheng, Shuyang Gu, Yi Ma, Hongyao Tang, Han Hu, Jianye Hao
提交时间：2026-06-09
要解决的问题：当前 embodied 模型经常把 cognition、planning、grounding、correction 分散在多个模块或多个模型里，导致长任务闭环弱、能力迁移成本高、对真实机器人适配仍重依赖额外数据。
核心创新点：提出统一的 Embodied Foundation Model 路线，把 embodied cognition、task planning、correction、pointing 集成到单一架构中；同时构建三条自动化数据流水线，形成 15B+ tokens 的大规模 embodied 数据体系，并用 multi-task balanced RL recipe 缓解异构任务冲突。
方法机制：论文里最关键的是 Planner-Grounder-Corrector, PGC 闭环。也就是先规划，再做空间 grounding，再基于执行状态自纠错，让一个模型而不是多个外部代理完成长时程执行闭环。
实验与结果：摘要称 8B 参数模型就在 24 个 embodied VLM benchmark 中拿下 16 个 SOTA，超过 Gemini-Robotics-ER-1.5 和 GPT-5.4；进一步少量数据微调为 VLA 后，在 4 套主流 manipulation benchmark 上超过 pi_0.5；还做了零样本真实机器人实验，覆盖 instruction following、affordance grounding、articulated object manipulation 和 long-horizon tasks。
为什么值得关注：这篇的信号非常明确，研究重心已经从“做一个更强 VLA policy”往“做一个更完整的 embodied foundation model”移动，尤其强调推理、定位、自纠错和下游控制的一体化。
局限与后续：摘要没有给出 24 个 benchmark 上的具体短板，也还不清楚 15B token 数据构建中 synthetic 与 real 的比例以及噪声控制方法；后续值得重点跟踪开源后的数据配方和真实机器人复现门槛。

4. HiMem-WAM: Hierarchical Memory-Gated World Action Models for Robotic Manipulation
链接：https://arxiv.org/abs/2606.10363
作者：Xiaoquan Sun, Ruijian Zhang, Chen Cao, Yihan Sun, Jiahui Chen, Zetian Xu, Bo Chen, Haijier Chen, Zhen Yang, Jiarun Zhu, Yijun Hong, JingZhe Xu, Jingrui Pang, Mingqi Yuan, Jiayu Chen
提交时间：2026-06-09
要解决的问题：World Action Model 在 manipulation 上已经能提供不错的 action-relevant dynamics，但遇到长时程、多阶段任务时，经常记不住关键状态切换点，导致后续动作脱轨。
核心创新点：作者把“记忆什么时候写、写什么、如何配合动作层级”作为中心问题处理。HiMem-WAM 同时引入 motion-centric latent actions、high-level skill latents 和 boundary-triggered memory updates。
方法机制：其结构不是简单堆 memory bank，而是先用分层 latent action 做时间抽象，再用 boundary-aware memory gate 在技能切换边界处写入紧凑任务状态，从而支持 causal inference；并且避免了测试时必须生成未来视频或估计光流的额外代价。
实验与结果：在 LIBERO、LIBERO-PLUS、RMBench 和真实任务上评测。摘要指出 hierarchical latents 能提升部署扰动下的鲁棒性，而 memory module 对 memory-dependent 的长时程操作有显著帮助。
为什么值得关注：这是近期世界模型路线里一个很有代表性的变化，即从“更会生成未来”转向“更会记住任务状态与阶段边界”。对于厨房、装配、收纳这类长任务尤其关键。
局限与后续：摘要没有公开不同任务类别上的增益分布，也未说明 memory gate 是否会在任务边界预测错误时引入级联误差；值得继续跟踪其消融实验和真实机器人长序列日志。

5. World Pilot: Steering Vision-Language-Action Models with World-Action Priors
链接：https://arxiv.org/abs/2606.12403
作者：Zefu Lin, Rongxu Cui, Junjia Xu, Xiaojuan Jin, Wenling Li, Lue Fan, Zhaoxiang Zhang
提交时间：2026-06-10
要解决的问题：VLA 模型在语义 grounding 上很强，但预训练主要来自静态图文，面对接触丰富、连续演化的 manipulation 过程时，常常缺少对“下一步场景怎么变”的动态先验。
核心创新点：提出用 World-Action priors 去“引导”VLA，而不是直接替代 VLA。具体分成两条通道：Latent Steering 把 scene-evolution latent 注入感知层，Action Steering 把预期轨迹作为动作先验送给动作生成器。
方法机制：一条线让模型先看到“场景将如何变化”，另一条线让模型先拿到“动作大致该怎么走”。两者和语言条件一起形成更强的决策链。
实验与结果：摘要报告在 LIBERO-Plus zero-shot OOD benchmark 上 total success rate 达到 84.7%，并在 4 个真实机器人任务的所有设置中都拿到最高成功率，尤其在视角变化、几何变化、形变状态和位姿变化下提升最大。
为什么值得关注：这篇很能代表 2026 年具身主线之一，不再争论“VLA 还是 world model”，而是把 world model 当作 VLA 的 prior provider，用结构化方式耦合二者。
局限与后续：摘要没有展开 world model 训练成本和不同先验注入位置的敏感性，也还需要看在更复杂双臂或移动操作任务上的稳定性。

【交叉方向】
6. DuoBench: A Reproducible Benchmark for Bimanual Manipulation in Simulation and the Real World
链接：https://arxiv.org/abs/2606.11901
作者：Tobias Jülg, Seongjin Bien, Simon Hilber, Yannik Blei, Pierre Krack, Maximilian Li, Sven Parusel, Rudolf Lioutikov, Florian Walter, Wolfram Burgard
提交时间：2026-06-10
要解决的问题：双臂系统显著扩展了 manipulation 能力，但现有 benchmark 往往对双臂协调失败模式刻画不足，sim2real 复现性也弱，导致方法间很难公平比较。
核心创新点：提出可复现的双臂操作基准 DuoBench，面向 FR3 Duo 平台，覆盖 11 个任务、4 类双臂协调模式，并提供 3D 打印资产、仿真到真实世界的对齐 recipe，以及 human-teleoperated 数据。
方法机制：它不仅给 binary success，还设计了 stage-based evaluation，用语义阶段失败分析去定位问题出在“早期接触、双臂并行、时序同步”还是“后段对位/转移”。
实验与结果：作者用 imitation learning 和 VLA 类 policy 在仿真与真实硬件上做基线测试，结论很直接：当前策略在双臂任务上仍明显吃力，尤其卡在 early interaction、parallel arm execution 和 sim-to-real transfer。
为什么值得关注：这不是单纯“又一个 benchmark”。它把双臂任务的失败分析粒度做细了，后面很多 VLA/WAM/skill policy 工作都可能借它作为更严苛的诊断平台。
局限与后续：目前平台中心较强，围绕 FR3 Duo；跨平台兼容性、移动底盘结合、以及更复杂接触任务还需要扩展。

【趋势总结】
1. 自动驾驶方向更强调“可部署的大模型系统”，而不是只比 reasoning demo。LUNA-AD 和 AutoMine 都在处理真实生产链路里的核心问题：不确定性、反馈闭环、数据引擎、执行鲁棒性。
2. 机器人方向明显从“单一 policy 更强”转向“foundation model + world model + memory + correction”的系统耦合。Embodied-R1.5、HiMem-WAM、World Pilot 都在补长时程任务闭环，而不是只做静态语义对齐。
3. world model 的角色正在变化。过去很多工作把它当生成器或规划器本体；这批论文里，它更像结构化先验、阶段记忆器、动态辅助器，服务于更稳的 policy。
4. benchmark 也在升级。DuoBench 说明社区开始系统化衡量双臂、多阶段、真实复现任务，而不是停留在单臂短轨迹成功率。
5. 和以往路线相比，新意在于“工程可用性 + 模型结构化耦合”。不是只做更大模型，而是更重视轻量部署、反馈反思、阶段记忆、world prior 注入和可诊断评测。
