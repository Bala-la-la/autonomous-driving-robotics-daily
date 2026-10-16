# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-17

## 日期与证据口径

北京时间 2026-10-17 检索 [arXiv API](https://export.arxiv.org/api/query?search_query=all%3Arobot&start=0&max_results=35&sortBy=submittedDate&sortOrder=descending)。以下选题均为 **2026-10-15 UTC** 首次提交；实验数字均为作者报告，未独立复现；“关注价值／局限”为编辑判断。

## 自动驾驶、预测与导航

### 1. FutureLift: Lifting Trajectory Proposals into Bidirectional Future Graphs for Motion Forecasting

- **论文／作者／时间**：[arXiv:2610.22215](https://arxiv.org/abs/2610.22215)；Daniel Grimm、J. Marius Zöllner；v1：2026-10-15 17:00 UTC。
- **问题、创新与机制**：多模态轨迹预测器会留下相关、可修正的残差，但既有 refiner 常把整条候选压缩，或按时间单向修改，后段证据无法反过来纠正前段。FutureLift 将每个候选未来表示为异构 future graph：时间节点连接历史、地图、其他 mode，以及联合预测中的其他体未来；双向时间边一次消息传递后共同输出坐标与置信度残差。
- **实验与关键结果**：在 Argoverse2、Waymo Open Motion Dataset 上为冻结候选持续改进；WOMD 标准输入比较中报告 **minADE 0.5049 m、minFDE 0.9942 m**，并有 **0.4874 Soft mAP**。**关注价值／局限**：这是能接到不同 backbone 后的结构化“预测校正层”，对多车交互有直接价值；但榜单离线误差未证明其对闭环风险、计算时延和低概率危险 mode 的校准收益。

### 2. Onboard Lightweight LLM Reasoning for Human-Aware Safe UAV Navigation

- **论文／作者／时间**：[arXiv:2610.22092](https://arxiv.org/abs/2610.22092)；Siwei Cai、Yuwei Wu、Vijay Kumar、Lifeng Zhou；v1：2026-10-15 15:43 UTC。
- **问题、创新与机制**：占据栅格将人、车、墙一律当障碍，且遮挡会丢掉人的专属安全间距。该系统以 BLIP 生成场景描述与文本条件分割，结合深度定位；Qwen-2.5-0.5B 经 RAG 和 grammar-constrained JSON 推理“类别—间距”规则。LLM 只对新类别调用、按类别缓存，物体身份跨遮挡持久化，因而不在控制临界回路内。
- **实验与关键结果**：Jetson Orin NX 感知链 **10 Hz**，LLM 回退约 **0.8 s**；Gazebo 城市场景碰撞约降 **3×**，动态落地成功率由 **34% 升至 96%**。**关注价值／局限**：展示语言推理可变成明确、缓存的规划约束；小物体远距感知、类别判断错配、缓存过期与仿真到真实人群行为仍是安全边界。

## 机器人／具身智能

### 3. Value as Memory: Online Value-Guided Post-training for General Robot Policies

- **论文／作者／时间**：[arXiv:2610.22368](https://arxiv.org/abs/2610.22368)；Wenye Yu、Yijin Chen、Kaiyi Xiong 等（含 Cewu Lu、Chuan Wen）；v1：2026-10-15 17:59 UTC。
- **问题、创新与机制**：部分可观测的长任务让单帧动作歧义，离线后训练又无法及时利用真机经验。VaM 把近期 value prediction 缓存为任务进度记忆，并将离线演示、离策略干预与在线 rollout 合并：先以 offline RL warm-up，再在稀疏奖励下自主更新。
- **实验与关键结果**：可变形与接触密集任务中，value cache 平均成功率绝对提升 **29.4%**，在线自主学习比配套离线训练高 **32.8%**；在同一梯度预算下完成 **8×** policy iteration，记录的单 step 时间低逾 **2×**。**关注价值／局限**：把 value 从训练信号变成固定长度控制状态；value 漂移、错误干预和在线探索的碰撞／恢复成本需要独立报告。

### 4. T2-z: Test-Time Optimization of Environment Latents for Robotic World Models

- **论文／作者／时间**：[arXiv:2610.22364](https://arxiv.org/abs/2610.22364)；Chenyuan Zhou、Yining Hong、Huang Huang 等（含 David Held、Li Fei-Fei、Jiajun Wu、Yejin Choi）；v1：2026-10-15 17:59 UTC。
- **问题、创新与机制**：摩擦、质量和人为规则等环境变量未必可见，世界模型遇到新环境会失配。T2-z 在 action-conditioned world model 上加紧凑 environment latent；训练交替冻结 latent 学通用动力学、冻结模型优化 latent 使结构自行涌现；测试时冻结世界模型，只从一次或数次交互优化新 latent。
- **实验与关键结果**：7 个仿真设置和 4 个真机任务中，对象预测误差从 **15.20 降至 7.00**，动作成功率从 **33.73% 升至 72.96%**，并称单条交互轨迹即可推断变量。**关注价值／局限**：以小型可适配状态连接环境变化和计划模型；测试时优化可能受噪声、局部极值和不安全探测动作影响，潜变量可解释性并非因可分离而自动成立。

### 5. CoDA: Co-Evolution of Data Engines and Action Policies

- **论文／作者／时间**：[arXiv:2610.22362](https://arxiv.org/abs/2610.22362)；Tianjiao Yu、Zhilin Ou、Yifan Shen 等；v1：2026-10-15 17:59 UTC。
- **问题、创新与机制**：生成出物理有效的仿真环境不代表它正好训练到策略失败点。CoDA 将环境构造、策略失败和学习进度写入异构记忆，由 VLM critic 的验证诊断编译为生成程序与训练程序；Text2potential 将诊断转为阶段化 potential，给 action-chunk value learning 稠密监督，同时保留最优策略的理论形状约束。
- **实验与关键结果**：四类操作任务的 OOD 成功率从 SFT 的 **5.3% 到 27.6%**，比最强闭环基线高 **9.5 个百分点**；LIBERO-Pro 在 15 轮生成—训练后，位置扰动成功由 **25% 到 84%**，指令扰动由 **1% 到 76%**。**关注价值／局限**：数据引擎终于按失败诊断而非视觉多样性自适应；critic 误诊、程序可执行性与生成分布偏置可能形成自证循环，需公开失败样本和停止条件。

### 6. Spark-0: Scaling Spatially Aligned Tactile Pretraining for Robot Dexterous Manipulation

- **论文／作者／时间**：[arXiv:2610.22342](https://arxiv.org/abs/2610.22342)；Tianxing Chen、Wenwei Lin、Chuqiao Lyu 等（含 Renjing Xu、Ping Luo、Wenbo Ding）；v1：2026-10-15 17:56 UTC。
- **问题、创新与机制**：视觉预训练难看见力、顺应性和初始滑移。Spark-0 将触觉手套生成的图像空间接触图和冻结 3D teacher 用作视觉 token 的预训练监督（推理时移除）；触觉支路则编码区域力历史与 3D taxel，条件化 action expert。HumanTouch 提供 **1,000 小时**全手人类触觉操作，SparkArena 同时含仅视觉仿真与触觉真机轨道。
- **实验与关键结果**：作者报告 SparkArena 两轨最高均值成功率、Ego Humanoid Manipulation Benchmark 八项 aggregate 第一；保留触觉监督令 vision-only 的 Ego Humanoid 成功率 **52.5%→71.7%**，真机触觉轨 **44.0%→52.0%**。**关注价值／局限**：触觉不只是部署输入，也是可规模化的视觉预训练监督；手套—机器人接触几何、材料和 taxel 标定迁移，以及大规模人类采集许可需核验。

### 7. Mem4Act: Learning Effective Latent Memory for Long-Horizon Robotic Manipulation

- **论文／作者／时间**：[arXiv:2610.22323](https://arxiv.org/abs/2610.22323)；Yun Zhang、Zhiyu Huang、Tianhui Cai 等；v1：2026-10-15 17:51 UTC。
- **问题、创新与机制**：保留原始历史会让控制输入越来越长，只压缩视觉 token 又会丢任务证据。Mem4Act 用多粒度时间聚合生成固定长度 memory，以 QA 监督保留语义、以关键帧 DINO 重建保留感知；memory-first 两阶段训练迫使策略实际使用它。
- **实验与关键结果**：RoboMME、RMBench 和四个真机操作任务的成功率分别报 **49.88%／61.0%／81.5%**。**关注价值／局限**：把长期记忆做成受限、可训练的动作接口，与今天 value cache 形成互补；固定容量在任务突变、误记和多阶段纠错下的失效证据尚需显示。

## 趋势总结

- **未来与历史都被显式结构化**：FutureLift 用未来图做残差校正，VaM 和 Mem4Act 把进度／历史压缩成控制状态；接下来应同时量化精度、记忆污染和端到端时延。
- **世界模型走向测试时环境适配与失败驱动数据闭环**：T2-z 以低维 latent 解释环境差异，CoDA 以诊断重排数据预算；两者的关键风险都是错误归因后的自强化。
- **部署约束进入学习目标**：Spark-0 用触觉作可迁移监督，UAV 系统把 LLM 推理降为缓存的非关键路径约束；高分不应替代传感器偏差、权限、回退和真机安全曲线。
