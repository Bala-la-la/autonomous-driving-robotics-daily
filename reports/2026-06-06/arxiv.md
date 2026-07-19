arXiv 自动驾驶与机器人晨报｜2026-06-06

时间范围：优先覆盖 2026-06-01 至 2026-06-06 的最新提交/更新；自动驾驶方向补充到 2026-05-16 至 2026-05-31 的高相关论文，并在条目中明确日期。

一、自动驾驶

1. StandardE2E: A Unified Framework for End-to-End Autonomous Driving Datasets
链接：https://arxiv.org/abs/2606.04271
作者/机构：Stepan Konev
提交时间：2026-06-02
要解决的问题：E2E 自动驾驶近两年最大工程瓶颈之一不是模型本身，而是 Waymo E2E、Argoverse 2、NAVSIM、WayveScenes 等数据集格式、坐标系、模态覆盖和预处理链路彼此割裂，导致跨数据集预训练、复现实验和辅助任务监督成本极高。
核心创新点：把“统一数据接口”本身做成研究基础设施，而不是再做一个单一数据集上的 planner；重点是统一 schema、统一预处理入口、统一 scenario 级过滤与多数据集采样。
方法机制/结构：定义 canonical schema，把各数据集映射到同一中间表示；支持在单一 PyTorch DataLoader 中混合六类数据集，便于跨域预训练、辅助任务联合训练和场景筛选；新增数据集时，只需实现从原始帧到 canonical schema 的映射层。
实验设置和关键结果：摘要未给出具体数值，但确认已支持六个数据集开箱即用：Waymo End-to-End、Waymo Perception、Argoverse 2 Sensor、Argoverse 2 LiDAR、NAVSIM(OpenScene-v1.1)、WayveScenes101。
为什么值得关注：这类工作短期不一定刷榜，但它直接决定多域 E2E 驾驶是否能进入“可复用、可组合、可持续扩展”的工程阶段；对做基础模型、world model、trajectory pretraining 的团队尤其关键。
可能局限/后续跟进：这是基础设施层创新，不直接证明统一接口后一定带来性能提升；后续要看社区是否基于该框架形成真正可比较的 cross-dataset benchmark。

2. Learning A Unified Risk Map for Autonomous Driving in Partially Observable Environments
链接：https://arxiv.org/abs/2605.22189
作者/机构：Jie Jia, Yaofeng Su, Zeyu Bao, Yun Hong, Bingzhao Gao, Zhongxue Gan, Wenchao Ding；Fudan University
提交时间：2026-05-29
要解决的问题：遮挡和部分可观测性一直是自动驾驶里最难“显式建模”的风险源。已有方法要么只给 reachable set 式的保守风险上界，要么在高遮挡时轨迹预测不准，导致 planner 不是太冒险就是太保守。
核心创新点：提出 unified risk map，把交通流风险和碰撞风险放到同一时空表征中统一建模，不再把“未来交通参与者分布”和“ego 可执行风险”分开处理。
方法机制/结构：用时空风险建模结合 diffusion-based scenario generation，显式生成遮挡区域内可能出现的交通场景，再把这些潜在场景投影到统一风险图上供下游规划使用。
实验设置和关键结果：摘要未披露具体百分比，但确认方法面向 partially observable driving，并通过场景生成缓解高遮挡不确定性；从问题设定看，重点不是平均 ADE/FDE，而是把 occlusion 下的风险表达变得可用于规划。
为什么值得关注：现在很多 AD 论文都在做 VLA、CoT 或 world model，但真正影响量产安全的，往往仍是遮挡场景下的风险表达。这个工作把 risk map 从“手工规则图层”推进到可学习、可生成、可联动 planner 的形式，实用价值很高。
可能局限/后续跟进：如果生成的遮挡场景与真实长尾分布偏差较大，风险图仍可能误导规划；后续值得看 closed-loop 评测、不同遮挡强度下的 calibration，以及是否能接入 VLA 或 world model planner。

