arXiv 自动驾驶与机器人晨报｜2026-06-18

说明：我先检索了 2026-06-16 至 2026-06-18 的最新 arXiv 更新；由于“自动驾驶/机器人”高相关新稿主要集中在 06-16 与 06-15，且自动驾驶纯相关论文数量不多，以下补入 06-12 的一篇高相关停车规划论文，并在各条目中明确日期。

【自动驾驶】
1. ParkingTransformer: LLM-Enhanced End-to-End Trajectory Planning for Autonomous Parking
链接：https://arxiv.org/abs/2606.17082
作者：Hauteng Wu, Xu Li, Dong Kong, Zihang Wang, Xieyuanli Chen, Benwu Wang, Wenkai Zhu
时间：2026-06-12 提交/更新
问题/痛点：端到端自动泊车方法通常像黑盒，既缺少高层语义理解，也不容易解释；从道路到车位的长距离泊车尤其需要同时处理多视角感知、历史信息和几何约束。
核心创新：把多视角感知与 LLM 的场景理解能力直接接进轨迹规划，不再依赖稠密 BEV；再用 3D 位置编码补 LLM 的空间推理短板。
方法机制：模型以 trajectory queries 为核心，联合历史信息与原始传感输入生成规划轨迹；固定窗口流式历史机制提升长时序效率；粗到细解码逐步细化轨迹精度。
实验与结果：摘要给出 CARLA 闭环 driving score 61.32，真实车辆平均成功率 88.70%。这说明它不是只在离线指标上好看，而是直接面向闭环与实车。
为什么值得关注：这条路线把“语言模型负责语义、几何编码负责空间、解码器负责轨迹”拆得比较清楚，代表自动驾驶端到端规划开始从纯感知-控制映射转向“可解释语义引导规划”。
可能局限/跟进：摘要未给出与强 BEV 基线的细粒度场景分解，也没有说明复杂动态交通中的鲁棒性边界；后续值得跟踪它在开放道路、长尾障碍物和失配地图下是否仍成立。

2. SPARK: Low Latency Single-Camera 3D Pose Estimation for Autonomous Racing using Keypoints
链接：https://arxiv.org/abs/2606.17936
作者：Dominic Ebner, Markus Lienkamp
时间：2026-06-16 提交/更新
问题/痛点：自动驾驶竞速需要极低时延地感知对手车辆姿态；LiDAR 检测虽然强，但在高速动态场景里成本、延迟和边缘部署难度都偏高。
核心创新：用单目关键点检测来做 3D 姿态估计，利用赛道场景的固定几何先验，换取更低延迟和更高部署性。
方法机制：整体基于优化后的 YOLO 关键点检测器，先提取与赛车几何相关的关键点，再结合赛道/车辆结构约束恢复 3D pose；重点不是通用 3D 检测，而是针对自动竞速场景做任务特化。
实验与结果：作者称其在真实自动竞速数据上，精度超过现有 SOTA 单目视觉检测器，同时延迟低于 LiDAR 和其他相机方案，且保持较低资源占用。
为什么值得关注：这类“场景受限但工程极强”的工作，对高动态自动驾驶子领域很重要；它提示我们并不是所有 3D 感知都必须走大一统通用模型，强先验下的小模型可能更有效。
可能局限/跟进：泛化能力可能严重依赖赛道几何和目标外形先验；后续需要看它迁移到开放道路、非合作目标多样化和遮挡场景时还能保留多少优势。

【机器人/具身智能】
3. Visual Verification Enables Inference-time Steering and Autonomous Policy Improvement
链接：https://arxiv.org/abs/2606.18247
作者：Mingtong Zhang, Dhruv Shah
时间：2026-06-16 提交/更新
问题/痛点：通用机器人策略部署后通常不会“边做边变强”；如果继续采集专家示范，成本高且扩展性差。
核心创新：提出 VERITAS，把预训练通用策略当 generator，再配一个无梯度 visual verifier，在推理时直接验证动作质量并做 steering；随后再把经过验证的自生成轨迹反哺离线微调。
方法机制：第一阶段是 inference-time verification，对候选动作做视觉层面的好坏打分；第二阶段把这些 verified rollouts 当监督信号做 self-improvement，相当于把“执行时筛动作”和“执行后自举训练”串起来。
实验与结果：摘要明确说，纯推理期验证已稳定优于原始 generalist policy；再用 verified rollouts 进行后训练后，性能继续稳定提升，而且效率可与专家示范接近，同时不需要人工介入。
为什么值得关注：这非常像机器人版 test-time compute + self-training，核心价值不在单次提分，而在于给“部署后持续进化”提供了一个现实可落地的闭环。
可能局限/跟进：验证器本身的误判会不会把策略带偏，是关键风险；另外该框架依赖视觉可验证性，遇到延迟奖励、接触隐变量或不可见失败模式时可能效果下降。

