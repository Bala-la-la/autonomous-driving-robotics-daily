# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-22

## 日期与证据口径

截至北京时间 2026-10-22，arXiv API 最新相关批次为 **2026-10-20 UTC 的 v1 提交**（API 索引更新至 2026-10-21 22:07 UTC；检索 10 月 21 日提交窗口为 0 篇）。本期选 8 篇，按自动驾驶、机器人/具身智能及交叉方向分组。作者与 v1 时间来自 arXiv；摘要/API 未提供机构时不推测。实验数字均限定在作者报告的设置中。

## 自动驾驶与交通系统

### 1. [Agentic discovery of interpretable car-following laws from multi-source trajectory data](https://arxiv.org/abs/2610.27836)

- **作者／提交时间：** Jiamei Xu、Jie Sun、Keshuang Tang、Jian Sun；v1 记录于 2026-10-20 08:25:21 UTC；arXiv API 未列机构。
- **问题与创新：** 微观交通仿真依赖跟驰方程，但手工规定的函数结构难覆盖不同道路与驾驶行为。本文把基于交通知识的假设生成、符号搜索和物理约束评估连成可迭代的模型发现流程。
- **机制／结构：** Agent 根据交通流知识和状态相关重建误差提出候选；进化式符号搜索再按多目标物理一致性筛选，得到 Adaptive Equilibrium Response Model（AERM）。AERM 将相对速度响应与间距相关的均衡速度恢复耦合，并推导均衡速度—间距、流量—密度关系及零时延稳定性条件。
- **实验与关键结果：** 候选发现使用 NGSIM US-101、highD、exiD；再与 7 种经典模型比较。在上海自然驾驶数据、NGSIM I-80 和 Waymo 轨迹上，逐轨迹标定的间距 RMSE 相对最强基线分别降低 **9.11%、7.59%、21.73%**；共享参数设置下仍具竞争力。
- **关注价值：** 让模型发现结果保留解析形式，可用于交通仿真、车队扰动分析和自动驾驶策略评测。
- **局限／跟进：** 数据集特定标定带来迁移风险；需要核验反应时延、异质驾驶者、切入/换道和传感噪声下的稳定性，不能把拟合改善直接等同于真实交通安全。

### 2. [When Does Experience Memory Help Closed-Loop LLM Driving Agents? A Controlled Evaluation with Resampled Warmup Pools, Token-Matched Fillers, and Audited Baselines](https://arxiv.org/abs/2610.27714)

- **作者／提交时间：** Yingxin Jia、Xuanyi Li；v1 记录于 2026-10-20 06:31:27 UTC；arXiv API 未列机构。
- **问题与创新：** 闭环 LLM 驾驶中，经验记忆看似提升表现，但记忆样本池、提示词长度与基线移植质量可能混杂结果。本文将这些因素拆开控制，检验“更复杂的检索记忆是否真的带来收益”。
- **机制／结构：** 在 1 Hz HighwayEnv、决胜对照使用 GPT-4o-mini；对 10 组互不重叠的 warmup 经验池重采样，并加入 token 数匹配的无关 filler。比较扁平检索、单帧网格、时间图记忆、压缩规则手册和 K 步观察历史，并审计基线移植。
- **实验与关键结果：** 两类检索记忆仅在 10 个池中的 1 个胜过无记忆基线；研究报告的“最好池”无法代表其他抽样。没有一种检索设计稳定超过 token 匹配的 filler；单条 15-token 谨慎提示已达到碰撞指标上的合并上限，按谨慎程度计价后规则手册优势消失。
- **关注价值：** 这是对驾驶 Agent 记忆评测的因果控制提醒：必须报告随机池、提示长度、谨慎度代价与基线端口质量。
- **局限／跟进：** 结论限于单一 HighwayEnv 测试床、控制频率与模型；不能据此断言所有记忆方法无效。需要在真实道路分布、不同模型和风险敏感指标上复验。

### 3. [Provisioning Robust and Efficient LiDAR Perception for Autonomous Driving](https://arxiv.org/abs/2610.27617)

