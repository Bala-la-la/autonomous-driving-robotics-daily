arXiv 自动驾驶与机器人晨报｜2026-07-01

说明：按 2026-07-01 北京时间抓取。联网检索后，当前能稳定检索到的最新高相关 arXiv 新稿主要来自 arXiv `cs.RO recent` 的 Tue, 30 Jun 2026 列表；对应 arXiv API 中多数条目的 `updated/published` 时间为 2026-06-29 UTC。今天相关论文数量充足，无需回退到更早 3-5 天窗口。作者信息来自 arXiv 条目；机构若摘要页未明确列出，则注明“未在 arXiv 摘要页明确给出”。

【自动驾驶】
1. Learning from Mistakes: Rollout-Retrieval Lifelong Policy Learning for Autonomous Driving
链接：https://arxiv.org/abs/2606.30537
作者/机构：Cheng Gong, Haoyang Wang, Chao Lu, Zirui Li, Jianwei Gong；机构未在 arXiv 摘要页明确给出
时间：2026-06-29 UTC 更新，对应 arXiv Tue, 30 Jun 2026 最新列表
要解决的问题/痛点：很多学习型自动驾驶策略在离线专家数据上看起来不错，但一旦进入闭环部署，长尾场景里暴露出的错误并不会自动转化成“下一轮应该学什么”；模型只能被动依赖泛化，缺少持续纠错与记忆机制。
核心创新点：作者把闭环驾驶改进明确建模成 lifelong learning 问题，提出 R²LPL（Rollout-Retrieval Lifelong Policy Learning），核心不是盲目把失败片段再喂给模型，而是从“可恢复的错误状态”中检索出可行纠正目标，把稀疏失败信号转成紧凑、稳定的监督知识。
方法机制或模型结构：框架先让预训练策略 rollout，定位 policy-induced mistakes；随后过滤出 still-recoverable 的弱点状态，再做 retrieval，找到可作为学习目标的 corrective targets；最后通过 continual learning 把这些纠正经验写回策略，避免只修新错却忘旧本领。
实验设置和关键结果：在大规模闭环 nuPlan benchmark 上评估。摘要明确指出，只需少量 rollout + continual-learning 循环，就能把一个初始表现中等的学习型 planner 提升到所评测基准上的 SOTA，尤其在更难、更长尾的 Test14-hard split 上增益更明显。
为什么值得关注：这篇论文的价值在于把“部署后持续进化”从口号变成了可以工程化执行的训练闭环。对真实车队而言，真正稀缺的不是更多静态数据，而是把线上暴露的弱点高效沉淀回模型的能力。
可能局限或后续可跟进点：摘要未给出每轮纠错的数据成本、计算成本和灾难性遗忘量化结果，也没有展开 retrieval 质量对最终策略提升的敏感性；后续值得跟踪其是否能扩展到更复杂交互和安全约束更强的车端闭环。

2. OWMDrive: Causality-Aware End-to-End Autonomous Driving via 4D Occupancy World Model
链接：https://arxiv.org/abs/2606.30421
作者/机构：Junjie Cheng, Ruiqi Song, Ye Wu, Nanxing Zeng, Ximiao Li, Yunfeng Ai；机构未在 arXiv 摘要页明确给出
时间：2026-06-29 UTC 更新，对应 arXiv Tue, 30 Jun 2026 最新列表
要解决的问题/痛点：很多端到端驾驶方法仍主要基于“当前时刻的静态场景表征”做决策，缺少显式未来 rollout 和交通参与者之间的时间因果建模，遇到遮挡、突发事件或高不确定交互时，往往变得不稳定或者过度保守。
核心创新点：OWMDrive 把 4D occupancy world model 放到端到端驾驶中间层，先预测多步未来占据，再把它作为 conditional prior 引导 diffusion planner。亮点在于，规划不再只看现在，而是显式利用“当前观测 + 预测未来状态”的联合条件去生成轨迹。
方法机制或模型结构：系统先用 Occupancy World Model 进行 multi-step 3D occupancy forecasting，形成对场景未来演化的生成式先验；随后 diffusion-based planner 在该先验约束下迭代细化 trajectory candidates，最终输出更具前瞻性和因果一致性的 reinforced trajectory。
实验设置和关键结果：摘要没有给出具体 benchmark 分数，但明确声称 extensive experiments 表明该方法在 challenging 和 partially observable driving scenarios 中显著提升 planning reliability 和 safety，尤其对高不确定条件更稳。
为什么值得关注：这代表自动驾驶端到端路线的一个鲜明变化：不再满足于“直接从图像到轨迹”，而是主动把世界模型作为中介，显式补足未来场景演化与因果交互这两块短板。
可能局限或后续可跟进点：摘要没有公开 world model 的预测跨度、误差传播情况和实时性预算，也未说明在更复杂多车博弈场景中，occupancy prediction 误差会怎样影响 diffusion planner。

