arXiv 自动驾驶与机器人晨报｜2026-07-15

说明：截至 2026-07-15 早晨，最新一批高相关 arXiv 更新主要集中在 2026-07-13（UTC）；由于 2026-07-14 至 2026-07-15 直接命中“自动驾驶/机器人/具身智能”的高质量新增不多，本文补充了最近 3-5 天内在 2026-07-13 更新的高相关论文。作者/机构信息以 arXiv 页面可见信息为准；“可能局限/后续跟进”部分如未被摘要直接陈述，已按摘要内容做审慎推断。

【自动驾驶】
1. FAST: A Framework for Aligned Sampling and Training in Parallel Reinforcement Learning for Autonomous Driving
链接：http://arxiv.org/abs/2606.21587
作者：Bonan Wang, Letian Tao, Bin Shuai, Jiaxin Gao, Wenxin Zhao, Wei Xiong, Kehua Sheng, Bo Zhang, Yang Guan, Shengbo Eben Li
时间：2026-07-13 更新（v2；初版 2026-06-19）
要解决的问题：闭环自动驾驶强化学习很吃仿真采样效率；传统并行采样虽然并行，但会被某个环境提前结束拖住，导致整批重置、样本利用率低、重启延迟高。
核心创新点：提出 FAST，同步并行但不再被单个 episode 的早停绑死；重点是把“采样对齐”和“训练无偏性”一起处理，而不是只做工程加速。
方法机制：一是 DPSA（Dynamic Parallel Sampling Alignment），对提前终止的轨迹做虚拟延展，保持向量化采样同步；二是按并行 clip 的终止率动态触发全局截断，减少无谓重置；三是用 SMPO（Scaled Mask-Padding Optimization）对 padding 数据做有效性 mask 与自适应归一化，避免训练偏差。
实验与结果：摘要给出的关键结果是，相比单 clip 基线，FAST 至少带来 1.78 倍 wall-clock 加速，同时保持统计无偏；这说明它不是单纯“更快但更偏”的折中。
为什么值得关注：自动驾驶 RL 近年瓶颈常常不是算法本身，而是闭环训练吞吐；这篇工作直接瞄准训练系统层，若可复现，会对 CARLA/MetaDrive 一类闭环训练栈很实用。
可能局限/后续跟进：当前摘要强调的是采样框架与理论一致性，尚未说明在更复杂 reward、稀有事故场景或大规模分布式集群上的稳定性；后续值得跟进其是否能和世界模型、离线数据回放、分层 RL 结合。

2. Event-RGB Adaptive Tracking for Nighttime Highway Perception
链接：http://arxiv.org/abs/2607.11646
作者：Haidong Wang, Hengxing Cai, Wanlei Li, Xiaogang Xiong, Renxin Zhong
时间：2026-07-13 提交
要解决的问题：夜间高速场景里，RGB 相机受弱光、模糊、曝光不足和高速运动影响很大，纯视觉跟踪在真正的公路环境中容易失效。
核心创新点：提出 JEAT（Joint Event-RGB Adaptive Tracking），不是硬编码地“某种光照下只信某个传感器”，而是在统一的数据关联优化里动态调 RGB 与事件流权重。
方法机制：JEAT 将异步 event stream 与同步 RGB frame 融到一个联合关联问题中；通过 Adaptive Extended Kalman Filter 用 NIS 统计持续估计观测噪声，再按噪声变化自适应分配两种模态的置信度。暗光和高速时更依赖事件相机，明亮或静态时更多利用 RGB。
实验与结果：作者同时构建了 SEHN 数据集，基于 CARLA 生成白天、夜间、无人工照明夜间等多条件同步 RGB+Event 高速场景，为这类研究补上了基准缺口。摘要未给具体百分点，但明确宣称该框架面向多环境条件下的稳健融合跟踪。
为什么值得关注：自动驾驶感知正在重新重视“非常规但高鲁棒”的传感器组合，尤其夜间和极端天气是量产系统短板；事件相机如果在高速跟踪里站稳脚跟，会对车路协同和路侧 ITS 先落地。
可能局限/后续跟进：目前数据集是合成的，sim-to-real 迁移会是首要问题；其次事件相机的硬件成本、标定和量产部署链路仍是现实门槛。后续值得看是否有真实高速夜景数据和端到端检测跟踪联合优化结果。

