# arXiv 自动驾驶、机器人与具身智能晨报｜2026-09-14

## 检索状态

截至北京时间 2026-09-14 06:00，已恢复访问 arXiv `cs.RO` 与 `cs.AI` 的 recent/list 页面，并逐篇核对原始摘要页与可用的 HTML 全文。本期选入 10 篇与自动驾驶、机器人、VLA、世界模型、安全和具身评测直接相关的论文。

需要区分两个日期：本期对应 arXiv 在 2026-09-14（周一）公布的最新工作日批次，但入选论文的 arXiv v1 提交历史均显示为 2026-09-11 UTC。以下不把“公布日”误写成论文原始提交日。

## 自动驾驶与导航

1. [ASTRIL-MPC: Autonomous Traversal Framework of Articulated Tracked Robots with Language-Guided Neural-Kinematic MPC](https://arxiv.org/abs/2609.13083)（[HTML](https://arxiv.org/html/2609.13083v1)）

   - **作者／机构**：Zhenfeng Gan、Yanbo Chen、Lirong Che、Junbo Tan、Xueqian Wang；arXiv HTML 首页未显式列出机构，未据作者信息臆补单位。
   - **问题与机制**：面向楼梯、台阶和杂物环境中的铰接履带机器人。系统用地形高度序列与近期状态训练轻量神经运动学模型，把它作为 NMPC 的状态转移约束；LLM 只允许在安全检查、范围裁剪、变化率限制和一致性检查之后，低频调整有限的代价权重、输入边界和履带板 PD 参数，不直接生成动作。编译后的预测器将完整控制周期压到 100 ms 内。
   - **实验**：单块跨越、楼梯上行、楼梯下行三种任务，每个控制器和场景重复 3 次；同时做多障碍高度泛化。相对非自适应 NMPC，平均综合分数提升 42%，相对 PPO 提升 67%；楼梯下行相对非自适应 NMPC 提升 71%，并消除了可测的下降碰撞冲击。
   - **关注价值**：把语言模型放在“受限参数调节器”而非动作策略的位置，形成“神经动力学 + 约束优化 + 低频语言反馈”的可审计接口，适合迁移到自动驾驶或其他接触丰富的控制系统。
   - **局限**：状态建模限制在二维 sagittal 平面，横滚稳定性依赖上游全局路径；预测地形在一个控制时域内保持固定。论文还显示错误或含糊的语言指令会引入不必要的配置变化，且真实平台、地形和接触条件仍较有限。

2. [Comfort by Construction: Adaptive, Comfort-Bounded Action Spaces for Learned Driving Policies](https://arxiv.org/abs/2609.13011)（[HTML](https://arxiv.org/html/2609.13011v1)）

   - **作者／机构**：Anna Rothenhäusler、Daniel Jost、Raghu Rajan、Faris Janjos、Oliver Scheel、Andreas Look、Joschka Boedecker；University of Freiburg、Bosch Center for Artificial Intelligence、Coburg University of Applied Sciences。
   - **问题与机制**：数据驱动驾驶模拟器常用固定加速度／转向率网格，却不约束实际加速度和 jerk，RL 因此可能学会人类不会接受的急刹急转。论文在每一步解析当前状态下的舒适可行控制集，并通过横向 jerk 约束的闭式反演重新离散动作网格，避免简单裁剪造成的“grid collapse”。同时提供浏览器工具 PufferDrive-Editor，用于检查实际运动学和制作压力场景。
   - **实验**：在 Waymo Open Motion Dataset 与手工 slalom 场景上，对比无约束、裁剪网格、jerk 控制和自适应网格。自适应模型将舒适违规率压到 1% 以下，并在可导航性上优于裁剪网格和直接 jerk 基线。
   - **关注价值**：把舒适度从训练后评价指标前移为动作空间设计，提醒自动驾驶 benchmark 先检查模拟器是否允许策略利用不现实的运动学漏洞。
   - **局限**：边界建立在无侧滑的运动学自行车模型和 OPM 行为舒适包络上；“舒适可行”不是完整车辆动力学安全，也未等价于真实乘员体验。结论主要验证在 PufferDrive 类模拟器中，真实车辆闭环仍需单独验证。

3. [READ: Learning Risk-Informed Fields for End-to-End Autonomous Driving](https://arxiv.org/abs/2609.12371)（[HTML](https://arxiv.org/html/2609.12371v1)）

   - **作者／机构**：Zhiyuan Liu、Yuanxin Tian、Zehong Ke、Jinhao Li、Hao Cheng、Zhenhua Xu、Wenhao Yu、Jianqiang Wang；清华大学车辆与运载学院。
   - **问题与机制**：传统端到端规划通常把环境因素如何影响动作隐含在 latent feature 中。READ 在 BEV 中学习连续时空风险场，用各向异性 Gaussian 表示场值和影响范围，并联合非可行区域、未来交通参与者占据、专家轨迹和运动学残差等部分约束。风险场既可作为端到端规划的辅助监督，也可编码为 VLA 的 risk tokens，还能沿候选轨迹做可微评价与可选的后处理优化。
   - **实验**：在 NAVSIM 上接入多个匹配的端到端骨干，并测试 VLA 设置及 NAVSIM v2。论文 HTML 表中，TransFuser 的 PDMS 从 84.0 提升到 84.6，Drive-JEPA 从 89.1 提升到 90.0；作者报告在不同骨干和 VLA 设置下均有一致增益。
   - **关注价值**：把“风险影响范围”从手工势场或不可解释 latent 中抽出来，形成可沿轨迹查询的中间接口；这比只增加占据预测更接近可诊断规划。
   - **局限**：训练依赖地图、未来参与者框和专家轨迹等证据，运动学残差还建立在示范轨迹局部可行的假设上。当前证据主要来自 NAVSIM 离线 benchmark，尚不能替代真实道路、传感器延迟和分布外交互验证。

4. [VertexCBF: Improving Neural Control Barrier Functions via Vertex-Restricted Control Search](https://arxiv.org/abs/2609.12831)（[HTML](https://arxiv.org/html/2609.12831v1)）

   - **作者／机构**：Bojan Derajić、Sebastian Bernhard、Wolfgang Hönig；Technical University of Berlin、AUMOVIO、Technical University of Applied Sciences Augsburg、Robotics Institute Germany。
   - **问题与机制**：学习神经控制屏障函数时，单纯的物理信息 PDE 损失容易落入常数或过度保守解。VertexCBF 用神经网络近似稳态 Hamilton-Jacobi 安全值函数，结合物理信息损失与稀疏监督；在控制仿射动力学和凸多面体输入集假设下，只在控制顶点上做 GPU 并行树搜索生成监督点。残差参数化保证学习到的 CBF 不会把安全集扩张到指定约束之外。
   - **实验**：在 15 个动力学系统上与多种基线比较，并在移动机器人避让行人硬件实验中使用训练出的神经 CBF。作者报告能恢复更大的可靠安全集，而基线在部分系统上过度保守或失败。
   - **关注价值**：将安全学习从“训练后加过滤器”推进到“以可扩展搜索生成安全值监督”，对自动驾驶、无人机和腿式机器人共享一套可解释安全接口。
   - **局限**：结论依赖控制仿射动力学、凸多面体输入集、时间离散化和有限时域／beam search；顶点限制、短时域和剪枝都会产生保守或近似误差。硬件证据只有一个移动机器人避人场景，不代表复杂交通参与者和感知不确定性下的完整安全保证。

## 机器人与具身智能

5. [Dynin-Robotics: Omnimodal Unified Diffusion Vision-Language-Action Model](https://arxiv.org/abs/2609.13053)（[HTML](https://arxiv.org/html/2609.13053v1)）

   - **作者／机构**：Hoeun Lee、Jaeik Kim、Jusang Oh、Jinhyeok Kim、Geon Choi、Hyeonggeun Kim、Jaeyoung Do；AIDAS Lab，Seoul National University。
   - **问题与机制**：Dynin-Robotics 在同一个 omnimodal masked-diffusion backbone 中，以离散 token 统一语言、视觉、目标状态和动作。通过改变可见上下文与待预测 span，同一模型支持动作预测、动作条件下一观测预测、终态目标预测和轨迹到指令重建；推理时可先预测目标、联合去噪动作和未来状态，或用世界模型给候选动作重排。
   - **实验**：持续预训练约 133 万条来自 48 个 Open X-Embodiment 数据集的轨迹；在 VLABench 的 shifted-instruction 任务上做预训练、目标函数和推理组合消融；LIBERO 平均成功率 98.1%，zero-shot LIBERO-Plus 为 73.0%，Franka Research 3 四种真实操作条件平均 78.4%。块并行解码在论文给出的 profiling 设置下最高带来 29.2 倍模型侧动作解码加速。
   - **关注价值**：将“策略、世界模型、目标预测和任务理解”收敛到一个可组合的轨迹接口，为测试时额外计算提供明确插槽，而不是为每个目标训练一套独立模型。
   - **局限**：论文明确指出不同预测组合的收益并不相同；离散动作 token、掩码调度和大规模预训练也增加了系统复杂度。真实验证集中在 Franka Research 3 的四种条件，跨本体、长时任务和接触异常的证据仍有限。

6. [Breaking the Vision-Action Shortcut: Latent Interface Training for Generalizable Robotics Foundation Models](https://arxiv.org/abs/2609.12641)（[项目页](https://magiclab-nus.github.io/)）

   - **作者／机构**：Jianman Lin、Shailesh Shailesh、Zhongyi Luo、Jiafei Duan；arXiv 摘要页未显式列出机构，原文提供 Magic Lab 项目链接。
   - **问题与机制**：机器人基础模型可能利用训练分布中与动作偶然相关的视觉线索，导致相机、光照或干扰物改变后性能下降。LIT 先在不看图像的条件下，用语言、机器人状态和示范动作块终端的 SE(3) 末端位姿训练目标导向动作先验；第二阶段把视觉和语义信息压缩到唯一的 latent interface，并监督它重建同一终端位姿，使动作专家只能接收保留任务相关空间信息的视觉通道。
   - **实验**：覆盖 Pi0.5、MolmoAct2、FAST-WAM 和 ImageWAM 四种 VLA／WAM 架构。LIBERO-Plus 总体成功率提升 3.87–10.70 个百分点，同时保持或提升 LIBERO；三个真实任务在未见相机、光照和 distractor 下，聚合成功率提升 13.30–16.70 个百分点。
   - **关注价值**：把视觉泛化问题转化为“视觉到底需要向动作专家传递什么”的接口约束，避免用更多数据掩盖 shortcut。
   - **局限**：方法依赖终端位姿监督和两阶段训练，收益可能随位姿标签质量、动作专家结构和架构冻结策略变化。真实实验只有三个任务，尚不能说明对更复杂接触、长时任务或不同本体都同样有效。

7. [STAR: Sparse Tactile Representation Learning in Vision-Tactile-Language-Action Models for Dexterous Manipulation](https://arxiv.org/abs/2609.12549)（[HTML](https://arxiv.org/html/2609.12549v1)）

   - **作者／机构**：Xiangcheng Liu、Tianhao Wu、Le Zheng、Yidong Wang、Bowen Jiang、Mingjie Pan、Xinlin Ren、Yi Liu、Jianlan Luo；Shanghai Innovation Institute、Agibot。
   - **问题与机制**：灵巧手触觉同时存在空间、时间和信息稀疏。论文构建带 10-DoF 灵巧手和 268 维压阻式触觉传感器的双臂移动平台，使用手套遥操作采集带视觉、触觉、状态、动作和语言的 200 小时数据。STAR 训练配方包括视觉—触觉联合预训练、只保留激活 patch 加每手 global token 的 sparse-global 表示，以及跨动作时域预测稀疏未来触觉。
   - **实验**：数据包含 10,576 条轨迹、65 个任务，其中 69.5% 涉及多指灵巧操作；所有数据按时间戳同步到 30 Hz。使用每任务 100 条后训练轨迹，在四个真实任务上取得 61% 平均成功率。
   - **关注价值**：把触觉 token 预算和未来接触监督纳入 VLA 设计，给“触觉应何时进入策略”提供了数据与结构两端的共同答案。
   - **局限**：主要证据来自自建硬件、四个真实任务和任务特定后训练，61% 不是零样本泛化结果。触觉传感器耐久、遥操作偏差、跨手型和跨材料泛化仍需更大范围验证。

8. [DWMP: Leveraging Dual World Models for Humanoid Obstacle Traversal](https://arxiv.org/abs/2609.12347)

   - **作者／机构**：Rongjun Jin、Jianming Ma、Yue Gao；arXiv 摘要页未显式列出机构。
   - **问题与机制**：本体感知是低维但受强非线性动力学支配，第一视角深度则高维、噪声大且冗余。DWMP 用 Koopman 动力学世界模型把本体状态提升到近似线性 latent，用 RSSM 视觉世界模型压缩深度观察并保留障碍几何，再融合两种表示供学生策略生成动作。
   - **实验**：在仿真和 Unitree G1 人形机器人上测试随机障碍布局；作者报告相对基线提升障碍穿越表现，并支持真实部署。
   - **关注价值**：不是把所有模态硬塞进一个编码器，而是按观测的物理属性拆分世界模型，再在策略端融合，适合继续研究“表示专门化后如何共享决策”。
   - **局限**：当前任务集中在障碍穿越，且依赖固定人形本体、深度相机和两类专门模型；摘要没有给出跨任务、跨本体或长时 rollout 的量化结果，仿真到真机的收益边界仍需补充。

## 世界模型与具身评测

9. [IMPLY: Physically Anchored Consistency for World-Model Rollouts](https://arxiv.org/abs/2609.12441)

   - **作者／机构**：Aman Mehta、Riya Baviskar；arXiv 摘要页未显式列出机构。
   - **问题与机制**：只检查多个 rollout 是否彼此一致，可能奖励一个始终预测“典型结果”但没有识别当前物体的模型。IMPLY 对 rollout 反演物理模拟器，读取其隐含的质量、摩擦等参数，再用模型观察到的两次 calibration push 作为证据锚点，评价同一组 rollout 是否能由同一个物体解释。
   - **实验**：在受控设置与适配场景的 V-JEPA 2-AC 上测试。使用模型自己的 calibration push 时，每对象预测与真实值的相关系数为 0.91，换用其他对象的 calibration push 后降到 0.05；普通 self-consistency 选择正确证据的比例约 52%，锚定不一致性提高到 73%，与 rollout 误差的相关性为 0.92–0.99；用于候选 rollout 选择时，结果距离看见真值的 oracle 仅 0.003。
   - **关注价值**：把世界模型评测从“未来之间像不像”推进到“未来是否与真实证据和可反演物理一致”，可直接服务 rollout 过滤、策略排序和安全回归。
   - **局限**：方法需要可用的模拟器或逆物理模型，以及额外 calibration push；当前证据主要是受控物理和一个适配的视觉世界模型，并非真实机器人长时闭环。未知物体、复杂接触和不可逆形变的参数可辨识性仍是开放问题。

10. [Embodied-BenchForge: A Closed-Loop Agentic Workflow for Embodied Benchmark Construction](https://arxiv.org/abs/2609.13082)

   - **作者／机构**：Baoyang Jiang、Fengchun Zhang、Leyuan Wang、Haotian Li、Yida Wang、Zhe Ji、Jinshan Lai、Xi Ren、Danyang Li、Zheng Yang、Jianwei Hu、Qiang Ma；arXiv 摘要页未显式列出机构。
   - **问题与机制**：具身 benchmark 的多步构建会产生相互依赖的中间 artifact，局部缺陷若没有逐项核验就会传播到最终评测。BenchForge 把构建定义为闭环合成：typed skills 负责可复用生成，artifact dependency graph 记录依赖，requirement-guided contracts 做逐项验证，provenance 决定局部重执行或回滚上游步骤。
   - **实验**：生成覆盖多个具身场景的 6 个 Offline EQA benchmark，以及一个含 220 个可执行任务的 Interactive benchmark；用代表性 MLLM 和具身 Agent 检验区分能力，另做质量评估、消融、repair 效率和 skill reuse 分析。
   - **关注价值**：把 benchmark 当成需要版本、依赖、契约和恢复机制的软件 artifact，而不是一次性手工题集；这与具身系统的可复现、可审计训练闭环直接相关。
   - **局限**：论文验证的是评测构建质量和 Agent 区分度，不是现实机器人安全或真实世界任务成功率。闭环修复的上限取决于需求契约、生成环境和 provenance 是否完整，未来仍需跨平台、跨仿真器和真机 benchmark 复核。

## 趋势总结

- **安全进入接口层**：舒适包络、风险场和 CBF 分别约束动作空间、候选轨迹评价和可行安全集，安全不再只是训练后的单一 penalty。
- **VLA 正在拆分“语义、未来和动作”**：Dynin 用共享 masked-diffusion 组合多个目标，LIT 约束视觉只通过任务相关空间接口进入动作专家，DWMP 则按模态物理属性拆分世界模型。
- **真实部署证据更重视过程状态**：触觉数据、接触冲击、障碍穿越、物理锚定 rollout 和 benchmark provenance 都在补“做成了没有”之外的中间证据。
- **下一步核查重点**：跨本体与跨传感器泛化、真实闭环延迟、复杂接触下的物理可辨识性，以及这些显式接口是否能稳定降低长尾风险，而不是只改善离线分数。
