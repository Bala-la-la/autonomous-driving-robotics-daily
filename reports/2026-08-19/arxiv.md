# arXiv 自动驾驶与机器人晨报｜2026-08-19

说明：截至北京时间 2026-08-19 06:00，最新可用相关批次为 2026-08-17 UTC；以下均为该批次论文，作者与摘要结果来自 arXiv 页面。

## 自动驾驶

### 1. Q-based Variational Inverse Reinforcement Learning
- 链接：https://arxiv.org/abs/2608.16888
- 作者／机构：Jingwei Chen 等；提交：2026-08-17。
- 问题：驾驶示范通常只提供轨迹，真实奖励与行为偏好不可见，且多峰行为难以由单一 IRL 奖励解释。
- 创新与机制：以 Q 函数为潜变量的变分逆强化学习，联合后验推断奖励并保留多种合理策略。
- 实验与关键结果：摘要报告在驾驶与控制基准上优于传统最大熵 IRL 和行为克隆；具体数值需待全文核验。
- 关注价值：为驾驶偏好建模提供不必硬编码奖励的概率接口，可服务规划与数据筛选。
- 局限／跟进：目前摘要未披露真实道路闭环、奖励可识别性和长尾安全结果。

### 2. CaliBench: Are the Stochastic Dynamics of Video World Models Physically Calibrated?
- 链接：https://arxiv.org/abs/2608.16829
- 作者／机构：Jonathan Sadeghi、Jenny Seidenschwarz、Jesse Allardice、Sirish Srinivasan、Benjamin Graham 等；提交：2026-08-17。
- 问题：视频世界模型可能生成“看起来合理”但概率不对的物理结果，FID 等指标难测量细粒度不确定性。
- 创新与机制：用骰子、二项分布、轮盘等有闭式参考分布的离散结果空间，分离可评分率与概率校准误差。
- 实验与关键结果：基准能区分逐样本准确率相同但不确定性质量不同的模型，提供物理可解释的校准曲线。
- 关注价值：驾驶世界模型不应只追求视频逼真度，还要让风险采样概率可信。
- 局限／跟进：合成离散现象与真实交通动力学仍有域差距，需接入轨迹和碰撞分布。

## 机器人／具身智能

### 3. Don’t Drop the BATON: Long-Horizon Robot Manipulation via Agentic Subtask Exploration and Transition-aware Memory
- 链接：https://arxiv.org/abs/2608.16889
- 作者／机构：Bingxin Xu、Yuzhang Shang、Emilio Ferrara；提交：2026-08-17。
- 问题：长任务错误会跨阶段累积，单独探索每个子任务的代价呈指数增长，且现有记忆缺少子任务进出条件。
- 创新与机制：冻结 VLA，由语言 Agent 规划；接触段调用 VLA、自由空间使用解析原语，并记录 transition-aware 记忆，定位失败发生在哪个阶段。
- 实验与关键结果：摘要显示在多阶段操作中显著降低探索预算并提升恢复能力；完整增益需结合论文表格核对。
- 关注价值：把“会做单个技能”转化为可诊断、可恢复的长时执行合同。
- 局限／跟进：语言记忆的错误归因和跨本体迁移仍需真实机器人长期验证。

### 4. τ₀-VLA: a Hierarchical Robot Foundation Model with World-Model-Guided Test-Time Computation
- 链接：https://arxiv.org/abs/2608.16885
- 作者／机构：Xiaowei Cai、Yunuo Cai、Bingao Chen、Jingxiao Chen、Zhi Chen 等；提交：2026-08-17。
- 问题：层级 VLA 通常一次前向就决定子任务，无法为困难或高后果决策追加计算。
- 创新与机制：高层策略用执行记忆生成子任务，必要时由世界模型搜索多个候选再提交；低层策略跨多个本体执行。训练数据约 40,115 小时异构真实数据。
- 实验与关键结果：摘要报告在长时任务和多本体设置中受益于测试时搜索；需全文确认各任务成功率与算力开销。
- 关注价值：把推理预算变成可按风险伸缩的控制变量，而非固定深度。
- 局限／跟进：搜索延迟、世界模型偏差与真实安全约束是部署瓶颈。

### 5. HAF: Adapting Generalist VLAs to Humanoid Whole-Body Loco-manipulation via Hierarchical Action Flow and Spectral Latent RL
- 链接：https://arxiv.org/abs/2608.16837
- 作者／机构：Langzhe Gu、Chengkai Hou、Meng Li、Xinhua Wang、Jiaming Liu 等；提交：2026-08-17。
- 问题：人形全身运动同时耦合行走、腰部姿态和双臂操作，直接在线微调大 VLA 代价高且有安全风险。
- 创新与机制：HAF-VLA 处理层级动作流，HAF-Stage 在谱潜空间进行低维在线强化学习，减少对大骨干的直接扰动。
- 实验与关键结果：摘要报告改善全身 loco-manipulation，并降低真实机器人探索成本；绝对提升待全文核验。
- 关注价值：提供从通用 VLA 到人形全身控制的分阶段适配路径。
- 局限／跟进：动作流分解是否覆盖跌倒恢复、接触切换和不同人形比例仍未知。

### 6. FlexWorm: Primitive-augmented Hybrid Contact-motion Planning for Suction-based Multi-segment Deformable Robots
- 链接：https://arxiv.org/abs/2608.16853
- 作者／机构：Zili Tang、Tiecheng Guo、Qinyue Zhang、Meng Guo；提交：2026-08-17。
- 问题：多节吸附软体机器人依赖手工步态，难以在复杂曲面上处理离散吸附切换与连续形变。
- 创新与机制：IKHS 对可行吸附转移做 best-first 搜索，只在诱导出的自由块上求逆运动学，再叠加可复用运动原语。
- 实验与关键结果：复杂曲面 3D 导航仿真中减少搜索量并提高可行规划率；摘要未给出统一跨场景数字。
- 关注价值：将软体接触规划从脚本化动作推进到几何约束下的组合搜索。
- 局限／跟进：准静态模型、吸附可靠性和真实材料迟滞需要实体验证。

## 交叉方向：安全、群体与长期自治

### 7. Security of Foundation-Model-Powered Embodied Agents: Attack Surfaces, Attacks, Defenses, and Evaluation
- 链接：https://arxiv.org/abs/2608.16843
- 作者／机构：Jiawei Liu、Jiacheng Guo、Tian Zhang、Yiwei Xu、Juan Wang 等；提交：2026-08-17。
- 问题：提示注入、后门、投毒和对抗样本可沿感知—推理—规划—动作链传播，传统按攻击名字分类难定位首个失守点。
- 创新与机制：以 first-compromised-trust-boundary 为原则，按供应链、指令、记忆、物理语义环境、多模态感知等五层十二类攻击面组织防御与评测。
- 实验与关键结果：综述建立攻击面—机制—防御映射和评测议程，而非单一新模型数字。
- 关注价值：为机器人与自动驾驶 Agent 的权限、记忆和动作前验证提供统一威胁模型。
- 局限／跟进：综述结论仍需标准化基准、真实硬件攻击和可复现防御成本支撑。

## 趋势总结
1. VLA 正从固定一次推理转向按阶段、风险和世界模型证据分配测试时计算。
2. 长时操作的核心接口变成子任务过渡条件、失败归因和可恢复记忆；人形与软体机器人则把层级动作和接触几何显式化。
3. 世界模型评价开始关注概率校准，具身安全开始按信任边界组织，二者共同推动“可执行且可审计”的长期自治。
