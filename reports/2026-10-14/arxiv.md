# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-14

## 日期与证据口径

北京时间 2026-10-14 检索 [arXiv API](https://export.arxiv.org/api/query?search_query=cat%3Acs.RO%20AND%20submittedDate%3A%5B202610090000%20TO%20202610092359%5D&start=0&max_results=100&sortBy=submittedDate&sortOrder=descending)。最新可取得的相关常规批次仍为 **2026-10-09 UTC**；以下 7 篇均为该日期此前未选论文，明确作为回溯，**不是 10 月 14 日新稿**。实验数值均为作者报告、未经独立复现；“关注价值／局限”是编辑判断。

## 自动驾驶、感知与移动自治

### 1. Beyond the Snowflakes: Disentangling Weather Effects from Confounding Meta-Factors in LiDAR Object Detection

- **论文／作者／时间**：[arXiv:2610.13891](https://arxiv.org/abs/2610.13891)；Yiming Yang、Jeremy P. Bos；v1：2026-10-09 17:38 UTC。
- **问题**：恶劣天气基准常把“雪越大、检测越差”当因果结论，但雪天同时改变目标可见点数与反射特性，可能混淆鲁棒性判断。
- **创新与机制**：在 WADS-3D、CADC 上按天气与目标级元信息细分评估，并以消融拆开空中雪粒噪声、车体积雪和点云密度；提出“积雪改变表面／反射、增加目标点数”是反向收益的候选物理解释。
- **实验与关键结果**：作者发现检测准确率会随雪强度上升而提高；分析显示雪粒负面影响被对象点数增加主导，说明宽泛天气分桶会给出误导性的鲁棒性结论。
- **关注价值／局限**：提醒驾驶感知不能把相关天气标签直接当干扰强度，数据集切分应报告对象点数等协变量；物理解释仍是假设，尚待跨传感器、车型、降雪类型的受控采集验证。

### 2. Tracking the Invisible: Self-Supervised Wheel Track Detection with Thermal-RGB Fusion

- **论文／作者／时间**：[arXiv:2610.13872](https://arxiv.org/abs/2610.13872)；Yiming Yang、Jeremy P. Bos；v1：2026-10-09 17:21 UTC。
- **问题**：白茫路面中一般可通行区域估计无法区分已有车辙；而车辙往往是已验证的附着与路径稳定线索。
- **创新与机制**：用同步 RGB 与长波红外组成四通道 RGB-I 输入，将记录 GNSS 的未来车轮轨迹反投影为自监督标注，训练网络检测雪面轮迹，并发布 ThermalTrack 数据集。
- **实验与关键结果**：作者在低纹理、近白化的雪路数据上展示轮迹检测有效性；摘要未披露统一 IoU／F1 数值，重点证据是低成本标签生成与跨可见／热成像融合。
- **关注价值／局限**：可将“可走”从纯外观分类改为具有车辆动力学含义的历史通行证据；GNSS 对齐、轮迹时效、其他车辆轨迹及冰层变化都会限制部署，不能把可见轮迹等同于当前安全轨迹。

### 3. Mapless, Stabilizing, and Anti-Stuck Flipper Control for Articulated Tracked Robots

- **论文／作者／时间**：[arXiv:2610.13838](https://arxiv.org/abs/2610.13838)；Valentýn Číhala、Pavel Sarga、Martin Pecka、Tomáš Svoboda、Karel Zimmermann；v1：2026-10-09 16:48 UTC。
- **问题**：履带翻转臂控制依赖车底高程图，而该区域观测被遮挡、只能靠里程计累积，漂移会污染控制依据。
- **创新与机制**：SAS 不建图，仅用 IMU、翻转臂关节角和短窗口“是否运动”提示，组合机身横滚／俯仰稳定项与脱困项；运动线索不累计，因此不继承积分漂移。
- **实验与关键结果**：仿真和真实障碍对比中，作者称 SAS 的通行质量可比拟 map-based SOTA；在 LiDAR 看不见的草丛圆木上，最佳地图控制器卡住，SAS 成功越过。
- **关注价值／局限**：为遮挡严重的野外移动平台提供“少状态、可退化”的控制基线；实验对象和障碍类型有限，短窗运动判断可能在湿滑、打滑或长时间悬空时失效。

## 机器人／具身智能

### 4. Dream to Remember: Continual Steering of Generalist Robot Policies with World Models

- **论文／作者／时间**：[arXiv:2610.13816](https://arxiv.org/abs/2610.13816)；Bahey Tharwat、Iman Nematollahi、Marvin Alles、Xingyuan Zhang、Akshay L. Chandra、Abhinav Valada；v1：2026-10-09 16:28 UTC。
- **问题**：连续任务适配会使全参微调或共享 steering 模块遗忘旧技能，真实回放数据又昂贵或不可得。
- **创新与机制**：D2R 冻结通用策略与世界模型，仅训练噪声 steering 模块；学习新任务时由冻结世界模型想象旧任务轨迹，作为无 replay buffer 的行为锚点。世界模型足够可信时可完全在想象中适配，否则只用它复习旧技能。
- **实验与关键结果**：CALVIN 八任务序列平均成功率从 **63.7%** 到 **74.8%**，同条件 LoRA 降至 **11.7%**；作者还报告在 Franka 上连续改进三个任务并保留先前改善。
- **关注价值／局限**：把持续学习代价限制到小接口，并明确区分“世界模型能优化新任务”与“只能做旧任务复习”；世界模型幻觉可能固化旧错误，任务切换、真实接触失败和长期累计偏差仍需安全评测。

### 5. SmolWAM: A Latent World-Action Model for Robotic Manipulation on Edge Devices

- **论文／作者／时间**：[arXiv:2610.13740](https://arxiv.org/abs/2610.13740)；Timi Owolabi、Hikmah Olawore、Frances Adelakun、Ayotomiwa Oyewumi；v1：2026-10-09 15:34 UTC。
- **问题**：视频扩散型 world-action model 的未来预测与动作能力强，但端侧难以承担完整视觉 token 和多步去噪。
- **创新与机制**：从 2B Cosmos Policy 保留预训练主干，改为单帧 latent、缓存文本 attention sink、仅用 28 层中的 12 层与 1,008 token，并以一步 rectified flow 同时读出动作和未来视觉 latent。
- **实验与关键结果**：作者称仅 **3.6 GPU-hours** 训练；400 个 LIBERO episode 成功率 **95.5%**，每 16 动作块 **57 ms**、2.3 TFLOP、2.4 GiB，较教师 **11×** 更快、**18.5×** 更少 FLOPs、**3.2×** 更少显存。
- **关注价值／局限**：给端侧世界模型提供可量化的延迟／显存接口；结果集中于 LIBERO，单帧与压缩层数是否保留遮挡、长程接触和真实安全风险尚未证明。

### 6. VLMs are Native Action Models: Unleashing the Manipulation Capabilities of VLMs with Explicit Action-Space Grounding

- **论文／作者／时间**：[arXiv:2610.12832](https://arxiv.org/abs/2610.12832)；Jingkun Yi、Shujie Zhang、Zirui Zhou、Haoxiao Wang 等；v1：2026-10-09 00:33 UTC。
- **问题**：VLA 通常另学动作 token／head，需大量机器人动作数据；纯模块化 VLM 操作又难端到端微调。
- **创新与机制**：EASG 把以 TCP 为中心的动作坐标系投影进腕部相机画面，并把连续动作表达为 VLM 原生的文本生成接口，让预训练视觉—空间推理直接看到动作语义；同一接口也可用轨迹继续微调。
- **实验与关键结果**：作者报告无需机器人动作预训练即可实现零样本操作，且跨物体位置、类别与机器人本体泛化；摘要未给出统一成功率数值。
- **关注价值／局限**：将关键瓶颈从“再训练一个动作头”转为可审计的视觉动作接口；文本化连续动作的精度、相机标定误差、时延和接触力约束仍是上真机前必须量化的边界。

## 交叉方向：世界模型规划

### 7. Sampling-based Kinodynamic Planning with World Models

- **论文／作者／时间**：[arXiv:2610.12910](https://arxiv.org/abs/2610.12910)；Yitian Gao、Hanlan Yang、Zachary Kingston；v1：2026-10-09 03:01 UTC。
- **问题**：CEM、MPPI 等优化器会在长时任务中陷入只奖励眼前进展的局部解，例如需要先绕开障碍再推物体的动作。
- **创新与机制**：以视觉世界模型作 latent-space tree search 的传播器，将 RRT 最近邻引导和 KPIECE 投影探索移植到高维 latent，并用 GPU 批量扩展树节点。
- **实验与关键结果**：在四个仿真域及真实推块任务中，作者称相对 CEM／MPPI 以最高 **13.8×** 更低规划时间达到或超过成功率，真机成功率提高 **20%**。
- **关注价值／局限**：为世界模型补上可解释的“搜索中间状态”能力，适合长程重排与导航；latent 距离和世界模型 rollout 的物理偏差会决定树是否扩到真实可达状态，真机样本规模仍有限。

## 趋势总结

- **退化环境的证据需要拆因果而非加标签**：雪天 LiDAR 与热成像车辙均把天气、表面、点密度和历史通行从一个“雪”标签中拆开；安全报告应同时给协变量、时效与误判代价。
- **世界模型正分成持续记忆、端侧预算和规划搜索三个接口**：D2R、SmolWAM、kinodynamic tree search 分别处理遗忘、算力与长程探索；它们的共同前提是模型误差要被显式审计，而非仅展示平均成功率。
- **动作语义逐步向可观察接口靠拢**：SAS 用局部运动证据摆脱漂移地图，EASG 把动作坐标可视化给 VLM；下一步应报告接口在标定、时延、接触与 OOD 下何时不再可信。
