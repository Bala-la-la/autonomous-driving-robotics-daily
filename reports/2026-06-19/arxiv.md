arXiv 自动驾驶与机器人晨报｜2026-06-19

说明：截至 2026-06-19 早晨检索，arXiv 最新一批高相关更新主要集中在 2026-06-17 UTC（北京时间 2026-06-18）。本期优先覆盖 automatic driving、AEB、robot manipulation、world model、SLAM、occupancy perception 等方向。机构信息以 arXiv 摘要页可见为准；本批多数条目公开作者，但未在摘要页直接列出机构。

【自动驾驶】
1. Learning to Annotate Delayed and False AEB Events: A Practical System for Extreme Class Imbalance and Asymmetric Label Noise
链接：https://arxiv.org/abs/2606.19186
作者：Mengxiang Hao, Xin Jiang, Xinghao Huang, Wenliang Su, Zhiteng Wang, Junjie Rao, Xiaotian Yang, Wei Liao, Chengyu Han, Gen Liang, Yulun Song, Zhitao Xu
时间：2026-06-17 更新
问题/痛点：真实车队里每天会产生海量 AEB 触发，但真正值得系统改进团队重点看的 delayed/false trigger 往往不到 5%；如果仍靠人工筛查，标注成本极高，而且正类极少、负类极多，模型很容易被“正常触发”淹没。
核心创新：把 AEB 事件自动标注问题正式建模成“极端类别不平衡 + 非对称标签噪声”联合难题；不仅做分类器，还做一套可上线的 annotation system。
方法机制：一方面做针对性数据增强，直接操控焦点目标属性、移植自车动力学并屏蔽非焦点参与者，尽量合成更贴近延迟/误触发的困难样本；另一方面用 stable hardness estimation 和 probe-guided adaptive threshold 清洗被错标成 true trigger 的样本，减少多数类噪声对少数类学习的压制。
实验与结果：作者给出生产结果，关键异常事件召回提升 80%，人工工作量下降 50%。这不是只在离线 benchmark 上提点数，而是直接改善车队事件流转效率。
为什么值得关注：自动驾驶近两年越来越受制于“数据闭环速度”而不是单一模型结构；这篇论文的价值在于，它把安全关键事件挖掘做成了可持续增益的数据基础设施。
可能局限/跟进：摘要没有展开误报代价在不同场景下的细分表现；后续值得继续跟踪它对稀有 corner cases、跨车型泛化、以及标注置信度校准的处理。

2. Scaling Learning-based AEB with Massive Unlabeled Data
链接：https://arxiv.org/abs/2606.18864
作者：Xiangyu Wang, Yang Zhan, Mengxiang Hao, Chuanchuan Zhong, Yansong Jia, Junjie Zhang, Yu Han, Xin Jiang, Zhen Cao, Ying Wang, Yulun Song, Zhitao Xu
时间：2026-06-17 更新
问题/痛点：学习式 AEB 想吃到车队海量无标签数据的红利，但 teacher 伪标签一旦带偏，就会把风险幻觉一并放大，最后带来 spurious trigger。
核心创新：提出 stabilized MF-SSL，把小规模高质量 anchor set 当作安全反馈来校正 teacher，同时显式处理 anchor 模糊性和标注/未标注分布不匹配。
方法机制：两处关键设计分别是 Noise-Aware Decoupling 和 kinematics-gated pseudo-labeling。前者把容易产生歧义的 anchor 从 teacher 的监督更新链路里拿掉，避免错监督；后者在生成伪标签时加入运动学门控和 teacher conflict penalty，抑制“看起来危险但实际上不该刹”的风险幻觉。
实验与结果：摘要给出很强的工程指标。模型从 1M 扩展到 1B windows 时持续获益；最终 1B 训练的 student 已部署到数十万辆车，并在超过 10^9 公里实驶中验证，positive-to-false activation ratio 超过 100:1，相比纯规则基线 accident-free driving mileage 提升 35%。
为什么值得关注：这说明 AEB 不只是靠规则兜底，已经开始进入“海量弱监督 + 安全反馈校正”的规模化学习阶段；而且论文直接给出车端部署量级，可信度很高。
可能局限/跟进：摘要没有拆出不同道路类型、天气、前车急减速/切入等场景的收益来源；后续值得观察它在新城市和新的传感器配置下是否仍稳定。