3. LWDrive: Layer-Wise World-Model-Guided Vision-Language Model Planning for Autonomous Driving
链接：https://arxiv.org/abs/2606.29879
作者/机构：Chen Yang, Yuhao Wei, Ze Xu, Ziheng Zou, Shuang Liang, Delin Ouyang, Lingfeng Qi, Jie Li, Guofa Li；机构未在 arXiv 摘要页明确给出
时间：2026-06-29 UTC 更新，对应 arXiv Tue, 30 Jun 2026 最新列表
要解决的问题/痛点：VLM 已经能给自动驾驶提供较强语义理解和常识推理，但直接由 VLM 产出的轨迹通常只有粗粒度意图，缺少几何精度、未来感知和多视角 grounding，离真正可执行规划还有距离。
核心创新点：LWDrive 把 VLM 生成的初始轨迹降格为“意图草图”，再用 layer-wise world-model guidance 去逐层修正。它不是把语言大模型当最终 planner，而是把其高层驾驶意图和 world model 的前瞻表征、BEV 约束以及历史时序状态结合起来，做 coarse-to-fine refinement。
方法机制或模型结构：作者先引入 future-frame generation supervision，让 VLM 内部表征学习 forward-looking dynamics；然后设计 Foresight Cascade Planner（FCP），在多层 VLM features 上结合 temporal states、Action-Query 表征和当前帧 multi-view BEV features，对候选轨迹逐级修正；最后由 score head 从候选中选出最优轨迹。
实验设置和关键结果：摘要给出了比较明确的结果：在 NAVSIM benchmark 上达到 92.0 分，在 NAVSIM-v2 上达到 89.6 分。论文还强调该框架能在保持高层驾驶意图的同时，逐步纠正空间位置和运动趋势。
为什么值得关注：这篇工作代表 VLM 驾驶规划进入“结构化降噪与校正”阶段。相比简单追求更大的多模态模型，它更像是在问：怎样让大模型负责它最擅长的语义意图，而把几何与动态细化交给更合适的模块。
可能局限或后续可跟进点：摘要未给出不同层特征各自贡献、候选轨迹数量与推理成本，也未说明该框架在闭环长时域场景中的稳定性和对少见危险事件的表现。

