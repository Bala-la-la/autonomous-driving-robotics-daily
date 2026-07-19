arXiv 自动驾驶与机器人晨报｜2026-06-14

说明：截至 2026-06-14 早晨，arXiv 当天在本主题下新增量不高；本期优先覆盖最近一批可见的最新高相关论文，主要为 2026-06-11 提交/更新。

一、自动驾驶
1. DrivingAgent: Design and Scheduling Agents for Autonomous Driving Systems
链接：http://arxiv.org/abs/2606.12236
作者/机构：Zhongyu Xia, Wenhao Chen, Yongtao Wang（北京大学王选所），Ming-Hsuan Yang（UC Merced）
时间：v2 更新于 2026-06-11
要解决的问题：自动驾驶系统越来越像“多模块+基础模型”的复杂系统，但设计新模块、做组合、再按实时算力预算动态调度，仍高度依赖人工；而通用 agent 又不理解车端实时性与模块结构。
核心创新：把“系统设计”和“在线调度”明确拆成两个 agent 问题。前者负责理解架构、生成模块代码、用 super-network 方式验证；后者用轻量 LLM + 强化学习做逐帧调度，而不是把 AD pipeline 当黑箱一把梭。
方法机制：设计阶段读取系统架构和模块画像，自动组织训练/评估闭环；调度阶段结合长期记忆和带时间戳的短期上下文，结合 FPS 估计工具与 GRPO 微调，在精度-速度之间做在线取舍。
实验与结果：论文报告在 nuScenes 和 Bench2Drive 上取得更好的 speed-accuracy trade-off；摘要与正文明确指出，GRPO 微调和 FPS calculator 能进一步提升 FPS 稳定性与高帧率条件下的准确率表现。
为什么值得关注：它不是再做一个 planner 或 VLA，而是在讨论“如何把日益膨胀的自动驾驶系统自动搭起来并跑得动”，这更接近工程落地痛点。
局限/后续：当前亮点主要是系统编排与调度层；如果底层模块质量不足，agent 只能做较优组合。后续要看它在更强闭环基线和真实车载算力约束下是否仍成立。

2. VISA: VLM-Guided Instance Semantic Auditing for 3D Occupancy World Models
链接：http://arxiv.org/abs/2606.13460
作者/机构：Ruiqi Xian（UMD）、Yuehan Xian（NUPT）、Jing Liang（Stanford，论文原文如此拼写）、Xuewei Qi（Motional）、Dinesh Manocha（UMD）
时间：提交于 2026-06-11
要解决的问题：3D occupancy/world model 已成为自动驾驶统一空间表征，但长尾类别、遮挡和相似类混淆会直接污染 free space、碰撞检查和后续时序传播。把 VLM/CLIP 当通用 caption embedding 蒸馏目标，往往“文图对齐更好了，闭集 occupancy mIoU 却没明显变好”。
核心创新：把 VLM 从“表征老师”改成“离线语义审计员”。不是逼 occupancy feature 对齐开放词汇 embedding，而是让 VLM 针对每个物理对象实例输出结构化审计：类别假设、可能混淆、可靠度、属性、证据，再蒸馏回 3D voxel logits。
方法机制：对代表性 crop 做离线 VLM 审计；将审计结果沿 object track 传播；再通过 reliability-weighted taxonomy loss、attribute-factor loss 和 scene-level audit graph loss 监督现有 occupancy world model。推理时不需要任何 VLM，部署开销不变。
实验与结果：在 nuScenes 上，VISA 将 OccWorld 从 19.06 提升到 20.05 mIoU，将 GaussianWorld 从 21.36 提升到 21.91 mIoU；在 GaussianWorld 上，object mIoU 从 18.18 提升到 19.16，rare-class mIoU 从 15.60 提升到 16.79。
为什么值得关注：这篇论文很有“路线纠偏”意味。它指出 VLM 对自动驾驶 3D 语义建模最有效的角色未必是开放语义对齐，而可能是带可靠度的闭集审计监督。
局限/后续：依赖离线 crop/track 质量；若实例关联错了，审计信号可能被错误传播。后续可以看它能否扩展到在线更新、占据预测 rollout 和更大规模 world model。

