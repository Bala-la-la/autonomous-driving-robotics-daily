# arXiv 自动驾驶与机器人晨报｜2026-07-24

说明：截至北京时间 2026-07-24 06:00，arXiv 已发布 2026-07-22（UTC）提交批次。本期 8 篇均来自该批次，不回填、更不把旧稿冒充当日新稿；机构信息未在摘要页披露时不作推断。

## 自动驾驶

### 1. LoRFT: Benchmarking Long-Range Vehicle Trajectory Reconstruction from Fixed Highway Cameras

- 链接：https://arxiv.org/abs/2607.19911
- 作者：Yufan Zhu、Kefu Yi、Xueju Zhang、Yunyang Tian、Long Chen、Zixuan Xiao；提交：2026-07-22；机构：摘要页未披露。
- 问题：高速公路固定摄像机中的车辆在远处会因透视压缩和尺度衰减出现轨迹碎裂，削弱交通安全分析和自动驾驶评测可用的数据长度。
- 创新与机制：发布首个面向长距离车辆轨迹重建的 LoRFT benchmark，并提出 Map-RSTNet，在道路几何对齐状态空间中做残差序列预测，解码时动态刷新局部道路几何。
- 实验与关键结果：数据集含 22 个高速场景、366,109 帧、6,601 条人工核验轨迹、2,694,889 个框及道路几何标注；相对最强基线，ADE、FDE 和 5 秒 RMSE 分别下降 11.0%、15.4% 和 10.5%。
- 关注价值：它不是继续堆近场检测，而是系统补足现有路侧基础设施最容易丢失的远场时空证据。
- 局限／跟进：当前任务是离线轨迹续接；需验证雨夜、遮挡、摄像机抖动及跨道路拓扑泛化，并防止几何先验把异常驾驶强行投影回常规车道。

## 机器人／具身智能

### 2. Closing the Lab-to-Store Gap: A Data-Efficient Post-Training and Experience-Driven Learning VLA Framework for Retail Humanoids

- 链接：https://arxiv.org/abs/2607.20345
- 作者：Roger Sala Sisó、Tiago Silvério、Jakob Sand、Tran Nguyen Le；提交：2026-07-22；机构：摘要页未披露。
- 问题：人形 VLA 在基准上有效，却常因控制频率不匹配、数据噪声和真实环境分布偏移在门店任务中失败。
- 创新与机制：DEED 围绕 GR00T N1.6 构建数据高效后训练流程，包括控制频率对齐、数据筛选、任务相关视觉高亮和降低 VLA 依赖；再以文本 advantage prefix、视觉语言价值函数和潜空间诊断做经验驱动修正。
- 实验与关键结果：在 Unitree G1-Edu 超市薯片补货任务中，仅用单 GPU，把朴素微调下失败的策略转为可完成真实任务的系统；摘要未给绝对成功率。
- 关注价值：结论把“实验室到门店”的瓶颈从新架构转向数据、频率、诊断和部署集成，更贴近机器人落地团队的真实成本结构。
- 局限／跟进：目前只验证单一补货任务；需补充多门店、长班次、货架变化和人工干预率，以及经验修正是否会遗忘已有技能。

### 3. SeededGrasp: Language-Guided Grasping in Complex Scenes with Multiple Embodiments

- 链接：https://arxiv.org/abs/2607.20207
- 作者：Yang Xu、Gurpreet Singh Mukker、Raymond Wang、Jasper Gerigk、Maria Attarian、Igor Gilitschenski；提交：2026-07-22；机构：摘要页未披露。
- 问题：VLM 擅长理解语言意图，却缺少精细 3D 抓取几何；端到端联合训练又昂贵且难扩展到多种机器人本体。
- 创新与机制：让 VLM 只预测语义 seed point，再由轻量抓取生成器完成低层几何执行，把高层语义与低层控制解耦；同时发布含 250 万以上杂乱场景抓取的首个多本体桌面数据集。
- 实验与关键结果：仿真抓取成功率 72%，真机成功率 78%，均优于文中对比基线。
- 关注价值：seed point 是比完整动作更轻的跨模型接口，既保留语言可指定性，也避免让 VLM 直接承担毫米级姿态回归。
- 局限／跟进：单点条件可能不足以表达双臂协同、接触序列与可达性约束；需看未见物体、透明反光材质和移动目标上的性能。

### 4. Evolving Cache Schedules for Fast Diffusion Policy Inference

- 链接：https://arxiv.org/abs/2607.20293
- 作者：Siying Wang、Kangye Ji、Di Wang、Fei Cheng；提交：2026-07-22；机构：摘要页未披露。
- 问题：扩散策略反复去噪动作块，闭环性能强但推理成本高；统一缓存频率忽略不同网络块和去噪步的冗余差异。
- 创新与机制：EVO 用进化搜索在“网络块 × 去噪时刻”网格上联合寻找缓存刷新计划，以冗余感知初始化和目标条件早停控制离线搜索成本；得到的计划可直接插入预训练策略，无需再训练。
- 实验与关键结果：操作基准中基本保持完整策略性能，动作生成最高加速 8.05 倍，FLOPs 从 15.77G 降至最低 1.96G。
- 关注价值：它把实时化问题转成一次性的全局调度优化，为已训练扩散策略提供低侵入部署路径。
- 局限／跟进：最优计划可能依赖模型、硬件和任务分布；需报告搜索成本、跨任务复用性及缓存误差在长时闭环中的累积。

### 5. Diffusion ReRoll: Revisable Denoising for Robotic Sequential Prediction

