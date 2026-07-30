# arXiv 自动驾驶与机器人晨报｜2026-07-31

说明：截至北京时间 2026-07-31 06:00，arXiv API 可核验的最新相关批次为 2026-07-29（UTC）。本期 8 篇均来自该新批次；机构信息未在摘要页披露时不作推断，实验数字以摘要公开结果为准。

## 自动驾驶

### 1. Controlled Experiments on Lane Changing by Transitional Autonomous Vehicle: Dataset and Behavioral Insights
- 链接：https://arxiv.org/abs/2607.27085
- 作者／机构：Abhinav Sharma、Md Abdullah Al Hasan、Danjue Chen、George F. List；机构未在摘要页披露；提交：2026-07-29。
- 问题：自动变道研究常只观察接受间隙的瞬间，缺少可重复公共道路实验来刻画整个强制变道过程中前后间隙与碰撞风险如何演化。
- 创新：发布 NC-tALC 数据集，以受控实车实验完整记录过渡型自动驾驶车辆的强制变道，并把车道线跨越前后风险连续化分析。
- 机制／结构：4 辆仪器化车辆在北卡罗来纳州 Apex 公共道路构造重复交通条件，共完成 78 次试验；用 RTK-GNSS/INS 轨迹提取关键时刻、前车／后车间隙及基于时距和速度的替代安全指标。
- 实验与关键结果：不同初始条件下，前后间隙在跨线附近收敛到较窄区间；风险随变道推进而上升，在物理进入目标车道附近达到峰值，且主要来自目标车道前车；变道完成不等于风险消失。
- 关注价值：为变道模型校准、仿真验证和安全评估提供了少见的可控公路实证基准，也提醒评价不能止于是否成功并线。
- 局限／跟进：仅 78 次、单一区域和强制变道设置；需扩展天气、交通密度、车辆控制栈和自然驾驶员反应，并检验代理风险指标与真实险情的一致性。

### 2. Risk-Aware Motion Planning with Learned Trajectory Primitives and Probabilistic Safety Assessment
- 链接：https://arxiv.org/abs/2607.26802
- 作者／机构：Marc Kaufeld、Dian Zhuang、Johannes Betz；机构未在摘要页披露；提交：2026-07-29。
- 问题：城市驾驶规划既要搜索足够丰富的轨迹，又要控制优化复杂度，并对动态障碍的不确定碰撞风险作可解释约束。
- 创新：用学习得到的 jerk 最小轨迹原语缩小 MPC 搜索空间，再以解析碰撞概率筛选候选并做优化细化，把学习效率与显式安全评价结合。
- 机制／结构：RBFN 生成动力学一致的候选轨迹；概率风险度量负责选择原语，优化器随后在约束下细化最终轨迹。
- 实验与关键结果：在多种城市驾驶场景中，相较基线表现出更好的风险感知和更少的车辆极限违规；摘要未给出统一绝对数值或真车结果。
- 关注价值：比直接端到端输出轨迹更易审计，又避免纯优化器在大搜索空间中的高成本，是学习规划与安全控制的务实组合。
- 局限／跟进：安全性依赖概率模型校准和候选覆盖；需要公开碰撞率、求解延迟、分布外交通参与者行为及闭环实车验证。

## 机器人／具身智能

### 3. TurboVLA: Real-Time Vision-Language-Action Model at 32 Hz on an RTX 4090 with <1 GB VRAM
- 链接：https://arxiv.org/abs/2607.27205
- 作者／机构：Hengyi Xie、Chenfei Yao、Xianjin Wu、Xuanyang Xi、Yiping Tang、Di Xu、Yingying Zhu、Dingkang Liang、Xiang Bai、Han Ding；机构未在摘要页披露；提交：2026-07-29。
- 问题：主流 VLA 把视觉 token 先投影进大语言模型再解码动作，每次策略调用都承担大模型计算与显存开销。
- 创新：把 `V→L→A` 改为直接的 `V+L→A`，不再让 LLM 成为感知与动作之间的中央接口。
- 机制／结构：视觉与语言分别编码，通过轻量双向视觉—语言交互形成任务条件表征，再由紧凑解码器输出连续动作块。
- 实验与关键结果：仅 0.2B 参数，在 RTX 4090 上延迟 31.2 ms、推理显存 0.9 GB，LIBERO 平均成功率 97.7%，达到或超过更大的 VLA。
- 关注价值：表明高成功率操作策略未必需要在每个控制周期运行大语言模型，为消费级 GPU 上 32 Hz 闭环提供了明确设计方向。
- 局限／跟进：结果集中于 LIBERO；语言组合泛化、真机扰动、长时任务和与更强大模型在开放世界中的能力差距仍需验证。

