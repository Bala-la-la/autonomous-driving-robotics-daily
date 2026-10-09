# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-10

## 日期与证据口径

北京时间 2026-10-10 检索 [arXiv API](https://export.arxiv.org/api/query?search_query=cat%3Acs.RO%20OR%20cat%3Acs.AI%20OR%20cat%3Acs.CV&start=0&max_results=100&sortBy=submittedDate&sortOrder=descending)。最新相关 v1 批次为 **2026-10-08 UTC**；周末尚无更晚的常规批次。本期从该批次精选 7 篇，均为 10 月 8 日新提交，未把它们冒充为 10 月 10 日新稿。论文信息及数字据官方摘要／版本记录，实验数字均为作者报告、未复现；“关注价值”和“局限”为编辑判断。

## 自动驾驶、定位与长期自治

### 1. GLIO2: A GPU-Parallelized Tightly-Coupled LiDAR-Inertial-GNSS System for Robust and Real-Time Global Localization and Mapping

- **论文／作者／时间**：[arXiv:2610.12411](https://arxiv.org/abs/2610.12411)；Qi Zhang、Xikun Liu、Qijun Qin、Xiangru Wang、Junzhe Wang、Naigui Xiao、Jianhao Jiao、Weisong Wen。v1：2026-10-08 17:49 UTC。
- **问题**：传统 scan-to-map 前端在 LiDAR 退化或动态物体干扰下会漂移；过早把配准压缩为单一、过度自信的位姿约束，也让 GNSS 无法重新权衡对应关系。
- **创新与机制**：将多扫描 LiDAR 对应、IMU 预积分和原始 GNSS 观测在滑窗因子图中紧耦合，GPU 并行前端实时优化；离线后端复用缓存因子做全局精修。
- **实验与关键结果**：作者称在 UrbanNav、MARS-LVIG、M3DGR 及自采 UAV／车辆数据总体最优；5.66 km、最高 96 km/h 桥梁退化场景中保持 **1.6 m** 水平精度，Jetson Orin NX 约 **25 Hz（39.60 ms/scan）**；30 分钟、4.51 km 序列离线优化约 24 秒。
- **关注价值**：把“前端匹配是否可信”保留到融合层，适合自动驾驶和无人机在城市峡谷、桥梁或弱纹理路段的长期自治。
- **局限／跟进**：代码与数据尚称将发布；应核对算力、传感器时间同步、GNSS 遮挡及与强视觉惯性基线的同预算比较。

## 机器人／具身智能

### 2. DreamTrue: Action-Faithful Robot World Model with Counterfactual Post-Training

- **论文／作者／时间**：[arXiv:2610.12468](https://arxiv.org/abs/2610.12468)；Junyan Li、Ruizhi Li、Yu Liu、Xiangshuo Liu、Mingchao Sun、Hongyu Pan、Mu Xu、Lue Fan、Zhaoxiang Zhang 等。v1：2026-10-08 17:59 UTC。
- **问题**：机器人视频世界模型会受动作／相机标定误差影响，且数据多是成功交互，模型容易把失败动作“美化”为成功。
- **创新与机制**：把动作轨迹渲染成图像条件并离线几何校准；反事实地修改记录动作以扩展接触与失败覆盖；再以人工标注的机器人／物体／交互缺陷视频训练 reward model，进行 RL 后训练。
- **实验与关键结果**：在 AgiBot 上，作者报告动作跟随达到所比较方法最佳，人工评估的交互缺陷率从 **48.12% 降至 6.25%**，并获 AgiBot World Challenge 2026 world-model 赛道第一。
- **关注价值**：把“动作忠实”和“物理合理”拆成可审计的校准、反事实覆盖与奖励信号，为闭环规划前的世界模型验收提供路径。
- **局限／跟进**：视频 reward 仍可能奖励视觉上合理但力学错误的未来；需看跨机器人、长时 rollout、真实接触和下游规划成功率，而非仅生成质量。

### 3. LeWAM: A JEPA World Action Model with Diffusion-Steering-Based MPC

- **论文／作者／时间**：[arXiv:2610.12407](https://arxiv.org/abs/2610.12407)；Shashank Hegde、Alexander Popov、Elie Aljalbout、Nikolai Smolyanskiy。v1：2026-10-08 17:46 UTC。
- **问题**：重建式 WAM 的 latent 含冗余噪声；直接在动作空间用 MPC 采样又会利用动力学模型漏洞。
- **创新与机制**：以 decoder-free JEPA latent 训练同一双向 Transformer 同时做前向、后向、逆动力学和策略预测；规划时不直接操纵动作，而在 diffusion policy head 的噪声空间 steering。
- **实验与关键结果**：作者报告其 latent 的机器人／物体状态线性探针优于仅前向 JEPA 与重建式 WAM；闭环控制达到同编码器、同规模 flow-matching policy 水平，噪声空间规划优于原始动作采样 MPC。
- **关注价值**：世界模型不必在“会预测”与“会执行”之间二选一，且为避免 model exploitation 提供了具体的规划变量设计。
- **局限／跟进**：摘要未给出跨任务绝对成功率、计算延迟和真实机器人对比；diffusion steering 对模型失配的失效边界仍需量化。

### 4. Dex-One2Many: Learning Dexterous Manipulation from a Single Human Demonstration

- **论文／作者／时间**：[arXiv:2610.12470](https://arxiv.org/abs/2610.12470)；Jusuk Lee、Sungha Kim、Yeonsoo Park、Jonguk Cheon、Yoonkyo Jung、Yongjun You、H. Jin Kim、Jia-Bin Huang、Furong Huang、Youngseok Jang、Seungjae Lee。v1：2026-10-08 17:59 UTC。
- **问题**：严格模仿单段人类视频难以泛化到未见物体位姿、目标位姿和抓取；从零 RL 又难探索高维多阶段任务。
- **创新与机制**：将单视频抽象成顺序场景图，用关系而非精确姿态生成多样 reset state，并为每阶段构造稠密奖励；策略在仿真中训练后零样本迁移多指手。
- **实验与关键结果**：五类工具使用／操作任务上，作者报告已见配置超过基线 **6.5%**，未见情形优势扩大至 **71%**。
- **关注价值**：把有限人类演示转化为可组合的关系约束，可能显著降低灵巧操作采集成本。
- **局限／跟进**：单视频中的接触、遮挡和动力学误差仍会进入场景图；需验证更复杂工具、视觉域偏移和失败恢复，而非仅 reset 分布内泛化。

### 5. A Balanced Data Diet: Addressing the Exploration Bottleneck in Mega-Scale RL for Robot Control

- **论文／作者／时间**：[arXiv:2610.12465](https://arxiv.org/abs/2610.12465)；Octi Zhang、Mateo Guaman Castro、Patrick Yin、Ignacio Dagnino、Abhishek Gupta、Rosario Scalise、Byron Boots。v1：2026-10-08 17:59 UTC；标注 CoRL 2026。
- **问题**：大规模并行仿真若均匀采样 reset，批量里会混入已掌握或尚不可学状态，吞掉探索预算，难以处理动态、精密控制。
- **创新与机制**：Success Guided Sampling（SGS）持续把采样质量集中在策略能力边界附近，而非人为设计任务奖励或示范；最后蒸馏为 RGB policy。
- **实验与关键结果**：作者在最多 **2^20（逾百万）**并行环境中解决多地形四足与接触装配任务，并展示真机零样本转移；摘要称既有方法在这些难任务上失败。
- **关注价值**：数据配比本身成为可调的训练控制器，提示具身 RL 的扩展瓶颈常在有效探索率，而非单纯环境数量。
- **局限／跟进**：能力边界的估计错误可能造成遗忘或跳过稀有安全状态；应报告采样开销、真实数据混入后效果及不同任务难度下的稳定性。

### 6. SpatialHarness: Test-Time Spatial Scaffolding for Fine Robotic Manipulation

- **论文／作者／时间**：[arXiv:2610.12457](https://arxiv.org/abs/2610.12457)；Jiayu Wang、Yue Yu、Bin Zhu、Zhiyao Yang、Jingjing Chen 等。v1：2026-10-08 17:59 UTC。
- **问题**：强多模态策略在精细操作失败，根因可能不是策略不会推理，而是实体相对几何没有被当前物理相机看清。
- **创新与机制**：不微调冻结策略、也不改硬件，在真机执行旁维护在线同步的模拟场景，识别关键空间关系并渲染互补虚拟视角；用静态／持握／过渡模式做交互感知同步。
- **实验与关键结果**：四项真机任务中，同一冻结 GPT-6 Astra 策略的插头插入成功率由 **26.7% 升至 66.7%**，汉诺塔由 **0% 升至 100%**。
- **关注价值**：把 test-time compute 用在“补齐可观测性”而非重训，适合高价值、小批量操作的数字孪生辅助执行。
- **局限／跟进**：场景同步错误会系统性误导策略；还需测量虚拟视角生成延迟、标定漂移、遮挡／软体物体和安全回退策略。

### 7. CSF: Contextual Safety Filtering for Motion Generators

- **论文／作者／时间**：[arXiv:2610.12467](https://arxiv.org/abs/2610.12467)；Lizhi Yang、Yiling Hou、Yao Tang、Junheng Li、Daniel Weng、Blake Werner、Aaron D. Ames。v1：2026-10-08 17:59 UTC。
- **问题**：文本驱动全身动作生成器并不理解场景语义，同一动作朝向物体或人可能有完全不同的风险；仅查 prompt 或几何约束不够。
- **创新与机制**：无需训练，为每条自然语言安全规则从生成器得到安全／不安全参考轨迹，构造仿射安全值，再由 safe-reference-tracking CBF-QP 强制执行。
- **实验与关键结果**：跨四种预训练生成器，作者报告触发全部显式与场景诱发的不安全规则，危险事件最高减少 **90%**，保留 **88–100%** 正常动作；并在 Unitree G1 真机阻止人和物体交互中的不安全动作。
- **关注价值**：将高层安全语言落到可验证的控制屏障，为人形机器人提供可解释、可插拔的末端防线。
- **局限／跟进**：参考轨迹和规则覆盖之外的危险无法保证发现；需审查多规则冲突、感知错误、CBF 可行性及紧急停止的完整安全论证。

## 趋势总结

- **世界模型转向可执行、可反驳的预测**：DreamTrue 的反事实失败覆盖与 LeWAM 的 diffusion-space planning 都试图限制“看起来合理”的模型漏洞。
- **能力扩展也在重画数据与观测边界**：SGS 把训练样本投向能力前沿；Dex-One2Many 用关系场景图放大单示范；SpatialHarness 直接补充测试时可见性。
- **长期自治的可信度来自保留原始证据**：GLIO2 不过早压缩对应关系，CSF 不把安全简化为 prompt 过滤；传感器、控制和安全层都更需要可重算的中间状态。
