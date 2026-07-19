arXiv 自动驾驶与机器人晨报｜2026-07-17

说明：本期以 2026-07-16 最新提交/更新为主；自动驾驶高相关条目不足 5 篇，因此补充 2026-07-15 的强相关论文，并在条目中明确日期。以下共选 8 篇，按“自动驾驶”“机器人/具身智能”“交叉方向”整理。作者来自 arXiv 摘要页；“机构”仅在一手信息可直接确认时写出；“局限/后续”属于基于摘要的审慎推断。

【自动驾驶】
1. S-squared-VLA: Decoupling Semantic and Spatial Streams in Vision-Language-Action Models for Autonomous Driving
链接：https://arxiv.org/abs/2607.13926
作者：Jianguo Yu, Rukang Wang, Duanfeng Chu, Chen Wang, Renju Feng, Liping Lu
时间：2026-07-15 提交
问题/痛点：自动驾驶 VLM/VLA 擅长高层语义推理，但把离散语言 token 和连续轨迹控制硬绑在一起后，常出现 spatial representation collapse，模型“能说会看”却丢掉边界感、几何感和精细可控性。
核心创新：把语义流与空间流显式解耦。语义流负责多尺度意图理解，空间流绕开自回归语言瓶颈，直接保留视觉编码器中的未压缩空间特征，再用双流 planning adapter 做融合。
方法/结构：semantic stream 用 hierarchical bridging 提取多尺度 VLM 特征；spatial stream 配合辅助感知监督保留几何先验；末端通过 cascaded attention 把高层驾驶意图和低层空间约束耦合到同一规划头。
实验/结果：NAVSIM 闭环评测上取得 87.1 PDMS、98.4 NC，在纯 SFT 设定下达到该类 VLA 新 SOTA。摘要强调它不是只提问答能力，而是把闭环无碰撞率一起抬高。
为什么值得关注：这代表自动驾驶 VLA 开始从“统一大模型一把梭”转向“把不可压缩的空间结构显式保留下来”，更像工程上可扩展的路线。
局限/后续：摘要未展开双流代价、推理延迟与长尾交通博弈收益；后续值得看其在跨城市、复杂路口和多车交互场景是否仍稳定领先。

2. Ego-Dynamics-Augmented World Model for Autonomous Driving with Zero-Shot Cross-Chassis Adaptation
链接：https://arxiv.org/abs/2607.13410
作者：Zhidong Wang, Jingsong Liang, Zirui Li, Zhan Chen, Han Yu, Chen Lv
时间：2026-07-15 提交
问题/痛点：大量 driving world model 建在 egocentric BEV 上，连续帧里自车运动和场景变化纠缠在一起，世界模型要先“猜出自车怎么动”，再建模环境，导致容量被白白消耗，想象精度和泛化能力都受限。
核心创新：提出 DynaDreamer，把可辨识的 ego dynamics prior 显式注入 Dreamer-style 世界模型，使模型把建模重点从 ego-motion 解缠出来，转向真正的 scene dynamics。
方法/结构：用 physics-informed ego-dynamics encoder-decoder 把自车历史状态压成紧凑上下文，再调制 causal Transformer world model 的 prior/posterior latent；rollout 时用 dynamics predictor 保持该上下文和想象轨迹同步。
实验/结果：相对最强基线，城市与高速场景任务成功率分别提升 28% 和 61%；外推到未见底盘时优势扩大到 73%，说明它不是仅对固定 vehicle dynamics 过拟合。
为什么值得关注：近期自动驾驶 world model 很多，但真正把“车本身能怎么动”拉回中心的不多；这篇把 dynamics-aware world modeling 和跨底盘泛化直接连起来，贴近真实部署问题。
局限/后续：摘要没有展开对动力学参数标定的依赖，也未说明真实车闭环与复杂附着系数变化下的稳定性；后续要重点看从仿真到真实的迁移。

3. Chat2Scenic: An Iterative RAG-Based Framework for Scenario Generation in Autonomous Driving
链接：https://arxiv.org/abs/2607.14387
作者：Yuan Gao, Wenting Miao, Mattia Piccinini, Haoyu Wang, Qunying Song, Johannes Betz
机构：TUM AVS（代码仓与作者页可直接确认）
时间：2026-07-15 提交
问题/痛点：自动驾驶验证需要大量合规、可执行、可编译的测试场景脚本，但把法规文本自动转成 DSL 场景一直很难。检索拼装法可编译率尚可但扩展性差，整段脚本生成又经常无法编译。
核心创新：提出迭代式 RAG 场景生成框架 Chat2Scenic，把法规知识、DSL 语法和交互式 refinement 结合起来，让 LLM 不是“一次写完”，而是持续纠偏。
方法/结构：通过聊天接口支持逐轮 refinement；RAG 负责把法规条款与 DSL 语法检索进上下文；同时作者构建了覆盖 NHTSA、联合国车辆法规等来源的 123 场景 benchmark。
实验/结果：在该 benchmark 上，CSR 达 76.42%，FA 达 58.17%，显著超过 retrieval-assemble（30.08%/11.03%）和 retrieval full-script generation（16.26%/10.86%）。
为什么值得关注：自动驾驶社区近两年更缺的是“可扩展验证内容生成”，不是再多一个 perception 分数；这篇把 scenario generation 从 demo 拉到可比较、可复用的 benchmark 级工作。
局限/后续：摘要未说明面对更复杂多车交互、长时序事故链时的退化幅度；后续值得看它和 corner-case synthesis、closed-loop simulator 的衔接。

