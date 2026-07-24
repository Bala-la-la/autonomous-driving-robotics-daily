# arXiv 自动驾驶与机器人晨报｜2026-07-25

说明：截至北京时间 2026-07-25 06:00，arXiv 已发布 2026-07-23（UTC）提交批次。本期 7 篇均来自该批次，不回填、不重复上一期选题；机构信息未在摘要页披露时不作推断。

## 自动驾驶

### 1. Boosting Robustness for All-Weather Self-Supervised Depth Estimation in Autonomous Driving

- 链接：https://arxiv.org/abs/2607.21526
- 作者：Mengshi Qi、Xiaoyang Bi、Xianlin Zhang、Huadong Ma；提交：2026-07-23；机构：摘要页未披露。
- 问题：雨雪雾等天气会破坏自监督深度所依赖的像素对应关系，而雷达在相机视角中又过于稀疏，导致恶劣天气下的单目深度不稳定。
- 创新与机制：以无配对真实全天候数据做自训练；不确定性感知多教师蒸馏按教师可靠度加权知识，并用相机像素射线约束连接 POV 与 BEV 雷达表征，利用更密集的雷达点。
- 实验与关键结果：摘要称在多个全天候数据集上取得 SOTA，代码与模型已开放；摘要未给绝对误差和相对提升幅度。
- 关注价值：把恶劣天气域适配与雷达几何融合放在同一训练链路，减少对成对晴天／恶劣天气数据的依赖。
- 局限／跟进：需核对各天气、距离段和传感器配置的分项结果，以及教师在罕见天气中共同失效时不确定性是否可靠。

### 2. Compact Latent Coordination for Autonomous Vehicles at Unsignalized Intersections

- 链接：https://arxiv.org/abs/2607.21488
- 作者：Gil Lifshits、Igal Bilik、Gilad Katz；提交：2026-07-23；机构：摘要页未披露。
- 问题：无信号交叉口的多车强化学习容易遭遇组合动作空间、特权全局信息依赖和固定智能体数量等问题。
- 创新与机制：MAPS 让中心 Master 生成紧凑连续的 proto-plan 表达全局协调策略，分布式 Worker 再结合本车观测执行控制，使战略意图与战术动作可独立优化。
- 实验与关键结果：在 HighwayEnv 的 72 种路口配置中实现无碰撞通行并缩短平均旅行时间；用 3 车训练的系统零样本部署到 5 车时成功率为 94%。
- 关注价值：它探索的不是传输完整轨迹或动作，而是广播一个可复用的低维协调意图，可能降低多车规模扩展的通信与决策复杂度。
- 局限／跟进：目前仅为仿真概念验证；需评估混合人类驾驶、通信延迟、Master 单点故障及 proto-plan 的可解释与安全约束。

## 机器人／具身智能

### 3. AXIS: A Growable Community-Driven Data Engine for Scalable Robot Manipulation

- 链接：https://arxiv.org/abs/2607.21588
- 作者：Mengfei Zhao、Dihong Huang、Yikai Tang、Peihao Li、Mingxuan Yan、Ruiqi Zhuang、Yanjia Huang、Jie Wang、Hai Zhai、Tony Zhou、Rui Zhang、Zhexi Luo、Yuchen Huang、Jianfei Yang、Jiachen Li；提交：2026-07-23；机构：摘要页未披露。
- 问题：机器人示范数据通常依赖专用硬件、集中式操作员和固定任务集，规模扩大后质量控制与评测版本也难维护。
- 创新与机制：AXIS 用浏览器遥操作开放社区采集，自动生成和验证新任务，再通过成功检查、质量过滤、轨迹平滑及视觉／物理增强产出训练数据；以 task snapshot 和留出协议管理持续增长的数据。
- 实验与关键结果：当前含 207 个任务、5 万余条轨迹；持续预训练使 π0.5 总成功率提升 5.8%，相对 RoboCasa365 预训练模型高 37.3%，布局、传感器噪声和相机扰动下增益最大。
- 关注价值：贡献不只是一份静态数据集，而是从社区采集到自动质检、版本化评测和策略训练的可增长数据引擎。
- 局限／跟进：社区数据的设备偏差、任务版权与隐私、自动成功判定误差和长期版本可比性仍需审计。

### 4. Beyond Episodic Evaluation: Memory Architectural Bottlenecks in Sequential Embodied Question Answering

- 链接：https://arxiv.org/abs/2607.21571
- 作者：Zikui Cai、Kaushal Janga、Tan Dat Dao、Seungjae Lee、Shivin Dass、Mingyo Seo、Kaiyu Yue、Mintong Kang、Nandhu Pillai、Monte Hoover、Aadi Palnitkar、Ruchit Rawal、Ruijie Zheng、Bo Li、Yuke Zhu、Roberto Martín-Martín、Tom Goldstein、Furong Huang；提交：2026-07-23；机构：摘要页未披露。
- 问题：EQA 常在每个 episode 后清空状态，但真实机器人需要连续回答同一场景中的多个问题；简单保留旧记忆会遭遇语义缺失或训练／部署时间尺度错配。
- 创新与机制：比较连续多问设置中的记忆架构，指出 2D 占用图只记得走过哪里，却不保留视觉语义证据；将持续视觉观测锚定到度量 3D 几何的结构化空间记忆能形成可复用场景表征。
- 实验与关键结果：仿真中同时提高回答准确率并降低导航成本，打破准确率／效率权衡；并在真实移动机器人上验证，摘要未披露绝对数值。
- 关注价值：它把“长期记忆”从扩大文本上下文转为可查询的 3D 视觉证据层，对长期自治和具身 Agent 的系统架构更具指向性。
- 局限／跟进：需量化地图增长、遗忘与场景变化处理，并验证跨楼层、动态对象及长达数日的连续运行。

