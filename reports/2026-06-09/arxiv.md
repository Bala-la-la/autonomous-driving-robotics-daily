arXiv 自动驾驶与机器人晨报｜2026-06-09

说明：今天是 2026-06-09。按 2026-06-09 检索时，arXiv `cs.RO recent` 最新可见高相关批次主要对应 2026-06-05 提交、在 2026-06-08/09 可见的论文；因此本期明确回看最近 3-5 天，并优先选自动驾驶、机器人学习、具身规划、导航/仿真中最值得跟进的 8 篇。

一、自动驾驶

1. Planning-aligned Token Compression for Long-Context Autonomous Driving
链接：https://arxiv.org/abs/2606.07464
作者/机构：Zhixuan Liang, Yuxiao Chen, Yurong You, Peter Karkus, Wenhao Ding, Boyi Li, Alexander Popov, Yan Wang, Maximilian Igl, Yiming Li, Danfei Xu, Nikolai Smolyanskiy, Boris Ivanovic, Ping Luo, Marco Pavone；摘要页未直接给出机构
提交时间：2026-06-05
要解决的问题：长上下文驾驶模型越来越依赖多帧历史，但 token 和显存成本会迅速失控；常见启发式压缩会把真正影响 stop/yield/proceed 决策的关键历史一起抹掉。
核心创新点：提出 COMPACT-VA，把“保留什么历史”直接和规划目标绑定，而不是把压缩当成独立预处理。模型保的不是平均意义上的历史信息，而是对未来驾驶意图最有用的记忆。
方法机制/模型结构：基于 conditional VQ-VAE。训练时 posterior encoder 从未来轨迹蒸馏 planning intent，prior encoder 用压缩后的观测去预测该隐变量；压缩记忆和意图表征一起送入 policy 端到端学习，让 working memory 更像规划导向缓存。
实验设置和关键结果：作者专门评估需要长历史才能判对的高动态场景。摘要给出，在可比 token 预算下，成功率提升超过 6%，达到 68.3%；闭环性能基本保持的同时，实现 3.3 倍速度提升和 2.7 倍显存下降。
为什么值得关注：这篇不是单点刷榜，而是在解决车端和大规模仿真都绕不开的“长上下文跑不动”问题。若效果稳定，它可以作为已有 driving foundation model 的可插拔压缩层。
可能局限/后续可跟进点：摘要尚未展开极端遮挡、多车博弈、异常交通规则冲突下的信息保真度；也值得继续看它在不同 backbone、不同 memory budget 下的收益边界。

2. Test-Time Trajectory Optimization for Autonomous Driving
链接：https://arxiv.org/abs/2606.07170
作者/机构：Yihong Xu, Eloi Zablocki, Yuan Yin, Elias Ramzi, Ellington Kirby, Alexandre Boulch, Matthieu Cord；摘要页未直接给出机构
提交时间：2026-06-05
要解决的问题：很多端到端 planner 先产出若干候选轨迹，再让 scorer 排名。但 scorer 只能“选最好”，不能“把候选变好”；候选池一弱，后端再强也救不回来。
核心创新点：提出 TOAD，把 scorer 改造成测试时可直接优化轨迹的 reward，而不是停留在 reranking。
方法机制/模型结构：在推理阶段使用 Cross-Entropy Method，对基础 planner 给出的候选做 warm start 搜索；因此无需重训原 planner，也不绑定单一架构，属于典型 plug-and-play test-time optimization 层。
实验设置和关键结果：在 6 个基础 planner 上验证；摘要明确给出 NAVSIM-v1 达到 94.7 PDMS，NAVSIM-v2 达到 56.3 EPDMS，并在闭环 HUGSIM 上继续带来提升。
为什么值得关注：这代表一个很实用的方向转变: 与其总是重训更大 planner，不如把已有 scorer 真正变成“会改候选”的优化器。对工业栈而言，这比整套重做更现实。
可能局限/后续可跟进点：CEM 会引入额外时延，真实上车时的稳定性和最坏情况开销仍要看；还需观察它是否会在 OOD 场景中过拟合 scorer 偏好。

3. A Causal Probabilistic Framework for Perception-Informed Closed-Loop Simulation of Autonomous Driving
链接：https://arxiv.org/abs/2606.07186
作者/机构：Zhennan Fei, Rickard Johansson, Mikael Andersson, Matthias Eng, Mattias Eriksson, Kaveh Kianfar, Sadegh Rahrovani, Chris van der Ploeg, Michael Borth, Maren Buermann, Michiel Braat, Henk Goossens, Zijian Han, Majid Khorsand Vakilzadeh, Gabriel Rodrigues de Campos；摘要页未直接给出机构
提交时间：2026-06-05
要解决的问题：许多 SIL 闭环仿真默认使用理想感知，相当于把真值直接喂给后端规划控制，导致 ADAS/ADS 安全性被系统性高估，尤其不利于 SOTIF 验证。
核心创新点：把因果概率模型引入标准化场景仿真链路，用“受物理条件触发的真实感知错误”替代随机噪声注入。
方法机制/模型结构：框架把漏检、尺寸误差、定位偏移、目标合并等感知故障，和雾、雨、遮挡等物理触发条件以 causal probabilistic model 组织起来，再接入 scenario-based simulation toolchain，统一评估 ADAS 与 ADS。
实验设置和关键结果：摘要未给具体分数，但明确指出 perception-informed testing 能暴露理想 SIL 无法发现的 latent operational risks，并为 ISO 21448/SOTIF 提供可扩展验证路径。
为什么值得关注：过去一段时间，社区注意力大量集中在 planner、world model、VLA，但量产安全论证真正脆弱的环节往往是“仿真里有没有把感知错误当回事”。这篇更偏 validation infrastructure，但工程价值很高。
可能局限/后续可跟进点：下一步关键是如何用真实车队数据校准这些故障分布，以及不同传感器组合和地域条件间的可迁移性。