### 4. HumanCLAW: Can Vision-Language Models Act Through a Body?
- 链接：https://arxiv.org/abs/2607.27180
- 作者／机构：Siyao Li、Jiawei Gu、Shuai Liu、Kairui Hu、Zekun Li、Linjie Li、Chengcheng Tang、Po-Chen Wu、Ivan Shugurov、Lingni Ma、Michael Zollhoefer、Sizhe An、Abhay Mittal、Amy Zhao、Ranjay Krishna、Manling Li、Ziwei Liu、Chuan Guo；机构未在摘要页披露；提交：2026-07-29。
- 问题：具身任务失败时，难以区分 VLM 决策错误与底层运动控制失误，导致“模型是否会通过身体行动”无法被干净测量。
- 创新：把高层动作选择与低层执行解耦，让现成 VLM 只逐步选择原子技能，而可靠控制器执行亚秒级全身动作并保留重力、碰撞等物理后果。
- 机制／结构：HumanCLAW-Bench 包含 41 个室内场景、1,218 条第一视角长时“寻找—导航—交互”任务；评测指标集中于模型每一刻选什么动作，而非平衡控制质量。
- 实验与关键结果：9 个先进 VLM 均未解决该基准，最好成功率仅 16.8%；瓶颈不是识别目标，而是模型会遗忘自身位置、是否到达以及是否碰撞。
- 关注价值：把“具身自我感知”从模糊能力拆成可测失效，为改进状态记忆、进度判断和身体边界建模提供了诊断工具。
- 局限／跟进：技能库和可靠控制器会限定可表达动作；结果能否迁移到真实人形、连续动作生成和动态多人环境仍待验证。

### 5. SymmGrid: Super-Scaling On-Robot Learning with Parallelized Symmetries and Egocentric-Exocentric Visual Perception
- 链接：https://arxiv.org/abs/2607.26985
- 作者／机构：Gabe Everett、Brice Gunter、Ryan Vander Stelt、Cleiver Ruiz-Martinez、Blake Hull、Juan Rojas；机构未在摘要页披露；提交：2026-07-29。
- 问题：直接在真机上强化学习受墙钟时间限制，单条昂贵轨迹产生的经验太少。
- 创新：把轨迹级对称变换并行扩展成“对称树／网格”，从一条真实经验生成大量几何一致、动作一致的回放样本。
- 机制／结构：对状态—动作施加允许的不变变换；外视角图像用单应变换与空间动作同步扭曲，兼容第一视角／第三视角视觉和本体感知。
- 实验与关键结果：在真机插销、走线和物体搬移上，训练收敛加速 1.37–2.17 倍，成功率提高 1.09–1.27 倍，最快分别在 16.6、10.9、79.3 分钟收敛；轨迹整体 nAUC 最高提升 2.59 倍。
- 关注价值：无需额外机器人或生成模型，就能提高真机数据利用率，向分钟级接触任务学习迈进。
- 局限／跟进：收益依赖任务存在可用对称性且变换物理有效；非对称场景、遮挡、柔性物体和变换误差可能产生错误经验。

### 6. Practice Makes Policies: Bootstrapping and Consolidating Robotic Capabilities from Zero Human Demonstrations
- 链接：https://arxiv.org/abs/2607.26809
- 作者／机构：Jialiang Li、Yuhan Wang、Haojun Li、Gaojing Zhang、Yangtian Ye、Qipeng Liu、Haotian Liang、Wenzhao Lian；机构未在摘要页披露；提交：2026-07-29。
- 问题：机器人能力通常以静态任务数据训练，难以在物理交互中自己积累经验并把反复出现的行为固化成高效技能。
- 创新：HERO 从零人类示范启动，将启发式推理、案例复用和反射式执行组织成分层、自我改进的能力演化循环。
- 机制／结构：系统自主采集任务经验、跨任务复用行为，并把重复交互逐步巩固为闭环视觉运动策略；调度器按经验积累阶段选择不同能力层。
- 实验与关键结果：多任务实验显示系统显著减少机器人数据采集中的人工干预并保持稳健操作；摘要未披露绝对成功率、任务数和人工时间降幅。
- 关注价值：研究重点从一次性策略训练转向“机器人如何练习并形成技能”，与长期自治和自主数据引擎直接相关。
- 局限／跟进：缺少摘要级量化结果；自主探索的安全边界、错误经验累积、技能遗忘和开放世界任务发现是关键风险。