4. ThinkingVLA: Interleaved Vision and Language Reasoning for Robotic Manipulation
链接：https://arxiv.org/abs/2606.17937
作者：Tianyi Lu, Hui Zhang, Zijie Diao, Junke Wang, Shengqi Xu, Xingyao Lin, Guojin Zhong, Ziyi Ye, Peng Wang, Zuxuan Wu, Yu-Gang Jiang
时间：2026-06-16 提交/更新
问题/痛点：许多 VLA 模型还是从观察直接回归动作，面对长程、多步、需要空间推理的任务容易失效；现有 CoT 式方法也常把语言推理、视觉预测和动作生成拆得过散。
核心创新：提出统一自回归框架，把“前向预测下一视觉子目标”和“基于目标状态反推动作”的逆向推理交织在同一个生成过程中。
方法机制：ThinkingVLA 采用统一的 Mixture-of-Transformers 架构。先用 forward CoT 定位当前子目标并预测下一视觉状态，再把预测图像作为目标状态输入 inverse CoT，显式推理空间关系与动作意图，最后输出动作。
实验与结果：摘要没有给出具体数字，但强调其在仿真和真实世界基准上持续超过现有 SOTA，且在长时序 manipulation 任务上的提升尤其明显。
为什么值得关注：它不是简单给 VLA 加“会说话的思维链”，而是把“看见未来状态”纳入中间表示，这使操控推理从语言链条扩展为视觉-语言联合计划。
可能局限/跟进：中间预测图像的误差会级联影响动作；未来值得看它在接触密集任务、遮挡、以及多机器人协作操控中的稳定性。

5. EBench: Elemental Diagnosis of Generalist Mobile Manipulation Policies
链接：https://arxiv.org/abs/2606.18239
作者：Ning Gao 等 25 位作者
时间：2026-06-16 提交/更新
问题/痛点：通用移动操作模型常被一个总 success rate 排名，但这个指标掩盖了模型究竟擅长“移动”“抓取”“灵巧操作”还是“泛化”中的哪一部分。
核心创新：提出诊断型基准 EBench，用 26 个任务、5 个能力维度、4 个泛化维度去拆解 generalist policy，而不只给一个总分。
方法机制：评测对象包括 π0、π0.5、XVLA、InternVLA-A1 等模型；除测试成功率外，还分析 train-test retention、分布偏移因素和各原子技能能力轮廓。
实验与结果：摘要给出关键发现：π0.5 测试成功率和 train-test retention 最优；InternVLA-A1 在移动操作上最强，但在灵巧任务上明显崩塌；XVLA 在与其他模型不同的一组 atomic skills 上占优。
为什么值得关注：机器人基础模型现在最缺的不是再来一个 leaderboard，而是知道“模型到底差在哪”；这种诊断基准会直接影响后续数据配比、架构设计和训练目标。
可能局限/跟进：作为仿真 benchmark，现实世界外推仍需谨慎；如果后续能补入实机诊断集或长程任务误差分解，会更有实际指导意义。

6. EvolveNav: Proactive Preflection and Self-Evolving Memory for Zero-Shot Object Goal Navigation
链接：https://arxiv.org/abs/2606.18235
作者：Qi Chai, Wenhao Shen, Nanjie Yao, Yue Xia, Kaiyong Zhao, Jie Ma, Guosheng Lin, Hao Wang
时间：2026-06-16 提交/更新
问题/痛点：零样本目标导航常依赖 foundation model 的静态常识，但测试时不会真的“从犯错里学”，导致重复试错、探索成本高。
核心创新：把 test-time adaptation 做成 agentic memory。模型一边跑任务，一边把过去轨迹提炼成可执行规则；同时在行动前做 preflection，先预测潜在结果再决定动作。
方法机制：一是 self-evolving rule memory，二是基于 UCB 的检索策略，在语义相关性与历史成功率之间做平衡，三是 memory-guided preflection 以减少无效探索。
实验与结果：摘要给出相对明确的数据：在零样本 Object-Goal Navigation 上，成功率比现有 baseline 高 10.1%，而且无效步数更少。
为什么值得关注：这是“把试错经验产品化”为导航记忆的代表工作，说明 embodied agent 的 test-time learning 正从纯 prompt/反思走向更结构化的规则记忆。
可能局限/跟进：规则提炼质量和记忆污染会直接影响后续决策；值得继续看它在开放世界目标歧义、错误观测和长时间运行时是否会出现灾难性偏置。

