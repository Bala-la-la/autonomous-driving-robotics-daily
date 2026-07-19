arXiv 自动驾驶与机器人晨报｜2026-07-03

说明：截至 2026-07-03 早晨检索，最新高相关论文主要集中在 2026-07-01 提交批次；自动驾驶强相关稿件数量有限，因此补入 2026-06-30 提交的 ASPIRE，并在条目中明确日期。

【自动驾驶】
1. What's Hidden Matters: Identifying Planning-Critical Occluded Agents using Vision-Language Models
链接：https://arxiv.org/abs/2607.00283
作者：Amirhosein Chahe, Tyler Naes, Jovin D'sa, Faizan M. Tariq, Sangjae Bae, Lifeng Zhou, David Isele。机构线索：摘要页未直接列出。日期：2026-07-01 提交。
问题/痛点：自动驾驶在遮挡场景里通常要么“对所有遮挡一视同仁地保守”，导致不必要的刹停和低效；要么只能恢复几何可见空间，却不知道哪些隐藏体真正会影响规划。
核心创新：把“感知谁重要”直接改写成“谁会改变规划结果”。论文引入 Planning KL-divergence (PKL) 给被遮挡体做规划影响排序，再让专家级 VLM 生成结构化解释数据，形成面向规划关键体的识别基准。
方法机制：先基于 PKL 对隐藏体做重要性排名，再用 GPT-5 生成带视觉证据和推理链条的标注，最后微调通用/领域 VLM 去判断哪些不可见体会影响 ego 车未来轨迹。
实验与结果：数据集建立在 nuScenes 高影响场景上；作者报告 PKL 引导的数据选择比随机/弱引导选择带来约 30% 性能提升，小模型微调后还能明显超过大模型零样本判断。
为什么值得关注：这不是再做一个“更会看图”的 VLM，而是把 VLM 直接接到规划价值函数上，代表自动驾驶里“planning-aware perception”路线在遮挡理解上的一次更实用推进。
可能局限/跟进点：目前更像离线判断器，还没完全证明闭环接入规划器后的稳定收益；依赖 VLM 生成标注也可能引入教师偏差。

2. DriveVer: Lightweight Trajectory Evaluator as Test-Time Verifier for Autonomous Driving
链接：https://arxiv.org/abs/2607.00399
作者：Chong He, Yuechen Luo, Fang Li, Shaoqing Xu, Fuxi Wen。机构线索：摘要页未直接列出。日期：2026-07-01 提交。
问题/痛点：端到端驾驶规划器常是一次性输出轨迹，缺少“生成后再验一次、错了就修”的推理环节；继续靠训练时扩模型、扩数据，成本高且收益递减。
核心创新：提出一个可插拔的 test-time verifier，把“测试时扩展”思想引入驾驶规划：不重训大底模，而是在推理阶段对候选轨迹做轻量打分和修正。
方法机制：基于 NAVSIM 构建条件驱动聚类与均衡采样的数据集；模型采用 dual-head 结构，把候选轨迹、多视角视觉特征和自车运动学特征融合，同时输出安全置信度和几何修正向量。
实验与结果：在 NAVSIM 上，DriveVer 能显著提升基础规划模型效果；模型仅 34M 参数，作者强调其额外开销很小，仍能保持实时推理。
为什么值得关注：它体现出自动驾驶规划一个很现实的方向：不必每次都训练更大的 planner，而是在推理端引入 verifier/refiner，形成“生成-审查-修正”闭环。
可能局限/跟进点：摘要尚未给出更细的闭环安全指标和长尾场景拆解；验证器若只学到训练分布内的错误模式，外推到新城市/新传感器栈仍需检验。

3. ECoSim: Data Efficient Fine-Tuning for Controllable Traffic Simulation
链接：https://arxiv.org/abs/2607.00545
作者：Yu-Hsiang Chen, Wei-Jer Chang, Yi-Ting Chen, Masayoshi Tomizuka。机构线索：从作者背景可推测包含加州大学伯克利相关团队，但摘要页未直接列机构。日期：2026-07-01 提交。
问题/痛点：闭环自动驾驶评测越来越依赖可控交通仿真，但现有做法常需要对大型生成模型重新训练，且要大量带控制标签的数据，成本高。
核心创新：论文不是重训 traffic generator，而是在预训练扩散/自回归交通模型上用轻量控制适配层接入多模态控制，包括 sketch、latent behavior code 和 text。
方法机制：核心是 identity-initialized FiLM 层，对中间特征做调制，让新控制模态“贴”到已有生成先验上；再结合 context-aware condition transfer，做反事实场景与长尾场景合成。
实验与结果：在 Waymo Open Sim Agents Challenge 上，用不到 1% 的成对控制数据就能获得较强 controllability，同时保持闭环驾驶真实性和安全性。
为什么值得关注：对自动驾驶团队更现实的价值在于“低数据成本地把仿真器变成可编排的场景生成器”，这比单纯追求更大 world model 更容易落到评测和数据闭环。
可能局限/跟进点：摘要没给出不同控制模态之间的稳定性对比；复杂交互和极端长尾危险场景下，FiLM 式轻量适配是否足够仍待看全文。

