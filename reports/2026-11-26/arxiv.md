# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-26

## 日期与证据口径

检索截至北京时间 2026-11-26 06:00。本期精选 **2026-11-24 UTC v1** 的 7 篇投稿；不是 11 月 26 日当日投稿，且未出现在 11 月 25 日报告。题目、作者、提交时间、方法和数值来自 arXiv 摘要/API；摘要无法完整核验机构归属，故不臆测。所有结果均为作者报告，尚未独立复现。

## 自动驾驶／移动自治

### 1. [Benchmarking Evidence Sufficiency in Vision-Language Models for Autonomous Driving](https://arxiv.org/abs/2611.32964)

- **作者／机构／提交：** Nhat Ha Nguyen、Sudipta Chowdhury、Lokesh Das 等；机构未完整披露；v1，2026-11-24 17:01 UTC。
- **问题：** 驾驶 VLM 即使答对或定位到相关目标，也可能没有足够视觉证据；现有评测把 grounding 和可回答性分开，掩盖“应当拒答”的风险。
- **创新与机制：** **DriveAnswer** 构造 20,151 个问题、七类推理任务的强／弱证据配对：保持场景事实和正确语义答案不变，只改变观测是否支持作答；联合计分回答、弱证据 abstain 与完整 grounding。
- **实验与关键结果：** 最强 zero-shot 的强证据准确率为 **67.31%**，但只有 **21.55%** 配对问题同时做到答对／拒答／完整定位；受控适配后 Gemma-4-12B 的联合能力为 **63.29%**，约为 zero-shot 的三倍。
- **关注价值：** 让驾驶模型的“不知道”成为可测接口，能直接服务遮挡、远距、低照等 ODD 下的降级策略设计。
- **局限／跟进：** benchmark 的配对操作未等同真实传感器失效；还应量化拒答如何接入规划器、误拒成本、跨相机/天气泛化及闭环安全收益。

### 2. [MemAnchorWorld: A Sparse World Model with Horizon-Conditioned Memory Retrieval for Autonomous Driving](https://arxiv.org/abs/2611.32745)

- **作者／机构／提交：** Xinyang Jia、Yuqi Zhang、Jiakai Wang 等；机构未完整披露；v1，2026-11-24 14:56 UTC。
- **问题：** 稀疏 4D occupancy 世界模型将历史压进递推 scene state，远期预测会累积几何和语义误差。
- **创新与机制：** **MemAnchorWorld** 按预测时域、信息有效年龄和语义兼容性做分层双路检索：query 级筛候选、point 级取 memory anchors；再用任务和时域共同门控的 residual adapter 分别修正语义、占据置信度和空间位置。
- **实验与关键结果：** Occ3D-nuScenes 的 1--3 秒平均 mIoU **13.55%**、IoU **22.84%**，作者称两项均为 SOTA。
- **关注价值：** 它把“何段历史实际影响哪个未来时刻”显式化，便于审计记忆过期、错检索和规划代价，而不只是扩大 latent state。
- **局限／跟进：** 需比较显式检索的车端延迟、记忆污染和地图变化下的错误回滚；占据 IoU 改善也不能替代碰撞与控制闭环验证。

### 3. [GeoVLDrive: Geometry-Grounded Vision-Language Reasoning for Autonomous Driving](https://arxiv.org/abs/2611.32510)

- **作者／机构／提交：** JiaHui Huang、Songyan Zhang、Hanbing Li 等；机构未完整披露；v1，2026-11-24 12:41 UTC。
- **问题：** 驾驶 VLA 从通用 VLM 继承语义知识，但理由通常未被 3D 结构与时间变化约束。
- **创新与机制：** 多层 3D foundation features 经 gated cross-attention 注入 VLM；结构化 latent CoT 分别监督未来几何、关键体运动与 meta-action，action expert 据此提议并以场景交互 score tokens 排序轨迹；同时发布 NAVSIM 3DQA。
- **实验与关键结果：** NAVSIM v1 **91.8 PDMS**、v2 **90.9 EPDMS**；NAVSIM 3DQA **89.2%**，较微调 Qwen3-VL-2B 高 **4.6** 点；LingoQA Lingo-Judge **68.6%**。
- **关注价值：** 将几何理由、候选动作和排序依据分离，是检查自然语言／视觉推理是否真正影响控制的较强中间接口。
- **局限／跟进：** 需防止 latent CoT 成为不可验证标签；应报告3D基础模型误差、雨雾／标定漂移、候选遗漏和端到端 p95 延迟。

## 机器人／具身智能

### 4. [OmniAct: One Policy, One Million Embodiments](https://arxiv.org/abs/2611.33158)

- **作者／机构／提交：** Xiang Fan、Yuheng Wang、Jiayuan Yan 等；机构未完整披露；v1，2026-11-24 18:59 UTC。
- **问题：** 共享动作空间能迁移任务知识，却难表达不同关节、自由度和连通性应如何改变操作策略。
- **创新与机制：** 用连接关节位置、运动轴和视觉观测的运动学图条件化策略；flow matching 为各节点预测相对关节运动。训练端程序化设计、物理筛选 **100 万** robot embodiments，并生成其仿真轨迹。
- **实验与关键结果：** 2,000 个 embodiment-scene held-out episode 成功率 **63.0%**，pi 0.5 为 **17.8%**、最强 baseline 为 **57.9%**；作者称在未见真机上接近 MolmoAct2 的两倍成功率。
- **关注价值：** 把跨本体泛化锚定到可检查的运动学条件，而不是仅靠统一 action token；适合评估硬件变化何时需要重新采集。
- **局限／跟进：** “百万形态”仍是合成分布；须披露真机数量、任务和统计区间，并测试标定偏差、关节限位、接触／动力学失配和安全停止。

