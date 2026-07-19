arXiv 自动驾驶与机器人晨报｜2026-06-30

说明：按 2026-06-30 北京时间抓取。联网检索后，当前能稳定检索到的最新高相关 arXiv 提交/更新主要集中在 2026-06-26 UTC；本期以这一天的新稿为主，无需回退到更早 3-5 天窗口。作者信息来自 arXiv 条目；机构若 arXiv 摘要页未明确列出，则注明“未在 arXiv 摘要页明确给出”。

【自动驾驶】
1. Drifting in the Future: Stabilizing Path Following Drifting on High-Latency Vehicle Systems
链接：https://arxiv.org/abs/2606.27914
作者/机构：Frederik Werner, Till Heintzenberg, Markus Lienkamp, Johannes Betz；机构未在 arXiv 摘要页明确给出
时间：2026-06-26 提交/更新
要解决的问题/痛点：自动漂移控制过去大多依赖研究平台，默认电机响应快、车轮可独立驱动；但量产车存在超过 250 ms 的动力总成时延和机械耦合车轴，很多实验室方法放到真实量产底盘就失效。
核心创新点：这篇工作不是简单“复现漂移”，而是针对高时延量产车重做控制器。作者引入 powertrain delay predictor、适配高延迟和差速器耦合的控制重构，以及基于制动的速度稳定机制，把研究型 drifting controller 推进到 production sports car 场景。
方法机制或模型结构：控制框架先用预测器补偿执行延迟，再在路径跟踪和侧滑控制中显式纳入高延迟与 driven axle differential coupling，最后用 brake-based velocity stabilization 抑制振荡和速度漂移。
实验设置和关键结果：真实车辆实验覆盖 circle 和 figure-eight 漂移。摘要给出的关键结果是：在执行器时延超过 250 ms 的条件下，系统仍能把横向误差控制在 1.1 m，把 sideslip overshoot 控制在 0.06 rad，同时维持稳定路径与侧滑跟踪。
为什么值得关注：它说明“极限工况自动控制”开始从炫技 demo 转向量产可迁移性，这对主动安全、失稳救车和高动态车辆控制都有现实意义。
可能局限或后续可跟进点：摘要未说明不同路面附着、湿滑工况、轮胎温度变化和更复杂轨迹下的性能，也未展开对模型失配的鲁棒性边界。

2. Characterizing Driver Interactions with Autonomous Vehicles via Response Maps
链接：https://arxiv.org/abs/2606.27656
作者/机构：Dave Broaddus, Rachel DiPirro, Chishang (Mario) Yang, Dan Calderone, Wendy Ju, Meeko Oishi；机构未在 arXiv 摘要页明确给出
时间：2026-06-26 提交/更新
要解决的问题/痛点：自动驾驶在共享交通环境中不能只“自己开得对”，还要预判人类驾驶员会如何回应自己的让行、不让行和博弈策略。过去很多交互建模强调单向预测，却较少把人类反应建成显式反馈律。
核心创新点：作者把人类驾驶员对 AV 的反应建模成 response map，即在耦合状态空间上刻画“AV 行为变化如何触发人类驾驶动作变化”的反馈函数，并用博弈论视角解释交互差异。
方法机制或模型结构：论文采用线性表示形式，把人类驾驶员加速度行为表示为 AV 行为的函数；核心不是只预测轨迹，而是提取“yielding / non-yielding / responsive”三类 AV 策略对人类驾驶输入的系统性影响。
实验设置和关键结果：基于 driving simulator 的经验数据建模。摘要给出的明确结论有两点：第一，人类驾驶员的加速度反应可被 response maps 有效刻画；第二，针对让行、不让行和对人类反应式三类 AV 行为，人类驾驶反应存在显著统计差异。
为什么值得关注：这类工作有助于把“社会兼容导航”从概念层推向可估计、可验证、可嵌入规划器的结构化模型，对 merge、unprotected turn、交叉口博弈尤其重要。
可能局限或后续可跟进点：当前结果来自模拟器数据；后续要看其在真实道路、不同文化驾驶风格、稀有冲突场景和非线性交互中的适用性。

