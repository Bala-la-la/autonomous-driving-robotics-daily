# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-09

## 日期与证据口径

北京时间 2026-10-09 检索 [arXiv API](https://export.arxiv.org/api/query?search_query=cat%3Acs.RO%20OR%20cat%3Acs.AI%20OR%20cat%3Acs.CV&start=0&max_results=100&sortBy=submittedDate&sortOrder=descending)，最新相关 v1 批次仍为 **2026-10-07 UTC**，尚未出现 10 月 8 日 UTC 的新相关批次。本期从该批次中精选 6 篇**未列入 10 月 8 日报告**的论文，不将其写成 10 月 9 日新稿。均据官方摘要／版本记录；实验数字为作者报告，未复现，“关注价值”和“局限”为编辑判断。

## 自动驾驶与移动／规划

本轮未发现未重复的道路自动驾驶 v1 主线；为避免重复，保留移动机器人规划论文，并继续关注 10 月 8 日 UTC 批次是否发布。

### 1. CMP-IRRT*: A Perception-Assisted Height-Adaptive Planner for Quadruped Robots

- **论文／作者／时间**：[arXiv:2610.10470](https://arxiv.org/abs/2610.10470)；Mingfan Zhao、Wendong Mao、Zhongfeng Wang。v1：2026-10-07 17:33 UTC；论文标注已接收 ACML 2026。
- **问题**：二维导航把障碍一概视为不可通行，忽略四足机器人可跨越的低矮物；有限采样预算下，传统采样规划也可能效率不足。
- **创新与机制**：以俯视 RGB、深度推断生成相对地面的高度图；CMP-IRRT* 用 Channel-Mamba PointNet 引导 Informed RRT* 采样，碰撞检查按高度区分“可跨越”与“必须绕行”，同时保留自由／informed 采样回退。
- **实验与关键结果**：作者报告在构造的可通行性场景中，路径最多缩短 **16.3%**；二维基准中搜索节点与迭代少于经典和神经引导基线，并在 Unitree Go2 展示绕开高障碍、跨越低障碍。
- **关注价值**：把感知高度、身体能力和规划代价连成显式接口；这种“非二元可通行性”也值得迁移到自动驾驶的路缘、坡道与可压越区域建模。
- **局限／跟进**：高度来自单张、校准的俯视观察，真实户外遮挡、深度偏差和动态物体未充分覆盖；需报告感知不确定性传播后的安全裕量。

## 机器人／具身智能

### 2. Rephrase Before You Act: Characterizing and Mitigating Language Sensitivity in Vision-Language-Action Models

- **论文／作者／时间**：[arXiv:2610.10526](https://arxiv.org/abs/2610.10526)；Mikey Watts（Independent Researcher）、Yuchen Cui（UCLA）。v1：2026-10-07 17:57 UTC。
- **问题**：VLA 对同义改写异常敏感，视觉语言骨干的语言鲁棒性并未自然传到动作策略。
- **创新与机制**：先以单词级改写和 oracle 短语搜索量化敏感性，再从少量任务的多种表述中由 LLM 归纳 10–20 条改写规则；部署时仅重写一次指令，不改冻结策略、也不逐步验证。
- **实验与关键结果**：π0.5 在 LIBERO 的 “switch on the stove” 与 “hot plate” 上成功率可从 **100% 到 2%**；规则使冻结 π0 在 12 个留出任务上相对提升 **16–27%**，π0.5 的 in-finetune 成功率从 **93.6% 至 97.8%**。
- **关注价值**：把语言失败转成可测试、可审计的输入预处理问题，适合加入机器人和驾驶语音／文本接口的上线前回归测试。
- **局限／跟进**：规则由特定模型、任务与语言产生；它不验证场景是否理解正确，危险任务仍需动作层安全检查与多语言测试。

### 3. RoboJEPA: Scaling Robotic Latent World Models

- **论文／作者／时间**：[arXiv:2610.10515](https://arxiv.org/abs/2610.10515)；Artem Zholus、Nicolas Beltran-Velez、Jianhao Yuan、Sarath Chandar、Jeannette Bohg、Mahmoud Assran 等。v1：2026-10-07 17:54 UTC。
- **问题**：机器人 latent world model 的模型、数据和算力扩展关系缺少可外推的指标，真机评测昂贵又难以频繁做。
- **创新与机制**：在 12 种机器人本体数据上训练 JEPA 预测器，提出以 latent rollout 的 imagination error 衡量世界模型；拟合二阶算力幂律，并以该误差预测下游规划表现，支持单目标图像条件的零样本规划。
- **实验与关键结果**：作者称 imagination error 可随计算量以二阶幂律拟合，且与下游规划相关；公开 8B 参数模型、checkpoint、训练及部署代码，并报告真机长时任务的零样本展示。
- **关注价值**：将“视频／latent 预测好不好”与可采购的规划代理指标相连，有利于将训练预算、离线验证和真机试验分层决策。
- **局限／跟进**：摘要未给出跨本体、跨任务的完整置信区间和真机对照细节；相关性不等于在新传感器或接触失配下仍能替代真实评测。

### 4. Robotic Boomerang Throwing via Model-Based Release Design

- **论文／作者／时间**：[arXiv:2610.10472](https://arxiv.org/abs/2610.10472)；Yang Liu、Colin Jones、Aude Billard。v1：2026-10-07 17:34 UTC。
- **问题**：带升力的抛掷取决于释放速度、姿态和自旋；机械臂的关节速度又很难复刻人类投掷动作。
- **创新与机制**：围绕“释放状态”分阶段辨识飞行／接触动力学，筛选在接触不确定下仍稳定控制自旋的动作与回旋镖参数，而不是模仿人类关节轨迹。
- **实验与关键结果**：6-DoF 机械臂在成功回飞试验中达到 **51 rad/s（8.1 rev/s）**，最远离基座 **2.03 m**，并落在距基座 **0.31 m** 处；作者称为首个完成回飞的机械臂演示。
- **关注价值**：说明动态操作的可迁移对象可为释放边界条件，而非人类动作外观；对投放、快速接触和飞行物交互均有启发。
- **局限／跟进**：核心证据是单类物体与受控试验；空气流、抓取摩擦和安全隔离的鲁棒范围需量化，不能外推为通用抛掷技能。

### 5. LLA-MPPI: Rapidly Adaptive Whole-body Control of Legged Robots with GPU-Accelerated Parallel Simulations

- **论文／作者／时间**：[arXiv:2610.10465](https://arxiv.org/abs/2610.10465)；Sebin Jung、Maitham F. AL-Sunni、Juan Alvarez-Padilla、Zachary Manchester、Changliu Liu、John M. Dolan。v1：2026-10-07 17:30 UTC。
- **问题**：腿式 MPC 的标称模型在负载变化、部件失效等动力学漂移下退化，逐故障离线训练不现实。
- **创新与机制**：GPU 批量运行物理／结构参数各异的接触仿真器，用近期窗口预测误差选择最能解释当前运动的模型，再以该模型进行全身 MPPI；模型假设可直接检查，无需离线训练。
- **实验与关键结果**：四项仿真任务成功率 **97.5%**，最强基线 **74%**、真实模型 oracle **98.5%**；Go2 演示中途加负载、禁用一条腿行走及逐渐增重推箱。
- **关注价值**：把在线适应化为并行模型选择，便于审计控制器何时认定物理条件改变，也可启发长期自治的故障模式库设计。
- **局限／跟进**：模型库未覆盖的故障无法被选择补救；尚需端到端控制频率、功耗、传感噪声和非结构化地形的系统对比。

## 交叉方向：3D 场景与多 Agent

### 6. Tetris3D: 3D Scene Generation With Objects That Fit Together

- **论文／作者／时间**：[arXiv:2610.10539](https://arxiv.org/abs/2610.10539)；Jaeyeong Kim、Jinhyuk Jang、Jongmin Lee、Kyehong Park、Seungryong Kim（项目页署名 KAIST CVLab）。v1：2026-10-07 17:59 UTC。
- **问题**：单图 3D 重建常将物体独立生成，遮挡的接触区域易出现互相穿插或无法稳定摆放的几何。
- **创新与机制**：逐物体生成时显式条件化周围物体几何与物理关系；同时构建含网格和成对物理关系标注的 ComOb 仿真数据集，包含 **120 万** 场景。
- **实验与关键结果**：作者报告在合成和真实场景中，即使交互区域遮挡，仍能提高生成质量与物理稳定性，达到所比较设置的 SOTA。
- **关注价值**：为操作仿真、数字孪生和长期 3D 资产补上“对象是否能共同存在”的可执行约束，而不仅是单物体形状指标。
- **局限／跟进**：摘要未给出真实机器人接触任务的闭环收益；物理模拟数据的材质、接触参数及真实长尾布局会决定迁移上限。

## 趋势总结

- **输入、模型和动作的接口都在成为可测变量**：语言改写、latent imagination error、地形高度与释放状态分别把过去隐含的失败来源显式化。
- **世界模型扩展需要代理指标，但不能跳过真机**：RoboJEPA 的幂律与 LLA-MPPI 的模型选择都提升了预算可见性；覆盖不足和分布外动力学仍必须由硬件验证发现。
- **三维资产开始接受物理可用性检验**：Tetris3D 的关系条件和 CMP-IRRT* 的高度可通行性共同表明，地图／重建不应只按视觉质量交付。
