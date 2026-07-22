# arXiv 自动驾驶与机器人晨报｜2026-07-23

说明：截至北京时间 2026-07-23 06:00，arXiv `cs.RO` 已出现 2026-07-21（UTC）提交的新批次。以下 5 篇来自 7 月 21 日，另 2 篇明确回溯至 7 月 20 日以补足机器人操作方向；没有把旧稿冒充今日更新。机构信息未在摘要页披露时不作推断。

## 自动驾驶

### 1. Cognitive Dual-Process Planning for Autonomous Driving with Structured Scene Knowledge and Verifiable Reasoning-Action Consistency

- 链接：https://arxiv.org/abs/2607.19194
- 作者：Zhongyao Yang、Haoyu Li、Yu Yan、Zhuangxuan Yu、Jiangfeng Nan、Jinrui Nan；提交：2026-07-21；机构：摘要页未披露。
- 问题：驾驶 VLM 的逐场景慢推理延迟高，自动生成的推理监督又可能与最终动作自相矛盾。
- 创新与机制：用机器可解析的结构化思维链表达规划知识；视觉 Arbiter 在语言解码前判断复杂度，将普通场景送入快速元动作路径、复杂场景送入慢推理路径。规则验证器检查结构化字段与动作的一致性，并把可验证奖励用于 GRPO。
- 实验与关键结果：195 个场景人工审计中，自动标注的 CoT 准确率为 91.8%、逻辑一致性为 98.5%；574 个 NAVSIM 人工核验样本上，规划准确率 80.14%、一致性 97.20%，比全量慢推理平均降延迟 17.39%。
- 关注价值：它把“是否需要推理”和“推理是否支持动作”拆成可测模块，路线比只追求更长 CoT 更接近部署需求。
- 局限／跟进：外部长尾子集上路由和规划仍会退化；需查看快速路径漏判关键场景的安全代价，以及规则验证覆盖不了的隐含因果错误。

### 2. Stochastic Multi-Objective Kinodynamic Planning Against Adversaries

- 链接：https://arxiv.org/abs/2607.19284
- 作者：Thomas Marshall Vielmetti、Daniel Cherenson、Dimitra Panagou；提交：2026-07-21；机构：摘要页未披露。
- 问题：传统机会约束规划按开环轨迹估计风险，无法计入自车对随机对手的闭环反应，容易过度保守。
- 创新与机制：SMO-RRT 在闭环策略序列空间建树，用 Monte Carlo 粒子 rollout 将风险评价直接嵌入扩展过程；SMO-SST 以稀疏剪枝换取数值效率。两者联合搜索执行成本与违规概率的 Pareto 前沿，并给出非高斯、状态相关不确定性下的有限样本风险界。
- 实验与关键结果：论文给出 SMO-RRT 概率完备性及有限样本安全界，摘要未披露具体仿真胜率或耗时提升。
- 关注价值：对自动驾驶、多智能体和社交导航而言，风险不再是固定轨迹的附加分数，而是随反馈策略变化的规划变量。
- 局限／跟进：粒子估计在稀有高后果事件上可能需要大量样本；SMO-SST 的剪枝会放弃完备性，仍需核对高维系统实时性。

## 机器人／具身智能

### 3. Masked Visual Actions for Unified World Modeling

- 链接：https://arxiv.org/abs/2607.19343
- 作者：Hadi Alzayer、Wenlong Huang、Haonan Chen、Christopher Luey、Lvmin Zhang、Maneesh Agrawala、Gordon Wetzstein、Li Fei-Fei、Yilun Du、Jiajun Wu、Jia-Bin Huang；提交：2026-07-21；机构：摘要页未披露。
- 问题：视频模型拥有丰富交互先验，但机器人动作通常处在关节或控制空间，与模型学习到的像素运动表征不对齐。
- 创新与机制：Masked Visual Actions 把动作表示为视频中任意实体被部分揭示的像素轨迹。揭示机器人运动时，同一模型预测环境响应；揭示目标物体运动时，模型反推出实现结果的机器人行为，因而统一正向动力学与逆向动作生成。
- 实验与关键结果：仅用真实与仿真视频中 15 小时的 masked 样本微调，一个 checkpoint 即覆盖多场景、多 embodiment；生成 rollout 能关联真实执行结果、排序候选未来改善模型规划，并从目标物体运动合成机器人动作。摘要未给成功率绝对值。
- 关注价值：视觉空间成为跨机器人形态的动作接口，可能减少为每种本体重建 action tokenizer 的成本。
- 局限／跟进：像素轨迹不直接保证动力学可行和力控制精度；需看遮挡、相机变化及接触丰富任务中的闭环误差。

### 4. Patch Policy: Efficient Embodied Control via Dense Visual Representations

