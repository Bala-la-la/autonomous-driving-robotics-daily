# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-11

## 日期与证据口径

北京时间 2026-10-11 检索 [arXiv API](https://export.arxiv.org/api/query?search_query=cat%3Acs.RO%20OR%20cat%3Acs.CV&start=0&max_results=100&sortBy=submittedDate&sortOrder=descending)。周末未出现比 **2026-10-08 UTC** 更晚的相关常规批次；本期明确回溯该日的 6 篇此前未选论文，不将旧稿称为当日新稿。实验数字均为作者报告、未复现；“关注价值／局限”是编辑判断。

## 自动驾驶、规划与长期自治

### 1. Control-Ready Uncertainty for Trajectory Diffusion

- **论文／作者／时间**：[arXiv:2610.12431](https://arxiv.org/abs/2610.12431)；Zhiwei Xue、Jia Yue Kam、Jinhang Qiu、Yifeng Cheng 等；v1：2026-10-08 17:57 UTC，CoRL 2026 Spotlight。
- **问题**：扩散轨迹能表达多模态未来，但反复 Monte-Carlo 才能给不确定性，实时避障与安全裕度难以使用。
- **创新与机制**：SCOPE 从 score-curvature 蒸馏结构化精度矩阵，在名义轨迹周围输出逐时刻的 calibrated Gaussian tube；该 tube 同时作为动态占用与探索引导。
- **实验与关键结果**：在行人预测、拥挤导航、Maze2D 和 Franka Panda 实验中，作者报告低开销不确定性估计带来更好的闭环表现；摘要未披露统一的绝对增益。
- **关注价值／局限**：把生成模型的“多样性”转成控制器可消费的协方差接口；但校准是否能覆盖罕见急刹、遮挡和模型失配，仍需实车风险分项验证。

### 2. FAITH: Feasibility-Aware Safety-Filtered RL for High-Dimensional Systems

- **论文／作者／时间**：[arXiv:2610.12432](https://arxiv.org/abs/2610.12432)；作者见 [arXiv 记录](https://arxiv.org/abs/2610.12432)；v1：2026-10-08 17:57 UTC。
- **问题**：将安全与任务回报塞进同一 RL 目标会相互拉扯；传统安全过滤又依赖解析动力学，且无安全动作时无定义。
- **创新与机制**：学习 state-action safety value，以前馈网络摊销最小干预过滤；任务策略通过“已过滤动力学”优化，当不可行时趋向最小预测峰值伤害动作。
- **实验与关键结果**：作者在 29-DoF 人形 Walking-Avoid 报告 **99.95%** 安全率并保留 **97%** 未过滤回报，也演示 Unitree G1。
- **关注价值／局限**：为自动驾驶／移动机器人提供“不可行时如何退化”的明确接口；学习到的安全值不是形式证明，应报告感知延迟、OOD 和紧急停机的失效边界。

## 机器人／具身智能

### 3. VersaCamVLA: Camera-Configurable VLA Policies for Robotic Manipulation

- **论文／作者／时间**：[arXiv:2610.12451](https://arxiv.org/abs/2610.12451)；Boyao Han、Chen Shi、Jingjing Qian、ZhuoTan Tian 等；v1：2026-10-08 17:58 UTC，NeurIPS 2026 接收。
- **问题**：固定相机数量与外参训练的 VLA，部署时只要机位、数量改变便容易失效。
- **创新与机制**：把任意带位姿 RGB 视图映为固定大小 scene tokens；通过多信号 target-view prediction 与 wrist-camera 的 WAPS 采样学习相机集合表示，再轻量注入冻结 VLA。
- **实验与关键结果**：作者在 RoboTwin、LIBERO 和真机上称优于多视角基线，且在未见机位／不同相机数时保持鲁棒；摘要未给出绝对成功率。
- **关注价值／局限**：把传感器布局变化改造成标准 scene-token 接口；真实部署仍应测量相机标定误差、遮挡与额外 encoder 延迟。

### 4. Generative Neural Retargeting for Human-to-Robot Dexterous Manipulation

- **论文／作者／时间**：[arXiv:2610.12440](https://arxiv.org/abs/2610.12440)；Dechen Gao、Yue Yang、Ben Abbatematteo、Nathan Godwin、Pengcheng Wang 等；v1：2026-10-08 17:57 UTC。
- **问题**：IK 忽略动力学，RL／MPC 每段重解又昂贵，人体演示难规模化转到灵巧手。
- **创新与机制**：GNR 用 flow matching 在可行动力学轨迹的低维流形采样，以人类运动为条件；嵌入 real-to-sim 数据引擎生成带稠密接触力的训练集。
- **实验与关键结果**：作者报告仅用 MPC **8.5%** 采样量，成功率 **56.20%** 对 **27.20%**；产出 **22.3 万**段演示、**3.3 千**物体几何的数据集。
- **关注价值／局限**：更像可复用“动作数据编译器”，而非逐轨迹优化；接触摩擦、未见手型和长时误差累积仍应在真机独立检查。

### 5. VioLA: Learning Generalist Humanoid Control Policies from Human Data

- **论文／作者／时间**：[arXiv:2610.12435](https://arxiv.org/abs/2610.12435)；Mert Albaba、Jens Beißwenger、Anna Manasyan、Daniel Marta 等；v1：2026-10-08 17:57 UTC。
- **问题**：人形全身动作高维耦合，机器人遥操作样本稀缺，人的视频动作又不能直接当关节命令。
- **创新与机制**：策略预测 body／hand motion latent，由预训练控制器执行；人和机器人动作编码到共享 latent，使人类视频可成为动作空间标签。
- **实验与关键结果**：训练池 **1.406 亿帧**、其中 **93.2%** 为人类数据；作者报告真机零样本行走成功 **100%**（GR00T N1.7 为 16.7%、Ψ0 为 0%），操作成功 **88.6%**。
- **关注价值／局限**：提出跨本体数据规模化的控制接口；需核实人类视频筛选、跌倒安全、指令分布和控制器本身对结果的贡献。

### 6. RoboRSI: Stable, efficient, and reusable robot self-evolution in complex real-world environments

- **论文／作者／时间**：[arXiv:2610.12424](https://arxiv.org/abs/2610.12424)；Zimo Wen、Yijin Chen、Yuxuan Cao、Wendi Chen 等；v1：2026-10-08 17:55 UTC。
- **问题**：执行反馈虽能修复机器人代码，却很难把故障归因、修复和复用限制在正确技能，造成不稳定遗忘。
- **创新与机制**：Top-Down Skill Refinement 将任务拆为 compound／atomic／base skills，并设输入输出契约；Manager、Planner、Engineer、Reviewer 分工，把修改限定到责任分支并验证后发布。
- **实验与关键结果**：移动操作臂完成 **104** 轮多物体家务演化；作者报告在 LIBERO、LIBERO-PRO、LIBERO-Plus、RoboTwin 上较最强基线高 **2.7–11.0** 个百分点。
- **关注价值／局限**：技能资产能带版本、证据与回归门槛，契合长时自治；但多技能冲突、人类审阅成本及真机安全回滚仍需量化。

## 趋势总结

- **可执行不确定性与安全退化成为接口**：SCOPE 和 FAITH 都把“预测不稳”接到控制可使用的量，而不是只提高离线分数。
- **跨本体扩展依赖中间表示**：VersaCamVLA、GNR、VioLA 分别把相机、人体动作和机器人控制拆成可迁移接口。
- **自我改进须有变更治理**：RoboRSI 的责任边界、验证与复用表明，机器人学习系统也需要像软件发布一样管理技能演进。