【机器人 / 具身智能】
4. VLK: Learning Humanoid Loco-Manipulation from Synthetic Interactions in Reconstructed Scenes
链接：https://arxiv.org/abs/2606.30645
作者/机构：Yen-Jen Wang, Jiaman Li, Sirui Chen, Takara E. Truong, Pei Xu, Pieter Abbeel, Rocky Duan, Koushil Sreenath, Angjoo Kanazawa, Carmelo Sferrazza, Guanya Shi, Karen Liu；机构未在 arXiv 摘要页明确给出
时间：2026-06-29 UTC 更新，对应 arXiv Tue, 30 Jun 2026 最新列表
要解决的问题/痛点：感知驱动的人形 loco-manipulation 需要把第一视角图像、语言指令和可执行的全身运动轨迹对齐起来，但现有数据源很难同时提供这三者，而且规模不足，导致人形机器人很难高效学到“看见场景后怎么带着全身去做事”。
核心创新点：VLK 通过 reconstructed scenes 合成 vision-language-kinematics supervision，把大规模高质量监督数据“造出来”。它不是单纯做视频仿真，而是利用 3D Gaussian Splatting 重建真实尺度室内场景，再基于特权信息合成导航与交互轨迹，最后反向渲染出成对的 egocentric observations。
方法机制或模型结构：整条流水线先重建 metric-scale indoor environments，再自动生成 navigation 和 object-interaction trajectories，形成“图像-语言-运动学轨迹”三元组；随后训练一个 VLK policy 预测 short-horizon whole-body kinematic trajectories，再由 whole-body tracker 转换成物理人形机器人的动作。
实验设置和关键结果：作者合成了 48,000 条 paired trajectories，无需人工示教；并在真实 Unitree G1 上评测导航与单物体搬运任务。摘要结论是：这些在重建场景中合成的交互监督，已经足以支撑 sim-to-real 的 perception-based humanoid loco-manipulation。
为什么值得关注：人形机器人当前一个核心瓶颈不是“模型不够大”，而是缺少足够多、足够对齐、足够真实的训练三元组。VLK 提供了一条绕开真人采集瓶颈的合成数据路线，而且直接落到真机验证上。
可能局限或后续可跟进点：摘要未说明更复杂长序列、多对象任务和动态障碍条件下的表现，也没展开重建质量、传感噪声和 tracker 误差对真机动作的影响。

5. GROW²: Grounding Which and Where for Robot Tool Use
链接：https://arxiv.org/abs/2606.30632
作者/机构：Yuhong Deng, Yuyao Liu, David Hsu；机构未在 arXiv 摘要页明确给出
时间：2026-06-29 UTC 更新，对应 arXiv Tue, 30 Jun 2026 最新列表
要解决的问题/痛点：机器人若想在开放世界里创造性地用工具，难点不只是“挑哪件物体当工具”，还包括“该用它的哪个部位、作用到目标的哪个区域”。传统 end-to-end affordance 学习往往数据饥渴，而且很难泛化到开放类别物体。
核心创新点：GROW² 把 open-world affordance grounding 拆成 Which 和 Where 两层：先决定工具与关键部位，再把这些部位落到精确 3D 区域。它利用“object parts”作为自然抽象层，把语义选择与几何定位分治，避免重型端到端训练。
方法机制或模型结构：语义层由 VLM 解析自然语言任务，选择合适工具，并识别工具与目标的 task-relevant parts；几何层再用视觉基础模型，把这些已选中的 parts 从单张 RGB-D 图像中精确 grounding 到 3D regions。
实验设置和关键结果：摘要明确说，该方法在 established benchmarks 上优于现有 SOTA affordance prediction baselines；同时在开放类别对象上实现 zero-shot generalization，并且在 simulated 与 real-world robot tool use 实验中都优于基线。
为什么值得关注：这篇论文很值得留意，因为它把“开放词汇理解”和“可执行几何 grounding”真正接了起来。相比单纯说机器人能看懂工具，这种做法更接近实际可操作的工具使用能力。
可能局限或后续可跟进点：摘要没有给出工具类别覆盖范围、失败类型和对 RGB-D 质量的依赖程度；后续要看在更复杂遮挡、软体目标和接触动力学更难的任务上是否仍稳。