3. RS-Diffuser: Risk-Sensitive Diffusion Planning with Distributional Value Guidance
链接：https://arxiv.org/abs/2606.27766
作者/机构：Shiqiang Gong；机构未在 arXiv 摘要页明确给出
时间：2026-06-26 提交/更新
要解决的问题/痛点：扩散式离线规划近来表现强，但大多默认 risk-neutral，只追求平均回报；在自动驾驶和机器人导航里，真正致命的是低概率高损失尾部事件，平均最优并不等于可部署。
核心创新点：作者把 distributional critic 引入 diffusion planner，在采样阶段直接用 tail-aware risk objective 的梯度去引导去噪过程，让同一个训练好的模型在推理阶段即可切换 risk-averse、risk-neutral 或 risk-seeking 行为。
方法机制或模型结构：系统由未来状态轨迹扩散生成器、逆动力学动作解码器和 Monte Carlo distributional critic 组成；critic 用 quantile regression 估计整条候选规划的 return distribution，再基于 CVaR 等目标为 denoising 过程提供 guidance。
实验设置和关键结果：摘要指出在 risk-sensitive D4RL 与 risky robot navigation 基准上达到 SOTA，同时在提升总体回报的同时降低最坏情形风险和 safety violation。
为什么值得关注：虽然论文实验不只限于驾驶，但这条路线非常契合自动驾驶规划正在强化的“风险显式可调”需求，比单纯做更保守的 cost shaping 更灵活。
可能局限或后续可跟进点：摘要未披露推理开销、风险参数与行为变化的可解释性，以及在更长时域闭环控制里的稳定性；后续值得跟踪是否能进入真实车端或高保真仿真栈。

【机器人 / 具身智能】
4. DexCompose: Reusing Dexterous Policies for Multi-Task Manipulation with a Single Hand
链接：https://arxiv.org/abs/2606.28323
作者/机构：Dihong Huang, Zhenyu Wei, Zhuxiu Xu, Yunchao Yao, Sikai Li, Mingyu Ding；机构未在 arXiv 摘要页明确给出
时间：2026-06-26 提交/更新
要解决的问题/痛点：灵巧手往往能学会单项技能，但一只手想在“先稳住已有物体状态”的同时继续完成第二个操作时，很容易出现手指资源冲突，导致旧任务被破坏、新任务也做不好。
核心创新点：DexCompose 提出 role-aware residual composition，不是从零训一个更大的统一策略，而是把两个预训练全手策略按“手指级 action ownership”重新分工，并用双残差模块分别照顾“保持已有状态”和“执行新增任务”。
方法机制或模型结构：先从第一项技能成功后的 post-task states 出发，做 release tests 找到哪些手指必须继续维持已建立的抓持或接触；再训练 bounded residual stabilizer 负责守住旧任务，训练 context-aware residual 在分配给新任务的动作子空间内改造下游 frozen policy。
实验设置和关键结果：在 16 个复合灵巧操作任务上评测，覆盖 4 类 object-retention 技能和 4 类后续交互。摘要给出的关键数值是平均 composite success rate 达到 77.4%。
为什么值得关注：这篇论文代表一种很务实的组合范式，强调策略复用和结构化干预，而不是把所有多任务冲突都丢给更大的端到端模型去硬学。
可能局限或后续可跟进点：目前是双技能合成场景，后续要看能否扩展到更长任务链、更复杂接触模式，以及 finger ownership 是否会在软体物体或高不确定环境里失效。