【机器人 / 具身智能】
4. RoboTTT: Context Scaling for Robot Policies
链接：https://arxiv.org/abs/2607.15275
作者：Yunfan Jiang, Yevgen Chebotar, Ruijie Zheng, Fengyuan Hu, Yunhao Ge, Jimmy Wu, Tianyuan Dai, Scott Reed, Li Fei-Fei, Yuke Zhu, Linxi "Jim" Fan
时间：2026-07-16 提交
问题/痛点：多数机器人 foundation policy 只看单步或短历史，长程操作时上下文很快丢失，所以一旦任务跨多阶段、需要模仿人类长视频示范或中途纠偏，性能会明显塌陷。
核心创新：提出 Test-Time-Training Robot Policies，把 test-time training 真正并入机器人策略，使上下文长度扩到 8K timesteps，且不显著增加推理延迟。
方法/结构：模型把 recurrent state 放进可在训练和推理期都能梯度更新的 fast weights 中，相当于把超长历史压缩进权重空间；训练配合 sequence action forcing 和 truncated BPTT 扩展长上下文学习能力。
实验/结果：真实机器人操作上，相比单步上下文基线整体提升 87%；能完整做完 5 分钟、10 阶段装配任务，而基线从未完成；8K context 预训练模型比 1K context 版本再提升 62%。
为什么值得关注：这篇把“上下文长度”明确提出为 robot foundation model 的新 scaling axis，不只是堆参数或堆数据，而是让策略真正能在长历史里做 in-context imitation 和在线改进。
局限/后续：摘要尚未给出算力成本、稳定训练区间和不同任务上收益上限；后续要看其在更多平台、多模态感知和更强干扰下是否仍成立。

5. Scaling Behavior Foundation Model for Humanoid Robots
链接：https://arxiv.org/abs/2607.15163
作者：Weishuai Zeng, Kangning Yin, Xiaojie Niu, Shunlin Lu, Weixiang Zhong, Jiahe Chen, Feiyu Jia, Xiao Chen, Zirui Wang, Furui Xu, Ming Zhou, Kailin Li, Weinan Zhang, He Wang, Li Yi, Dahua Lin, Jiangmiao Pang, Jingbo Wang
时间：2026-07-16 提交
问题/痛点：人形机器人控制要求全身协调、实时响应和跨场景泛化，但行为基础模型怎么真正“scale”一直不清楚，尤其是学习范式、行为数据和架构应如何协同。
核心创新：论文重新梳理 humanoid BFM 的 scaling recipe，认为关键不是单点增大，而是三者联动：运动跟踪式学习范式、on-policy rollout 与参考动作多样性的配比、以及可扩展的 Humanoid Transformer。
方法/结构：把多类 humanoid control 统一重写为 global-frame whole-body behavior reproduction；用 Humanoid Transformer 促成结构化行为表征自然涌现；通过 rollout 数量与参考动作多样性协同提升泛化。
实验/结果：仿真与真实部署中，测试集 MPKPE 相比现有 controller 在 local mode 降低 10% 以上、在 global mode 降低 82%，说明不仅姿态复现更准，跨任务泛化也更强。
为什么值得关注：人形机器人现在最稀缺的是稳定、可扩展的底座控制范式；这篇在“如何 scale”上给出相对系统的 recipe，可能比单个新任务 demo 更重要。
局限/后续：摘要未交代训练数据规模、真实硬件成本与安全恢复机制；后续值得跟踪其在接触丰富任务和真实长期运行中的鲁棒性。