### 5. Grasp, Handover, Rotate: Bimanual Object Reorientation via Compositional Diffusion and Energy-Based Optimization

- 链接：https://arxiv.org/abs/2607.21341
- 作者：Wun Lam Yeung、Wenjun Liu、Yui Cheung Yu、Zhengyan Lambo Qin、Qijin She、Heng Li、Ziqi Wang、Ping Tan；提交：2026-07-23；机构：摘要页未披露。
- 问题：双臂重定向需联合选择抓取、交接、再抓取和运动轨迹，并同时满足碰撞、运动学与最终姿态约束。
- 创新与机制：BiCompoDiff 将预训练抓取扩散模型与双臂规划 EBM 组合，在逆扩散中注入碰撞避免、可微逆运动学平滑、交接可行性和再抓取安全的梯度，再用退火 MCMC 精修抓取姿态。
- 实验与关键结果：仿真家庭物体任务中相对强采样基线成功率高 20% 以上、关节位移衡量的轨迹平滑度最高提升 37%；真机验证显示可进行 sim-to-real 迁移。
- 关注价值：同一生成过程可以组合多个可微约束，比为每种双臂任务重训端到端策略更灵活。
- 局限／跟进：多轮采样和梯度引导可能影响实时性；需看透明／柔性物体、感知误差和动态交接中的鲁棒性。

## 交叉方向：导航、SLAM 与长期自治

### 6. VoLN: Vision-Only Long-Horizon Navigation—Paradigm, Benchmark, and Method

- 链接：https://arxiv.org/abs/2607.21400
- 作者：Jiabin Lou、Haopeng Wang、Yuanshuai Wang、Xinyu Liu、Xuxin Lv、Yuxin Guo、Lei Huang、Rongye Shi、Wenjun Wu；提交：2026-07-23；机构：摘要页未披露。
- 问题：传统 VLN 的路线级语言指令暗含方向、距离和布局先验，使评测混入了部署时未必存在的全局提示。
- 创新与机制：VoLN 只给目标视图，要求 Agent 从局部可见的场景线索在线选择路线；VoLN-UAV 含 7,210 个长航程连续 3D 飞行 episode，基线用视觉语义 token 检索、历史观测和本体状态预测短程航点。
- 实验与关键结果：五个未见环境中，Easy／Normal／Hard 成功率仅 7.4%／4.5%／1.8%，直接暴露长时证据整合、跨视角目标匹配和闭环稳定性的巨大缺口。
- 关注价值：低分在这里是有信息量的基准结果，它剥离语言路线先验，更接近 GPS 拒止开放环境中的真实视觉导航。
- 局限／跟进：当前实例集中于 UAV；需验证地面机器人、多目标搜索、动态障碍以及目标视图本身存在歧义时的可达性。

### 7. GLAM-SLAM: Real-time Gaussian Large-scale Mapping via Flow Densification and Spatial Decomposition

- 链接：https://arxiv.org/abs/2607.21416
- 作者：Panagiotis Mermigkas、Argyris Manetas、Petros Maragos；提交：2026-07-23；机构：摘要页未披露。
- 问题：现有单目 3DGS SLAM 常局限于短序列，或无法实时、显存随场景增长过快，难用于室外长时建图。
- 创新与机制：以稳健特征 SLAM 前端做轻量跟踪，稀疏 anchor grid 保持大尺度地图一致；用极线约束的 flow densification 满足高斯初始化，再把大地图分区为多场景并以局部 MLP 初始化施加空间归纳偏置。
- 实验与关键结果：在 KITTI Odometry、Oxford RobotCar 和 Málaga 长序列上，相对第二名重建质量提升 15%，同时保持实时并可扩展到更长序列。
- 关注价值：把 3DGS 的高保真地图与成熟几何跟踪解耦，直接针对室外长序列的速度和内存约束。
- 局限／跟进：摘要未给帧率、峰值显存与最长轨迹；还需评估动态交通、回环后的地图一致性和跨分区接缝。

## 趋势总结

1. 自动驾驶的鲁棒性从单传感器增强走向“不确定性蒸馏＋跨视角雷达几何”，多车协同则尝试用低维潜计划替代完整动作共享。
2. 机器人数据扩展正在产品化：AXIS 把采集、质检、增强、版本和评测连成持续增长的闭环，而不只发布一次性数据包。
3. 长期自治的关键表征愈发空间化：连续 EQA 需要锚定 3D 几何的视觉语义记忆，GLAM-SLAM 则解决这种地图在长序列中的实时与容量问题。
4. 生成式操作开始把可复用先验与显式约束组合：扩散模型负责候选分布，EBM 和可微运动学负责把双臂任务要求注入采样。
5. 新基准更愿意主动移除“隐形提示”：VoLN 不再让语言指令泄露路线结构，极低的未见环境成功率说明纯视觉长航程导航仍远未解决。