【交叉方向】
7. Qwen-RobotNav Technical Report: A Scalable Navigation Model Designed for an Agentic Navigation System
链接：https://arxiv.org/abs/2606.18112
作者：Jiazhao Zhang 等 33 位作者
时间：2026-06-16 提交/更新
问题/痛点：指令跟随、找物、跟踪、甚至自动驾驶，都共享感知-规划骨架，但对视觉历史的读取策略不同；传统导航模型通常缺少这种推理时可重配置性。
核心创新：提出带参数化接口的导航底座模型，把“任务模式”和“观察参数”都开放给上层 agent，在同一 backbone 上动态切换。
方法机制：Qwen-RobotNav 在训练时对 task mode、token budget、camera weights 等参数做随机化，使模型在推理期无需改结构就能适配不同导航形态；长程任务由上层 planner 分解子任务，再多次调用同一模型完成组合行为。
实验与结果：摘要称其基于 1560 万样本训练，在主要导航 benchmark 上达到新的 SOTA，并在 2B 到 8B 参数规模间呈现良好扩展，同时保持对真实机器人场景的强零样本泛化。
为什么值得关注：它把“导航基础模型”定义成可编排的底层服务，而不是单一固定任务模型，这个思路与 agent system 的工程形态很一致。
可能局限/跟进：技术报告体例下，很多 benchmark 细节和失败案例尚未完全展开；后续需要跟踪公开代码、评测细表与真实部署成本。

8. RICH-SLAM: Radar SLAM with Incremental and Continuous Hilbert Mapping
链接：https://arxiv.org/abs/2606.17534
作者：Bingbing Zhang, Huan Yin, Yang Xu, Shuo Liu, Shaojie Shen, Fumin Zhang, Wen Xu
时间：2026-06-16 提交/更新
问题/痛点：雷达在雨雾夜间更稳，但数据稀疏且噪声大，传统 radar SLAM 很难同时得到连续、致密、可量化不确定性的地图。
核心创新：把 Rao-Blackwellized particle filter 后端与增量式 Hilbert 空间降秩高斯过程建图结合，直接做连续占据地图和不确定性感知建图。
方法机制：粒子滤波负责位姿，Kalman filtering 更新地图；posterior-aware particle weighting 利用地图参数后验来做更稳健的似然评估；核心不是单点栅格，而是连续函数空间表示。
实验与结果：作者在自采数据和公开 ColoRadar 数据集上验证，能从稀疏 radar 测量构建连续 occupancy map，并支持 uncertainty-aware planning。
为什么值得关注：自动驾驶和户外机器人都在重新重视雷达，这篇工作代表 SLAM 社区正把关注点从“能不能定位”推进到“能不能输出可规划、可带不确定性的连续地图”。
可能局限/跟进：摘要未给出与视觉/激光方案的量化差距，且高斯过程映射的实时性与大场景扩展性仍需观察。

【趋势总结】
1. 最近一批论文最明显的共同点，是“test-time intelligence”在变重：VERITAS 做推理期验证与自提升，EvolveNav 做推理期记忆演化，Qwen-RobotNav 做推理期配置切换。相比过去一次训练、固定部署的范式，系统开始强调上线后还能持续调整。
2. VLA/具身模型不再满足于“观察到动作”的短路映射，ThinkingVLA 这类工作把视觉预测、逆向推理和动作生成显式串联，说明长程操控正在从 end-to-end imitation 走向显式中间推理。
3. 自动驾驶方向的增量点集中在“语义可解释规划”和“高动态低延迟感知”：ParkingTransformer 把 LLM 接入泊车规划，SPARK 则反过来证明任务特化的小模型在竞速场景里更现实。
4. 评测与系统层研究比单纯新 backbone 更值得看。EBench 说明社区正在补“诊断工具链”，而 RICH-SLAM 说明传感器融合与可规划地图表征仍然是机器人落地的硬问题。
5. 与前两年的通用基础模型热潮相比，这一批工作的真正新意不只是“模型更大”，而是把验证器、记忆、上层 planner、结构化 benchmark 和连续地图这些系统组件重新放回核心位置。