3. A Mixed-Reality Testbed for Autonomous Vehicles
链接：https://arxiv.org/abs/2606.19267
作者：H. M. Sabbir Ahmad, Ehsan Sabouni, Emrullah Celik, Zean Wan, Damola Ajeyemi, Christos G. Cassandras, Wenchao Li
时间：2026-06-17 更新
问题/痛点：纯仿真很难覆盖真实硬件延迟、通信抖动和传感误差；纯实车又很难安全复现危险场景。自动驾驶尤其缺少“能大规模造险、又能带真实硬件进环”的验证平台。
核心创新：提出 mixed-reality HIL testbed，把物理移动机器人、光真实虚拟环境和多智能体交通仿真整合到同一测试回路里，同时支持车联网通信和 Connected/Autonomous Vehicles 研究。
方法机制：系统把真实机器人作为可感知、可执行的硬件代理，再叠加大量虚拟交通体实现混合规模扩展；在控制层，作者把 perception、planning 和基于 Control Barrier Functions 的在线学习控制器联动起来，用 safety-guaranteed 方式做闭环验证。
实验与结果：摘要没有给出单一 SOTA 数字，而是强调该平台已能验证多模态感知、规划控制与多车连接场景，并用实验展示测试台桥接 simulation 与 hardware deployment 的能力。
为什么值得关注：这类工作的重要性不在“算法多新”，而在于自动驾驶验证栈正在从离线数据集和 CARLA 分数，走向更接近真实部署条件的中间层验证。
可能局限/跟进：摘要没展开 testbed 的规模上限、传感保真度和场景迁移成本；后续如果开源场景协议、通信栈和复现实验，会更有行业影响力。

【机器人 / 具身智能】
4. Zero-Shot Long-Horizon Dexterous Manipulation via Multi-View 3D-Grounded VLM Reasoning
链接：https://arxiv.org/abs/2606.19340
作者：Jisoo Kim, Sangwon Baik, Taeksoo Kim, Sungjoo Kim, Junyoung Lee, Mingi Choi, Hanbyul Joo
时间：2026-06-17 更新
问题/痛点：长程灵巧操作最大的瓶颈之一，是语言指令到可执行 3D 操作点的落地仍不稳定；单视角或 RGB-D grounding 容易在遮挡、工具使用和新物体上失效。
核心创新：不训练端到端 policy，而是用多视角 RGB + VLM 推理，先做 reference-frame task grounding 和 primitive-level 2D keypoint，再通过几何一致性把它们抬升到 3D，形成可执行任务计划。
方法机制：关键是 multi-view fusion。作者一边用多视角三角化整合 VLM 在各视角给出的 grounding，一边用 reference-view ray voting 沿语义射线搜索跨视角几何一致的 3D 候选点。对 tool-use 场景，再检索对象中心的 atomic action，并把已有 6D 工具轨迹对齐到当前场景；对 dexterous grasp，则把 grasp keypoint 扩展成 task-conditioned affordance region，再用 arm-hand motion generator 产出可执行抓取与运动对。
实验与结果：实机实验显示，该方法在 3D grounding accuracy 和 execution reliability 上都优于单视角 RGB-D grounding 与 fine-tuned VLA baseline；同时借助闭环状态验证与重规划，能在未见物体和新场景里零样本完成长程任务。
为什么值得关注：这条路线代表机器人界一个明显转向，即把“大模型理解”与“几何可执行性”分开做，而不是指望单个 VLA 直接吞掉全部推理与控制。
可能局限/跟进：系统依赖多视角标定质量，也依赖原子动作库覆盖度；后续值得看其在接触高度复杂、连续力控制更强的任务中还能否保持零样本能力。

