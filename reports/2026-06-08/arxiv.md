arXiv 自动驾驶与机器人晨报｜2026-06-08

说明：今天是 2026-06-08。arXiv 周末通常没有大批量新提交，因此本期优先覆盖 2026-06-05 提交、在 2026-06-08 仍属于“最新一批可见”的高相关论文；如果你周末没刷论文，这一批基本就是今天最值得补的内容。

一、自动驾驶

1. Planning-aligned Token Compression for Long-Context Autonomous Driving
链接：https://arxiv.org/abs/2606.07464
作者/机构：Zhixuan Liang, Yuxiao Chen, Yurong You, Peter Karkus, Wenhao Ding, Boyi Li, Alexander Popov, Yan Wang, Maximilian Igl, Yiming Li, Danfei Xu, Nikolai Smolyanskiy, Boris Ivanovic, Ping Luo, Marco Pavone；摘要页未给出机构
提交时间：2026-06-05
要解决的问题：单体 vision-action 驾驶模型一旦拉长上下文，就会被 token 数量和实时算力预算卡死。现有压缩多靠时间衰减等启发式规则，容易把真正影响决策的历史片段一起丢掉。
核心创新：提出 COMPACT-VA，把上下文压缩和规划目标绑在一起学，而不是把压缩当成独立预处理。模型不是“把历史都压一压”，而是围绕未来驾驶意图来保留决策关键记忆。
方法机制：框架建立在 conditional VQ-VAE 上。posterior encoder 在训练时从未来轨迹中蒸馏 planning intent，prior encoder 再从压缩后的观测中预测这一隐变量；压缩记忆与预测意图拼接后送入 policy，端到端联合优化，使 working memory 更像“为规划服务的可学习缓存”。
实验设置与结果：作者专门在 stop/yield/proceed 这类高度依赖长历史的高信号动态场景评测，并设计行为级指标。摘要给出，在相近 token 预算下，成功率提升超过 6%，达到 68.3%；闭环评测中，相比不压缩处理保住整体驾驶性能，同时实现 3.3 倍速度提升和 2.7 倍显存下降。
为什么值得关注：这类工作击中的不是某个单 benchmark 小技巧，而是驾驶 foundation model 能否真跑在车端/仿真集群里的核心瓶颈。相比改 backbone，压缩层更容易作为现有系统的插拔式升级。
可能局限/跟进点：摘要还没展开更多长尾场景和不同 backbone 的收益边界；后续值得跟进它在复杂城市博弈、极端遮挡和多车交互中的信息保真度。

2. A Causal Probabilistic Framework for Perception-Informed Closed-Loop Simulation of Autonomous Driving
链接：https://arxiv.org/abs/2606.07186
作者/机构：Zhennan Fei, Rickard Johansson, Mikael Andersson, Matthias Eng, Mattias Eriksson, Kaveh Kianfar, Sadegh Rahrovani, Chris van der Ploeg, Michael Borth, Maren Buermann, Michiel Braat, Henk Goossens, Zijian Han, Majid Khorsand Vakilzadeh, Gabriel Rodrigues de Campos；摘要页未给出机构
提交时间：2026-06-05
要解决的问题：大量 SIL 仿真默认使用“理想感知”，等价于直接把真值喂给规划与控制，结果会系统性高估 ADAS/ADS 的安全性，尤其不利于 SOTIF 验证。
核心创新：把因果概率模型显式接入标准化场景仿真链路，用可解释的物理触发条件去注入真实感知错误，而不是随机打噪声。
方法机制：框架把雨雾、目标合并、定位偏移、尺寸误差、漏检等问题，用 causal probabilistic model 组织成可采样故障模式，再注入 scenario-based simulation toolchain。这样既能保持工程流程标准化，又能把 perception failure 从“黑盒风险”改成“可枚举、可控制、可审计”的测试变量。
实验设置与结果：摘要没有给细分数字，但明确指出 perception-informed 测试能暴露理想 SIL 无法发现的潜在运行风险，并给出其对 ISO 21448/SOTIF 更可扩展的验证路径。
为什么值得关注：社区过去几年更爱写 planner、world model、VLA，但真正影响量产安全论证的，往往是仿真是否把感知错误建模进来了。这篇更偏 validation infrastructure，但非常实用。
可能局限/跟进点：目前从摘要看，关键价值在方法框架而非统一 benchmark 分数；后续要看模型参数如何从真实车队数据校准，以及不同传感器栈间的可迁移性。