- **作者／提交时间：** Tingxu Han、Zijie Shen、An Guo、Lyuke Wang、Chunrong Fang、Zhenyu Chen、Wei Song；v1 记录于 2026-10-20 04:31:30 UTC；arXiv API 未列机构。
- **问题与创新：** LiDAR 3D 检测部署同时受天气类点云扰动、推理延迟和显存约束；常见做法分别处理鲁棒性或轻量化。本文把精度、时延与显存作为联合配置目标。
- **机制／结构：** 构造模拟极端天气的点云扰动；用 7 种异构检测器的置信度、BEV 重叠和未匹配检测变化估计扰动敏感度，再排序干净/扰动样本训练候选检测器。通过缩窄网络及离线邻域密度统计，限制各采样层处理的点数和邻居数。
- **实验与关键结果：** KITTI Car / PointRCNN 在受扰 Moderate AP 提升 **3.32 个百分点**，平均时延降低 **19.8%**、峰值 GPU 显存降低 **53.9%**。跨 2 个数据集、2 种架构和 3 类目标，受扰 AP 平均提升 **4.03 个百分点**，时延和显存分别降低 **14.4%**、**38.0%**。
- **关注价值：** 将现实部署常被分开汇报的性能和资源约束放进同一验证面。
- **局限／跟进：** 扰动合成与真实传感器故障未必一致；需检查不同天气、传感器型号、点云稀疏度及硬件上的最坏时延，而不只看平均值。

## 机器人／具身智能

### 4. [Learning Adaptable Dexterous Skills via Hybrid Dexterous Mimicking](https://arxiv.org/abs/2610.28628)

- **作者／提交时间：** Yuxuan Kuang、Jiashun Wang、Yixuan Sun、Yufei Ye、Sungjae Park、Umar Iqbal、Katerina Fragkiadaki、Shubham Tulsiani；v1 记录于 2026-10-20 17:59:32 UTC；arXiv API 未列机构。
- **问题与创新：** 目标奖励策略能适配新物体位姿，却易学出不自然的手指策略；动作跟踪保留人类动作先验，却难以偏离单一演示。AdaDex 用短时手—物轨迹同时提供先验和目标适应性。
- **机制／结构：** Hybrid Dexterous Mimicking 在共享策略中混合两类并行环境：一类以稠密动作跟踪奖励学习人类运动先验，另一类扰动初始状态与目标、以稀疏物体成功奖励训练偏离演示后的泛化。输入可来自 mocap 或野外 RGB(D) 视频重建。
- **实验与关键结果：** 展示功能抓取、物体重定位、手内重排和抛接等技能；论文报告优于基线，并跨模拟器迁移至真机，但摘要未列统一成功率。
- **关注价值：** 以数秒级的人类示范启动灵巧技能，降低每项技能依赖长时间专门采集的门槛。
- **局限／跟进：** 需关注手—物重建误差、物体/手型迁移范围、接触力安全和真机样本量；摘要级“优于基线”不足以判断长时可靠度。

### 5. [UniWALM: Unified World Action Language Model for Embodied Robot Control](https://arxiv.org/abs/2610.28626)

- **作者／提交时间：** Rahul Sajnani、Diego Romeres、Mingyuan Zhang、Kai Gao、Carl Qi、Baichuan Huang、Srinath Sridhar、Dylan Randle、Lillian J. Ratliff、Jose Barreiros、Manikantan Nambi、Jeroen Vanbaar；v1 记录于 2026-10-20 17:59:04 UTC；arXiv API 未列机构。
- **问题与创新：** 将 VLM/语言规划器串接在视频—动作模型之外会形成分阶段调用与外置记忆。UniWALM 在同一模型中联合生成未来视频、动作和语言，使语言成为可回馈的任务记忆。
- **机制／结构：** Mixture-of-Transformers 主干配每模态 diffusion head，同步去噪视频、动作和文本；本步产生的子任务描述/记忆在下一步重新作为输入，不另设规划器或记忆库。Flow Matching with Correction（FMC）训练策略从扰动动作轨迹中恢复，推理时无额外校正成本。
- **实验与关键结果：** RMBench 记忆依赖子集成功率 **34.5%**，不使用预训练语言/推理模型，超过配有关键帧的 Mem-0 设置 **28.5%**；真实 Find-the-Item 任务加入文本记忆后成功率从 **11.1% 升至 61.1%**，对照的 SOTA VLA 不高于机会水平 **33.3%**。
- **关注价值：** 把记忆写入动作生成闭环，并用无推理成本的轨迹恢复目标来增强动作流鲁棒性。
- **局限／跟进：** 真机证据集中在单项找物任务；需测量文本记忆错误累积、视频预测误差、端到端时延及失败后恢复能力。

### 6. [Industrial ReMEmbR: Scaling Spatiotemporal Memory to Robot Fleets](https://arxiv.org/abs/2610.28624)

