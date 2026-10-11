# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-12

## 日期与证据口径

北京时间 2026-10-12 检索 [arXiv API](https://export.arxiv.org/api/query?search_query=cat%3Acs.RO%20OR%20cat%3Acs.AI%20OR%20cat%3Acs.CV&start=0&max_results=100&sortBy=submittedDate&sortOrder=descending)。周末尚无晚于 **2026-10-08 UTC** 的相关常规批次；本期明确回溯该日的 7 篇此前未选论文，未将其表述为当日新稿。实验数值均为作者报告、未经独立复现；“关注价值／局限”是编辑判断。

## 自动驾驶、规划与长期自治

### 1. MAP2: Model- and Acceleration-Based Pursuit with MPC and Gaussian Process Residual Learning for Autonomous Racing

- **论文／作者／时间**：[arXiv:2610.12196](https://arxiv.org/abs/2610.12196)；Weizhan Huang、Cheng Hu、Edoardo Ghignone、Nicolas Baumann 等；v1：2026-10-08 15:52 UTC。
- **问题**：极限工况下 Ackermann 几何与轮胎模型偏差会使低算力几何控制器偏离实际车辆响应。
- **创新与机制**：MAP2 以曲率运动学 MPC 给出预测控制量，再经轮胎模型与稀疏高斯过程（SGP）残差校正映射为转向命令；把模型误差限制在可在线查询的残差层。
- **实验与关键结果**：作者在真实赛车实验中报告，相比 MAP／Pure Pursuit，平均横向跟踪误差分别下降 **37.99%／44.65%**，平均圈速至少下降 **1.5%**。
- **关注价值／局限**：适合把学习项嵌进可解释、低延迟控制栈；但赛道轮胎、路面和速度分布有限，不能直接外推为开放道路安全结论。

### 2. MiniWAM: Learning Compact Future Targets for Efficient World-Action Modeling

- **论文／作者／时间**：[arXiv:2610.12194](https://arxiv.org/abs/2610.12194)；Jie Chen、Ruofei Bai、Yuxin Cai、Yifeng Zhang 等；v1：2026-10-08 15:51 UTC。
- **问题**：世界动作模型直接预测视觉 backbone 的高维未来特征，训练和部署成本高，且其中有大量与控制无关的信息。
- **创新与机制**：PRISM 用逆动力学监督加特征重建，先抽取控制相关的紧凑未来表征；冻结该 encoder 后，MiniWAM 联合预测未来 latent 与动作。
- **实验与关键结果**：在 LIBERO、LIBERO-Plus、RoboTwin 2.0 中，作者称稳定优于原生 future-feature 预测；以 **65×** 更少未来 token 获得最高 **8×** 训练加速，0.25B 模型已能与更大 WAM 竞争。
- **关注价值／局限**：为车端／机器人端的预测—控制模型提供明显的算力接口；应继续核验该压缩是否丢失罕见风险、长时遮挡与跨本体动力学信息。

### 3. RESETTLE: Robotic Recovery through Disagreement-Triggered Retrieval and Efficient Corrective Control

- **论文／作者／时间**：[arXiv:2610.12185](https://arxiv.org/abs/2610.12185)；Yuxin Chen、Senqiao Yang、Zixuan Wang、Jinhui Ye 等；v1：2026-10-08 15:49 UTC。
- **问题**：冻结策略执行偏离时，反复 VLM 推理或在线优化介入太慢，且难在不破坏主策略的前提下恢复。
- **创新与机制**：同条件下两次动作提议持续不一致即触发；检索同任务演示，以 state-servo 先验和受保护的视觉残差只执行一次校正，再交还原策略。
- **实验与关键结果**：作者在 LIBERO-Plus、Meta-World、RoboCasa Tabletop 最高带来 **8.70／6.28／6.83** 个百分点绝对成功率提升；监测与恢复延迟比 VoLoAgent 低 **74.04%–93.57%**。
- **关注价值／局限**：把“不确定时何时恢复”落到可审计的触发条件，亦可迁移到驾驶执行监控；双样本分歧未必等于危险，检索库覆盖不足时可能漏报或误触发。

## 机器人／具身智能

### 4. Dex-One2Many: Learning Dexterous Manipulation from a Single Human Demonstration

- **论文／作者／时间**：[arXiv:2610.12470](https://arxiv.org/abs/2610.12470)；Jusuk Lee、Sungha Kim、Yeonsoo Park、Jonguk Cheon 等；v1：2026-10-08 17:59 UTC。
- **问题**：单段人类视频既不足以覆盖未见物体位姿／抓取，又难为高维多阶段 RL 提供有效探索。
- **创新与机制**：把视频抽象为连续 scene graph；图关系而非精确姿态用于采样多样 reset，并为每阶段提供稠密奖励，形成 real-to-sim-to-real 学习链。
- **实验与关键结果**：五项工具使用／操作任务上，作者报告已见配置较基线高 **6.5%**，未见情形优势扩大至 **71%**，并零样本迁移至真机多指手。
- **关注价值／局限**：把人类演示变成可重组的关系约束而非单一路径；scene graph 构建质量、接触摩擦与更复杂长时任务的误差累积仍待验证。

### 5. DreamTrue: Action-Faithful Robot World Model with Counterfactual Post-Training

- **论文／作者／时间**：[arXiv:2610.12468](https://arxiv.org/abs/2610.12468)；Junyan Li、Ruizhi Li、Yu Liu、Xiangshuo Liu 等；v1：2026-10-08 17:59 UTC。
- **问题**：现有机器人视频世界模型受标定误差和“成功样本偏置”影响，动作跟随及接触失败预测不可信。
- **创新与机制**：将动作轨迹渲染成图像条件并做离线几何标定；反事实改写已录制动作扩展失败接触，人工标注缺陷视频训练 reward model，再以 RL 后训练改善物理合理性。
- **实验与关键结果**：作者在 AgiBot 报告取得 action-following SOTA，并将人工评估的交互缺陷率从 **48.12%** 降至 **6.25%**；获 AgiBot World Challenge 2026 world-model track 第一。
- **关注价值／局限**：反事实动作和人评缺陷可补齐“只会预言成功”的数据缺口；生成未来并非真实动力学，标注协议、跨机械臂泛化和安全置信度需单独披露。

### 6. A Balanced Data Diet: Addressing the Exploration Bottleneck in Mega-Scale RL for Robot Control

- **论文／作者／时间**：[arXiv:2610.12465](https://arxiv.org/abs/2610.12465)；Octi Zhang、Mateo Guaman Castro、Patrick Yin、Ignacio Dagnino 等；v1：2026-10-08 17:59 UTC。
- **问题**：大规模并行仿真均匀采样 reset，会把大量计算花在已掌握或尚不可学的状态，放大规模不等于增加有效探索。
- **创新与机制**：Success Guided Sampling（SGS）按照当前成功前沿自适应调配任务配置，把 batch 集中到策略“将会但尚未完全会”的区域；随后将策略蒸馏为 RGB 输入。
- **实验与关键结果**：作者使用最多 **2²⁰**（逾百万）并行环境，在多地形四足与接触装配任务解出先前方法失败的难例，并报告 RGB 策略在真机装配零样本迁移。
- **关注价值／局限**：说明数据调度是与网络规模同等重要的训练变量；success frontier 可能偏向易度量任务，真实世界成本、故障样本与安全探索如何纳入尚不明确。

### 7. SpatialHarness: Test-Time Spatial Scaffolding for Fine Robotic Manipulation

- **论文／作者／时间**：[arXiv:2610.12457](https://arxiv.org/abs/2610.12457)；Jiayu Wang、Yue Yu、Bin Zhu、Zhiyao Yang 等；v1：2026-10-08 17:59 UTC。
- **问题**：强多模态策略在精细操作失败，常是物理相机没有暴露关键相对空间关系，而不一定是策略缺少能力。
- **创新与机制**：不微调冻结策略，在执行期维护与真机同步的在线模拟场景，识别关键关系并渲染补充虚拟视角；用静态／持握／转换模式保持交互中的场景同步。
- **实验与关键结果**：四类真机任务中，固定 GPT-6 Astra 策略的插头插入成功率由 **26.7%** 至 **66.7%**，汉诺塔由 **0%** 至 **100%**。
- **关注价值／局限**：强调测试时“补足可观测性”可释放已有策略能力；模拟同步误差、渲染延迟、遮挡和更开放环境下的虚拟视角可信度仍是部署边界。

## 趋势总结

- **控制接口正走向残差、压缩和恢复三层**：MAP2、MiniWAM、RESETTLE 分别处理模型失配、预测预算与执行偏离，系统指标需要同时报告精度、时延和误触发代价。
- **数据规模必须带结构化反事实与课程**：Dex-One2Many、DreamTrue、SGS 不只是增加样本，而是重写状态关系、失败未来和采样分布。
- **强策略仍需运行时空间证据**：SpatialHarness 表明改善观测可能比改模型更有效，但该收益依赖可验证的同步质量与安全退化机制。