3. HEAT: Heterogeneous End-to-End Autonomous Driving via Trajectory-Guided World Models
链接：https://arxiv.org/abs/2605.19631
作者/机构：Hoonhee Cho, Giwon Lee, Jae-Young Kang, Hyemin Yang, Heejun Park, Kuk-Jin Yoon
提交时间：2026-05-19
要解决的问题：很多 E2E 驾驶方法在单一数据域上效果很好，但一旦把 nuScenes、NAVSIM、Waymo E2E 这类异构域混训，域差异会带来冲突梯度，模型会学成“哪里都不够好”的折中解。
核心创新点：把 trajectory 当作跨域不变量，用 trajectory-guided learning 组织世界模型和下游 planner 的学习，让模型优先对齐“驾驶意图”而不是传感器风格或数据域表面统计。
方法机制/结构：先预训练 trajectory-conditioned world model，学习观测与未来动作耦合的 latent；再通过 trajectory-guided behavior clustering 构造 domain-invariant prototype 和 visual-coupled action memory；最后用对比对齐与 episodic memory refinement 训练统一 E2E 模型。
实验设置和关键结果：在 nuScenes、NAVSIM、Waymo End-to-End 三个 benchmark 上评测，摘要确认其相对既有方法在全部域上都有明显提升，并展示单一统一模型可在异构数据集上维持强性能。
为什么值得关注：这篇不是简单做 domain generalization，而是把“多域驾驶基础模型”问题重新表述为 trajectory 对齐问题，和最近机器人领域用 action/token/world model 统一不同 embodiment 的思路高度一致。
可能局限/后续跟进：目前摘要只给出“substantial improvements”而无细粒度数值；后续要看是否在真实闭环安全指标上依然成立，以及 memory/prototype 机制是否会增加部署复杂度。

4. DriveSafer: End-to-End Autonomous Driving with Safety Guidance
链接：https://arxiv.org/abs/2605.16737
作者/机构：Shounak Sural, Raj Rajkumar
提交时间：2026-05-16
要解决的问题：当前生成式 E2E planner 平均指标变好，但在安全关键场景里仍存在相当多“PDMS=0”的灾难性失败。很多论文关注平均 planning quality，却没有把 catastrophic failure 当第一优化目标。
核心创新点：明确采用 failure-centric safety 视角，对训练和推理两端同时加安全约束，不是追求更像人类轨迹，而是优先减少会直接导致碰撞、越界或错误行驶方向的失效案例。
方法机制/结构：在 DiffusionDrive 基础上加入 safety-aware 与 physics-informed losses，并在推理阶段增加 safety guidance，过滤不可行轨迹并把生成结果拉回安全可行域。
实验设置和关键结果：在 NAVSIM 上，相比 DiffusionDrive，灾难性失败数（PDMS=0）降低 48%，drivable-area compliance failure 降低超过 65%，整体 PDMS 也提升到 90.3。
为什么值得关注：这是少见把“长尾灾难失败压降”单独拎出来做核心目标的 E2E AD 论文，方向上比继续卷平均 L2/ imitation error 更接近真实部署诉求。
可能局限/后续跟进：安全 guidance 是否会牺牲驾驶风格、效率或舒适性，需要更完整的 trade-off 报告；另外它仍基于已有 planner 做修正，距离形式化安全保证还有距离。

二、机器人 / 具身智能

