# arXiv 自动驾驶与机器人晨报｜2026-08-13

说明：截至北京时间 2026-08-13 06:00，最新可用常规批次为 2026-08-11 UTC；以下 8 篇均为该批次且未见于往期报告。作者、日期与数字来自 arXiv 摘要页；机构未完整披露时不作推断。

## 自动驾驶

### 1. XCoT-VLA: Executable Chain-of-Thought for Vision-Language-Action Driving
- 链接：https://arxiv.org/abs/2608.10976
- 作者／机构：XPeng Inc. Foundation Model Team；提交：2026-08-11。
- 问题：自然语言 CoT 开放、解码慢且难直接优化为实时驾驶动作。
- 创新与机制：从日志轨迹和场景语义自动构造 Reason-Action 监督，用 2–6 个可执行 XCoT token 条件化固定轨迹 query；Reason／Control FFN 分路，并可用 XCPO 在同一 token 空间细化。
- 实验与关键结果：通用分布纵向 ADE 从 1.645 降至 1.323；变道场景横向 FDE 从 1.616 降至 0.648，同时保持实时规划预算。
- 关注价值：把“解释”压缩为动作模型可消费、可优化的紧凑中间状态。
- 局限／跟进：自动监督可能继承日志偏差；仍需公开闭环碰撞、极端场景、token 可解释性和 XCPO 稳定性结果。

## 机器人／具身智能

### 2. Surgical WAM: A World-Action Model for Data-Efficient Surgical Robot Learning
- 链接：https://arxiv.org/abs/2608.11204
- 作者／机构：Wenrui Bao、Tianyun Jiang、Zhiben Chen、Ser-Nam Lim、Peter D. Peng、Yuzhang Shang；机构未完整披露；提交：2026-08-11。
- 问题：手术机器人动作标注昂贵，而接触、双臂协调和长时操作又需要大量动力学经验。
- 创新与机制：基于 Cosmos Policy 联合预测内窥镜未来和动作块；先用无动作手术视频学习视觉动力学，再在固定动作预算上微调，以滚动时域执行短动作前缀并重规划。
- 实验与关键结果：4 个仿真手术任务平均成功率由 63.5% 升至 77.8%；PegTransfer 绝对提升 20 个百分点，接触密集和双臂任务收益最大。
- 关注价值：证明低成本临床视频可转化为闭环控制先验，而不只用于模拟或评估。
- 局限／跟进：仅报告仿真；真实组织形变、器械差异、视觉遮挡和安全验证是落地关键。

### 3. Flex-π: A Multi-Stream World-Action Model with Compute Flexibility
- 链接：https://arxiv.org/abs/2608.10855
- 作者／机构：Ge Yan、Jinghao Liu、Yuzhi Fan、Lei Cai、Minwen Liao、Jesse Zhang、Dieter Fox；机构未完整披露；提交：2026-08-11。
- 问题：多数 WAM 只用 RGB latent 和像素重建监督，缺少操作所需的显式 3D 几何与对象语义。
- 创新与机制：发现冻结视频 VAE 也能近无损编码 3D pointmap；6B 参数模型在共享 latent 中联合去噪 RGB、3D、DINO 语义和动作，并以逐流 dropout／跨模态 forcing 支持从 action-only 到全联合生成的单检查点运行。
- 实验与关键结果：真实双臂灵巧操作的分布内外任务上，相对最强基线提升最高 2–7 倍，同时快于 π0.5；新增监督不需要新传感器、预训练或推理延迟。
- 关注价值：用现有视频表征免费引入控制相关几何／语义，又能在部署时裁剪视觉流。
- 局限／跟进：6B 参数仍大；需核验各流消融的绝对成功率、action-only 的退化边界和跨本体迁移。

### 4. Neural Introspection Gating for Adaptive KV-Cache Reuse in Vision-Language-Action Models
- 链接：https://arxiv.org/abs/2608.10824
- 作者／机构：Zhijie Wu、Kento Kawaharazuka、Kei Okada；机构未完整披露；提交：2026-08-11。
- 问题：VLA 相邻帧重复计算视觉 KV；仅按视觉相似度复用缓存会在决策不确定时损害动作准确率。
- 创新与机制：训练免费地监控前两名动作 token 的 logit margin；置信度低时立即废弃缓存并全量重算，把模型自身不确定性加入缓存门控。
- 实验与关键结果：在 OpenVLA、OpenVLA-OFT 和 4 个 LIBERO 套件上，LIBERO-Goal／Long 恢复超过 100% 的盲缓存精度损失，同时保留 80% 计算节省。
- 关注价值：几乎零额外成本地把“何时不能省算力”交给策略自身判断。
- 局限／跟进：logit margin 未必跨模型校准；连续动作、视觉突变、真机控制频率和阈值迁移仍需验证。

## 交叉方向：导航、长期记忆与安全规划

