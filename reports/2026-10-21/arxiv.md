# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-21

## 日期与证据口径

截至北京时间 2026-10-21，arXiv API 可核验的最新相关批次为 **2026-10-19 UTC 首次提交、10 月 20 日公告**。以下论文均来自该批次；实验数字来自作者摘要，价值与局限为编辑判断。

## 自动驾驶与导航

### 1. [Drive2Gauss: FeedForward 4D Gaussian Reconstruction from Multimodal Generative Driving Videos](https://arxiv.org/abs/2610.26585)

- **作者与时间：** Tong Zhao、Zhiyuan Han、Lin Chen、Bowen Xie、Yunxi Qiao；v1 2026-10-19 15:34 UTC。
- **问题与创新：** 生成式驾驶视频若要成为可复用环境，还需显式、可换视角的动态场景；以往从视频恢复 4D 场景要逐序列优化。Drive2Gauss 将生成 RGB、度量深度和动态光流直接转成动态 4D Gaussian。
- **机制／结构：** 多模态视频生成器根据多视角参考和未来控制信号生成三种模态；Gaussian Query Decoder 用深度初始化稀疏 3D query、用光流跨时关联，再做时空特征聚合与迭代细化，单次前馈完成重建。
- **实验与关键结果：** nuScenes 上未来 RGB 的 FID **6.38**、FVD **12.43**，生成观测重建 PSNR **29.91 dB**，并支持横向相机偏移渲染及下游视频修复。
- **关注价值／局限：** 将驾驶世界模型输出变成可规划的显式场景；生成深度/流的系统误差、长时滚动漂移和闭环碰撞有效性仍需验证。

### 2. [CAOS-SLAM: Class-Agnostic Object-Aware Real-Time vSLAM for Dynamic Environments](https://arxiv.org/abs/2610.26633)

- **作者与时间：** Gaia Borghi、João Carlos Virgolino Soares、Angelo Bratta、Shahab Heshmati-Alamdari、Claudio Semini；v1 2026-10-19 16:00 UTC。
- **问题与创新：** 动态物体会污染 vSLAM；固定语义类别或逐像素分割又昂贵。CAOS-SLAM 在 ORB-SLAM3 上同时处理已知和未知类别的运动对象。
- **机制／结构：** 按需全景分割发现对象，未分类区域用深度聚类实例化候选；两次分割间以轻量检测或世界坐标 Kalman 预测、深度一致性和外观相似度传播轨迹，再剔除动态特征。
- **实验与关键结果：** 多个动态 RGB-D 数据集及真实实验中，未知动态物体场景定位误差最多降低 **59%**，严重遮挡场景最多降低 **88%**，笔记本中位处理速度 **30 FPS**。
- **关注价值／局限：** 不依赖封闭类别表并输出对象速度，可接导航和规划；分割触发策略、深度聚类误检、快速相机运动和代码尚未公开是落地风险。

## 机器人／具身智能

### 3. [Ropedia W0: Scaling Loco-Manipulation World Models across Embodiments with Human Experience](https://arxiv.org/abs/2610.26855)

- **作者与时间：** Tianqi Liu、Hanfei Zhao、Qifeng Liang、Hui En Pang、Jiarui Xu 等；v1 2026-10-19 17:59 UTC。
- **问题与创新：** 人、轮式/腿式及人形机器人动作空间异构，统一建模运动与操作缺少大规模多模态监督。Ropedia W0 提出跨人类与多机器人本体的第一类 loco-manipulation world foundation model。
- **机制／结构：** Xp-Data 含 **1 万小时人类第一视角 + 3,000 小时机器人数据**；以相机位姿表征运动、投影骨架表征操作，机器人骨架结合本体正运动学与人工校正；另建 Xp-Teleop 长时基准。
- **实验与关键结果：** 在 DreamDojo、Ψ0、ω-HOME、Xp-Teleop、AgiBot 五个跨本体基准达 SOTA；增加人类预训练数据同时提升人和机器人评测，蒸馏后支持实时分钟级 rollout 与 VR 交互。
- **关注价值／局限：** 把人类经验变成跨本体预测先验；骨架标注成本、动作可执行性差异、数据许可和长时 rollout 误差累积需进一步公开。

### 4. [Physical Words: A Vocabulary for Structuring Latent Reasoning in Robot Manipulation](https://arxiv.org/abs/2610.26854)

- **作者与时间：** Jiaming Liu、Xinghao Zhu、Yiming Zhang、Shanghang Zhang、Yinxi Wang 等；v1 2026-10-19 17:59 UTC。
- **问题与创新：** 语言推理难表达细粒度物理动态，纯 latent 推理又缺少可复用结构。PhysWord 用原子动作动词作为连续物理表示的语义锚点。
- **机制／结构：** 预测即将发生的物理词，并把上下文隐状态对齐到未来观测生成的 latent target；构建带视觉/可选触觉变体的时间结构空间，逐时自回归预测动作阶段后再生成动作。
- **实验与关键结果：** UniVTAC 视觉触觉任务成功率 **90.3%**，LIBERO-Long 视觉任务 **99.6%**，双臂夹爪和灵巧手真机优于对比方法，并能泛化到未见长时场景。
- **关注价值／局限：** 为 VLA 增加可解释的阶段级中间接口；动作词边界、语言锚点对新本体的迁移和触觉缺失时的退化仍待评估。

