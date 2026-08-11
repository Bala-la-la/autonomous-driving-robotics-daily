# arXiv 自动驾驶与机器人晨报｜2026-08-12

说明：截至北京时间 2026-08-12 06:00，最新可用常规批次为 2026-08-10 UTC；以下 7 篇均为该批次。作者、提交日期与数字来自 arXiv 摘要页；机构未完整披露时不作推断。

## 自动驾驶

### 1. FactorDrive: Adaptive Multi-Step Reasoning Driven by Planning-Critical Factors for End-to-End Autonomous Driving
- 链接：https://arxiv.org/abs/2608.09591
- 作者／机构：Guolei Huang、Tengfei She、Yuxuan Lu 等；机构未完整披露；提交：2026-08-10。
- 问题：驾驶 VLM 的推理缺少与轨迹相关的空间物理证据，推理长度也难随场景风险自适应。
- 创新与机制：构建以 planning-critical factors 组织的 PCF-CoT 数据，以轨迹奖励引导 MCTS 搜索，再通过 QS-GRPO 优化高质量推理路径。
- 实验与关键结果：在 nuScenes 开环和 NAVSIM 闭环导向基准上报告 SOTA 规划表现；摘要未给出统一数值，仍需按基准表格复核。
- 关注价值：将“多想几步”约束到真正影响轨迹的因素与可验证规划奖励。
- 局限／跟进：CoT 可靠性、搜索成本、闭环长尾事故与奖励投机仍需真实道路验证。

### 2. DH-VLM: Dual-Horizon Cooperative Latent Reasoning for Autonomous Driving
- 链接：https://arxiv.org/abs/2608.09333
- 作者／机构：Ziyi Song、Chen Xia、Hang Yu、Sheng Zhou、Zhisheng Niu；机构未完整披露；提交：2026-08-10。
- 问题：单车感知受遮挡和视距限制，直接共享高维协同特征又增加通信、显存与延迟负担。
- 创新与机制：路侧聚合多层隐状态形成全局长时域 latent guidance，车端通过 Infrastructure-Driven Latent Evolution 在本地短时域细化并保留自主决策。
- 实验与关键结果：相对此前 SOTA，L2 误差降低 14.6%、碰撞率降低 26.9%；相对 query-based 协同驾驶，通信成本降低 57.3%、GPU 显存降低 25.5%。
- 关注价值：给出“路侧负责长视野语义、车端负责局部执行”的紧凑协同接口。
- 局限／跟进：需测试时延、丢包、恶意或失准引导，以及基础设施不可用时的降级边界。

## 机器人／具身智能

### 3. XPolicyLab: A Unified Standard and Open Ecosystem for Robot Policy Evaluation and Deployment
- 链接：https://arxiv.org/abs/2608.09892
- 作者／机构：XPolicyLab Community、Tianxing Chen、Yue Chen 等；机构未完整披露；提交：2026-08-10。
- 问题：不同策略、环境、数据格式和依赖栈形成 N×M 集成成本，妨碍可复现评测与真机部署。
- 创新与机制：标准化 observation、action、trajectory schema 与最小 adapter；以依赖隔离的 client/server 架构解耦推理和环境，使复杂度降为 O(N+M)。
- 实验与关键结果：已接入 42 个策略；代表性策略接入从超过 5 小时降至 2 小时，借助 Agent Skills 进一步降至 30 分钟，并共用适配器连接 RoboTwin、RoboDojo 与真机评测。
- 关注价值：标准接口和可复现部署可能比单一排行榜更能降低横向比较成本。
- 局限／跟进：能否覆盖高频控制、异步多传感器、触觉、安全急停和长期社区治理仍待观察。

### 4. RynnValue: Scaling Robotic Value Foundation Models with Temporal Distance
- 链接：https://arxiv.org/abs/2608.09853
- 作者／机构：Dongchi Huang、Hongyin Zhang、Bohan Hou 等；机构未完整披露；提交：2026-08-10。
- 问题：通用 reward/value model 依赖偏好或归一化进度标注，难跨任务、本体与数据源扩展。
- 创新与机制：以观测到语言目标的有向 temporal distance 作为 cost-to-go；时间戳自动产生监督，并以随机时序采样、顺序打乱和 value-isolation attention 抑制捷径。
- 实验与关键结果：使用 7,000+ 小时、约 300 万片段训练；RBM-EVAL-OOD Kendall tau_a 为 0.675，超过偏好监督 SOTA 0.655；稠密奖励使真机在线成功率从 52.5% 升至 72.5%，离线从 63.8% 升至 82.5%。
- 关注价值：把廉价时间戳转换成跨数据源的统一价值监督。
- 局限／跟进：耗时并不总等于任务价值，停顿、绕路、速度差异和安全违规可能污染标签。