4. VeriDrive: Verifiable Counterfactual Supervision for Cost-Efficient Vision-Language Planning
链接：https://arxiv.org/abs/2606.07338
作者/机构：Zikai Zhang, Hubert P. H. Shum, Toby P. Breckon；摘要页未直接给出机构
提交时间：2026-06-05
要解决的问题：驾驶 VLM/VLA 越来越依赖 reasoning supervision，但自由文本 rationale 昂贵、难验证，也容易把“像推理”误当成“真监督”。
核心创新点：把驾驶推理监督改写成可验证、可反事实修正的结构化链条，而不是继续堆昂贵的自由文本 CoT。
方法机制/模型结构：VeriDrive 设计 Perception-Evaluation-Revision 三段式监督。先对关键交通体及未来运动做 grounding，再用可规则校验的证据评估不同 ego 轨迹风险，最后把危险意图修正到接近 expert 行为；数据构建上使用 local generation + validator-guided selective correction，只把困难样本升级给更贵模型。
实验设置和关键结果：基于 nuScenes 构建 VeriDrive 数据集，并在 Omni-Q 协议下训练。摘要明确称在受控 open-loop 实验中，L2、Collision、Intersection 均优于 OmniDrive，同时降低日志 token 用量、生成时间和实际付费 LLM/VLM 成本。
为什么值得关注：它把“推理监督”从不可审计文本泡沫，拉回到了可检查中间变量和标注成本控制，非常契合真实数据生产链。
可能局限/后续可跟进点：目前公开结果仍以 open-loop 为主；闭环收益、长尾规则冲突、跨法规域迁移能力还需要后续验证。

二、机器人 / 具身智能

5. Spline Policy: A Structured Representation for Robot Policies
链接：https://arxiv.org/abs/2606.07386
作者/机构：Mengze Tian, Yiming Li, Sichao Liu, Auke Ijspeert, Sylvain Calinon；摘要页未直接给出机构
提交时间：2026-06-05
要解决的问题：很多 manipulation policy 仍把动作表示为固定分辨率 action chunk，简单但几何和时间结构暴露很弱，也不方便执行前做编辑、约束、安全过滤或不确定性分析。
核心创新点：提出 Spline Policy，用样条参数替代 action chunk，同时尽量不改动现有 policy backbone，把策略输出重新结构化。
方法机制/模型结构：policy 直接预测 spline 参数，解码后得到连续轨迹，可按不同时间分辨率重采样；对二次样条，还能构造解析距离场并转成 state-dependent vector field，提供局部纠偏机制。该表示还支持把观测不确定性传播到样条参数、轨迹和流场，并与 null-space collision avoidance 等经典控制模块对接。
实验设置和关键结果：作者在低维运动学习、仿真 manipulation、灵巧操作和真实机器人案例中，把 SP 接到 diffusion、flow matching、transformer、VLA 等多类 backbone 上。摘要表明它在保持兼容性的同时，带来了紧凑解码、时间重采样、局部修正、不确定性评估和控制器兼容等性质。
为什么值得关注：这不是“再堆一个更大的模态模型”，而是让 learned policy 更容易被控制理论、安全层和约束优化接住，属于很值得工程团队认真看的输出表示创新。
可能局限/后续可跟进点：样条表示对强接触、瞬时切换、高速双臂协同任务的表达能力还有待验证；实际收益可能依赖具体任务频谱。

6. CAPE: Contrastive Action-conditioned Parallel Encoding for Embodied Planning
链接：https://arxiv.org/abs/2606.07304
作者/机构：Cong Chen, Haowen Wang, Zhixiang Zhang, Pei Ren, Zhengping Che；摘要页未直接给出机构
提交时间：2026-06-05
要解决的问题：不少 embodied dynamics model 把大量容量花在重建视觉上显眼但与规划无关的细节，导致模型更擅长“复原画面”，却不一定更懂“动作会带来什么后果”。
核心创新点：提出 CAPE，把学习目标从 future observation reconstruction 转成 future outcome discrimination，聚焦 action-conditioned change。
方法机制/模型结构：给定初始观测和候选动作序列，CAPE 用单次前向并行解码完整未来 latent trajectory；训练时用 Goal-Convergent Contrastive Objective，把通向同一未来结果的预测拉近、不同结果拉远，使表征能力集中到规划相关变化。
实验设置和关键结果：在真实世界 DROID 和零样本迁移 RoboCasa 上，摘要称其在 future-state retrieval、offline action matching 和 closed-loop planning 上都显著优于基线，并在长时预测时明显降低规划阶段推理成本。
为什么值得关注：这代表具身 world model 从“像视频模型那样重建一切”转向“为规划服务的差异建模”。对 manipulation 和 model-based planning 来说，这是方向性变化。
可能局限/后续可跟进点：复杂接触、罕见失败模式、跨 embodiment 泛化还未在摘要里展开；需要继续看长时滚动误差是否会重新累积。