5. CacheMPC: Certified Cached Model Predictive Control for Quadruped Locomotion
链接：https://arxiv.org/abs/2606.28300
作者/机构：Nimesh Khandelwal, Mehul Anand, Shakti S. Gupta, Mangal Kothari；机构未在 arXiv 摘要页明确给出
时间：2026-06-26 提交/更新
要解决的问题/痛点：四足机器人分层控制里，MPC 很强但每周期都要求解 QP，嵌入式算力经常吃不消，更新频率上不去；可如果简单缓存历史解，又会担心失稳或代价劣化。
核心创新点：作者提出 Certified CacheMPC，把 horizon contact-force trajectories 做 locality-sensitive hashing 缓存，并且只在每次检索结果通过 a-posteriori certificate 后才允许复用，从而把“快”与“可验证安全边界”结合起来。
方法机制或模型结构：缓存按接触模式分桶，在线时先做 top-K certified retrieval，再在 deadline 预算内决定是否继续做 QP solve；若预算不足，则退回 shifted last-certified fallback。证书部分同时检查 primal feasibility，并给出基于拉格朗日 dual gap 的 cost suboptimality 上界。
实验设置和关键结果：在 Unitree Go2 上完成 2,038 个可用 MuJoCo 冷启动试验、包含 600 个 failure-boundary 栅格实验，并做了 Orin NX 真机首轮部署。摘要结果显示：simulation 中位求解加速 25 倍，硬件上中位加速 18.7 倍；在 n=50 的边界单元实验中，缓存版本与无缓存基线的闭环稳定率无显著差异。
为什么值得关注：这不是单纯刷 locomotion policy 成功率，而是直指“控制器算不算得过来”的工程瓶颈。对边缘部署和高频控制场景特别有价值。
可能局限或后续可跟进点：作者也坦率指出，当前样本量还不足以解析 certificate 对闭环安全的真实增益；后续需看更复杂地形、接触突变和更高自由度平台上的表现。

6. PA-BiCoop: A Primary-Auxiliary Cooperative Framework for General Bimanual Manipulation
链接：https://arxiv.org/abs/2606.28192
作者/机构：Bai Qicheng, Wang Ziru, Ma Teli, Dai Guang, Wang Jingdong, Wang Mengmeng；机构未在 arXiv 摘要页明确给出
时间：2026-06-26 提交/更新
要解决的问题/痛点：很多双臂操作方法把两只手看成完全对称的执行器，缺少明确的主辅分工，导致跨阶段协作不稳定，也难处理“主手做核心动作、辅手做支撑/定位”的真实操作逻辑。
核心创新点：PA-BiCoop 借鉴人类双手协作习惯，提出 primary-auxiliary arm differentiation，并且角色不是人工固定，而是可以随任务阶段动态调整。
方法机制或模型结构：系统共享一个全局特征编码器，但分出两个专门 decoder。primary decoder 预测主手在基坐标系下的 pose 和核心任务 affordance heatmaps；auxiliary decoder 则在主手坐标系下输出辅手相对 pose。另有 dynamic role assignment module 自动决定左/右手谁担任主辅角色。
实验设置和关键结果：摘要指出该方法在 RLBench2 仿真任务上平均比 SOTA 基线高 48%，在真实世界任务上平均提升超过 50%。
为什么值得关注：相比继续堆更大 VLA 或更复杂语言接口，这篇论文回到双臂协作最本质的结构问题，说明显式角色建模依然有巨大回报。
可能局限或后续可跟进点：摘要未展开任务类别分布、失败模式以及在双臂动力学强耦合或遮挡严重条件下的表现；后续值得关注其在开放环境双臂操作上的泛化。

【交叉方向】
7. LXD-SLAM: LiDAR+X Dense SLAM with Σ(i=0..5)C(5,i) Configurable Sensor Combinations
链接：https://arxiv.org/abs/2606.27811
作者/机构：Zhong Wang, Lin Zhang, Linfei Li, Ying Shen, Shaoming Zhang, Pengcheng Shi, Shengjie Zhao；机构未在 arXiv 摘要页明确给出
时间：2026-06-26 提交/更新
要解决的问题/痛点：复杂环境中的定位退化、传感器漂移和平台异构性长期困扰自动驾驶与机器人。很多多传感器 SLAM 系统可用，但模块化不足，且融合公式或地图表达并不统一，换平台代价高。
核心创新点：LXD-SLAM 试图把 LiDAR、Camera、IMU、Wheel Encoder、GNSS 统一到一个以 3D LiDAR 为中心的 plug-and-play 框架里，最多支持 32 种传感器组合，并同时兼顾实时里程计、全局一致性和稠密网格建图。
方法机制或模型结构：前端采用统一的 Iterative Error-State Kalman Filter，并加入 adaptive hierarchical prediction；更新阶段联合最小化 point-to-mesh 距离与视觉重投影误差。地图表示采用连续 multi-layer GP sub-meshes，用于高效 ray-to-mesh 深度恢复；回环侧则提出来自 GP sub-meshes 的 Extended Scan Context 和 Bidirectional PnP 优化。
实验设置和关键结果：在公开数据集与真实环境实验中，摘要指出该系统在多种传感配置下达到或超过专用 SOTA odometry 方法，同时能实时生成高保真、全局一致的 dense meshes。
为什么值得关注：这类统一式 SLAM 底座很适合自动驾驶、移动机器人和多平台部署团队，因为它把“换传感器=重写系统”的痛点往平台层解决。
可能局限或后续可跟进点：摘要没有量化各传感组合的增益差异、不同组合下的算力占用和标定敏感性；后续应关注代码开放后的复现复杂度。