### 5. SLIM-0.5B: Learning Action-Grounded Predictive Latents for Robot Manipulation
- 链接：https://arxiv.org/abs/2608.09771
- 作者／机构：Jingkai Wang、Zihan Tang、Gu Zhang 等；机构未完整披露；提交：2026-08-10。
- 问题：大 VLA 每步保留大量开放域语义容量，像素世界模型又消耗算力预测与控制无关的视觉细节。
- 创新与机制：0.5B 参数 SLIM 通过 masked trajectory prediction 联合动作重建和未来 latent 预测，Mixture-of-Transformers 建模观测—动作交互，再以 flow matching 生成语言条件动作。
- 实验与关键结果：仿真和真机中匹配或超过代表性大型 VLA/WAM，且无需额外具身预训练，推理延迟与显存更低；摘要未披露逐项数字。
- 关注价值：说明控制相关预测 latent 可在小模型中保留关键动力学，适合边缘部署。
- 局限／跟进：需检查开放词汇指令、长时任务、分布外物体和复杂接触下是否仍需大模型容量。

## 交叉方向：定位、导航与世界模型

### 6. WRAP: Wasserstein-Robust Adaptive Plug-in for Robot Localization
- 链接：https://arxiv.org/abs/2608.09807
- 作者／机构：Minhyuk Jang、Astghik Hakobyan、Jungjin Lee 等；机构未完整披露；提交：2026-08-10。
- 问题：感知条件变化会造成定位误差偏置和协方差失校准，而替换整套 EKF/ESKF 代价高。
- 创新与机制：以因果适配模块估计时变过程／测量统计，再用保持均值的 Wasserstein 更新计算最不利协方差与鲁棒增益，不改传播、残差或流形 retraction。
- 实验与关键结果：18 条未参与适配训练的 UWB–IMU 序列上，相对 nominal ESKF，adapter-only 与 WRAP 的 3D RMSE 分别降低 19.8% 和 27.4%；Jetson Orin Nano 上 UWB/GNSS 求解耗时 0.05/2.92 ms。
- 关注价值：提供可插拔、实时的定位不确定性鲁棒化路径。
- 局限／跟进：GNSS–INS 为样本内研究；半径选择、强非平稳故障和闭环一致性仍需外部验证。

### 7. Energy-Structured Latent World Models with Neural Time Fields for Physically Consistent Open-World Motion Planning
- 链接：https://arxiv.org/abs/2608.09876
- 作者／机构：Yapeng Liu、Yuanzhao Zhai、Bo Ding、Huaimin Wang、Lin Wang；机构未完整披露；提交：2026-08-10。
- 问题：普通 latent world model 把物理规律隐含在表征中，开放环境中容易生成动力学不可执行轨迹。
- 创新与机制：ELWM 在 latent 中显式携带能量与动量，以耗散和控制端口保证因果转移；PC-NTF 通过 Eikonal 方程把物理 latent 融入到达时间场。
- 实验与关键结果：0.8 秒运动预测 NRMSE 从 0.36 降至 0.29；相对 Active Neural Time Fields，导航成功率由 81.3% 升至 89.7%，SPL 由 0.64 升至 0.73，碰撞率由 12.1% 降至 5.8%。
- 关注价值：把守恒／耗散结构从软监督提升为 world model 状态结构，并直接连接可行运动规划。
- 局限／跟进：复杂接触、可变形体、未知动力学和感知误差下的适应性仍需检验。

## 趋势总结
1. 驾驶推理从自由文本 CoT 转向规划关键因子、轨迹奖励和双时域协同 latent，强调可验证性与通信效率。
2. 机器人 scaling 的新支点是接口、价值监督和控制相关 latent，共同降低数据和部署成本。
3. 世界模型与定位开始把物理结构和不确定性显式写入状态更新，而非期待大模型自行吸收全部规律。