二、机器人/具身智能
3. Mana: Dexterous Manipulation of Articulated Tools
链接：http://arxiv.org/abs/2606.13677
作者/机构：Zhao-Heng Yin（UC Berkeley/Amazon FAR）、Guanya Shi（CMU/Amazon FAR）、Pieter Abbeel（UC Berkeley/Amazon FAR）、C. Karen Liu（Stanford/Amazon FAR）
时间：提交于 2026-06-11
要解决的问题：灵巧手操作“带关节工具”比刚体难得多，因为既要稳定抓持，又要驱动内部自由度并处理强接触。现实里又很难采到足够真机演示。
核心创新：把 articulated tool manipulation 重新表述成“动画生成”问题。先用极低人工成本指定功能 affordance 和 grasp keyframe，再用运动规划 + 强化学习把关键帧补成可执行操作轨迹。
方法机制：Mana 采用 coarse-to-fine pipeline：程序化生成 grasp keyframe，做 collision-aware 手指/接触优化，再用 MP 和 RL 生成中间操作轨迹；最后训练 point-cloud-conditioned transformer diffusion policy，把点云观测映射到腕部与手指动作。每种工具只需少量鼠标点击，单工具 affordance 标注小于 1 分钟。
实验与结果：覆盖钳子、夹子、注射器、食物夹 4 类不同尺度和关节属性工具；论文给出 zero-shot sim-to-real 结果，表 1 显示抓取和 in-hand manipulation 大约都能达到 70% 左右成功率，显著强于基线。
为什么值得关注：它抓住了“工具操作”这个比单物体抓取更接近真实生产/家务任务的空白点，而且数据生成效率很高。
局限/后续：当前主要在 4 类工具上验证；对更复杂多关节工具、可变形材料、完整任务链仍有距离。真实部署中对几何、力学和位姿误差仍较敏感。

4. Improving Robotic Generalist Policies via Flow Reversal Steering
链接：http://arxiv.org/abs/2606.13675
作者/机构：Andy Tang（Stanford）、William Chen（UC Berkeley）、Andrew Wagenmaker（UC Berkeley）、Chelsea Finn（Stanford）、Sergey Levine（UC Berkeley）
时间：提交于 2026-06-11
要解决的问题：机器人 generalist policy 明明学了很多技能先验，但面对新任务时，语言指令或 VLM 提示往往只能给出粗糙语义，不能直接落成高质量低层动作。
核心创新：提出 Flow Reversal Steering，核心不是直接执行“粗动作”，而是把粗动作反推回 flow policy 的 latent noise，再映射到附近更“在分布内”的好动作模态。
方法机制：给一个人类或 VLM 提供的 reasonable but suboptimal action，先通过 flow policy 反向求 noise，再走正向 denoise 得到更精细动作；这个过程还能产出可用于 DSBC/DSRL 的训练信号，从而进一步蒸馏或强化。
实验与结果：在仿真与真实 manipulation 任务上验证；论文报告对困难任务可带来最高 95 个百分点的绝对成功率增益，且少量轨迹、不到 1 分钟训练即可把收益蒸馏进辅助策略；真实 6 个 DROID 任务也有明显提升。
为什么值得关注：这篇论文代表一种新思路：不急着重训大模型，而是学会“调用 generalist 内部已经存在的行为模态”。这对 VLA/flow policy 的 test-time adaptation 很关键。
局限/后续：依赖 coarse action 至少要“方向正确”；如果高层 reasoner 提示本身偏离任务，flow reversal 仍可能把错的意图精修而不是纠正。

5. WEAVER: Better, Faster, Longer: An Effective World Model for Robotic Manipulation
链接：http://arxiv.org/abs/2606.13672
作者/机构：Arnav Kumar Jain（Mila/蒙特利尔大学）、Yilin Wu（CMU）、Jesse Farebrother（Mila/McGill）、Gokul Swamy（CMU）、Andrea Bajcsy（CMU）
时间：提交于 2026-06-11
要解决的问题：机器人 world model 经常三者难兼得：保真度高的推理太慢，快的模型又难以长时一致；结果是评估、规划、策略改进都很难真正落地到机器人上。
核心创新：WEAVER 试图同时满足 fidelity、consistency、efficiency 三个目标，而不是只优化其中一个。论文强调多视角建模、显式记忆和 flow-matching 预测目标的组合设计。
方法机制：这是一个 multi-view world model，预测未来 latent 与 reward value；在架构、memory 和 prediction objective 上做了系统性取舍，使模型既能长时 rollout，又能为下游 evaluation / improvement / planning 直接服务。
实验与结果：真机上，WEAVER 做 policy evaluation 时与真实成功率相关系数达到 0.870；用于 policy improvement 时可在 π0.5 foundation model 基础上带来 38% 的真实成功率提升；用于 test-time planning 时较既有 world model 带来 14% 的真实成功率提升，并实现 5-10x 推理加速，文中还给出最高约 20x 的规划推理速度优势。
为什么值得关注：world model 正从“生成好视频”转向“真能用于控制决策”。WEAVER 的价值在于证明：只要设计得当，world model 可以同时做评估器、数据扩增器和规划器。
局限/后续：目前仍聚焦 manipulation；一旦场景更开放、接触更复杂、观测更稀疏，多视角记忆是否仍足够稳定，还需要更广泛验证。