### 7. Route by Kinematics, Act by Observation: Kinematics-Supervised Expert Routing in MoE-Augmented VLA
- 链接：https://arxiv.org/abs/2607.26807
- 作者／机构：Tianhang Yang、Yanze Zheng、Junjie Wang、Wei-Bin Kou、Ruotong Li、Yujiu Yang；机构未在摘要页披露；提交：2026-07-29。
- 问题：MoE-VLA 的路由器只看观测时难以按动作运动学选择专家，而推理阶段又没有未来动作可直接提供运动学信号。
- 创新：训练期用动作轨迹的运动学聚类 ID 显式监督专家路由，推理期则只从视觉—语言观测预测同一类路由。
- 机制／结构：KinRT 将不同任务归并为运动学原型，以非对称蒸馏把动作空间中的结构迁移到观测空间；同时搭建低于 2,000 美元的 3D 打印 DIYRobot 做跨平台验证。
- 实验与关键结果：相对稠密及其他 MoE VLA，RoboTwin 提升超过 23.26%，DIYRobot 提升超过 20.27%。
- 关注价值：让专家分工围绕“怎么动”而非表面任务语义形成，可能提高 MoE 的可解释性和跨任务复用。
- 局限／跟进：运动学聚类数与质量会限制路由；需检验新本体、新动作原型、专家负载均衡及真实长时操作。

## 交叉方向：SLAM／长期自治

### 8. VidMap: Exploiting Temporal Structure for Video-Based Structure-from-Motion
- 链接：https://arxiv.org/abs/2607.27194
- 作者／机构：Zador Pataki、Paul-Edouard Sarlin、Marc Pollefeys；机构未在摘要页披露；提交：2026-07-29。
- 问题：在线 SLAM 易受初始化和瞬时失败影响且常要求已知标定，离线 SfM 虽能全局优化，却忽略帧序并容易被视觉对称与极端运动干扰。
- 创新：把视频时间顺序作为一等约束，将 SLAM 的序列结构与 SfM 的全局灵活性结合，恢复长时、任意、未标定视频的度量相机轨迹。
- 机制／结构：使用宽基线稠密匹配，以时序约束提高回环可靠性，并用单目度量深度先验增强全局优化和自标定。
- 实验与关键结果：在包含极端运动和视觉对称的多样数据集上，相较经典与学习式 SLAM/SfM、无论标定已知与否都显著更稳健准确；摘要未给出统一数值。
- 关注价值：可把互联网和机器人历史视频转成导航、空间理解所需的度量训练数据，补足实时 SLAM 不适合离线数据生产的场景。
- 局限／跟进：离线计算成本、动态物体、深度先验域偏差、超长视频全局一致性和绝对尺度可靠性需要进一步核查。

## 趋势总结
1. 自动驾驶安全评价从“是否并线／是否碰撞”转向风险全过程与概率校准；学习轨迹原语也更倾向嵌入显式优化和安全度量。
2. VLA 正同时削减计算冗余和改善专家分工：一条路线绕开每周期 LLM，另一条路线用训练期运动学监督建立可解释路由。
3. 真机学习的扩展单位开始从“更多真实轨迹”变为“每条轨迹产生更多有效经验”，对称增强与自主练习都在提高物理交互复用率。
4. 新评测暴露出具身模型的核心短板不是看见目标，而是持续知道身体在哪里、任务进展到哪一步；长期状态记忆将成为下一阶段重点。
5. SLAM 与 SfM 的边界继续融合，视频时序、稠密匹配、全局优化和度量深度被组合成离线空间数据生产管线。
