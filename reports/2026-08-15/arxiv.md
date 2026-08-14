# arXiv 自动驾驶与机器人晨报｜2026-08-15

说明：截至北京时间 2026-08-15 06:00，最新可用常规批次为 2026-08-13 UTC；以下 8 篇均为该批次且未见于往期报告。作者、提交日期与数字来自 arXiv 摘要页；机构未完整披露时不作推断。

## 自动驾驶

### 1. FIRE-VLA: Failure-Informed Self-Evolution for Vision-Language-Action Models in Autonomous Driving
- 链接：https://arxiv.org/abs/2608.13395
- 作者／机构：Hao Dou；机构未完整披露；提交：2026-08-13。
- 问题：GRPO 在一组轨迹全部很差时只能排序失败，无法告诉策略失败区域之外应该怎么改。
- 创新与机制：低回报且低多样性 rollout 触发同尺度冻结教师；教师可见隐藏未来轨迹，学生只按自身 prefix 接收 answer-token 蒸馏，GRPO 仍作用于所有组，下一轮策略再成为新教师。
- 实验与关键结果：Qwen2.5-VL-3B、nuScenes 150 个留出场景的 6,019 个样本中，G=4 平均 L2 从 1.848 降至 1.500 m，评测持续失败率从 13.03% 降至 11.20%；收益主要来自少数严重失败 rollout。
- 关注价值：把“失败但无相对优势”的样本转成特权监督，不依赖更大的外部教师。
- 局限／跟进：隐藏未来轨迹只在训练可得；需检查闭环分布漂移、教师错误累积和真实道路安全收益。

### 2. TraVEL: Trajectory-Guided Video Embedding Learning for Driving-Video Retrieval
- 链接：https://arxiv.org/abs/2608.13495
- 作者／机构：Yi-Chung Chen、Philip Jacobson、Tom Lampo、Yiren Lu 等；机构未完整披露；提交：2026-08-13。
- 问题：通用视频 embedding 易依赖静态场景捷径，难区分左转／右转、加速／减速等运动事件。
- 创新与机制：先用 nuReasoning 的片段与推理轨迹对 Qwen3-VL-Embedding 做 InfoNCE 微调，再用 ego 轨迹相似度作为 GRPO 奖励；轨迹只作训练特权监督，检索时仍是单向量，不需要位姿、规则或额外感知。
- 实验与关键结果：相对 SFT，2B 模型纵向／横向 mAP 分别提升 9.8／4.7 个百分点，8B 提升 7.2／1.5 个百分点。
- 关注价值：把驾驶日志检索从规则堆叠转成可扩展的物理运动语义索引。
- 局限／跟进：训练轨迹质量、跨车队泛化和极少见风险事件召回仍需验证。

## 机器人／具身智能

### 3. DreamX-Phi 1.0: Action-Conditioned Video World Model for Robotic Manipulation
- 链接：https://arxiv.org/abs/2608.13489
- 作者／机构：DreamX Team、Rui Chen、Xiangxiang Chu、Geng Li 等；机构未完整披露；提交：2026-08-13。
- 问题：视频 rollout 即使看起来逼真，也可能走错手臂或丢失小物体，不能直接支持操作规划。
- 创新与机制：将每臂 SE(3) 动作以 PRoPE 几何编码注入注意力，保留手臂身份与刚体结构；增加深度分支约束场景几何，用 SAM3 mask 与冻结 V-JEPA teacher 维持抓取对象一致性，再做分布匹配蒸馏得到少步学生。
- 实验与关键结果：在 WorldArena 2.0 Challenge 获 Track 1 第一、Track 2 第二；论文称模型与代码将公开。
- 关注价值：把“动作可控、对象不漂移”置于世界模型核心，而非只追求像素逼真。
- 局限／跟进：排行榜与真实闭环之间仍有距离，需公开长时 rollout、接触失败和少步蒸馏的代价。

### 4. ContactGuard: Pre-Contact Execution Monitoring with Action-Conditioned Latent World Models
- 链接：https://arxiv.org/abs/2608.13438
- 作者／机构：Gehan Zheng、Matthew Johnson-Roberson、Weiming Zhi；机构未完整披露；提交：2026-08-13。
- 问题：腕部相机下，机器人往往在真正接触前就已推偏、漏抓或扰动物体，事后检测太晚。
- 创新与机制：以策略动作 chunk 为条件预测短时 latent 视觉后果；世界模型只预测紧凑多视角 embedding，不做像素生成；小规模标注训练 failure probe，部署时在接触前滚动并核验预测的 post-contact latent，失败则中止。
- 实验与关键结果：真实接触丰富任务中，较直接预测和 corrupted-action 消融更准确，并能迁移为在线接触前 abort 信号，不修改底层策略。
- 关注价值：提供与既有策略解耦的“动作前刹车”层，适合安全增量部署。
- 局限／跟进：短时 latent 误差、接触时刻预测和新物体迁移仍需量化最坏情况。