6. LabVLA: Grounding Vision-Language-Action Models in Scientific Laboratories
链接：http://arxiv.org/abs/2606.13578
作者/机构：浙江大学、上海 AI Lab、哈工大等
时间：提交于 2026-06-11
要解决的问题：现有 VLA 主要在家庭/桌面任务训练，对实验室里的透明液体、固定流程、精密仪器、跨平台机器人操作几乎没有覆盖。
核心创新：同时从“数据”和“统一 embodiment”两侧补齐短板。数据侧构建 RoboGenesis，把实验流程从 atomic skills 组合成仿真工作流；模型侧提出 LabVLA，用视觉语言骨干 + DiT action expert 学实验室操作。
方法机制：两阶段训练。先做 FAST action token pretraining，让 Qwen3-VL-4B-Instruct 先具备动作意识；再用 flow matching post-training 接入动作专家，并用 knowledge insulation 降低动作损失对原 VLM 知识的干扰。RoboGenesis 还能把工作流自动实例化到 10+ 机器人平台，并附带多维 domain randomization。
实验与结果：在 LabUtopia benchmark 上，LabVLA 在 ID 和 OOD 设置下都取得最高平均成功率；文中还指出，仅引入 LabEmbodied-Data 就能把 X-VLA 五任务平均从 49.3% 提升到 64.3%（ID），从 43.7% 提升到 63.0%（OOD）。
为什么值得关注：这是具身智能向“垂直行业场景”推进的典型信号。实验室不是通用桌面任务的简单换皮，对流程性、液体状态、设备约束都提出了新要求。
局限/后续：当前还是 technical report，真实实验室部署、物理误差、耗材变化和安全要求仍比仿真复杂得多。

三、交叉方向
7. NavWAM: A Navigation World Action Model for Goal-Conditioned Visual Navigation
链接：http://arxiv.org/abs/2606.13494
作者/机构：东京大学、NII、AIRoA、ATR
时间：提交于 2026-06-11
要解决的问题：navigation world model 能想象未来视角，但通常还要外接 planner；直接 policy 又缺少显式 foresight。两边各有长处，也各有断层。
核心创新：把“未来观察预测、goal-progress value、action chunk”统一进一个 shared latent sequence，让 world model 直接产出可执行动作，形成 world action model。
方法机制：基于 diffusion-transformer，在当前观测和目标条件下联合去噪未来 egocentric view、进度价值与动作块；推理时直接输出 action chunk 做 receding-horizon 控制，不再依赖 CEM 式测试时搜索。
实验与结果：在长短视界上都优于传统 NWM。文中报告长视界 h=8 时 ATE 从 0.262 降到 0.192（-27%），RPE 从 0.103 降到 0.070（-32%）；真实 Diablo 机器人 24 个闭环 image-goal episode 中，NavWAM 达到 19/24 成功，即 79.2%，高于对比基线。
为什么值得关注：它体现出 navigation 和 manipulation 正在共享“world model 直接出 action”的范式，而不是 world model 只当 planner 的前端预测器。
局限/后续：目前任务设定仍是 image-goal navigation；扩展到更复杂语义目标、动态人群和长期地图记忆后，联合建模的稳定性还需验证。

趋势总结
1. 最新一批论文的共同趋势，是把 foundation model / VLM / world model 从“单一预测器”改造成“可执行系统组件”。DrivingAgent 做系统编排，VISA 做训练时审计，NavWAM/WEAVER 直接把预测能力接进控制闭环。
2. 机器人侧明显在加速从“通用桌面操作”走向更强约束场景：Mana 攻具有关节工具，LabVLA 攻实验室流程。这比过去单纯做 pick-place 或语言跟随更接近真实部署。
3. 一个新意是“尽量不在推理时加重外部开销”。VISA 把 VLM 放到训练时，推理零额外成本；NavWAM 去掉 CEM 搜索；WEAVER 强调比旧 world model 更快。这说明社区越来越在意部署时延而不是只拼离线指标。
4. 与以往路线相比，最近论文更少强调“更大模型本身”，更多强调：如何让现有模型通过结构化监督、shared latent、agent 编排或 latent steering 真正产生可用动作与系统收益。