3. Test-Time Trajectory Optimization for Autonomous Driving
链接：https://arxiv.org/abs/2606.07170
作者/机构：Yihong Xu, Eloi Zablocki, Yuan Yin, Elias Ramzi, Ellington Kirby, Alexandre Boulch, Matthieu Cord；摘要页未给出机构
提交时间：2026-06-05
要解决的问题：端到端驾驶 planner 常见流程是“先出一组候选轨迹，再打分挑最好的一条”。问题在于 scorer 只能事后挑选，不能反向改善候选集；一旦 proposal pool 本身弱，再好的 scorer 也救不了。
核心创新：提出 TOAD，把 scorer 直接视为轨迹级 reward function，在测试时做轨迹优化，而不是只做 ranking。
方法机制：方法在推理阶段使用 Cross-Entropy Method，对基础 planner 给出的候选做 warm start 搜索；因此它不需要重训原模型，也不绑定某个特定 planner，可作为 plug-and-play 的 test-time optimization 层叠在现有系统上。
实验设置与结果：作者在 6 个基础 planner 上验证，摘要给出 NAVSIM-v1 上 PDMS 94.7，NAVSIM-v2 上 EPDMS 56.3，并在闭环 HUGSIM 上也有提升。
为什么值得关注：这篇体现了一个很明确的新方向：不是急着重训更大的 planner，而是在 test-time 把现有 scorer 真正用起来，靠搜索把“会判断”转成“会改进候选”。这比完全重训一套新系统更工程友好。
可能局限/跟进点：CEM 带来额外推理开销，真正上车时延与稳定性仍要看；后续值得关注不同 reward landscape 下的收敛性，以及它对 OOD 场景是否会过拟合 scorer 偏好。

4. VeriDrive: Verifiable Counterfactual Supervision for Cost-Efficient Vision-Language Planning
链接：https://arxiv.org/abs/2606.07338
作者/机构：Zikai Zhang, Hubert P. H. Shum, Toby P. Breckon；摘要页未给出机构
提交时间：2026-06-05
要解决的问题：视觉语言驾驶模型越来越依赖 reasoning supervision，但自由文本 rationale 一方面贵，另一方面很难验证真假，容易把“看起来像推理”当成有用监督。
核心创新：把驾驶推理改写成可验证、可反事实修正的结构化监督，而不是继续堆昂贵的 free-form CoT。
方法机制：VeriDrive 将监督拆成 Perception-Evaluation-Revision 链。先把关键交通体及其未来运动 grounding 出来，再基于可校验规则评估不同 ego 轨迹的风险，最后把危险意图修正到接近 expert 行为。为控制标注成本，框架采用 local generation + validator-guided selective correction，只把无效或困难样本升级给更昂贵模型处理。
实验设置与结果：基于 nuScenes 构建 VeriDrive 数据，并在 Omni-Q 协议下训练。摘要称开放环实验中，L2、Collision、Intersection 均优于 OmniDrive，同时降低日志 token 用量、生成时间和实际 LLM/VLM 标注成本。
为什么值得关注：最近自动驾驶 VLM/VLA 很容易陷入“给更多文字解释就更聪明”的幻觉，这篇把重点拉回到可审计中间变量和低成本监督，非常契合真实数据生产。
可能局限/跟进点：目前结果仍以 open-loop 为主；后续要看结构化推理字段在闭环驾驶、长尾规则冲突、以及不同法规域下的稳定性。

二、机器人 / 具身智能

5. Spline Policy: A Structured Representation for Robot Policies
链接：https://arxiv.org/abs/2606.07386
作者/机构：Mengze Tian, Yiming Li, Sichao Liu, Auke Ijspeert, Sylvain Calinon；摘要页未给出机构
提交时间：2026-06-05
要解决的问题：当前 imitation learning 和很多 manipulation policy 常把动作表示为固定分辨率的 action chunks，简单有效，但几何和时间结构暴露得很少，也不方便在执行前做编辑、约束或不确定性分析。
核心创新：提出 Spline Policy，用样条参数代替 action chunk，同时尽量不改 policy backbone，把“输出轨迹本身的结构”显式带回来。
方法机制：policy 直接预测 spline 参数，随后可解码为连续轨迹，并可按不同时间分辨率采样。对于二次样条，作者还给出解析距离场构造，使其转成 state-dependent vector field；在一定正则和投影假设下，这个场提供局部纠偏能力。该表示还能把观测不确定性传播到样条参数、轨迹和流场，并与 null-space collision avoidance 等经典控制模块对接。
实验设置与结果：作者在低维运动学习、仿真 manipulation、灵巧操作和真实机器人案例中，将 SP 适配到 diffusion、flow matching、transformer 和 VLA 等不同 backbone。摘要强调其保持兼容性的同时，获得了紧凑解码、时间重采样、局部修正、置信传播和控制器兼容等额外性质。
为什么值得关注：这不是单纯追更大模型，而是把机器人策略输出重新结构化，让 learned policy 更容易被控制理论、约束优化和安全层接住，工程价值很高。
可能局限/跟进点：样条表示可能对高度接触密集、瞬时切换快的任务存在表达边界；后续值得跟进在高速动态操作和双臂协同上的表现。