### 5. AECNav: Active Evidence Consolidation for Efficient Zero-Shot Open-Vocabulary Object Navigation
- 链接：https://arxiv.org/abs/2608.10817
- 作者／机构：Guanlin Liu、Shaobin Ling、Renyuan Liu、Zeying Gong、Junjie Hu；机构未完整披露；提交：2026-08-11。
- 问题：零样本开放词汇目标导航既有重复感知开销，也会把相似干扰物的单次高置信检测误当目标。
- 创新与机制：共享编码统一各推理阶段；用簇级 log-odds 累积正、负证据，再按信息增益／路程成本主动选择 frontier，全流程无需训练。
- 实验与关键结果：HM3D-v2、HM3D-OVON、MP3D 成功率分别为 84.7%、57.3%、51.3%；实体四足机器人 40 次试验成功率 95%，约 5 Hz。
- 关注价值：把目标导航从“看见即确认”改成可积累、可反证的证据决策。
- 局限／跟进：代码待接收后发布；实体试验规模较小，开放世界类别、动态遮挡和检测器系统偏差仍需扩大验证。

### 6. R4DSG: Relative 4D Scene Graph Memory for Object-Centric Question Answering in Long Egocentric Video
- 链接：https://arxiv.org/abs/2608.11017
- 作者／机构：Ke Ma、Yamin Mao、Weiming Li、Shuai Tan、Yijie Zhong、Hao Chen、Haofen Wang、Meng Wang；机构未完整披露；提交：2026-08-11。
- 问题：字幕式长期记忆难保持对象身份、位置变化和状态时间线，而自由移动 RGB 又缺少可靠全局 3D 对齐。
- 创新与机制：区分稳定 anchor 与动态对象，以相对 anchor 的状态转移代替全局地图；将时间、地点、持久对象和交互上下文压缩为可检索 4D 场景图条目。
- 实验与关键结果：EgoLifeQA 的 255 个对象问题上，在仅按问题检索设置中总体超过 EgoRAG-Text 6.7 分，when 类问题提升 12.5 分。
- 关注价值：为穿戴助手和长期自治提供无需 RGB-D／位姿重建的对象级时空记忆。
- 局限／跟进：评测子集较小；身份切换、anchor 自身移动、长时间漂移及在线更新成本需检查。

### 7. Risk-Aware Kinodynamic Motion Planning Under Uncertainty For Safe Navigation on Planetary Environments
- 链接：https://arxiv.org/abs/2608.11175
- 作者／机构：Sachin Sunil Kelkar、Tanmay Dokania、Yashwanth Kumar Nakka；机构未完整披露；提交：2026-08-11。
- 问题：行星地形力学和感知均不确定，纯成本最优规划可能选择任务失败风险极高的动力学轨迹。
- 创新与机制：先以 AO-RRT 搜索渐近最优、动力学可行的风险轨迹，再以其初始化顺序凸规划；用 CVaR 显式约束尾部风险。
- 实验与关键结果：仿真和硬件实验中，跨轨迹风险降低超过约 97%。
- 关注价值：将尾部风险、动力学可行性与可求解的两阶段优化连起来，适用于低容错长期任务。
- 局限／跟进：需报告风险降低对应的路程／时间代价，以及模型失配、非平稳地形和感知灾难失效下的保证。

### 8. VIScore: Diagnosing Planning-Relevant Quality in Latent World Models
- 链接：https://arxiv.org/abs/2608.11174
- 作者／机构：Haiyu Wu、Randall Balestriero、Morgan Levine；机构未完整披露；提交：2026-08-11。
- 问题：latent 看起来规整或能线性探测物理状态，并不代表搜索规划真的会成功。
- 创新与机制：VIScore 同时度量编码表征的 veracity、预测器 influence/capacity 与搜索规划器 hallucination，覆盖 encoder—predictor—planner 全链路。
- 实验与关键结果：在已见和未见模型／数据集的跨任务成功率池中 Spearman 相关均超过 0.75；也是所有测试场景中唯一校准误差低于常数拟合的指标。
- 关注价值：让世界模型选型从“重建好不好”转向“是否支持可靠规划”的可诊断度量。
- 局限／跟进：相关性不是因果；需检验在真实机器人、长 rollout、多模态未来和不同搜索算法上的迁移性。

## 趋势总结
1. 驾驶与 VLA 的动态计算进一步细化：既压缩推理 token，也用策略置信度决定缓存是否安全，优化目标从平均速度转向风险条件下的算力分配。
2. 世界模型价值正从生成逼真度转向闭环控制收益和规划可诊断性；无动作视频、可伸缩多流结构与全链路评分形成互补路线。
3. 长期自治开始显式管理证据、对象时空记忆和尾部风险，说明“知道什么、何时确认、失败代价多大”正成为统一系统问题。