- 链接：https://arxiv.org/abs/2607.18236
- 作者：Gaoyue Zhou、Zichen Jeff Cui、Ada Langford、Bowen Tan、Yann LeCun、Lerrel Pinto；提交：2026-07-20（最近 3 日回溯）。
- 问题：全局视觉 token 丢失细粒度空间信息，而完整 VLA 又给高频控制带来过大的参数与延迟成本。
- 创新与机制：策略直接消费预训练 ViT 的密集 patch token，通过 block-causal attention 同时允许单帧内部充分交互并保持跨时间因果性，不必挂载十亿参数级 VLM。
- 实验与关键结果：在 4 套仿真和 3 套真机环境中，相对使用先进全局池化表征的策略提升 40%；比微调 OpenVLA-OFT 高 18%，参数量约为其 0.7%。
- 关注价值：说明机器人策略可直接继承视觉表征学习进展，而不必把语言模型成本一并带入控制回路。
- 局限／跟进：需核对不同 ViT、相机数量与遮挡条件下的收益，以及大量 patch 对高频长序列的显存增长。

### 5. FM-VLA: Force-based Memory for Vision-Language-Action Models in Contact-Rich Manipulation

- 链接：https://arxiv.org/abs/2607.18231
- 作者：Ruicheng Li、Qixiu Li、Ruichun Ma、Yu Deng、Lin Luo、Zhiying Du、Jianfeng Xiang、Huizhi Liang、Ruicheng Wang、Jiaolong Yang、Baining Guo；提交：2026-07-20（最近 3 日回溯）。
- 问题：重复按键、擦拭计数等非马尔可夫接触任务，视觉历史既昂贵，也难区分幅度很小但语义不同的接触事件。
- 创新与机制：先用 VAE 从力时序重建中学习紧凑力记忆，再把力潜变量与短状态历史投影为 action expert 的条件 token，以低额外开销累计接触事件。
- 实验与关键结果：在寻找隐藏积木、按键和指定次数擦盘三类记忆任务上成功率超过 80%，显著优于基线，且摘要称推理开销很小。
- 关注价值：记忆不再等于缓存更多图像；按任务选择低带宽、信息密度高的传感历史，是 VLA 工程化的重要方向。
- 局限／跟进：仅覆盖三类任务；力传感器漂移、本体接触耦合及跨硬件迁移仍待验证。

## 交叉方向：导航／规划／长期自治

### 6. From Distances to Trajectories: Real-Time Signed Distance Function Mapping and Distance-Accelerated Motion Planning for UAVs

- 链接：https://arxiv.org/abs/2607.19306
- 作者：Jason Stanley、Zhirui Dai、Qihao Qian、Tzu-Chin Ho、Tianxing Fan、Siddharth Saha、Christopher Barngrover、Ki Myung Brian Lee、Nikolay Atanasov；提交：2026-07-21；机构：摘要页未披露。
- 问题：无人机常把地图与规划分开优化，二值占据图又丢失到障碍物的连续距离信息，限制机载实时性。
- 创新与机制：OREN 用显式八叉树先验加隐式神经残差在线重建可微 SDF；Bubble* 利用距离场生长最大无碰撞球，以球图搜索生成安全走廊，并给出终止、完备和失败检测保证。
- 实验与关键结果：真机机载飞行中，OREN 相对基线改善 SDF 估计 22%；Bubble* 在拥挤环境中对约 90 米轨迹用时 1–3 秒，基线最高需 10 秒。
- 关注价值：地图与规划围绕同一连续距离表征协同设计，量化结果也直接落在机载计算预算和长距离路径上。
- 局限／跟进：需检查快速动态障碍、点云退化和八叉树分辨率切换时的安全保证是否仍成立。

### 7. No Training, Better Flights: Test-Time Scaled VLMs for UAV Navigation

- 链接：https://arxiv.org/abs/2607.19288
- 作者：Feinan Cheng、Dongliang Xu、Wenli Nong、Zhiheng Zhang、Ang Liu、Tianyu Wang、Yue Yao；提交：2026-07-21；机构：摘要页未披露。
- 问题：UAV 视觉语言导航通常只做一次推理，复杂场景下容易形成次优或不安全轨迹。
- 创新与机制：冻结 VLM，先并行生成多个候选，再迭代自纠；以安全、目标一致性和前向进展组成多指标评分选择修正后的计划，无需再训练。
- 实验与关键结果：摘要报告该方法在 UAV VLN 上达到 SOTA，但没有给出数据集、绝对指标或推理成本。
- 关注价值：它把 test-time scaling 从语言推理迁移到空间规划，并显式把安全纳入候选选择。
- 局限／跟进：缺少量化延迟与能耗；多候选推理在机载算力下可能抵消无需训练的优势，自评偏差也可能让错误候选共同强化。

## 趋势总结

1. 机器人世界模型正在寻找比关节向量更通用的动作接口：Masked Visual Actions 用像素轨迹统一正向预测与逆向控制，重点从“生成视频”转向“用生成结果做选择”。
2. 模型规模与控制频率开始解耦：Patch Policy 保留密集视觉信息但舍弃完整 VLM，FM-VLA 则用紧凑力记忆替代昂贵图像历史。
3. 可验证结构进入规划链路：驾驶双过程模型用规则检查 reasoning-action 一致性，风险界等形式工具也在把不确定性转为运行时约束。
4. 地图和规划重新围绕共同表征协同设计：OREN-Bubble* 的 SDF 既是地图产物也是搜索加速器，避免二值地图到轨迹优化之间的信息损失。
5. 测试时计算成为导航的新旋钮，但“更多候选”必须同时报告延迟、能耗和校准，否则离机载闭环仍有距离。
