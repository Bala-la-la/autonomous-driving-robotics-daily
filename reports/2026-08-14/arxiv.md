# arXiv 自动驾驶与机器人晨报｜2026-08-14

说明：截至北京时间 2026-08-14 06:00，最新可用常规批次为 2026-08-12 UTC；以下 8 篇均为该批次且未见于往期报告。作者、日期与数字来自 arXiv 摘要页；机构未完整披露时不作推断。

## 自动驾驶

### 1. Redistribution-based Cost Inference Improves Sparse Safe Offline RL
- 链接：https://arxiv.org/abs/2608.12306
- 作者／机构：Ebenezer Gelo、Geraud Nangue Tasse、Steven James、Benjamin Rosman；University of the Witwatersrand；提交：2026-08-12。
- 问题：安全离线 RL 通常需要逐步成本标注，现实监督却常只有首次危险时的轨迹级停止反馈。
- 创新与机制：RCI 用 return decomposition 将稀疏停止反馈重分配为稠密逐步成本，再训练约束离线策略；理论上保持 CMDP 的可行策略集和最优拉格朗日量不变。
- 实验与关键结果：高速公路驾驶和机器人操作中，违规率显著低于稀疏监督及分类器基线，并对数据组成和标签噪声保持鲁棒；摘要未披露统一数值。
- 关注价值：把低成本人工干预信号转化为可训练的安全信用分配，而不改变原问题最优解。
- 局限／跟进：停止反馈仍需覆盖真正危险事件；应检查长时延迟后果、漏标风险和真实闭环策略分布偏移。

### 2. Learning-Based Behavior Planning for Automated Driving: Real-World Integration and Deployment
- 链接：https://arxiv.org/abs/2608.12198
- 作者／机构：Jean-Pierre Busch、Guido Linden、Jan Bergmann、Lutz Eckstein；机构未完整披露；提交：2026-08-12。
- 问题：学习式行为规划能处理复杂交通，但不透明输出难以做安全保证和稳定真车集成。
- 创新与机制：神经网络解释场景并提出驾驶行为，优化监督层再验证提议并显式施加可驾驶性与安全约束，形成学习提案—确定性审查的混合架构。
- 实验与关键结果：在真实城市数据上完成开环研究，并部署到研究车 karl 做闭环运行；摘要未给出量化改进。
- 关注价值：关注从模型指标到实车系统边界的最后一段，将安全层放在可审计的优化模块中。
- 局限／跟进：需公开道路里程、接管、闭环失败模式、监督层拒绝率与实时延迟。

### 3. Do Not Forget the Obvious - RISC: A Risk-Informed Slice-Coverage Protocol for Safe Autonomous Driving
- 链接：https://arxiv.org/abs/2608.12051
- 作者／机构：Fabian Hueger；机构未完整披露；提交：2026-08-12。
- 问题：聚合指标会掩盖高风险条件中样本覆盖不足和关键失败未被审计的问题。
- 创新与机制：RISC 将安全关切编码为机器可读 risk slices，以轻量信号标注候选数据，按风险选择有限审计集，并强制同时报告各切片覆盖证据；LLM 仅可辅助发现遗漏条件。
- 实验与关键结果：在 Zenseact Open Dataset 的 1,000 帧行人感知概念验证中，风险选择把关键失败发现率从随机抽样的 34.0% 提高到 98.5%。
- 关注价值：让“平均性能不错”必须附带“哪些高风险切片确实测过”的可核验声明。
- 局限／跟进：单数据集、单检测代理和小规模概念验证；风险定义、切片交叠、审计偏差及 LLM 建议可靠性仍需标准化。

### 4. High-Order Liquid Evidence Encoding for Gradual GNSS Spoofing Detection in Autonomous Driving
- 链接：https://arxiv.org/abs/2608.11790
- 作者／机构：Muhammad Ayub Sabir、Junbiao Pang、Fatima Ashraf；机构未完整披露；提交：2026-08-12。
- 问题：渐进式 GNSS 欺骗让单次观测保持合理，却持续扩大卫星位移与车载运动估计之间的不一致。
- 创新与机制：构造物理引导的 GNSS—运动残差，并分别编码残差值、一阶和二阶变化；三个因果 liquid encoder 的时序状态分层耦合，仅用当前及过去观测判定攻击。
- 实验与关键结果：AV-GPS 三个子集上，在 Dataset 1/3 的 F1 达 0.9535/0.9777；Dataset 3 两次正常到攻击转换均在 4 个采样步内检出。
- 关注价值：高阶变化把“缓慢但持续”的攻击轨迹显式化，比静态特征更贴近渐进欺骗机制。
- 局限／跟进：需跨车辆、传感器和攻击速率复现，并报告误报、计算预算及融合定位闭环影响。

## 机器人／具身智能