4. Beyond Line of Sight: Hybrid Validation of V2X Collective Perception in Complex Scenarios
链接：https://arxiv.org/abs/2607.00874
作者：Markos Antonopoulos, Anastasia Bolovinou, Bill Roungas, Elena Daskalaki, Angelos Amditis。机构线索：摘要页未直接列出。日期：2026-07-01 提交。
问题/痛点：单车感知天然受视距和遮挡限制，V2X collective perception 很有前景，但往往缺乏既考虑不确定性又能贴近实车验证的评估体系。
核心创新：提出一个概率式集体感知框架，把多智能体异构观测融成带不确定性的 occupancy grid；同时搭建 CARLA + vehicle-in-the-loop 的混合验证流程。
方法机制：使用 Bayesian fusion 把多车/多源感知压到共享概率栅格，每个栅格同时表达占据概率与不确定性，因此输出不仅更远，而且更可解释。
实验与结果：在环岛场景中，作者报告感知视野覆盖提升 260%；occupied-cell recall 从 ego-only 的 0.82 提升到六车协同感知时的 0.94。
为什么值得关注：这篇工作把“协同感知有效”从概念演示推进到更工程化的验证范式，对 V2X 量产前的系统论证、法规和安全 case 都有价值。
可能局限/跟进点：结果目前集中在特定复杂路口；真实通信延迟、定位漂移和参与车辆渗透率变化下的鲁棒性仍是关键。

【机器人 / 具身智能】
5. FurnitureVLA: Learning Long-Horizon Bimanual Furniture Assembly with Vision-Language-Action Model
链接：https://arxiv.org/abs/2607.01212
作者：Chenyang Ma, Yue Yang, Radu Corcodel, Siddarth Jain, Andrew Wu, Chiori Hori, Diego Romeres。机构线索：摘要页未直接列出。日期：2026-07-01 提交。
问题/痛点：家具装配这类真实双臂长程任务，远比抓放基准复杂，但过往研究多停留在玩具尺度或单臂场景，VLA 在这类超长时序任务上容易误差累积。
核心创新：这是首个系统研究“真实尺度双臂家具装配 + VLA”的工作。作者同时补了三块短板：仿真专家数据、单人双臂 VR 示教，以及 progress-enhanced VLA。
方法机制：任务最长可达 7 个子任务、1550 个控制步；模型在语义子任务上微调，并联合预测动作与连续 progress signal，让系统自动切子任务，减少推理时的级联漂移。
实验与结果：在三类家具上，平均仿真成功率从 48% 提升到 80%；设计因子研究还能再带来 21% 提升；迁移到真实 Kinova Gen3 平台后，最难任务仅出现 16% 的性能下降。
为什么值得关注：具身圈常说“VLA 缺少真正长程、强接触、双臂协作任务”，这篇正面补这个空白，而且给出了比较完整的数据与系统栈。
可能局限/跟进点：任务域仍围绕家具装配；连续 progress 预测在更开放、分支更强的任务里是否仍稳定，需要更多验证。

6. Human-Centric Transferable Tactile Pre-Training for Dexterous Robotic Manipulation
链接：https://arxiv.org/abs/2607.01067
作者：Chi Zhang, Penglin Cai, Ziheng Xi, Haoqi Yuan, Hao Luo, Wanpeng Zhang, Sipeng Zheng, Chaoyi Xu, Zongqing Lu。机构线索：摘要页未直接列出。日期：2026-07-01 提交。
问题/痛点：视觉能看见“要去哪里”，却很难可靠恢复“接触到了多少、力够不够”。而现有触觉数据集规模小、覆盖窄，导致带触觉的操作模型上限一直被卡住。
核心创新：作者构建 H-Tac，大规模 human tactile-action 数据集，并提出 Transferable Tactile Pre-Training (TTP)，把人类触觉经验迁到机器人灵巧操作。
方法机制：H-Tac 包含 160 小时第一视角人类视频、300+ 任务、13.5 万 episodes；论文通过统一的 tactile/action space 连接 human 与 robot，再做基于触觉的预训练和下游适配。
实验与结果：摘要未展开完整数字，但作者称在仿真与真实机器人上都取得更强泛化与更细粒度的操作能力，尤其适合接触密集任务。
为什么值得关注：过去大多数 VLA/操控基础模型是“视觉中心主义”，这篇把触觉从附加传感器提升为预训练主角，方向上很重要。
可能局限/跟进点：人机触觉域差距是否会限制迁移上界，仍取决于触觉硬件标准化程度；多种触觉阵列之间的兼容性也值得继续看。