6. CAPE: Contrastive Action-conditioned Parallel Encoding for Embodied Planning
链接：https://arxiv.org/abs/2606.07304
作者/机构：Cong Chen, Haowen Wang, Zhixiang Zhang, Pei Ren, Zhengping Che；摘要页未给出机构
提交时间：2026-06-05
要解决的问题：很多 embodied dynamics model 把学习容量浪费在重建视觉上显眼但与规划无关的背景内容，导致模型会“复原画面”，却不一定会“预测动作后果”。
核心创新：提出 CAPE，把学习目标从重建 future observation 改成区分不同动作序列诱发的未来结果，更聚焦 action-conditioned change。
方法机制：给定初始观测和候选动作序列，CAPE 用单次前向并行解码完整未来 latent trajectory；训练时使用 Goal-Convergent Contrastive Objective，让通向同一未来结果的预测彼此对齐，不同结果则拉开，从而把表征能力集中到“动作会改变什么”。
实验设置与结果：在真实世界 DROID 以及零样本迁移 RoboCasa 上，CAPE 在 future-state retrieval、offline action matching 和 closed-loop planning 上都显著优于基线，并在长时预测时明显降低规划阶段推理成本。
为什么值得关注：这类工作说明具身 world model 正从“重建型视频模型”转向“面向规划的差异建模”。它更接近机器人真正关心的 counterfactual dynamics。
可能局限/跟进点：摘要没展开复杂接触、稀有失败模式和跨 embodiment 泛化；后续要看它在多步误差累积下是否仍稳。

7. Coarse-to-Control: Action-Token Planning for Vision-Language-Action Models
链接：https://arxiv.org/abs/2606.07107
作者/机构：Jinhao Wu, Shiduo Zhang, Yicheng Liu, Xiaopeng Yu, Sixian Li, Siyin Wang, Hang Zhao, Jing Huo, Yang Gao, Jingjing Gong, Xipeng Qiu, Yu-Gang Jiang；摘要页未给出机构
提交时间：2026-06-05
要解决的问题：多数 VLA 直接把观测映射到动作，没有显式中间规划层，因此长时任务里一旦前几步偏了，错误会持续累积。
核心创新：提出 Coarse-to-Control，在 action-token 空间内原生做 plan-execute，而不是先生成抽象语言计划再翻译回控制。
方法机制：policy 先预测一串粗粒度 action tokens，用来概括未来意图轨迹；再在同一离散动作词表内，条件化生成可执行动作 tokens。因为计划与执行共用统一 action vocabulary，规划信号天然贴近控制流形，不会像文本计划那样在落地时产生额外语义损耗。
实验设置与结果：在 LIBERO、SimplerEnv-WidowX 和真实机器人操作任务上，摘要称该方法持续优于直接动作生成，尤其在多阶段长程任务上收益最大。
为什么值得关注：这篇和 CAPE、Spline Policy 一起反映出明显趋势：具身系统开始重新把“规划”和“控制结构”带回模型内部，而不是继续押宝全黑盒 end-to-end。
可能局限/跟进点：离散 action token 设计对效果影响会很大；后续值得看它在高自由度、连续精细控制场景里的分辨率瓶颈。

三、交叉方向 / 趋势判断

1. 这批论文最强的共同点不是“更大模型”，而是“把系统里真正贵或真正脆弱的环节补起来”。
自动驾驶这边，COMPACT-VA 解决长上下文 token 爆炸，TOAD 解决 proposal 质量受限，因果仿真框架解决理想感知导致的虚高评测，VeriDrive 解决昂贵且不可验证的推理监督。

2. 机器人这边开始重新重视结构。
CAPE 明确围绕 action-conditioned future 来学，Coarse-to-Control 把 planning 拉回 action token 空间，Spline Policy 直接把输出表示从 chunk 改成可控连续样条。和过去“更大 backbone + 直接吐动作”相比，这一批明显更强调可控性、可解释性和可接控制层。

3. 自动驾驶与具身智能正在共享同一种研究品味。
无论是驾驶还是机器人，今天更受关注的都不是单点 perception 刷榜，而是 memory/compression、test-time optimization、可验证 supervision、结构化 action representation 这些更靠近部署链路的环节。

4. 相比前一波流行路线，这一批的新意在于把“推理/规划/压缩/表示”做成系统级部件，而不是再额外堆一个大模型头。
这意味着接下来值得重点跟的，不只是谁在 benchmark 上多 1-2 分，而是谁能把这些模块真正接进闭环系统、把算力和安全账一起算清楚。
