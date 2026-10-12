# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-13

## 日期与证据口径

北京时间 2026-10-13 检索 [arXiv API](https://export.arxiv.org/api/query?search_query=cat%3Acs.RO%20OR%20cat%3Acs.AI%20OR%20cat%3Acs.CV&start=0&max_results=100&sortBy=submittedDate&sortOrder=descending)。周末后可取得的最新相关常规批次为 **2026-10-09 UTC**；以下 7 篇均为该日新提交，明确作为回溯，**不是 10 月 13 日新稿**。实验数值均为作者报告、未经独立复现；“关注价值／局限”是编辑判断。

## 自动驾驶、规划与长期自治

### 1. SimVTA: Simulation-Grounded Video-Trajectory Alignment for Driving World Action Models

- **论文／作者／时间**：[arXiv:2610.13781](https://arxiv.org/abs/2610.13781)；Changhui Jing、Haochen Tian、Hongchen Li、Hao Zhao 等；v1：2026-10-09 16:01 UTC。
- **问题**：驾驶世界动作模型在 RL 后训练时会探索日志中不存在的候选轨迹，因而没有与这些轨迹匹配的未来视频监督。
- **创新与机制**：SimVTA 在 3D Gaussian Splatting 重建的真实场景中，以 World Engine 等模拟器渲染高奖励候选轨迹的未来视频；按预测误差优先分配有限渲染预算，并以 GRPO 轨迹优化和 flow-matching 视频损失共同更新表征。
- **实验与关键结果**：作者报告 NAVSIM v1 PDMS 从 **86.2 升至 91.3（+5.1）**，NAVSIM v2 为 **88.2 EPDMS**，HUGSIM 闭环平均 HD-Score 为 **38.8**；推理时不调用模拟器。
- **关注价值／局限**：将“探索到的驾驶动作”重新接回可视未来证据，适合闭环后训练；收益依赖重建、渲染与奖励是否覆盖长尾交互，仿真视频误差仍可能反向塑形策略。

### 2. When LiDAR Fades, Radar Takes Over: LiDAR Reliability-Aware Adaptive Localization Under Airborne Obscurants

- **论文／作者／时间**：[arXiv:2610.13788](https://arxiv.org/abs/2610.13788)；Moumita Mukherjee、Avijit Banerjee、Anton Koval、George Nikolakopoulos；v1：2026-10-09 16:04 UTC。
- **问题**：烟尘等空气遮挡会使 LiDAR-inertial odometry 在 GNSS 拒止地下环境中突然失效，而雷达往往更耐受。
- **创新与机制**：以仅在健康运行数据上训练的滑窗 LSTM autoencoder 建模空间、跨模态、几何／运动、强度与测量新鲜度特征；异常分数生成 LiDAR 可靠度，并在 LIO 与 radar-inertial odometry 间切换定位权。
- **实验与关键结果**：作者在真实地下隧道的正常与浓烟地面机器人数据中展示退化检测、模态切换和严重退化下持续输出；特征族消融显示，在该浓烟场景中较精简的表示反而改善定位。
- **关注价值／局限**：把传感器失效检测直接连接到冗余定位执行；目前未给出跨粉尘类型、速度、雷达干扰及切换误报代价的广泛定量安全边界。

## 机器人／具身智能

### 3. Splat2Act: From Captured Scenes to Personalized VLA Manipulation

- **论文／作者／时间**：[arXiv:2610.13945](https://arxiv.org/abs/2610.13945)；Xiaomeng Ye、Krishna Jaganathan、Gyubeum Lim、Zsolt Kira 等；v1：2026-10-09 17:59 UTC。
- **问题**：通用 VLA 在用户家居／办公室中面对私人物品与布局常失效，逐场景采集真机示范成本很高。
- **创新与机制**：仅用手持手机扫描和物体图像构建含碰撞几何的建筑级 3DGS 数字孪生，自动找容器、生成抓取任务，并以特权模拟 oracle 合成示范；两阶段微调先适应公共资产、再适应用户物体与摆放。
- **实验与关键结果**：101 个扫描校园环境（中位可通行面积 **104.87 m²**）产生 852 个容器与逾 **68,000** 条示范；作者报告目标场景聚合抓取成功率 **62.5%**，Stretch 3 的 12 任务真机子集为 **63.9%**，仿真为 **66.7%**。
- **关注价值／局限**：把场景个性化从人工遥操移到可复用采集—仿真管线；scan 质量、物体物理参数、动态家居环境与 12 项真机任务外的泛化仍需检验。

### 4. Noise Space Learning for VLA Adaptation

- **论文／作者／时间**：[arXiv:2610.13943](https://arxiv.org/abs/2610.13943)；Junjie Lu、Chuheng Zhang、Yucen Wang、Li Zhao 等；v1：2026-10-09 17:58 UTC。
- **问题**：把预训练 flow-matching VLA 适配到具体任务时，直接调模型既消耗机器人交互与算力，也难维持部署安全约束。
- **创新与机制**：冻结 VLA 主干，只学习上下文条件化的噪声分布；以该“噪声接口”承载 PPO、SAC、AWR 等不同学习算法，并给出信息论分析解释适配效率。
- **实验与关键结果**：在 LIBERO、RoboTwin 和 4 个真机操作任务、不同交互／算力／执行限制下比较多个 NSL 变体，作者给出按资源与部署条件选算法的经验建议；摘要未披露统一单一百分比增益。
- **关注价值／局限**：为低风险、小预算在线适配提供比全参微调更窄的改动面；噪声空间的可控性不等于动作安全，真实失败恢复、OOD 目标和长期遗忘需单独报告。

### 5. Chronos Policy: Learning Robot Policies on Physical Time

- **论文／作者／时间**：[arXiv:2610.13929](https://arxiv.org/abs/2610.13929)；Changhao Wang、Jaden Clark、Shuran Song；v1：2026-10-09 17:55 UTC。
- **问题**：将感知—控制压到固定频率 token 序列，会在传感异步、动作延迟或推理时延变化时失真。
- **创新与机制**：把观测采集时刻与目标动作执行时刻显式条件化进 diffusion transformer；比较 timestamp embedding 与 time-aware RoPE，并在训练中随机化观测采样和 action chunk 起点。
- **实验与关键结果**：作者称 time-aware RoPE 更稳健；在仿真与真机动态、多传感任务上优于固定时间网格，同时在准静态任务保持标称表现并提升时序变化鲁棒性。
- **关注价值／局限**：时间戳可成为多速率机器人系统的标准策略接口；摘要未给出任务级幅度，硬件时钟同步误差和极端网络抖动下的退化曲线仍是部署关键。

### 6. BT-Agent: Deploying Onboard Robot Agents with Behavior Trees and Multi-Fidelity Evaluation

- **论文／作者／时间**：[arXiv:2610.13862](https://arxiv.org/abs/2610.13862)；Fabio Hübel、Adam Lilja、Yue Yin、Claire Tomlin、Marco Pavone 等；v1：2026-10-09 17:08 UTC。
- **问题**：移动机器人上的语言 Agent 既要在有限板载资源内决策，也必须在导航异常时即时停止，不能等下一轮模型推理。
- **创新与机制**：LLM 负责任务层决策，预定义行为树技能负责前置条件、执行与结构化失败反馈；建立 161 任务多保真评测，文本全量筛选、Habitat 对 39 项做具身验证。
- **实验与关键结果**：9B 模型在四足机器人上完成 5 类任务；文本评测吞吐是仿真的 **10.9×**，相对最强 Act/ReAct 基线，4B／9B 时最大成功率约提升 **10／5 个百分点**。
- **关注价值／局限**：把高层 Agent 与可即时拦截的本地控制合同分开，利于安全审计；行为树技能覆盖决定上限，文本到仿真的筛选可能漏掉视觉、运动与接触失败。

## 交叉方向：3D／导航

### 7. HorizonNav: Geometry-Guided Video Diffusion for Anticipatory 3D Robot Navigation

- **论文／作者／时间**：[arXiv:2610.13849](https://arxiv.org/abs/2610.13849)；Hajira Amjad、Valerii Serpiva、Viacheslav Liubimov、Dzmitry Tsetserukou 等；v1：2026-10-09 16:57 UTC。
- **问题**：仅由单张 RGB 想象未见空间时，视频扩散的时间连贯并不保证深度与碰撞几何一致，规划会把生成幻觉当可通行区域。
- **创新与机制**：VLM 将文本目标转为视频扩散提示，再用 ORB-SLAM3 相机位姿、Video Depth Anything 深度和三角化地标作 geometry-guided depth alignment，最后在想象 3D 空间中运行 RRT。
- **实验与关键结果**：19 场景中可规划场景从 P20 的 **13/19** 到 P81 的 **15/19**，成功 RRT 从 **62/90** 到 **75/90**；25 条可评轨迹中 6 条违反重建碰撞约束，RRT 修复其中 5 条，15 条走廊重建平均地标误差约 **0.30 m**。
- **关注价值／局限**：没有 LiDAR 时仍主动暴露可行性与碰撞失败，而非只展示视频；其安全性受视频先验、单目尺度和静态走廊评估限制，不能作为真实避障保证。

## 趋势总结

- **世界模型开始接收“轨迹对齐的证据”而非只生成好看的未来**：SimVTA 将高奖励动作配回模拟视频，HorizonNav 则把生成视频再压回多视几何约束；两者都应按罕见风险和重建误差审计。
- **部署接口正在显式化为可靠度、时间与技能合同**：LiDAR／雷达切换、Chronos 的物理时间编码、BT-Agent 的行为树守卫，共同把不可控隐状态拆为可监测、可中止的运行时变量。
- **个性化与适配强调少改主干、少采真机**：Splat2Act 用捕获场景合成数据，NSL 冻结 VLA 改造噪声分布；下一步不是只比较成功率，而是核验动态环境、OOD 和失败恢复的成本。