5. τ_0-WM: A Unified Video-Action World Model for Robotic Manipulation
链接：https://arxiv.org/abs/2606.01027
作者/机构：Pengfei Zhou, Shengcong Chen, Di Chen, Jiaxu Wang, Rongjun Jin, Bingwen Zhu, Yike Pan, Songen Gu, Kuanning Wang, Shufeng Nan, Xingyu Qiu, Chenhao Qiu, Pu Yang, Yunuo Cai, Jianxiong Gao, Yifan Li, Yanwei Fu, Xiangyu Yue, Zhi Chen, Jianlan Luo
提交时间：2026-06-02
要解决的问题：机器人操作里，policy learning、future video prediction、action evaluation 往往是三套系统，动作能不能执行、执行后会看到什么、候选动作哪个更好，通常被拆开做，导致长程任务和细粒度纠错能力不足。
核心创新点：把视频预测、动作生成和动作打分统一进单个 video-action world model；不仅能直接出 action chunk，还能 roll out 候选动作并评估任务进度。
方法机制/结构：基于共享的视频 diffusion backbone，提供两个接口：一是 video action model，同时预测 future visual latent 和 continuous action chunk；二是 action-conditioned video simulator，对候选动作做多视角未来展开并输出 dense task-progress score。推理时结合 test-time computation、re-denoising consistency 排序，以及 simulator-based rectification 修正低质量候选。
实验设置和关键结果：训练数据规模约 27,300 小时，覆盖真实机器人遥操作、UMI 风格交互、人类第一视角视频以及 rollout/failure 轨迹；摘要确认在长时程、精细操作任务上优于相关 baseline。
为什么值得关注：这是“机器人版 world model 不只做 imagination，还直接服务动作筛选和在线修正”的代表作，说明 manipulation 正在从单次前馈 policy 走向带 test-time compute 的 deliberative control。
可能局限/后续跟进：训练代价极高，对算力与多源数据质量要求很高；后续要看真实机器人 latency、闭环稳定性，以及 simulator score 是否真能泛化到 OOD 任务。

6. PlatonicNav: Unveiling Semantic Correspondence in Navigation with Platonic Topological Maps
链接：https://arxiv.org/abs/2606.01788
作者/机构：Junlin Long, Zeyu Zhang, Xu Deng, Yiran Wang, Yue Yang, Luke Borgnolo, Maxwell Twelftree, Yang Zhao；Maincode
提交时间：2026-06-03
要解决的问题：具身导航常依赖 paired vision-language data、目标特定训练或重型语义建图。问题是这类方案数据依赖强，换环境和目标语义时泛化有限。
核心创新点：提出 training-free 的 embodied navigation 框架，用纯视觉方式建立 semantic topological map，再通过“blind matching”把语言目标与环境语义结构对齐，不依赖配对的 vision-language 监督。
方法机制/结构：核心是 Platonic Topological Maps，把场景中的语义对应关系抽象成拓扑结构，再做跨模态但免训练的语义匹配与路径决策。
实验设置和关键结果：摘要未给出具体数值，但明确定位在 embodied visual navigation，目标是 household service、assistive robotics 和大规模自主探索等场景下的 zero-/low-training 泛化。
为什么值得关注：当前很多 embodied navigation 工作在堆更大 VLM 或更复杂 planner，这篇反而强调“训练自由”和语义对应结构，和近期具身领域追求更轻、可迁移、少标注的方法形成呼应。
可能局限/后续跟进：训练自由通常也意味着上限受表征质量制约；需要继续观察在复杂多层室内环境、动态障碍和长指令导航上的鲁棒性。

7. AFUN: Towards an Affordance Foundation Model for Functionality Understanding
链接：https://arxiv.org/abs/2606.02551
作者/机构：Zhaoning Wang, Yi Zhong, Jiawei Fu, Henrik I. Christensen, Jun Gao；University of Michigan
提交时间：2026-06-02
要解决的问题：很多机器人操作模型知道“抓哪里”，但不真正理解“这个物体能怎么被用、沿什么运动轨迹被作用”，导致 open-world manipulation 泛化弱、可解释性差。
核心创新点：把 affordance 从局部接触预测提升到功能理解层，既预测 functional mask，也预测 3D motion curve，试图给机器人一个“在哪里交互 + 如何交互”的统一接口。
方法机制/结构：输入 RGB-D 观测和语言描述，输出可操作区域与对应三维运动曲线，面向跨对象、跨环境、跨任务的 affordance 泛化。
实验设置和关键结果：摘要没有公开数值，但明确目标是 generalizable manipulation in open and unstructured environments；从问题定义看，它更像操作前的中间可解释层，而不是直接端到端动作头。
为什么值得关注：具身领域近一年一个明显趋势是重新重视中间表征，AFUN 代表的就是“不是所有问题都直接丢给 VLA 动作头”，而是引入更强功能归纳偏置。
可能局限/后续跟进：如果 affordance 标注和 3D motion curve 的监督成本太高，扩展速度会受限；后续值得看它如何与 VLA、grasp planner、tool-use 数据结合。