6. Learning Agile Navigation in Crowded Environments for Quadruped Robots
链接：https://arxiv.org/abs/2607.15036
作者：Shuyu Wu, Zeyu Liu, Tianbao Zhang, Fanxing Li, Fangyu Sun, Mingkang Xiong, Wei Xi, Wenxian Yu, Danping Zou
时间：2026-07-16 提交
问题/痛点：四足机器人在拥挤动态环境里容易受遮挡与人群随机运动影响。纯模型法依赖准确运动估计，密集人群里常失真；纯端到端法虽更鲁棒，但缺少对动态障碍运动约束的显式刻画。
核心创新：提出 VOP-Nav，把 Velocity Obstacle 的几何安全先验与端到端学习的适应性结合起来，且只依赖机载局部观测，不走显式检测/跟踪流水线。
方法/结构：VOP-Net 直接处理多帧 LiDAR，隐式编码动态约束并预测源于 VO 理论的 safe velocity region；这些 VO 预测既作为推理输入，也作为训练奖励，形成“安全约束 + 学习策略”的双重作用。
实验/结果：在 Isaac Gym 中，VOP-Nav 在成功率、速度与避撞平衡上优于全部基线；在 Unitree Go2 实机室内外动态环境部署中也验证了鲁棒性和效率。
为什么值得关注：导航研究一个明显新意是重新把显式安全几何先验接回学习系统，而不是继续在纯黑箱策略里碰运气；这对人机混行环境尤其关键。
局限/后续：摘要未给出极端密度、夜间感知退化或跨传感器配置下的掉点；后续要看其对不同 crowd statistics 的泛化能力。

【交叉方向】
7. DriftWorld: Fast World Modeling through Drifting
链接：https://arxiv.org/abs/2607.15065
作者：Susie Lu, Haonan Chen, Weirui Ye, Yilun Du
时间：2026-07-16 提交
问题/痛点：world model 对规划有吸引力，但 diffusion world model 推一次 rollout 要多步采样，在线动作搜索成本太高，导致“想得准”和“想得快”难以兼得。
核心创新：提出 drifting generative model，训练时学 action-conditioned drift，推理时用单次前向就生成未来帧，把 diffusion 的多步采样瓶颈砍掉。
方法/结构：输入当前观测与候选动作序列，模型直接输出未来帧；因此既能做在线 imagined planning，也能作为离线 simulator 给真实策略打分排序。
实验/结果：在 Bridge-V2、RT-1、Language Table、Push-T、Robomimic 上，平均比 diffusion world model 快 17 倍，推理速度达到 30+ fps，同时取得 SOTA 决策表现；rollout-based policy score 与真实表现相关性最高到 0.99。
为什么值得关注：这篇很可能会影响“世界模型到底能不能进实时控制栈”这个关键问题；如果 imagination 成本显著下降，规划式具身控制会重新变得有吸引力。
局限/后续：摘要未说明长时 rollout 漂移累积、跨域视觉变化和复杂接触任务上的退化情况；后续值得看其与真实机器人在线 MPC/搜索的结合。

8. BadWAM: When World-Action Models Dream Right but Act Wrong
链接：https://arxiv.org/abs/2607.15207
作者：Qi Li, Xingyi Yang, Xinchao Wang
时间：2026-07-16 提交
问题/痛点：WAM 常被认为比纯 policy 更安全，因为动作可以拿想象出来的未来做“自检”；但这个假设到底有多稳，之前缺少专门针对 WAM 的攻击框架。
核心创新：提出 World-Action Drift Attacks，并统一建模两类攻击：偏破坏性的 action-only attack，以及偏隐蔽的 imagination-preserving attack，后者会尽量保持模型“看起来想象正常”，但实际动作已被悄悄带偏。
方法/结构：作者从攻击强度和隐蔽性两个维度刻画攻击面，专门利用小幅视觉扰动去打破 WAM 中“想象未来”和“执行动作”的对齐关系。
实验/结果：闭环执行中，action-only attack 可把任务成功率从 96.5% 打到 43.1%；而 imagination-preserving attack 进一步暴露出 WAM 特有脆弱性，即未来预测看起来还合理，但动作已经和想象脱节。
为什么值得关注：自动驾驶和具身系统近期大量押注 world-action model，这篇提醒大家“可想象 ≠ 可验证 ≠ 可防御”，对安全验证和鲁棒训练都很关键。
局限/后续：摘要没有给出防御手段的有效上限；后续值得跟踪 detection、certification 与 adversarial training 是否能真正修复这种对齐裂缝。

【趋势总结】
1. 这一批论文最明显的共同点，是从“更大的端到端模型”转向“把关键结构显式写进系统”：双流 VLA、ego-dynamics prior、VO 安全先验、drift-based world model 都是这个方向。
2. 自动驾驶的新意主要有三条：一是 VLA 开始认真处理 semantic-physical gap；二是 world model 从“生成未来画面”转向“服务闭环控制与跨底盘泛化”；三是验证内容生成开始 benchmark 化、法规化，而不只是手工编场景。
3. 机器人/具身智能方向则更强调长时上下文、可扩展行为底座和拥挤环境中的安全导航，说明社区关注点正在从单次成功 demo 转向持续执行能力。
4. 交叉方向里，world model 既在被加速（DriftWorld），也在被审计（BadWAM）。这和过去只追求更逼真生成不同，研究重点正在转向“是否能进实时系统”“是否真的可信”。