3. RealityBridge: Bridging Editable 3D Gaussian Splatting Driving Simulations and Real-World Videos
链接：http://arxiv.org/abs/2606.16278
作者：Zhenhua Wu, Yun Pang, Mingkun Chang, Yuwei Ning, Liangzhi Wang, Yi Xiao, Guanbin Li
时间：2026-07-13 更新（v2；初版 2026-06-15）
要解决的问题：长尾危险场景很难大量采集，但可编辑 3DGS 驾驶仿真视频又常有渲染伪影、前景资产退化、光照不一致和时间闪烁，导致仿真到真实视频的鸿沟很大。
核心创新点：把“3DGS 编辑视频修复”单独当成一个结构保持、资产感知的 Sim-to-Real 问题来建模，而不是直接套通用视频生成或图像增强。
方法机制：RealityBridge 用渲染视频、前景 mask、边缘图、语义 mask 等多模态控制信号，并设计轻量 GateNet 在主干不同层自适应分配条件信息；同时构建针对性训练数据，再配合自回归长视频训练和 reward-guided 后训练，提升长序列一致性并抑制 hallucination。
实验与结果：摘要称其在内部与公开驾驶数据集上，均优于现有方法，优势集中在伪影去除、光照协调和长序列时间一致性三方面。
为什么值得关注：自动驾驶数据生成正在从“纯仿真”转向“真实场景重建+可控编辑”；如果 RealityBridge 这类方法成熟，长尾 corner case 的数据生产成本会显著下降。
可能局限/后续跟进：摘要没有给出对下游检测/规划收益的量化结果，因此目前更像“数据引擎层创新”；后续要看它是否真正提高 closed-loop 评测或安全验证，而不只是视觉上更真。

【机器人 / 具身智能】
4. Mixture of Frames Policy: Multi-Frame Action Denoising for Bimanual Mobile Manipulation
链接：http://arxiv.org/abs/2607.11884
作者：Dian Wang, Jisang Park, Xiaomeng Xu, Han Zhang, Shuran Song, Jeannette Bohg
时间：2026-07-13 提交
要解决的问题：双臂移动操作天然是多坐标系问题，末端局部操作、基座搬运、直立物体保持等适合不同参考系；但现有 diffusion visuomotor policy 通常预先固定一个 action frame，逼同一个 denoiser 去拟合本不该混在一起的动作分布。
核心创新点：提出 MoF（Mixture of Frames Policy），在多个坐标系上同步做动作去噪，不再假设“一个参考系打天下”；这比传统 MoE 更贴近机器人任务本质。
方法机制：MoF 保持一个 canonical diffusion state，把它重表达为多个任务相关坐标系，在每个 frame 上用专门 denoiser 预测噪声，再把噪声预测融合回 canonical frame。为支持中间噪声状态下的可微 frame 变换，作者引入列式 6D rotation 表示配合 SE(3) action 参数化，不要求噪声旋转始终落在 SO(3) 流形上。
实验与结果：在 9 个仿真双臂操作任务中，作者发现“最佳动作参考系”高度任务相关，而 MoF 优于 oracle 单 frame 选择与标准 MoE；在 2 个真实双臂移动操作任务里也超过所有单 frame 基线。
为什么值得关注：这篇论文的价值不只在双臂 manipulation，而是在提醒具身策略学习一个常被忽略的问题：动作表征本身就是归纳偏置。多参考系去噪如果成立，可能扩展到足式机器人、空地协同和接触丰富任务。
可能局限/后续跟进：摘要未说明多 frame 数量增加后的计算成本与训练稳定性；此外多 frame 选择是否需要人工任务先验、能否自动学习，都是后续关键。

5. Freeform Preference Learning for Robotic Manipulation
链接：http://arxiv.org/abs/2606.32027
作者：Marcel Torne, Anubha Mahajan, Abhijnya Bhat, Chelsea Finn
时间：2026-07-13 更新（v2；初版 2026-06-30）
要解决的问题：长时程操作任务里，手写 reward 很难，稀疏成功标签信号又太弱；传统二元 preference 只问“哪个更好”，把速度、安全、摆放质量、谨慎程度等不同标准压成一个模糊标签。
核心创新点：提出 FPL（Freeform Preference Learning），让人类直接用自然语言定义偏好轴，再沿每个偏好轴给出成对偏好，而不是只做单一总排序。
方法机制：先学习一个语言条件奖励模型，把“轨迹 + 偏好标签”映射到某一偏好维度上的 reward；再训练 reward-conditioned policy，使策略在多维人类意图之间可控切换。重要的是，它能学到密集进度信号，而不需要人工子任务切分。
实验与结果：在 4 个真实世界和 2 个仿真长时程操作任务中，FPL 相比稀疏 reward 和二元 preference 方法提升 38 个百分点；并展示了组合式行为能力，以及测试时无需重训即可切换行为风格。
为什么值得关注：机器人对齐问题正在从“单一成功率最优”转向“多维偏好可控”，这和 agent/LLM 对齐趋势一致；对真实机器人来说，这比再堆一个 reward engineer 更可扩展。
可能局限/后续跟进：自由文本偏好会带来标注一致性与语义歧义问题，跨标注者泛化也值得关注；后续可跟进其在更复杂家庭任务和更大语言模型奖励器上的表现。