- **作者／提交时间：** Jad Yammine、Malek Wahidi、Abrar Anwar、Yan Chang、Mihir Acharya、Anthony Rizk；v1 记录于 2026-10-20 17:58:32 UTC；arXiv API 未列机构。
- **问题与创新：** 仓储车队持续产生视频，若写入时就生成语义描述，会增加边缘/服务器计算、通信和存储成本，也可能暴露原始画面。该系统将共享时空记忆改成按需解码。
- **机制／结构：** Jetson 端分别将视频编码成检索 embedding、视觉 token 和 Wan2.2 VAE latent，不上传原始相机帧；在人像图像块上做遮蔽以支持 PII 抽象。Cosmos3-Edge 在视觉编码器与语言解码器边界切分，前者留在机器人、后者运行于本地服务器；Nemotron Agent 按内容、位置、时间检索并请求解码。
- **实验与关键结果：** 写入时不生成 caption；缓存视觉 token 的拆分式解码在 **450 次测试**中与未拆分模型输出一致。此项结果证明输出一致性，不代表已验证现场检索质量或隐私合规。
- **关注价值：** 给多机器人车队提供可查询的时间—地点—内容记忆，同时控制原始视频上行。
- **局限／跟进：** 人像遮蔽不等于完整去标识化；需审计遮挡/漏检、非人敏感信息、访问控制、保留期限、网络中断和边缘吞吐。

### 7. [Planning under Noise with Neural Operators](https://arxiv.org/abs/2610.28623)

- **作者／提交时间：** Michael Chen、Hong Chul Nam、Xi Deng、Anima Anandkumar；v1 记录于 2026-10-20 17:58:30 UTC；arXiv API 未列机构。
- **问题与创新：** 执行噪声使机器人需要兼顾几何约束与控制随机性的反馈规划；逐场景采样求解高维随机最优控制代价高且梯度易被局部 Monte Carlo 噪声翻转。PUN 学习可迁移的噪声感知 value field。
- **机制／结构：** 在 screened-Poisson 控制方程上，将障碍物设为反射 Neumann 边界、目标设为 Dirichlet 边界；扩展 Walk on Stars 求解高维几何样本，再以有噪、未充分收敛的标签训练 geometry-to-field 神经算子。部署时以预测的全局场引导有界局部搜索。
- **实验与关键结果：** 四种噪声等级的 4D 重规划基准上成功率 **95–100%**；最高噪声下相对基线成功率提高 **10.7–60.6%**，运行速度快 **3.29–32.15 倍**。
- **关注价值：** 把控制噪声直接写入规划值函数，并以学习摊销高维几何求解成本。
- **局限／跟进：** 证据仍是基准场景与受控噪声；需考察模型失配、障碍动态变化、传感/执行噪声耦合和真机闭环。

## 交叉方向：协同感知与空间表示

### 8. [CoGaussian: Open-Vocabulary Gaussian-based Collaborative 3D Scene Understanding](https://arxiv.org/abs/2610.28530)

- **作者／提交时间：** Om Shivam Verma、Shaya Farahmand、Lingjun Zhao、Lu Gan；v1 记录于 2026-10-20 17:04:38 UTC；arXiv API 未列机构。
- **问题与创新：** 单个机器人/车辆受视野限制，协同语义占据又常依赖密集体素标注和封闭类别集。CoGaussian 用与基础模型表征对齐的稀疏 3D Gaussian 同时承载几何与开放词汇语义。
- **机制／结构：** 多主体交换和融合稀疏 Gaussian 场景表示，再用于协同语义占据预测，目标是在无需预设类别全集的前提下扩展单体观察范围。
- **实验与关键结果：** 在 Semantic-OPV2V 上优于文中比较的开放词汇单车方法；摘要未给绝对提升幅度或通信成本数据。
- **关注价值：** 将 Gaussian 表征从单体重建推进到可通信的协同场景状态，对多车感知和多机器人建图都有意义。
- **局限／跟进：** 需补充带宽/压缩率、不同步融合、坐标误差、动态遮挡、开放词汇误检与闭环规划收益。

## 趋势总结

本批次出现三条相互关联的变化：自动驾驶研究一边用可解析符号搜索发现跟驰律，一边以重采样、token filler 和基线审计检验“记忆增益”，显示方法复杂度必须与因果评测并行；感知部署开始将受扰精度、延迟和显存联合优化；机器人侧则把语言记忆、纠错动作流、车队时空记忆与稀疏协同 3D 状态做成运行时接口。下一步应从平均分数推进到跨种子、真实传感扰动、通信受限和安全回退下的可复现实证。