### 5. [HAF-VLA: Hierarchical Action Flow Framework for Humanoid Vision-Language-Action Control](https://arxiv.org/abs/2610.26584)

- **作者与时间：** Langzhe Gu、Chengkai Hou、Meng Li、Xinhua Wang、Xinyuan Lv 等；v1 2026-10-19 15:33 UTC。
- **问题与创新：** 人形机器人要同时协调行走、姿态、视线和双臂；一次生成全身动作容易让错误腰部/底座运动诱发上肢激烈补偿。HAF-VLA 将动作流分层生成。
- **机制／结构：** 在预训练 flow-matching VLA 上加入阶段 embedding 和跨阶段 KV cache；先去噪行走/头部，再细化腰部，最后生成全身操作，后续阶段读取前一阶段动作表示。
- **实验与关键结果：** 六个真实世界任务中显著提升既有模型的人形 loco-manipulation 表现；摘要未给统一成功率和失败分解。
- **关注价值／局限：** 将高维全身控制拆成可检查的时序依赖；阶段顺序固定时的异常恢复、接触冲击与不同人形比例泛化仍是关键问题。

## 交叉方向：鲁棒性、协作与评测

### 6. [CoopUQ: Robust Multi-Robot Social Navigation via Uncertainty-Aware Cooperative Forecasting](https://arxiv.org/abs/2610.26852)

- **作者与时间：** Zehao Wang、Jianpeng Yao、Yuping Wang、Yiping Li、Jiaqi Li 等；v1 2026-10-19 17:59 UTC，CoRL 2026。
- **问题与创新：** 单体导航扩展到多机器人后，在遮挡和分布外行人行为下容易低估风险。CoopUQ 将跨机器人占据预测的不确定性接入受约束多智能体 RL。
- **机制／结构：** 融合各机器人时空特征预测未来占据栅格；策略成本同时惩罚预测占据区和高不确定区域，使风险敏感度随分布偏移调整。
- **实验与关键结果：** Unity3D 多布局、不同人群密度及奔跑行为的 ID/OOD 场景中，预测和安全优于基线；真实机器人多场景实验显示鲁棒性，摘要未给绝对碰撞率。
- **关注价值／局限：** “预测—不确定性—控制”形成可审计协作接口；通信丢包、共享地图延迟和不确定性校准会直接影响安全成本。

### 7. [PICA-WAM: Visual Perturbation Invariance via Cross-Appearance Self-Alignment in World Action Models](https://arxiv.org/abs/2610.26813)

- **作者与时间：** Yude Zou、Yifei Yao、Guanbo Jiao、Jianming Ma、Guanjie Zheng；v1 2026-10-19 17:50 UTC。
- **问题与创新：** WAM 视频预测会保留与任务无关的外观变化，进而污染动作表示；普通增强没有强制名义/扰动观测输出一致动作。PICA-WAM 把不变性变成自监督辅助任务。
- **机制／结构：** EMA teacher 处理名义观测提供深层目标，online WAM 处理扰动观测，以轻量投影头将浅层动作表示对齐。
- **实验与关键结果：** 在 RoboTwin 2.0、LIBERO-Plus、EBench 和真机上，四种 WAM 均提升视觉扰动鲁棒性、保持仿真名义性能并提高真机成功率；层级诊断显示外观敏感性向动作传播减少。
- **关注价值／局限：** 把“该忽略什么视觉变化”写进 WAM 训练；扰动集合可能遗漏真实光照/遮挡，过强不变性也可能抹掉任务相关线索。

### 8. [HandsOn: A Large-Scale Simulation Benchmark for Generalizable Dexterous Manipulation](https://arxiv.org/abs/2610.26765)

- **作者与时间：** Tianwei Luo、Yiming He、Hongjin Wu、Ting Pan、Debin Ren；v1 2026-10-19 17:22 UTC。
- **问题与创新：** 通用灵巧操作需要跨本体、物体和任务稳定泛化，但现有基准覆盖窄。HandsOn 支持 5 种机械臂、6 种灵巧手、约 200 个刚体/关节/可变形资产。
- **机制／结构：** 18,000 条精选人类演示配 66 个经人工核验任务；Core-50 评估演示学习和执行，Transfer-16 评估资产/关系迁移、技能组合和无目标示例的可变形操作。
- **实验与关键结果：** 最佳多任务策略 Core-50 成功率 **29.1%**；未微调 GPT-6 通过 move_eef 仅为 Core-50 **5.2%**、Transfer-16 **1.9%**（660 次试验），失败集中在接触建立、动作协调和目标保持。
- **关注价值／局限：** 把“能否泛化”拆成可复现实验；仿真接触与真机差异、任务难度分布及基准对模型提示的敏感性仍需持续审计。

## 趋势总结

本期研究把“可执行性”拆成显式接口：Drive2Gauss 将生成视频落到 4D 场景，CAOS-SLAM 追踪未知动态物，PhysWord/HAF-VLA 将动作阶段写入中间表示，CoopUQ 将不确定性直接收费，PICA-WAM 则约束外观变化不污染动作。共同局限是摘要级结果仍少报告最坏时延、通信/感知失效、回退策略和真机失败分布；下一步应把这些运行时证据与平均成功率并列。
