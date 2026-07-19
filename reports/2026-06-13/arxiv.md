arXiv 自动驾驶与机器人晨报｜2026-06-13

说明：截至北京时间 2026-06-13 06:02，arXiv `cs.RO` recent 最新可见批次为 Fri, 12 Jun 2026，`cs.CV/cs.AI` 近两日也出现多篇具身与世界模型相关论文。自动驾驶当天直接强相关新条目偏少，因此本文在明确标注日期的前提下，补充覆盖 2026-06-07 至 2026-06-11 的高相关论文。

【自动驾驶】
1. LUNA-AD: Lightweight Uncertainty-Aware Language Model with Lifelong Learning for Autonomous Driving
链接：https://arxiv.org/abs/2606.08470
作者：Ruoyu Yao, Pei Liu, Ruiguo Zhong, Mingxing Peng, Rui Yang, Jun Ma
机构：arXiv 摘要页未列出
提交时间：2026-06-07
要解决的问题：把 LLM 用进自动驾驶时，常见瓶颈不是“会不会解释”，而是三件更硬的事：候选决策缺少不确定性表达、推理成本太高、模型上线后难以根据闭环反馈持续更新。
核心创新点：提出 tri-system 架构，把“重推理”和“轻部署”拆开。前端用 multi-agent analytical system 做多假设探索，生成带不确定性的驾驶决策示范；中间蒸馏成 dual-head 轻量启发式模型，同时输出决策分布和文字解释；后端再接入 reflection-driven lifelong learning，让系统根据执行反馈继续修正候选行为和理由。
方法机制：本质是“重 teacher 负责多样化推理，轻 student 负责上车部署，反思模块负责闭环更新”。相比单次推理式的 AD-LLM 方案，它把 uncertainty、explanation、online refinement 放进同一个训练和部署框架里。
实验与结果：在 nuPlan benchmark 的 non-reactive 与 reactive 两种模式上评测。摘要明确给出：success rate 达到同类 knowledge-driven AD 框架的 SOTA，同时 inference latency 相比已有方法显著下降。
为什么值得关注：它不是把语言模型当“副驾驶嘴替”，而是在认真处理安全关键系统的可部署性问题，尤其是决策分布、不确定性和闭环学习三者的统一。
可能局限或后续点：摘要没有披露不同场景类型的细粒度收益，也还看不到 corner case 失败分析；后续值得跟踪它在真实车端算力预算、数据回流和长期稳定性上的表现。

2. AutoMine Solution for AV2 2026 Scenario Mining Challenge
链接：https://arxiv.org/abs/2606.11874
作者：Songliang Cao, Jiele Zhao, Yuru Wang, Hao Li, Daqi Liu, Zehan Zhang, Fangzhen Li, Yu Wang, Yue Zhang, Bing Wang, Guang Chen, Hao Lu, Hangjun Ye
机构：arXiv 摘要页未列出
提交时间：2026-06-10
要解决的问题：自动驾驶迭代越来越依赖从海量日志里挖出“高价值、规划相关、安全关键”的真实场景，但纯规则方法易脆、纯 LLM 标注又容易对 prompt 和感知噪声过敏。
核心创新点：提出 AutoMine，自我修正的 scenario mining 框架。它一边用 semantics-preserving prompt augmentation 降低 prompt sensitivity，一边把 robust trajectory atomic functions 与 VLM-based functions 组合起来，同时通过真实日志的 execution feedback 反复修正生成代码。
方法机制：这不是直接让模型打标签，而是让模型生成可执行的 mining 逻辑。轨迹原子函数负责几何/运动约束，VLM 负责开放世界视觉信号，代码跑在真实日志上失败后再回流修补，从而形成 self-refining loop。
实验与结果：论文基于 Argoverse 2 Scenario Mining Competition at CVPR 2026。摘要给出的关键指标是 HOTA-Temporal 36.38、Timestamp BA 77.21，说明不仅能找到场景，还兼顾时序边界质量。
为什么值得关注：这类工作直接贴近 AD 数据引擎，而不是只做感知或规划模型本身。当前很多团队真正缺的是“高价值样本如何自动回流”，这篇给出了大模型与可执行规则协作的实用路线。
可能局限或后续点：现阶段更像强工程导向方案，摘要里对跨城市、跨日志 schema、跨传感器泛化的讨论还不够；后续值得看它是否能沉淀成通用场景 DSL 或安全回归流水线。