6. Sequential Planning via Anchored Robotic Keypoints
链接：https://arxiv.org/abs/2606.30613
作者/机构：Bryce Grant, Aryeh Rothenberg, Logan Senning, Zonghe Chua, Zach Patterson, Peng Wang；机构未在 arXiv 摘要页明确给出
时间：2026-06-29 UTC 更新，对应 arXiv Tue, 30 Jun 2026 最新列表
要解决的问题/痛点：多轮代码生成式操控代理在任务变化或感知出错时，常需要反复重新问大模型、从头生成新方案，代价高且不稳定；真正拖后腿的层往往不是高层推理，而是对象感知与失败恢复。
核心创新点：SPARK 提出一个 training-free 的 neurosymbolic manipulation system，把一次 Gemini 调用得到的 typed behavior tree 作为固定计划骨架，把更多计算预算投给 perception 和 recovery loop，而不是每次失败都重新生成全流程代码。
方法机制或模型结构：第一步由单次 Gemini 调用生成由 composable primitives 组成的 typed behavior tree；第二步再用第二次 Gemini 调用给每个对象提出三种替代文本提示，交给 SAM3 检测，并保留最自信的 prompt-label 对；若 primitive 失败，recovery loop 会基于重新检测到的对象重试，而不再额外调用 LLM。
实验设置和关键结果：摘要给出的结果很扎实：在六个 LIBERO-PRO position/task cells 上达到 43.7%，超过 CaP-Agent0 的 18.2% 和若干 VLA 基线；替代 prompts 在 spatial suite 上带来 +27.7 点、在 object suite 上带来 +10.0 点，recovery loop 再整体增加 +5.0 点。相同 primitives 在 UR10e、Franka FR3 和双臂 Franka 三类机器人上覆盖 9 个任务、每任务 20 次试验，平均成功率 68%。
为什么值得关注：这篇工作说明“少调 LLM，多修感知与恢复机制”可能比一味增加 agent 推理链更有效。对工业落地来说，这种可追责、可复用、可换模块的 typed plan 很有吸引力。
可能局限或后续可跟进点：摘要没有展开复杂长时序任务和高遮挡环境下的失败模式，也未说明当 primitives 本身不够强时，behavior tree 框架的上限在哪里。

【交叉方向】
7. Robust and Efficient Monocular 3D Gaussian SLAM for Kilometer-Scale Outdoor Scenes
链接：https://arxiv.org/abs/2606.30436
作者/机构：Sicheng Yu, Dongxu Shen, Beizhen Zhao, Guanzhi Ding, Hao Wang；机构未在 arXiv 摘要页明确给出
时间：2026-06-29 UTC 更新，对应 arXiv Tue, 30 Jun 2026 最新列表
要解决的问题/痛点：把 monocular 3DGS SLAM 推到公里级室外场景，会同时撞上两个瓶颈：长时间位姿跟踪容易漂，地图里的 Gaussian primitives 又会快速膨胀，导致大场景重建既不稳也不省。
核心创新点：KiloGS-SLAM 把“抗漂移跟踪”和“生命周期受控的 Gaussian mapping”一起做。它不是只在后端补个小修补，而是从跟踪解算路径切换、灾难性漂移救援到 primitive 冗余控制，都做了系统级设计。
方法机制或模型结构：前端采用 motion-adaptive hybrid tracking，通过 condition-triggered three-tier solving pipeline，在 Essential matrix 与 PnP 之间动态切换以应对退化；必要时还会按需启用 foundation model 来救援轨迹。后端则用 probabilistic initialization、chunk-based multi-view densification 和 pruning 做 lifecycle-managed Gaussian mapping，在保留高频细节的同时压缩冗余。
实验设置和关键结果：摘要指出，在三个具有挑战性的 outdoor datasets 上，该方法实现了 SOTA tracking accuracy 和 rendering quality，并且能在单 GPU 上扩展到超过 10,000 frames 的长序列。
为什么值得关注：SLAM 社区近一年大量工作在追 3DGS 画质，但真正可用于自动驾驶或户外机器人系统的关键，仍然是规模、漂移与显存预算。KiloGS-SLAM 关注的是这三件更硬的事。
可能局限或后续可跟进点：摘要没有给出 foundation model 介入频率、整体实时性和不同场景动态物体占比下的稳定性；后续要看代码开源后工程复杂度是否可控。