7. ASPIRE: Agentic /Skills Discovery for Robotics
链接：https://arxiv.org/abs/2607.00272
作者：Runyu Lu, Yubo Wu, Ethan Kou, Letian Fu, Wenli Xiao, Ajay Mandlekar, Yinzhen Xu, Guanya Shi, Ken Goldberg, Ang Chen, Mosharaf Chowdhury, Yuke Zhu, Linxi "Jim" Fan, Guanzhi Wang。机构线索：从作者与项目页可识别出 NVIDIA Research、UC Berkeley 等团队参与。日期：2026-06-30 提交。
问题/痛点：让机器人完成复杂任务，真正难的不是单次推理，而是把感知、接触、失败恢复和技能复用连成持续迭代系统；传统 code-as-policy 经常一次写完就停，经验也难沉淀。
核心创新：ASPIRE 把机器人编程做成一个持续自举过程：执行、诊断、修复、验证、沉淀技能库，再把积累下来的技能迁到新任务和新本体。
方法机制：系统包含三个环节：闭环执行引擎暴露多模态 trace；持续扩张的技能库把验证过的修复抽成可复用知识；进化式 skill search 在新任务里重组旧技能并继续探索。
实验与结果：在受扰动 LIBERO-Pro manipulation 上最高超过先前方法 77%，在 Robosuite 双臂 handover 上提升 72%，在 BEHAVIOR-1K 长程家务任务上提升 32%；对未见过的 LIBERO-Pro Long，成功率 31%，而已有方法仅 4%。
为什么值得关注：这是近期“robot agents 不只会调用 API，而要自己长技能库”的代表作，明显比一次性 planner 或一次性 VLA 更接近长期自治系统。
可能局限/跟进点：系统复杂度高，工程落地成本不低；安全边界、探索预算和真实硬件试错代价会决定这类 agentic robot 系统能否规模化。

【交叉方向】
8. Path Planning in Physically Viable World Models
链接：https://arxiv.org/abs/2607.00673
作者：Su Ann Low, Cheng-Hsi Hsiao, Xingjian Li, Adam J. Thorpe, Ufuk Topcu, Krishna Kumar。机构线索：摘要页未直接列出。日期：2026-07-01 提交。
问题/痛点：很多机器人/无人系统在部署前依赖旧地图做长程规划，但真实环境会因为积水、塌陷、松软地形等物理变化而失效，导致“纸面可通、实地不可过”。
核心创新：把 3D Gaussian splat 场景重建和物理仿真拼成 physically viable world model，让系统提前回答“如果环境变化，会不会走不过去”这类 what-if 问题。
方法机制：先基于已有重建场景生成带物理变化的多版本环境，再用 terrain-aware planner 在这些变化条件下评估路线是否仍可行，从而在出发前暴露潜在长程失败模式。
实验与结果：在美国得州 Central Texas 的真实户外场地上，以多级别模拟洪水做测试。结果显示，这类世界模型能显式暴露原始重建地图上看不出的长程失效和重规划行为。
为什么值得关注：它把 world model 从“学像什么”推进到“学将来还能不能走”，对自动驾驶越野、野外机器人、灾害场景导航都很关键。
可能局限/跟进点：目前主要验证地形退化与积水类变化；若扩展到动态交通参与者或高频交互，建模与计算成本会迅速上升。

【趋势总结】
1. 自动驾驶方向更强调“规划感知一体化”。遮挡体识别、轨迹 verifier、可控仿真都不再停留在感知或生成本身，而是直接围绕闭环规划是否更安全、更高效来设计。
2. 机器人方向继续从“更大 VLA”转向“更完整系统栈”。双臂长程装配、触觉预训练、agentic skill discovery 都在补 VLA 过去薄弱的执行、接触和失败恢复。
3. 世界模型的重心在变化。和早期更关注视频预测或视觉真实性不同，这一批更强调物理可行性、未来地形变化、以及对下游路线决策的直接价值。
4. 与以往路线相比，新意在于越来越多工作把“可解释中间量”显式加入系统：PKL 排序、occupancy uncertainty、progress signal、skill library、terrain feasibility。这说明社区正从单点模型指标，转向能被规划器和工程系统真正消费的结构化能力。