8. SimFoundry: Modular and Automated Scene Generation for Policy Learning and Evaluation
链接：https://arxiv.org/abs/2606.28276
作者/机构：Nadun Ranawaka, Josiah Wong, Wei-Lin Pai, Wei-Teng Chu, Tianyuan Dai, Masoud Moghani, Hang Yin, Yunfan Jiang, Wesley Durbano, Brandon Huynh, Yu Fang, Linxi Fan, Danfei Xu, Ruohan Zhang, Li Fei-Fei, Bowen Wen, Ajay Mandlekar, Yuke Zhu；机构未在 arXiv 摘要页明确给出
时间：2026-06-26 提交/更新
要解决的问题/痛点：真实机器人训练和评估太贵，传统仿真场景制作又太慢，导致真实数据、仿真数据和策略评测之间难以形成高频闭环。
核心创新点：SimFoundry 做的是从一段视频自动构建 sim-ready digital twin，并进一步自动生成 digital cousins，即在保持 affordance 的前提下，对对象、场景和任务进行系统化变体编辑。
方法机制或模型结构：框架强调模块化自动场景重建，以及 object/scene/task 三层编辑能力。重点不是只做更像真的重建，而是让场景可被系统性改写，以生成更大、更可控的训练与评测分布。
实验设置和关键结果：覆盖 7 个 manipulation tasks 和 5 种 policy architectures。摘要给出的关键结果是：simulation evaluation 对真实表现的平均 Pearson 相关系数为 0.911，mean maximum ranking violation 为 0.018；在 real-world zero-shot 评测中，加入 object、scene、task cousins 的 sim 训练，平均成功率分别提升 17%、21% 和 40%。
为什么值得关注：这篇论文把“仿真是否真的能预测真实机器人表现”回答得更有说服力，而且不只支持训练，还支持系统级评测与分布扩展。
可能局限或后续可跟进点：摘要没有展开视频到 digital twin 的失败边界、场景重建耗时，以及更复杂动态场景中的可扩展性；后续值得持续跟踪其开源工具链成熟度。

【趋势总结】
1. 最近这一批论文的一个鲜明变化，是研究重心继续从“更大的统一模型”转向“更可部署的系统结构”。DexCompose、CacheMPC、PA-BiCoop 和 LXD-SLAM 都在回答同一件事：怎样把已有模块更稳定地组合起来，而不是盲目端到端吞并一切。
2. 自动驾驶方向的信号是“闭环现实主义”进一步加强。无论是高时延量产车漂移控制、显式人机交互 response map，还是风险可调的 diffusion planning，都比过去更强调系统约束、博弈反馈和尾部风险。
3. 机器人方向则继续往两端分化：一端是更强结构先验与可验证控制，比如 CacheMPC、主辅双臂分工；另一端是更高质量的数据与仿真生成基础设施，比如 SimFoundry。这说明社区开始同时补“控制可靠性”和“训练闭环效率”两块短板。
4. 相比前一阶段更偏“VLA/世界模型统一吃掉一切”的叙事，这批新稿的新意在于把组合、证书、风险、角色分工、异构传感与仿真预测性重新拉回中心。对真正要落地到车和机器人上的团队，这条路线通常更有工程价值。