6. InCoM: Intent-Driven Perception and Structured Coordination for Mobile Manipulation
链接：http://arxiv.org/abs/2602.23024
作者：Jiahao Liu, Cui Wenbo, Zhongpu Xia, Yongliang Wang, Haoran Li, Dongbin Zhao
时间：2026-07-13 更新（v5；初版 2026-02-26）
要解决的问题：移动操作里，底盘与机械臂控制强耦合，同时视角持续变化，导致感知注意分配和动作优化都很难稳定。
核心创新点：提出 InCoM，把“潜在运动意图”引入感知和控制两侧，让 perception 不再静态看图，而是跟随任务阶段和动作目的动态分配注意力；控制侧则显式建模 base-arm 协同，而不是把所有自由度扔给一个统一 decoder。
方法机制：感知侧通过 intent-driven feature reweighting 动态重标多尺度特征，并加入 geometric-semantic structured alignment 做跨模态对应；控制侧设计 decoupled coordinated flow matching action decoder，显式生成协同的 base-arm 动作。
实验与结果：在 3 个 ManiSkill-HAB 场景中，相比 SOTA 成功率分别提升 28.2%、26.1%、23.6%，且不依赖 privileged information；真实世界移动操作实验也保持领先。
为什么值得关注：移动操作目前从“能抓”转向“能边走边看边抓”，这要求 perception-action 更紧耦合但又要可训练。InCoM 给出的路线是“结构化解耦”，不是简单做更大的 end-to-end 模型。
可能局限/后续跟进：摘要没有交代实时性、算力开销和跨机器人泛化幅度；真实部署时，意图估计误差是否会误导注意力分配，也是需要验证的点。

【交叉方向：导航 / 具身 / 自动驾驶仿真】
7. DA-Nav: Direction-Aware City-Scale Vision-Language Navigation
链接：http://arxiv.org/abs/2607.11638
作者：Ye Yuan, Kehan Chen, Xinqiang Yu, Wentao Xu, Heng Wang, Libo Huang, Chuanguang Yang, Yan Huang, Jiawei He, Zhulin An
时间：2026-07-13 提交
要解决的问题：城市级户外导航长期依赖稠密地图或昂贵导航监督，难扩展到真实开放环境；而商用导航工具给的是“向东走 100 米后左转”这类方向指令，不直接对应机器人可执行动作。
核心创新点：DA-Nav 把商用导航里的方向指令利用起来，并把导航重写成自我视角 2D 图像平面上的离散空间指向问题；同时把“偏航恢复”作为核心能力显式建模，而不是只管理想轨迹。
方法机制：框架包含 direction-aware spatial grounding 和 CoT recovery reasoning。恢复过程分成偏差评估、动作预测、目标网格选择三步；作者还构建 ReDA 数据集，补上方向感知指令和恢复轨迹数据。
实验与结果：在 CARLA 未见城市环境中，DA-Nav 成功率达到 56.16%，超过现有 SOTA，且恢复能力更强；更重要的是，在不微调的情况下还能迁移到四足与 humanoid，实现公里级真实闭环户外导航。
为什么值得关注：这篇工作把自动驾驶仿真、VLN、具身导航和现实导航产品连接起来，强调“廉价监督 + 恢复能力”而不是只追求静态 benchmark；这条线很可能比纯地图依赖路线更有部署价值。
可能局限/后续跟进：摘要未给出在复杂行人互动、恶劣天气和 GPS/视觉漂移下的鲁棒性细节；另外“CoT 恢复”在真实系统里的时延和可解释性是否稳定，也值得继续观察。

【趋势总结】
1. 最近一批论文的共同点，是从“单点模型性能”转向“系统瓶颈拆解”：FAST 解采样吞吐，RealityBridge 解仿真到真实数据链路，JEAT 解夜间多模态融合，说明社区在补自动驾驶工程化短板。
2. 机器人侧明显在从“单一成功率优化”走向“结构化表征 + 人类偏好对齐”：MoF 重新设计动作参考系，FPL 让人类用自然语言定义多维偏好，InCoM 则把意图驱动引入感知-控制协同。
3. 导航方向比以往更强调恢复能力和弱监督。DA-Nav 不是继续堆更重的地图或更多专家标注，而是直接利用商用导航指令并显式学习偏航恢复，这比传统 VLN 更贴近真实部署。
4. 与过去“更大 backbone / 更多数据”路线相比，这一批工作的新增量在于：把 action frame、偏好轴、恢复轨迹、仿真视频修复、采样同步等过去常被视作工程细节的因素，提升为一等研究对象。