8. Training Vision-Language-Action Models with Dense Embodied Chain-of-Thought Supervision
链接：https://arxiv.org/abs/2606.30552
作者/机构：Haoyang Li, Guanlin Li, Youhe Feng, Chen Zhao, Zhuoran Wang, Yang Li, Qizhe Wei, Shifeng Bao, Haitao Shen, Yihan Zhao, Tong Yang, Jing Zhang；机构未在 arXiv 摘要页明确给出
时间：2026-06-29 UTC 更新，对应 arXiv Tue, 30 Jun 2026 最新列表
要解决的问题/痛点：VLA 模型跨机器人本体迁移困难，一个根本原因是不同平台的低层 state/action spaces 差异很大；如果直接共享动作层，往往很难迁得稳。
核心创新点：作者提出 ZR-0，一个 2.6B 参数端到端 VLA 模型，抓住“不同机器人虽然动作空间不同，但高层认知过程相似”这一点，用 dense Embodied Chain-of-Thought（ECoT）监督，把跨本体共享的感知、识别、规划和子任务分解对齐到 VLM 内部表征中。
方法机制或模型结构：ZR-0 采用 dual-stream 结构：预训练 VLM 作为 System 2，在训练期生成结构化 ECoT；基于 Diffusion Transformer 的 action expert 作为 System 1，通过 flow matching 生成连续动作块。两者用 cross-attention 耦合，但通过 attention mask 限制 action expert 只读取输入提示特征，因此推理时可以完全跳过 ECoT 生成而不损失性能。
实验设置和关键结果：预训练数据为 ProcCorpus-60M，约 6000 万帧、1000 小时、40 万+ trajectories，其中 96.8% 帧带有密集 ECoT 标注。评测覆盖单臂 LIBERO、双臂 RoboTwin 2.0、类人 RoboCasa GR-1 Tabletop，以及 xArm 真机实验。摘要没有给出单项具体分数，但明确声称在这些设置中都取得了强表现。
为什么值得关注：它的重点不是“再造一个更大的 VLA”，而是把推理过程蒸到训练里，把跨本体共享的 cognition 层抽出来，对当前机器人基础模型的可迁移性问题很有针对性。
可能局限或后续可跟进点：摘要未给出不同 embodiment 间的细粒度增益拆解，也没说明 dense ECoT 标注的生成成本、噪声控制和对下游性能的边际贡献。

【趋势总结】
1. 最新这一批论文里，自动驾驶最明显的信号是“部署后闭环改进”和“世界模型介入规划”同时升温。R²LPL、OWMDrive、LWDrive 分别从持续纠错、4D occupancy 未来建模、VLM 分层校正三条路线出发，但共同点都是不再满足于一次性离线训练后直接上车。
2. 机器人方向的重心继续从“单一大模型包打天下”往“结构化感知-规划-恢复体系”回摆。SPARK 把 LLM 调用压缩到规划骨架，GROW² 把工具使用拆成语义与几何两层，VLK 则把训练瓶颈前移到高质量合成监督数据上，三者都很务实。
3. 交叉方向上，SLAM 和具身基础模型都在强调可扩展性。KiloGS-SLAM 关注公里级 outdoor 规模、漂移救援和内存生命周期；ZR-0 则关注跨本体共享 cognition。相比前一波只强调更大统一模型，这批工作更在意怎样把系统真正撑到长时程、异构平台和真实闭环里。
4. 和以往路线相比，新意不只是“模型更强”，而是开始系统性补齐长期被忽视的工程断点：闭环纠错机制、未来场景显式生成、typed plan 恢复、开放世界 affordance grounding、公里级 3DGS-SLAM 资源管理，以及跨本体 reasoning 对齐。对要落地到真实车和机器人的团队，这些点通常比单纯刷新离线榜单更有价值。