5. Do as I Do: Dexterous Manipulation Data from Everyday Human Videos
链接：https://arxiv.org/abs/2606.19333
作者：Bhawna Paliwal, Haritheja Etukuru, William Liang, Pieter Abbeel, Nur Muhammad Mahi Shafiullah, Jitendra Malik
时间：2026-06-17 更新
问题/痛点：多指灵巧手最缺的不是模型名义容量，而是可扩展数据。现实里高质量机器人示教稀缺，而互联网上海量人类操作视频又很难直接变成机器人可执行轨迹，因为存在 hand-object interaction 估计困难和 human-to-robot embodiment gap。
核心创新：提出 DO AS I DO，把日常单目 RGB 人类视频重建并重定向为多指机器人手的执行数据，目标是从“人类视频”直接产出“robot-complete manipulation data”。
方法机制：先从第一视角和第三视角 in-the-wild 视频中恢复手物交互，再把估计出的 hand-object interaction 重定向为真实机器人能够执行的动作序列。论文强调的是完整链路：从原始 RGB 视频，到 interaction estimate，再到实机可执行轨迹，而不是只做 pose reconstruction。
实验与结果：作者报告在带真值的数据集和在线收集视频集上，DO AS I DO 在 hand-object interaction estimation 与 dexterous trajectory extraction 上都超过先前方法，并据此总结出人类视频采集与筛选的 efficacy playbook。
为什么值得关注：如果这条路线成立，灵巧操作训练数据的瓶颈会被大幅松动，因为可用数据源将从实验室示教扩展到互联网视频。
可能局限/跟进：从视频到机器人动作仍有接触动力学和手型差异损失；值得继续关注作者是否公开大规模重定向数据，以及这些数据对真实策略训练的边际增益。

6. Mem-World: Memory-Augmented Action-Conditioned World Models for Persistent Robot Manipulation
链接：https://arxiv.org/abs/2606.18960
作者：Zirui Zheng, Jiaqian Yu, Xiongfeng Peng, Jun Shi, Mingyi Li, Chao Zhang, Weiming Li, Dong Wang, Huchuan Lu, Xu Jia
时间：2026-06-17 更新
问题/痛点：机械臂操控中，腕部相机会频繁被末端和被操物遮挡，动作条件世界模型很容易遗忘前几帧看见过的场景细节，导致 rollout 出现 hallucination，进而影响策略评估和数据合成。
核心创新：提出 Mem-World，把历史观测做成 multi-view、action-conditioned 的显式记忆系统；核心记忆单元 W-VMem 以 wrist-view 为中心，用 4D surfel-indexed memory 记录“哪个表面元素在何时何地被看见过”。
方法机制：生成未来视频前，系统会基于 future action 通过 surfel-based rendering 和 scoring 检索相关历史帧，只把真正对当前预测有帮助、且不冗余的记忆喂给模型，从而提升长期一致性。
实验与结果：摘要给出两个硬指标。首先，Mem-World 用于 policy evaluation 时，与真实世界表现的 Pearson correlation 相比 Ctrl-World 提升 14.5%；其次，用合成数据反哺策略后，长程任务成功率从 58% 提升到 72%。
为什么值得关注：世界模型最近很热，但真正落地到操作时最大的难点不是“视频好不好看”，而是“记不记得之前看过什么”。这篇工作直接打在 persistent manipulation 的关键短板上。
可能局限/跟进：记忆检索开销和 surfel 表示在复杂多材质物体上的鲁棒性仍需验证；后续值得看它和更强的 VLA、规划器结合后的收益。