### 5. Policy-Induced Hand Priors in Humanoid Dual-Arm Manipulation: Diagnosing and Mitigating Initial-Pose Dependence
- 链接：https://arxiv.org/abs/2608.11769
- 作者／机构：Chaeyeon Jung、Juyoun Park；机构未完整披露；提交：2026-08-12。
- 问题：双臂 VLA 的总成功率会掩盖初始姿态触发的错误选手与局部失败。
- 创新与机制：以 HandPriorScore、残余手偏置和目标响应度刻画策略诱导的早期选手先验；把局部初始臂姿态作为因果操控点，并用针对性数据增强修复低性能区域。
- 实验与关键结果：多策略、17 种初始配置显示显著姿态—策略交互；扩充姿态覆盖普遍提高鲁棒性，围绕低性能配置增强可提升该点成功率，摘要未给统一幅度。
- 关注价值：提示机器人策略评测必须覆盖初始状态切片，而不能只看任务平均分。
- 局限／跟进：配置规模有限；需验证真机、不同本体、目标布局以及选手偏置与碰撞安全的关系。

### 6. ContactIPM: A Structure-Exploiting Interior-Point Solver for Contact-Implicit Trajectory Optimization
- 链接：https://arxiv.org/abs/2608.11731
- 作者／机构：Yucheng Chen；机构未完整披露；提交：2026-08-12。
- 问题：接触隐式轨迹优化的互补约束退化，通用原始—对偶求解器不稳，而专用方法又未利用分阶段最优控制结构。
- 创新与机制：用 barrier-coupled elastic relaxation 嵌入互补不等式，逐阶段消去 slack/dual 变量，并以 Riccati recursion 解约化 Newton 系统；固定多阶段恢复计划从朴素初始化重试。
- 实验与关键结果：四个 CRISP 基准快 2.17–8.87 倍；对 IMPACT 在 Push T/Cart Transport 快 2.96/4.91 倍，但 Push Box 慢 4.46 倍，并做了 50 次闭环 Push Box 鲁棒 rollout。
- 关注价值：将接触互补的稳健处理与控制问题的稀疏结构真正合并，适合在线重规划探索。
- 局限／跟进：优势依任务而变；需检查更高维接触、实时最坏延迟、恢复失败率和真机数值稳定性。

### 7. StellaVLA: In-Context Structured Demonstration for Generalizable Vision-Language-Action Models
- 链接：https://arxiv.org/abs/2608.11671
- 作者／机构：Siyu Xu、Yunke Wang、Zijian Wang 等；机构未完整披露；提交：2026-08-12。
- 问题：VLA 遇到新场景、视角或物体时性能骤降，逐场景采集数据微调成本高。
- 创新与机制：离线自动把一条原始轨迹转为任务计划、子目标和语言化 3D 运动的结构化示范；测试时检索单条示范作上下文，双路训练内化动作—语言推理，推理仅保留动作专家以维持高频控制。
- 实验与关键结果：VLA-Arena 总分 0.63，对比 pi0.5 的 0.44 和 LingBot-VLA 的 0.22；LIBERO/Plus 平均成功率 98.8%/85.1%，并展示人、机器人及 XR 示范的真机适配。
- 关注价值：把示范从像素轨迹提升为可跨本体复用的结构化任务解释，且不增加部署延迟。
- 局限／跟进：自动语言化可能引入错误；需核验检索失败、示范冲突、长时任务和真实 OOD 的规模化结果。

## 交叉方向：导航与动态环境

### 8. DaViNCi: A Dataset Towards Outdoor Vision-and-Language Navigation with Continuous Actions and Dynamic Elements
- 链接：https://arxiv.org/abs/2608.11901
- 作者／机构：Zihao Xie、Pingrui Lai、Yitong Wu、Hua Yang；机构未完整披露；提交：2026-08-12。
- 问题：现有户外 VLN 多依赖固定离散拓扑图，无法反映连续控制和动态现实环境。
- 创新与机制：DaViNCi 同时引入连续动作与不可预测动态元素，覆盖 6 张地图和 6,933 条轨迹，并单独分析动作粒度与动态因素影响。
- 实验与关键结果：相较既有数据集，模型在 DaViNCi 离散设置成功率下降超过 10%，连续设置下降更大。
- 关注价值：将户外 VLN 的 sim-to-real 缺口从视觉域偏移扩展到控制粒度和动态交互。
- 局限／跟进：地图和轨迹规模仍有限；需披露动态主体多样性、语言复杂度、真实户外迁移及安全交互指标。

## 趋势总结
1. 自动驾驶安全正在形成“训练信号—规划监督—风险切片审计—攻击检测”的分层闭环，可验证覆盖比单一平均指标更重要。
2. 机器人泛化开始从模型平均能力转向条件化诊断：初始姿态、单条结构化示范和接触求解器分别暴露或修复具体失败边界。
3. 连续控制、动态元素和真车部署成为检验论文是否跨出静态离线基准的共同尺度。