三、交叉方向

8. RoboSemanticBench: Diagnosing Semantic Grounding in Action Prediction for VLA Models
链接：https://arxiv.org/abs/2606.02277
作者/机构：Bin Yu, Yao Zhang, Haishan Liu, Shijie Lian, Yuliang Wei, Xiaopeng Lin, Zhaolong Shen, Changti Wu, Ruina Hu, Bailing Wang, Cong Huang, Kai Chen；Zhongguancun Academy
提交时间：2026-06-02
要解决的问题：VLA 常被默认继承了 VLM/LLM 的语义能力，但机器人微调后，这些语义能力是否真的转化为正确动作选择，其实缺少专门 benchmark 去验证。
核心创新点：设计一个专门测“semantic grounding in action prediction”的 embodied benchmark：机器人先回答多选题，再去抓取正确答案对应的物块，借此把“会不会抓”和“能不能语义选对”拆开评估。
方法机制/结构：数据覆盖算术、小学数学、常识/事实理解，并有四选一和十选一两种设置；关键评价不是单纯 success，而是控制 grasp success 后，看语义选对率是否仍成立。
实验设置和关键结果：摘要给出的结论很强：代表性 VLA 模型在许多设置下虽然会抓，但在控制抓取成功率后，语义选择接近随机甚至低于随机，暴露出 backbone 语义能力与 action prediction 之间存在明显断裂。
为什么值得关注：这篇对自动驾驶和机器人都重要，因为它提醒大家“有语言链路”不等于“语义已进入控制回路”；很多 VLA 成果可能高估了真实的指令理解能力。
可能局限/后续跟进：当前 benchmark 偏向离散答案选择，和开放式长任务仍有差距；但它已经足够成为后续 VLA 评测必须补上的一块短板。

四、趋势总结

1. 自动驾驶方向的新意，不再只是继续卷 E2E planner 本体，而是明显转向“三层补强”：数据基础设施统一（StandardE2E）、部分可观测风险建模（Unified Risk Map）、多域 world model 迁移（HEAT）、以及 failure-centric safety correction（DriveSafer）。这比过去单纯追逐 imitation/planning 平均指标更贴近真实部署难题。
2. 机器人/具身方向出现两个同步趋势：一是 world model 从离线 imagination 工具变成在线动作筛选与纠错模块，代表是 τ_0-WM；二是社区重新重视 affordance、topology、semantic grounding 这类中间结构，而不是把所有能力都寄托在更大的 VLA 动作头上。
3. 交叉方向最值得警惕的是“语义能力错觉”：RoboSemanticBench 表明，预训练模型的语义理解并不会自动流入动作决策。这和自动驾驶中“有 reasoning 文本输出不代表规划更安全”是同一类问题。
4. 相比 2024-2025 年那波“把 VLM/LLM 接到控制器上”的路线，这一批论文更强调可部署性：统一数据、异构域训练、遮挡风险、在线安全修正、test-time compute、可解释中间表示。说明领域重心正从“会不会做 demo”转向“能不能跨域、可控、可纠错地运行”。

信息来源说明：以上内容基于最近 arXiv 摘要页、arXiv 索引页及 Hugging Face Papers 对应论文页整理；带具体数值的结果仅引用摘要/论文页明确给出的信息，未给出数值的条目已显式标注“摘要未披露具体数值”。
