# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-16

## 日期与证据口径

北京时间 2026-10-16 检索 [arXiv API](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.RO%20OR%20cat%3Acs.AI%20OR%20cat%3Acs.CV%29%20AND%20submittedDate%3A%5B202610140000%20TO%202610142359%5D&start=0&max_results=100&sortBy=submittedDate&sortOrder=descending)。以下 7 篇均为 **2026-10-14 UTC** 首次提交的新稿；实验数字均为作者报告，未独立复现；“关注价值／局限”为编辑判断。

## 自动驾驶、感知与安全运行时

### 1. SafeDriveVLA: Navigation-Conditioned World Model Dreaming for Conflict-Aware End-to-End Autonomous Driving

- **论文／作者／时间**：[arXiv:2610.20609](https://arxiv.org/abs/2610.20609)；Shaoyuan Xie、Zihan Zhang、Jingxuan Wang 等（含 Lingdong Kong、Henrik I. Christensen、Qi Alfred Chen）；v1：2026-10-14 17:59 UTC。
- **问题、创新与机制**：自由文本导航让驾驶 VLA 能理解更多指令，也引入“指令与当前交通冲突”的攻击面。SafeDriveVLA 新建同时评测语言跟随、冲突感知与对抗鲁棒性的基准；先预测三档 navigation-compliance mode，将“该不该服从”从动作生成中拆出，再让世界模型假设严格执行指令进行 dreaming，以识别跟随是否安全。
- **实验与关键结果**：Bench2Drive 上报告 **88.16 DS、68.64% SR**；相对最强 SimLingo 变体，闭环语言跟随提升 **49.3%**，不安全指令下碰撞从 **60 降至 38**。**关注价值／局限**：世界模型不只预测“专家会做什么”，而用于反事实的指令安全审查；但三档模式、仿真冲突覆盖与 dream 误差能否承受真实感知延迟、法规差异和长尾交互仍待验证。

### 2. VITAL: From Visual Motion to Precise Action

- **论文／作者／时间**：[arXiv:2610.20604](https://arxiv.org/abs/2610.20604)；Ao Liang、Youquan Liu、Mingxiao Li 等（含 Lingdong Kong）；v1：2026-10-14 17:59 UTC。
- **问题、创新与机制**：世界—动作模型通常把视觉未来和轨迹 token 分开训练，导致动作没有以视觉动力学为主坐标。VITAL 将动作拆成视觉推导的运动 scaffold 与编码厘米级轨迹偏差的紧凑 residual；flow matching 仅由当前图像、车体状态和导航命令预测二者，后训练只在残差坐标内受限优化，不必在线生成未来视频。
- **实验与关键结果**：NAVSIM v1 navtest 一步去噪即 **90.8 PDMS**，距十步仅 **0.13**，端到端速度 **3.29×**；不重训迁至 NAVSIM v2 报告 **91.1 EPDMS**、navhard **38.6**。**关注价值／局限**：把可解释视觉运动和高精度校正分层，直接对准实时部署；不过离线指标未替代真实闭环安全，视觉 scaffold 在遮挡、湿滑和传感器失效时的误差上界仍需给出。

## 机器人／具身智能

### 3. HiRe-MoMa: Hierarchical Residual Policy Learning for Real-World Mobile Manipulation with Sparse Human Guidance

- **论文／作者／时间**：[arXiv:2610.20607](https://arxiv.org/abs/2610.20607)；Zhefei Gong、Hefeifei Jiang、Zehao Wang、Jiachen Li 等；v1：2026-10-14 17:59 UTC。
- **问题、创新与机制**：移动底盘与机械臂耦合、动作维高，真机微调既昂贵又容易破坏底座策略。HiRe-MoMa 冻结基策略，只学习 policy-agnostic additive residual；将残差拆为底盘与手臂 head，并用单向条件减少梯度干扰；Expert-Guided Value Alignment 用覆盖不足 20% 的稀疏人类干预重塑 critic，指引探索。
- **实验与关键结果**：作者称在 TIAGo++ 上仅约 **30 分钟**在线交互即可稳定提升不同底座策略的任务表现。**关注价值／局限**：残差与稀疏干预提供低风险、低样本的真机适配接口；摘要没有统一成功率、碰撞或回退统计，跨平台、人与环境动态变化、以及人为纠正偏差是否会被价值函数放大仍需审计。

### 4. KinoGen: Customizable Humanoid Loco-Manipulation References via Kinematically Grounded Video Generation

- **论文／作者／时间**：[arXiv:2610.20552](https://arxiv.org/abs/2610.20552)；Qi Wu、Lulu Zhao、Sanghyun Hahn 等；v1：2026-10-14 17:43 UTC。
- **问题、创新与机制**：视频生成的类人参考通常要经人体代理重定向，容易造成穿透、脚滑和无法精确满足物体目标。KinoGen 以目标机器人和物体的标定仿真渲染条件化视频生成器，再将同一模型拟合回双视角视频，令参考天然落在机器人构型空间；编辑关键帧的物体位姿即可重新生成并反优化参考。
- **实验与关键结果**：八项 loco-manipulation 任务中，相比视频基线穿透与脚滑更低、保留 **90% 以上**标注接触；定制参考满足全部指定目标，并在 Unitree G1 灵巧手上部署跟踪策略。**关注价值／局限**：把生成先验绑定到运动学可执行性，而不是仅追求视觉真实；物理接触、摩擦、动力学稳定和生成偏差是否会在长时全身执行中累积仍需实机风险曲线。

### 5. TacClaw-Infinity: A Large-Scale Vision-Tactile-Language-Action Dataset for Dexterous Manipulation

- **论文／作者／时间**：[arXiv:2610.20320](https://arxiv.org/abs/2610.20320)；论文团队；v1：2026-10-14 15:06 UTC。
- **问题、创新与机制**：触觉操作数据难大规模收集，且多模态数据常缺乏质量控制和结构化接触监督。TacClaw 以带触觉的 UMI 式手持接口同步记录视觉、指尖触觉与末端轨迹，无需采集时指定目标机器人；分布式采集后通过轨迹重建、多模态质检、具身过滤、接触分段、子任务描述和空间标注形成 VTLA 数据。
- **实验与关键结果**：论文报告全球家庭、实验室、工厂、零售与户外采集超过 **10,000 小时、100 万 episode、10 亿帧、1,000+ 任务类型**，并展示向三种异构机器人迁移且不使用机器人专属演示。**关注价值／局限**：数据规模首次把触觉、语言和接触过程放进同一可筛选管线；采集设备校准、触觉材料／传感器差异、分布式标注一致性、隐私和任务长尾仍比帧数更决定可用性。

### 6. AdaRSI: On-Demand Recursive Self-Improvement for Embodied Agents

- **论文／作者／时间**：[arXiv:2610.20474](https://arxiv.org/abs/2610.20474)；论文团队；v1：2026-10-14 16:51 UTC。
- **问题、创新与机制**：具身 RSI 若只改 harness，补不了执行器缺失技能；若见失败就微调，又会浪费数据并拟合系统调用错误。AdaRSI 先由 coding agent 修改 Skills／harness，再从保存状态重试失败子步骤作归因；仅对持续不可靠的子步骤用自采演示微调 VLA，并跨任务保留经验。
- **实验与关键结果**：以 GR00T N1.5 为执行器、无人工演示，在 RoboCasa365 未见组合任务成功率从 **4.6% 到 13.8%**；相较每个子步骤都微调，略高成功且仅用 **28% GPU 时间、22% 自采演示**。**关注价值／局限**：把“改调用方式”与“改权重”作为可验证决策，减少盲目在线训练；仿真存档状态、代码 agent 权限和自采失败样本的安全／偏差，仍是上真机前的硬约束。

## 交叉方向：SLAM／3D／多智能体世界模型

### 7. Tiered-Resolution Volumetric Mapping for Real-Time Simultaneous Planning and Mapping on Natural Outdoor Environments

- **论文／作者／时间**：[arXiv:2610.20476](https://arxiv.org/abs/2610.20476)；论文团队；v1：2026-10-14 16:51 UTC。
- **问题、创新与机制**：全局细粒度 LiDAR 体素图占用集成、存储和 CPU，但规划器真正要走的区域很少。方法把同一地图同时以路径走廊内细分辨率、其他区域粗分辨率集成；规划反向给建图反馈，动态调节 leaf resolution，而非传统单向“建图后再规划”。
- **实验与关键结果**：两个真实遥操作数据集离线回放中，分层图比统一细图小 **13–15×**、集成 CPU 少 **6–8×**，路径每米成本近似；统一粗图虽同样省空间，困难场景路径成本却恶化 **210%**。**关注价值／局限**：为长期户外自主把地图预算与任务相关性绑定；离线路径代价不等于在线安全，走廊外突发障碍、规划变更滞后和多传感器不一致还需闭环评测。

## 趋势总结

- **把“是否执行”从动作模型中剥离**：SafeDriveVLA 审查语言指令，AdaRSI 诊断失败属于 harness 还是执行器；后续应报告该决策层的误报、漏报、时延与权限边界。
- **生成模型正被约束为可执行中间表示**：VITAL 的视觉 scaffold+残差、KinoGen 的运动学视频参考都不是只生成内容；评价必须延伸到真实闭环、接触与回退成本。
- **真实数据和地图走向“任务条件化”**：TacClaw-Infinity 以接触与具身过滤组织大规模数据，Tiered Mapping 以规划走廊配置空间分辨率；规模收益需要附带采集质量、传感器迁移与异常场景覆盖证据。