【交叉方向：感知 / SLAM / 机器人移动性】
7. FAST-LIVGO: A Degeneracy-Robust LiDAR-Inertial-Visual-GNSS Fusion Odometry
链接：https://arxiv.org/abs/2606.19190
作者：Zhiyu Chen, Chunran Zheng, Jiayu Wen, XiaoLei Zhang, Jiaming Xu, Feng Pan, Yukang Cui
时间：2026-06-17 更新
问题/痛点：现有 LIVO 系统本地精度不错，但长距离累计漂移难免；一旦进入几何退化、纹理稀缺或高动态环境，里程计容易崩，连带 GNSS 融合的 outlier rejection 也会失效。
核心创新：提出紧耦合的 LiDAR-Inertial-Visual-GNSS 融合框架，并显式感知 LIVO degeneracy，在“用里程计指导 GNSS”与“用 GNSS 帮里程计恢复”之间做双模切换。
方法机制：后端基于 Error-State Iterated Kalman Filter；对高动态条件，引入基于 Dynamic Time Warping 的在线时空对齐；在 GNSS 侧加入基于 Doppler shift 和 fixed-anchor Time-Differenced Carrier Phase 的观测模型，试图在不扩展历史锚点状态的前提下拿到毫米级相对约束。
实验与结果：作者在公开 M3DGR 数据集和自建 20m/s 固定翼无人机数据集上验证，结果显示能减少 accumulated drift 和 map ghosting，并在精度和鲁棒性上超过现有方法。
为什么值得关注：GNSS 重新被认真纳入多传感融合主链，而不是只做松耦合校正，是一个很实用的方向；对于自动驾驶、无人机和户外机器人都很关键。
可能局限/跟进：系统工程复杂度高，对传感同步和标定质量要求高；摘要也未给出实时算力预算，部署成本仍需继续看。

8. Monocular 3D Occupancy Perception for Robots on Sidewalks via Hybrid 2D-3D Learning
链接：https://arxiv.org/abs/2606.19122
作者：Yukai Ma, Joe Lin, Liu Liu, Honglin He, Lulu Ricketts, Brad Squicciarini, Yong Liu, Bolei Zhou
时间：2026-06-17 更新
问题/痛点：送货机器人、电动轮椅这类 sidewalk robot 面对的环境比车道更拥挤、更杂乱，也更不规则；但现有 3D occupancy 方法主要围绕道路自动驾驶设计，往往依赖昂贵的多相机和 dense LiDAR-RGB 标注。
核心创新：提出 WalkOCC，用 hybrid 2D-3D learning 把少量配对 LiDAR-RGB 序列和大规模单目 2D 图像一起利用，目标是在只用单目输入的前提下做更稳的 sidewalk occupancy prediction。
方法机制：框架通过 paired sequence 自举 pseudo occupancy supervision，再和额外的 2D-only 数据联合训练；核心是把来自 3D 配对数据的几何 grounding 与来自大量单目图像的可扩展表征学习结合起来，避免完全依赖昂贵 3D 标注。
实验与结果：摘要称其在预测精度、对 curb/gutter 等细粒度城市结构的分割，以及环境变化和跨机体迁移鲁棒性上，均优于 self-supervised image-based baseline；同时发布 Sidewalk3D 数据集用于评测。
为什么值得关注：自动驾驶社区的 occupancy 表征正在向“非车道场景”迁移，而人行道机器人是一个更贴近落地、也更少被充分研究的场景。
可能局限/跟进：单目 occupancy 的深度与遮挡不确定性仍然是硬伤；后续应关注 Sidewalk3D 是否足以支撑跨城市泛化，以及模型在夜间/雨雪场景中的表现。

【趋势总结】
1. 这批论文里最强的信号是“数据闭环和系统验证重新回到中心”。AEB 两篇论文一个解决异常事件挖掘，一个解决无标签规模化学习，说明车端安全功能正在从规则工程走向数据工程与弱监督工程。
2. 机器人操作方向明显在拆解端到端大模型。Zero-shot dexterous manipulation 把 VLM 语义 grounding、3D 几何提升、原子动作检索和运动生成拆开；Mem-World 则把“记忆检索”独立成世界模型的关键部件。相比早期一股脑训练更大的 VLA，这一批更强调结构化中间层。
3. 感知与定位方向的新意在于“更面向真实部署限制”。FAST-LIVGO 关注退化工况下的恢复能力，WalkOCC 关注人行道与单目低成本部署，Mixed-Reality Testbed 关注从仿真到硬件的验证断层。
4. 和以往只追求单一 benchmark SOTA 相比，最近这批工作更在意系统可扩展性：是否能吃到 1B 级别无标签数据，是否能在硬件在环里验证，是否能把互联网视频真正转成机器人数据，是否能在长时操控里保住记忆一致性。