【机器人 / 具身智能】
3. Embodied-R1.5: Evolving Physical Intelligence via Embodied Foundation Models
链接：https://arxiv.org/abs/2606.11324
作者：Yifu Yuan, Yaoting Huang, Xianze Yao, Yutong Li, Shuoheng Zhang, Linqi Han, Pengyi Li, Jiangeng Sun, Wenting Jia, Zhao Zhang, Yuhao Liu, Ruihao Liao, Yucheng Hu, Qiyu Wu, Yuxiao Li, Zibin Dong, Fei Ni, Yan Zheng, Shuyang Gu, Yi Ma, Hongyao Tang, Han Hu, Jianye Hao
机构：arXiv 摘要页未列出
提交时间：2026-06-09
要解决的问题：很多 embodied 系统把 cognition、planning、grounding、correction 分散到多个模块，导致长任务执行链条长、误差积累大、迁移到真实机器人仍需要大量额外工程。
核心创新点：提出统一的 Embodied Foundation Model，把 embodied cognition、task planning、correction、pointing 放进单一架构；同时构建 3 条自动化数据流水线，形成 15B+ tokens 的具身数据体系，并设计 multi-task balanced RL recipe 处理异构任务冲突。
方法机制：最关键的是 Planner-Grounder-Corrector, PGC 闭环。也就是模型先规划，再完成空间 grounding，再依据执行状态自纠错，由一个模型内部完成长时程任务闭环，而不是依赖多个外部代理拼接。
实验与结果：摘要给出 8B 模型就在 24 个 embodied VLM benchmark 里拿下 16 个 SOTA，超过 Gemini-Robotics-ER-1.5 和 GPT-5.4；微调成 VLA 后，又在 4 套 manipulation benchmark 上超过 `π_0.5`；还做了大量 zero-shot real-robot 实验，覆盖 instruction following、affordance grounding、articulated object manipulation 和 long-horizon tasks。
为什么值得关注：信号非常强，社区焦点正在从“更强 VLA policy”转向“更完整的 embodied foundation model”。这篇尤其强调 reasoning、grounding、自纠错和下游控制的一体化。
可能局限或后续点：摘要没有展开 24 个 benchmark 上的短板，也没说明 15B token 里真实数据与合成数据的比例、噪声控制和去偏方式；这些会决定其可复现性与真实泛化上限。

4. NavWAM: A Navigation World Action Model for Goal-Conditioned Visual Navigation
链接：https://arxiv.org/abs/2606.13494
作者：Daichi Azuma, Taiki Miyanishi, Koya Sakamoto, Shuhei Kurita, Yaonan Zhu, Petr Khrapchenkov, Motoaki Kawanabe, Yusuke Iwasawa, Yutaka Matsuo
机构：arXiv 摘要页未列出
提交时间：2026-06-11
要解决的问题：视觉导航在部分可观测条件下需要既“想象未来视角”，又把这种 foresight 直接转成闭环动作。传统导航 world model 往往只能预测未来，仍依赖外部 planner 把预测结果变成控制。
核心创新点：提出 Navigation World Action Model，把 future observations、goal-progress values、action chunks 放进共享 latent sequence 中联合建模，用 diffusion-transformer policy 直接把“预测未来”变成“输出动作”。
方法机制：它不是先 world model、再 planner、再 policy 的串联结构，而是 jointly learn future prediction、action target 和 value target，让视觉前瞻能力直接进入 policy。这样就能在没有 CEM 式动作搜索的默认 policy 模式下完成闭环导航。
实验与结果：论文采用 simulation pretraining 加 real-robot adaptation，在 offline benchmark 和闭环真实机器人部署中，对比 planning-based world model 和 direct navigation policy。摘要指出，在作者评测设置下，NavWAM 整体优于基于规划的 world-model baseline。
为什么值得关注：这篇代表“world model 从外部规划器组件，转成 policy 内部表示”的趋势。对移动机器人和 embodied navigation 来说，这比单纯提升预测质量更关键。
可能局限或后续点：摘要没有给出具体百分比增益，也没有展开不同环境复杂度、长走廊/遮挡/回环场景下的表现；后续应重点看其真实机器人稳定性与 latency。

5. Mana: Dexterous Manipulation of Articulated Tools
链接：https://arxiv.org/abs/2606.13677
作者：Zhao-Heng Yin, Guanya Shi, Pieter Abbeel, C. Karen Liu
机构：arXiv 摘要页未列出
提交时间：2026-06-11
要解决的问题：灵巧手操作关节工具时，机器人既要处理工具自身自由度，又要处理接触丰富的 in-hand manipulation。过去大量工作聚焦刚体物体，articulated tools 长期是难点。
核心创新点：提出 Mana，把灵巧操作重新解释为“动画生成”问题。系统采用 coarse-to-fine pipeline，把程序化生成的 grasp keyframes 转成真实可执行的 manipulation trajectories，再结合 motion planning 与 reinforcement learning 完成策略落地。
方法机制：最有意思的是数据生成侧。作者只需少量人工点击就可指定 functional affordances，单个工具标注时间低于 1 分钟；随后系统自动完成 keyframe 到轨迹再到策略的转换，明显降低了新工具接入成本。
实验与结果：在 4 类 articulated tools 上评测，覆盖不同尺度和关节类型；摘要给出的亮点是 grasping 与 in-hand manipulation 都实现了 zero-shot sim-to-real transfer。
为什么值得关注：这篇把“数据怎么来、工具怎么扩展、sim2real 怎么稳”连在一起看，不只是做一个新 policy。对于家务机器人、工业工装、辅助机器人都很有启发。
可能局限或后续点：目前展示工具数仍有限，复杂双接触或高柔顺工具是否还能保持同样效果有待观察；另外 affordance 点击虽少，但仍是人工介入点。