### 5. [PyRUA-Dex: Learning Programmatic Policies for Dexterous Bimanual Manipulation with Coding Agents](https://arxiv.org/abs/2611.33144)

- **作者／机构／提交：** Feixiang Ruan、Guodong Lv、Kewei Zhang 等；机构未完整披露；v1，2026-11-24 18:56 UTC。
- **问题：** 灵巧双手的高质量示范稀缺：视频重定向不精确、遥操缺力反馈、外骨骼扩展困难。
- **创新与机制：** 多个 coding agents 并行探索 skill 与组合方式，distilling agent 将成功尝试压成任务库和一个程序策略；随后通过随机布局 refinement 改善鲁棒性与执行效率，无需示范训练。
- **实验与关键结果：** Bench2Dex **72.9**、完全随机化 DexJoCo **81.0%**，作者称均领先已训练策略；双 22-DoF 真机上可学钢琴、书法等，谱面到新曲最短约 **30 分钟**。
- **关注价值：** 将 agent 的代码探索产物变成可检查、可组合的控制程序，为示范稀缺任务提供不同于端到端模仿的迭代路径。
- **局限／跟进：** 成功程序的搜索成本、碰撞／超力失败、权限边界和真机试错预算仍未由摘要说明；应公开程序审查、stop rule 与跨任务复用失败率。

### 6. [iWAM: Efficient Action Prediction from World Models without Explicit Future Prediction](https://arxiv.org/abs/2611.33141)

- **作者／机构／提交：** Vansh Kapoor、Max Sobol Mark、Sreyas Venkataraman 等；机构未完整披露；v1，2026-11-24 18:56 UTC。
- **问题：** WAM 依赖视频模型生成未来来选动作，但逐帧高分辨率想象太慢，难用于实时控制。
- **创新与机制：** 利用 flow-matching 的可逆动力学把训练未来反演到噪声；学习 bidirectional flow map 摊销生成计算。推理时从 prior 采 latent，仅一次 video-backbone forward 的中间特征条件化策略，不显式渲染未来帧。
- **实验与关键结果：** 作者报告在仿真及真机上恢复 WAM 的泛化收益，同时显著降低推理开销；摘要未列统一绝对成功率、帧率或硬件配置。
- **关注价值：** 清楚区分“预测图像”和“保留动作判别信息”，是让世界模型进入快控制回路的实用方向。
- **局限／跟进：** 缺少摘要级成本与安全数字；应报告 p50/p95 时延、latent 不确定性、反事实失败例和相对显式预测的接触风险。

## 交叉方向：SLAM／长期空间智能

### 7. [GOLD-SLAM: Gaussian-splatting Omnidirectional LiDAR-Depth SLAM](https://arxiv.org/abs/2611.32335)

- **作者／机构／提交：** Weicong Zhang、Yuan Huang、Yu Zheng 等；机构未完整披露；v1，2026-11-24 10:20 UTC。
- **问题：** 全景相机近球面覆盖与 LiDAR 有限视场不匹配，使依赖 LiDAR 深度先验的全景 3DGS SLAM 出现无深度区域和增量浮点伪影。
- **创新与机制：** 在球面域跟踪／建图，用无 LiDAR 覆盖区的视觉特征改善位姿；**DAEP**（Depth-Aware Map Extension and Pruning）扩展新表面并清理浮点。作者采集 UAV **WHOLE** 数据集，覆盖弱几何、高动态、全景、低照等。
- **实验与关键结果：** 相较全景 baseline，平均 PSNR 提升 **5.56--9.10 dB**、Depth-L1 降 **71.9--83.9%**；Jetson Orin NX 16 GB 配置可在线运行，但牺牲重建质量。
- **关注价值：** 直接面向空中平台的全向观测与端侧资源，补充长期空间状态不仅要更密，也要说明观测盲区如何处理。
- **局限／跟进：** 渲染／Depth-L1 不能代替跨日重定位、回环和避障表现；应公布高动态遮挡、LiDAR失配、内存增长和嵌入式 p95 的退化曲线。

## 趋势总结

- **把“不确定／无证据”变成控制前的显式门。** DriveAnswer 的拒答能力、MemAnchorWorld 的时域检索、GeoVLDrive 的结构化几何理由都让模型说明依据何在；下一步必须验证这些门是否真实降低闭环风险。
- **具身规模化的焦点正从单一主干移向结构接口。** OmniAct 的运动学图、PyRUA-Dex 的程序技能库、iWAM 的一次前向动作特征分别连接形态、探索产物和计算预算；应共同报告试错伤害、尾延迟和可回滚性。
- **空间表征向全向、资源受限和可清理状态发展。** GOLD-SLAM 的覆盖补偿／地图修剪有助于 UAV 在线运行，但长期自治仍需跨时证据、内存上界和错误回环隔离。