### 5. Decoding Task Progress from VLA Representations
- 链接：https://arxiv.org/abs/2608.13474
- 作者／机构：Atiksh Bhardwaj、Edward Weiyi Duan、Prithwish Dan、Wei-Chiu Ma、Preston Culbertson；机构未完整披露；提交：2026-08-13。
- 问题：部署中的 VLA 缺少轻量、可解释的运行时状态监控。
- 创新与机制：在线性 probe 读取 π0.5 residual stream 中的任务进度（轨迹剩余时间归一化）；信号在机器人数据训练前的 PaliGemma backbone 已存在，多 prompt 训练后可泛化到未见任务并响应语言反事实。
- 实验与关键结果：probe 可作为无标签 OOD 检测器识别任务停滞，效果与 SOTA 方法竞争；但不能有效 steering 策略。
- 关注价值：把基础模型内部可读语义量变成低成本观测仪表，而不是再训练一个大监控器。
- 局限／跟进：线性可读不等于因果可控；需检验不同本体、传感器故障和长时任务的校准。

### 6. NestDex: Nested Policy Learning with Copilot Assisted Teleoperation for Dexterous Manipulation
- 链接：https://arxiv.org/abs/2608.13362
- 作者／机构：James Zhao、Jinhe Tang、Mingyuan Ba、Weiming Zhi；机构未完整披露；提交：2026-08-13。
- 问题：灵巧手示教要求操作者持续协调手臂与接触丰富的手指轨迹，数据难稳定采集。
- 创新与机制：内层手技能根据本体历史自适应，操作者用单自由度 clutch 调节激活技能；VLM selector 按任务阶段选技能，外层 visuomotor policy 学习部署时无需内层策略的完整控制；手动作 VAE 压缩目标，臂动作保留关节空间。
- 实验与关键结果：真实灵巧操作中提高示教可靠性与效率，并支持自主策略学习；摘要未给统一提升数字。
- 关注价值：将人类示教的高频手指负担变成可复用技能接口，降低灵巧数据门槛。
- 局限／跟进：技能库覆盖、VLM 误选、不同手型和接触安全边界需更广验证。

## 交叉方向：主动学习与多智能体安全

### 7. Deliberate Practice: Learning Robot Skills under a Budget
- 链接：https://arxiv.org/abs/2608.13415
- 作者／机构：Shivam Vats、Sudarshan Harithas、Mete Tuluhan Akbulut、Arvind Raghunathan、George Konidaris；机构未完整披露；提交：2026-08-13。
- 问题：长时任务的练习时间有限，盲目平均分配会学到暂时不能解锁高价值计划的技能。
- 创新与机制：同时估计技能掌握时间与其解锁计划的累计回报，把组合技能计划的预算最优分配化为可由通用求解器精确求解的双线性规划。
- 实验与关键结果：仿真和真实长时操作显示，DP 能在有限练习时间内优先获得有用策略，并改善长时规划；摘要未披露统一成功率数字。
- 关注价值：把“机器人该练什么”从启发式课程设计提升为可解释的资源分配问题。
- 局限／跟进：掌握时间估计误差、技能间负迁移和真实练习成本需在更大任务库中评估。

### 8. Safety-Critical Control for Quadrotor UAVs via Decentralized Navigation Functions
- 链接：https://arxiv.org/abs/2608.13507
- 作者／机构：Omayra Yago Nieto、Alexandre Anahory Simoes、Leonardo Colombo；机构未完整披露；提交：2026-08-13。
- 问题：分散导航函数产生全驱动平移参考力，但四旋翼只能沿机体竖直轴产生推力，直接执行会破坏安全保证。
- 创新与机制：构造推力—姿态实现并量化其相对全驱动参考的误差，再用聚合 robust HOCBF-QP safety filter 最小修改名义推力，在学习模型不确定性下以高概率保证机间避碰。
- 实验与关键结果：摘要给出高概率 pairwise collision avoidance 保证，但未披露统一实飞或仿真数字。
- 关注价值：连接分散导航、欠驱动执行和形式安全过滤器，适用于多无人机协同部署。
- 局限／跟进：概率界依赖不确定性模型；需报告通信丢包、密集编队、姿态饱和和真实飞行验证。

## 趋势总结
1. 驾驶研究把失败轨迹和运动轨迹变成训练信号：前者修复稀有严重 rollout，后者让日志检索关注真实运动而非静态外观。
2. 机器人世界模型和 VLA 正形成“预测—监控—中止”链条，latent 几何、任务进度和接触前后果都成为可观测接口。
3. 数据与算力预算被显式优化：灵巧示教用嵌套技能减负，主动练习用双线性规划选技能，多无人机则把不确定性和安全过滤写入执行层。