6. WEAVER, Better, Faster, Longer: An Effective World Model for Robotic Manipulation
链接：https://arxiv.org/abs/2606.13672
作者：Arnav Kumar Jain, Yilin Wu, Jesse Farebrother, Gokul Swamy, Andrea Bajcsy
机构：arXiv 摘要页未列出
提交时间：2026-06-11
要解决的问题：机器人 world model 过去常在三件事里只能占两件：要么拟真但慢，要么快但长时程不一致，要么能 rollout 但和真实执行成功率相关性不够高，导致难以服务 policy evaluation、policy improvement、test-time planning。
核心创新点：提出 WEAVER，多视角 world model，通过 flow-matching loss 预测 future latents 和 reward values，明确围绕 fidelity、consistency、efficiency 三个目标同时设计架构、memory 与 prediction objective。
方法机制：它不是单纯生成未来视频，而是面向下游机器人决策去学“对评估、提升、规划真正有用的模拟器”。多视角建模加 reward-aware prediction，使 world model 更像可执行的 task model。
实验与结果：摘要给出几个非常硬的数字：在硬件上做 policy evaluation 时，与真实成功率的相关系数达到 `ρ=0.870`；在 `π_0.5` 基础上做 policy improvement，真实世界成功率提升 38%；做 test-time planning 时，成功率提升 14%，同时比已有 world model 快 5-10 倍；对 OOD 场景也优于已有方法。
为什么值得关注：这篇是目前“world model 真正开始服务机器人训练闭环”的代表作之一，尤其把速度和长时程一致性一起拉上来，离在线迭代更近一步。
可能局限或后续点：摘要没有展开多视角输入带来的传感器成本，也没有说明在特别长任务上的误差传播边界；后续需要看更细致的失效模式和算力开销。

【交叉方向】
7. VISA: VLM-Guided Instance Semantic Auditing for 3D Occupancy World Models
链接：https://arxiv.org/abs/2606.13460
作者：Ruiqi Xian, Yuehan Xian, Jing Liang, Xuewei Qi, Dinesh Manocha
机构：arXiv 摘要页未列出
提交时间：2026-06-11
要解决的问题：语义 3D occupancy world model 已同时服务自动驾驶与机器人决策，但对象级和 rare class 的语义错误会直接影响 free-space interpretation、collision checking 和 temporal propagation。问题在于，VLM 对齐文本空间相似度不代表 occupancy mIoU 真会提升。
核心创新点：作者不再把 VLM 当通用 caption embedding teacher，而是把它定位为“训练时的 reliability-aware semantic auditor”。VISA 会对每个物体实例取代表 crop，用离线 VLM 生成结构化审计，包括类别假设、可能混淆、可靠度、属性与证据，再把这些信息沿对象轨迹传播并蒸馏回 occupancy 模型。
方法机制：训练损失由 reliability-weighted taxonomy、attribute-factor、scene-level audit graph 等部分组成；推理时不需要额外 VLM，因此不会增加在线部署成本。
实验与结果：在 nuScenes 上，VISA 让 OccWorld 的 mIoU 从 19.06 提升到 20.05，GaussianWorld 从 21.36 提升到 21.91；在 GaussianWorld 上，object mIoU 从 18.18 提升到 19.16，rare-class mIoU 从 15.60 提升到 16.79。
为什么值得关注：这篇很有方法论价值。它说明 VLM 未必应该直接替代闭集 3D 语义学习，而更适合作为“高语义但低频调用”的审核器，这对自动驾驶和机器人世界模型都成立。
可能局限或后续点：当前收益主要体现在训练时辅助监督，是否能扩展到在线数据清洗、主动学习和持续更新还不明确；另外 VLM 审计本身的偏差如何传导，也值得跟踪。

【趋势总结】
1. 这批论文最明显的变化，是“大模型/世界模型不再只是展示推理能力”，而是更强调如何进入可部署闭环。LUNA-AD、NavWAM、WEAVER 都在解决从 prediction/reasoning 到 executable control 的最后一公里。
2. 自动驾驶方向的热点正在从单模块性能比较，转向数据引擎与系统可靠性。AutoMine 这种日志挖掘工作说明，评测样本生产和安全回流正在成为核心基础设施。
3. 机器人方向进一步走向统一化。Embodied-R1.5 把 cognition、planning、grounding、correction 融合；Mana 和 WEAVER 则分别从数据生成与世界模型两个角度降低真实部署门槛。
4. VLM 与 world model 的角色也在变化。VISA 把 VLM 用作语义审计器，World/Action model 则越来越像 policy 的结构化先验，而不是孤立的生成器或外挂规划器。
5. 和更早一批路线相比，新意不在“模型再大一点”，而在“模块耦合更合理、反馈闭环更清晰、部署成本更受控、评测信号更接近真实任务”。