- 链接：https://arxiv.org/abs/2607.19919
- 作者：Seonsoo Kim、Seongil Hong、Jun-Gill Kang；提交：2026-07-22；机构：摘要页未披露。
- 问题：常规扩散序列模型单向、单调去噪，早期已经稳定的片段无法利用后来形成的长程上下文再次修正。
- 创新与机制：ReRoll 选择性地把局部稳定区域重新加噪，让前后时段在保持局部一致性的同时反复互相修订；同一机制覆盖长时规划、动作预测和视频—动作联合建模。
- 实验与关键结果：在 OGBench PointMaze/AntMaze 中相对 Diffusion Forcing 和 Diffuser 的平均成功率分别提升 21% 和 23%；LIBERO-10 上相对 Diffusion Policy 平均提升 56.5%，分布外视频—动作一致性也最佳。
- 关注价值：它直指长时生成中“局部决定过早冻结”的结构性问题，而非仅增加模型规模或采样步数。
- 局限／跟进：重复加噪会增加推理预算；需核对绝对延迟、不同重噪区域选择策略以及安全关键动作被反复改写时的稳定性。

### 6. Towards Miniature Humanoid Tele-Loco-Manipulation Using Virtual Reality and Reinforcement Learning

- 链接：https://arxiv.org/abs/2607.20399
- 作者：Nicolas Kosanovic、Jordan Dowdy、Jean Chagas Vaz；提交：2026-07-22；机构：摘要页未披露。
- 问题：VR 上肢遥操作加 RL 下肢平衡的全身控制栈多集中在昂贵全尺寸人形，小型平台因自由度与传感器有限而缺少同类能力。
- 创新与机制：在 ROBOTIS OP3 上从零构建顺应式全身遥临控制，将上肢操作者动作与下肢行走和平衡解耦，使单人能够远程观察、移动和操作。
- 实验与关键结果：手臂运动不影响最高 0.45 m/s 行走；专家操作者平均在 10 分钟内搬运 2 个 40 g 方块并累计行走 5 m。
- 关注价值：提供了低成本研究平台上的完整 tele-loco-manipulation 基线，利于教学、数据采集和人形控制快速迭代。
- 局限／跟进：实验规模和任务复杂度有限，且依赖专家；需测试通信延迟、跌倒恢复、非专家学习曲线和更重物体的动态耦合。

## 交叉方向：规划、SLAM 与多智能体

### 7. DINS-IO: Learned Inertial Odometry via Differentiable INS Consistency

- 链接：https://arxiv.org/abs/2607.20232
- 作者：Hao Qiao、Yan Wang、Jian Kuang、Xiaoji Niu；提交：2026-07-22；机构：摘要页未披露。
- 问题：学习式惯性里程计依赖动捕、VIO 或 SLAM 提供密集高精度位置真值，数据获取成本高。
- 创新与机制：把捷联 INS 速度递推写成可微一致性约束，在滑动窗口内联合消除未知初速度和全局加速度计偏置，用闭式最小二乘残差自监督高频网络；再用少量标注轨迹和 LoRA 完成米制校准。
- 实验与关键结果：摘要称使用少量标注微调即可在标准基准上匹配或超过全监督基线，未披露具体数据集与绝对误差。
- 关注价值：把经典惯导方程变成可反传的学习信号，为低成本、大规模 IMU 预训练提供了清晰路线。
- 局限／跟进：常值偏置假设可能不适应温漂和长时运行；还需验证激烈运动、不同 IMU 等级及无充分激励轨迹下的可观测性。

### 8. Distributed Motion Planning with Safety Guarantees for Self-Reconfiguring Robotic Boats

- 链接：https://arxiv.org/abs/2607.20352
- 作者：Alejandro Gonzalez-Garcia、Wei Wang、Wei Xiao、Wilm Decre、Jan Swevers、Carlo Ratti、Daniela Rus；提交：2026-07-22；机构：摘要页未披露。
- 问题：可自重构水面机器人既要分布式形成目标形状，也要在非凸、多智能体运动中实时避免碰撞。
- 创新与机制：以 ADMM 求解分布式 MPC，让各艇通过局部优化和信息交换规划协同轨迹；执行前再用分布式控制屏障函数过滤器强制满足艇间安全约束。
- 实验与关键结果：仿真扩展到 25 个智能体，并在 4 艘实体机器人上验证；摘要未给重构时间或最小间距等绝对指标。
- 关注价值：预测控制负责绕开局部极小值，CBF 负责运行时形式安全，体现“性能规划器＋安全过滤器”的可组合架构。
- 局限／跟进：真实实验规模仍小；需看水流、通信丢包、模型失配和密集接触式拼接阶段是否保持保证与实时性。

## 趋势总结

1. 具身模型的工程重点继续从“再造大模型”移向接口与系统：DEED 优化频率和数据，SeededGrasp 用语义种子连接 VLM 与几何抓取。
2. 扩散策略开始系统解决推理预算和长程可修订性：EVO 决定哪些计算可缓存，ReRoll 决定哪些已生成片段值得重新打开。
3. 经典机器人结构正在变成学习系统的约束和安全层：DINS-IO 把惯导方程用作自监督损失，分布式机器人艇则把 MPC 与 CBF 分工组合。
4. 评测数据从近场、短时走向更真实的长尾：LoRFT 专门处理固定摄像机远场轨迹断裂，补上交通数据链中的隐性缺口。
5. 人形路线呈现高低两端并进：一端是门店级 VLA 系统集成，另一端是低成本小型平台的全身遥操作，二者都把可用性置于单项模型指标之前。