7. Coarse-to-Control: Action-Token Planning for Vision-Language-Action Models
链接：https://arxiv.org/abs/2606.07107
作者/机构：Jinhao Wu, Shiduo Zhang, Yicheng Liu, Xiaopeng Yu, Sixian Li, Siyin Wang, Hang Zhao, Jing Huo, Yang Gao, Jingjing Gong, Xipeng Qiu, Yu-Gang Jiang；摘要页未直接给出机构
提交时间：2026-06-05
要解决的问题：多数 VLA 直接从观测映射到动作，缺少显式中间规划层，长时任务里前几步一偏就会连锁失误。
核心创新点：提出 Coarse-to-Control，在统一 action token 空间内原生做 plan-execute，而不是先写抽象文本计划再翻译成控制。
方法机制/模型结构：策略先预测一串粗粒度 action tokens，用来概括未来意图轨迹；再在同一离散动作词表内条件化生成可执行 action tokens。由于规划和执行共用 action vocabulary，规划信号天然贴近控制流形，减少“会说不会做”的落差。
实验设置和关键结果：在 LIBERO、SimplerEnv-WidowX 和真实机器人操作任务上，摘要明确称相较直接动作生成始终更优，且在长时、多阶段任务上的收益最大。
为什么值得关注：这和 CAPE、Spline Policy 一起说明，具身系统正在把规划结构重新带回模型内部，而不再盲目押注全黑盒直接吐动作。
可能局限/后续可跟进点：离散 action token 词表如何设计会强烈影响性能；高自由度精细连续控制下，分辨率与量化误差仍值得警惕。

三、交叉方向 / 部署与仿真

8. RhinoVLA Technical Report
链接：https://arxiv.org/abs/2606.07383
作者/机构：Huixi Intelligence 团队，作者列表含 Chen Zhang, Chenyang Zhou, Guanglei Ding, Guanghui He 等
提交时间：2026-06-05
要解决的问题：VLA 在机器人操作上潜力很强，但真正落到边缘硬件实时闭环控制时，视觉 token、上下文 token 和投影算子开销常常直接把系统拖慢到不可用。
核心创新点：提出与 Huixi R1 edge SoC 协同设计的部署导向 VLA，不是只追离线任务成功率，而是把 token 效率、统一接口和编译部署一起优化。
方法机制/模型结构：采用 token-efficient 的 Qwen3-VL backbone 和 continuous Action Expert，削减 VLM 侧 token 与算量；再引入统一接口，把 View Registry、72D physical state-action slot space、robot-instance LoRA 组合起来，对齐异构机器人观测与动作模式；部署侧再做硬件感知编译、混合精度和并行视觉编码。
实验设置和关键结果：摘要明确给出，在相近参数规模下，下游表现可与 pi0.5 相当，同时在 Huixi R1 上达到 11.69 Hz 端到端推理，超过 10 Hz 实时闭环控制目标。
为什么值得关注：这类论文很少见，因为它不只是“训练一个通用 VLA”，而是把模型、接口、芯片、编译链一起打包考虑。对于机器人落地，这是比纯 benchmark 胜负更稀缺的信号。
可能局限/后续可跟进点：摘要尚未完整展开跨机器人任务谱和更开放环境下的泛化边界；后续值得跟其开源代码、模型和硬件接口是否足够复现。

趋势总结

1. 这批论文的主线不是“更大的模型”，而是“把真正影响部署成败的系统瓶颈拆出来做”。自动驾驶这边是长上下文压缩、test-time 优化、感知误差注入、可验证监督；机器人这边是动作表示、面向规划的 dynamics 学习、统一 action-token 规划和边缘部署。

2. 自动驾驶与具身智能正在共享同一套研究趣味：更强调 memory/compression、可验证中间变量、test-time adaptation、结构化 action representation，而不是继续无差别堆大 backbone。

3. 和上一波“端到端黑盒全吞”路线相比，新意在于把规划、控制、监督、仿真、部署重新拆成可审计模块。换句话说，社区开始更认真地算两本账：一是性能账，二是算力/安全/标注成本账。

4. 接下来最值得跟的不是谁单点 benchmark 多 1 分，而是谁能把这些模块真正接进闭环系统：例如 COMPACT-VA 是否能跨 backbone 泛化，TOAD 是否能在时延预算内稳定收敛，VeriDrive 是否能转成闭环收益，RhinoVLA 是否能形成可复用的“模型-芯片-接口”共设计范式。
