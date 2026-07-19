arXiv 自动驾驶与机器人晨报｜2026-07-19

说明：今天是周日，arXiv 7 月 18–19 日无常规新批次；以下选自当前最新的 2026-07-16（UTC）提交，避免用旧论文冒充“今日新稿”。作者机构若摘要页未明确披露则不推断。

【自动驾驶】

1. WorkDrive: Roadwork Chain of Causation for Autonomous Driving
链接：https://arxiv.org/abs/2607.14727
作者：Tianyi Jiang、Wen Zhang、Sihan Yang、Ming Lu、Wentao Zhang；提交：2026-07-16。
问题：施工区会移除/改写车道线、永久标志等熟悉线索，锥桶和围栏临时定义可行驶走廊；驾驶 VLM 即使看见物体，也容易继续依赖预训练中的常规道路先验，无法把施工元素连到正确规划。
创新与机制：提出面向施工区的“因果链”（CoC）。自动多任务感知先抽取结构化场景事实，再把事实注入标注流水线，强制推理关注施工域元素；先用因果推理标签监督微调，再用“横向元动作与预测轨迹是否一致”这一单一奖励做 GRPO，使语言决策和几何轨迹闭环对齐。
实验/结果：在最大公开施工区数据集 ROADWork 上，CoC 相对仅轨迹基线将轨迹 ADE 降低 9.0%，一致性 GRPO 再降 3.0%。
为何关注：它不是继续堆通用 VLM，而是用领域因果结构纠正视觉先验，并用可计算的一致性奖励连接 reasoning 与 planning。
局限/跟进：摘要只报告 ROADWork；应检查对未见施工布局、夜间/恶劣天气、纵向动作及真实闭环安全指标的泛化。代码和数据尚为“将公开”。

2. MIND-CAVs: Multi-Intelligence Negotiation and Decision System for CAVs based on Intent-Driven Autonomy
链接：https://arxiv.org/abs/2607.14688
作者：Mainak Mondal、Yihang Feng、Yangchao Luo、Han Song；提交：2026-07-16。
问题：现有车联网多交换 BSM 低层运动状态，或有限共享传感器，很少交换“准备并线/驶出”等高层意图；多车冲突因此仍由孤立决策器处理。
创新与机制：车辆把原始观测压缩成结构化意图，通过 V2X 送往路侧边缘服务器；边缘智能体混合学习式与规则式仲裁，协商冲突意图并返回全局一致方案，云端记录决策以便审计和持续训练。核心新意是把协同对象从感知/轨迹提升到可审计的意图层。
实验/结果：在 CARLA AI-in-the-loop、多车道高速、冲突机动与受路线约束出口场景中，相比孤立自治、先到先服务和多智能体 RL，缩短机动完成时间，并减少不安全近距与无谓制动；摘要未给绝对数值。
为何关注：给“车端—路侧—云端”协同决策提供了较完整的系统接口和基线比较，适合观察 edge-assisted cooperative driving 是否从信息共享转向谈判。
局限/跟进：仍是仿真；通信延迟/丢包、恶意或错误意图、边缘单点失效、混合仲裁的形式安全保证是落地关键。

3. Variational Inference for Bird's Eye View Segmentation in Autonomous Driving
链接：https://arxiv.org/abs/2607.14710
作者：Jingyue Shi、Huaicheng Li、Junhui Zhao、Yanxiang Jiang；提交：2026-07-16。
问题：多摄像头到统一 BEV 的映射天然多解且受遮挡、复杂道路环境影响，常规确定性投影/融合难表达不确定性。
创新与机制：TVB 将 BEV 分割重写为变分推断：用 CVAE 和训练期后验 BEV 监督隐式学习多视角到规范 BEV 的映射，并生成多个候选地图；normalizing flow 扩展潜变量分布表达力，BEV-attention fusion（BAF）再自适应融合候选。
实验/结果：在 nuScenes 与 OPV2V 上评估多相机 BEV 分割和车道环境感知，摘要称优于现有方法，但未披露具体指标与提升幅度。
为何关注：相比只输出单一 BEV，候选分布更贴近遮挡场景的认知不确定性，也可能为下游规划提供风险信息。
局限/跟进：需核对候选多样性是否真正校准、BAF 是否把分布重新压成过度自信单解，以及计算开销和跨域鲁棒性。

【机器人／具身智能】

4. RoboTTT: Context Scaling for Robot Policies
链接：https://arxiv.org/abs/2607.15275
作者：Yunfan Jiang、Yevgen Chebotar、Ruijie Zheng、Fengyuan Hu、Yunhao Ge、Jimmy Wu、Tianyuan Dai、Scott Reed、Li Fei-Fei、Yuke Zhu、Linxi “Jim” Fan 等；提交：2026-07-16。项目页：https://research.nvidia.com/labs/gear/robottt/
问题：机器人基础策略通常只看一步或很短历史，长时装配、扰动恢复、从示范即时学习所需的上下文无法保留；直接加长 Transformer KV 又会推高延迟。
创新与机制：把 Test-Time Training 嵌入 VLA，令循环状态不是不断增长的 token，而是推理时也由梯度下降更新的“fast weights”，把历史压进权重空间；训练以 sequence action forcing 配合截断 BPTT，将视觉—动作上下文扩到 8K timestep，较当前策略长三个数量级，同时不随上下文增长推理延迟。
实验/结果：真实机器人困难操作任务总体性能比单步上下文基线提升 87%；完成基线从未完成的 5 分钟、10 阶段装配；8K 预训练比同模型 1K 上下文高 62%。还展示单次人类视频上下文模仿、在线改进和扰动鲁棒性。
为何关注：把“上下文长度”明确变成机器人基础模型的新 scaling axis，并提供了一条绕开 KV 成本的机制路线。
局限/跟进：推理期梯度更新的稳定性、遗忘与安全边界，以及跨机器人/跨任务的长期累积误差仍需验证；强结果主要来自作者设定的真实任务。

5. Scaling Behavior Foundation Model for Humanoid Robots
链接：https://arxiv.org/abs/2607.15163
作者：Weishuai Zeng、Kangning Yin、Xiaojie Niu、Shunlin Lu、Weixiang Zhong、He Wang、Li Yi、Dahua Lin、Jiangmiao Pang、Jingbo Wang 等；提交：2026-07-16。
问题：人形全身控制既要自然协调、实时跟随，又要跨行为和环境泛化；已有 BFM 虽显示潜力，却缺少数据、训练范式和架构如何协同扩展的清晰 recipe。
创新与机制：用全局坐标下整合全身行为复现的 motion tracking 统一多类控制问题；联合扩大 on-policy rollout 数量与参考动作多样性；设计可扩展 Humanoid Transformer，让结构化行为表征随规模自然出现。
实验/结果：仿真加真机部署；相较现有人形控制器，测试集平均关键点位置误差 MPKPE 在 local mode 降逾 10%，global mode 降 82%，并提升控制保真和任务泛化。
为何关注：它把“扩模型”改写为训练数据覆盖、在线采样和全身表征三者的联合 scaling，可能成为通用人形控制的基础配方。
局限/跟进：摘要未说明模型/数据规模曲线、真机任务覆盖和实时算力；需确认提升是否来自数据量而非架构，以及接触丰富任务的稳定性。

6. SoftNav: Injecting 3D Scene Tokens into VLMs for Embodied Navigation
链接：https://arxiv.org/abs/2607.14586
作者：Yi Wu、Junjie An、Xiao Liu、Yiqun Zhou、Yuechen Wu、Xiaoqing Guan、Shuyang Yu、You Wang、Guang Li；提交：2026-07-16。
问题：目标导航方法常把 3D 场景序列化成文本喂给 VLM，丢失连续几何关系；作者的受控消融显示 embedding 级传递明显优于所测文本格式。
创新与机制：把每个检测物体或 frontier 编成一个实体级连续 3D 表征，经轻量 projector 注入 VLM 隐空间作为 soft token；冻结 3D encoder 和 VLM，仅训练约 17M 参数，用约 1,200 样本完成对齐。
实验/结果：HM3D-OVON 三个 split 的 SR 为 74.2%/68.3%/66.7%，SR 与 SPL 均超此前方法；同一策略零样本迁移至 GOAT-Bench（67.2% SR）、SG3D（47.2% s-SR）及真实机器人，无需重训或改架构。
为何关注：结果说明具身系统不必把几何“翻译成句子”，小型接口层即可复用冻结 VLM，同时获得显著迁移性。
局限/跟进：依赖上游检测/3D 编码质量；应测试动态场景、长期记忆、frontier 数量扩展，以及不同 VLM/传感器下是否仍成立。

【交叉方向：世界模型 × 规划】

7. DriftWorld: Fast World Modeling through Drifting
链接：https://arxiv.org/abs/2607.15065
作者：Susie Lu、Haonan Chen、Weirui Ye、Yilun Du；提交：2026-07-16。
问题：预测世界模型要支持规划，必须快速生成大量候选动作 rollout；扩散模型多步去噪使想象成为在线搜索瓶颈。
创新与机制：用 drifting generative model 学习动作条件 drift，把原本推理期的迭代去噪搬到训练中；给定当前观测和候选动作序列，只需一次前向就生成未来帧。由此把世界模型从“高质量但慢的视频生成器”改造成可参与实时 action search 的模拟器。
实验/结果：在 Bridge-V2、RT-1、Language Table、Push-T、Robomimic 等视觉操作基准上达到 30+ fps，平均比扩散基线快 17 倍，并以更少推理时间取得 SOTA 决策表现；离线排序真实机器人策略时，rollout 分数与真实结果相关性最高 0.99。
为何关注：世界模型是否有用常由每秒能评估多少动作决定；单步生成直接改善规划预算，也兼顾离线 policy evaluation。
局限/跟进：单步生成可能牺牲多模态未来覆盖；需检查长时误差累积、真实闭环部署、稀有失败预测及 0.99 相关性在不同策略分布上的稳健性。

【趋势总结】
1）研究重心由“看懂场景”转向“让中间表征直接约束动作”：WorkDrive 用轨迹一致性奖励约束因果推理，MIND-CAVs 直接交换可协商意图，SoftNav 则绕过文本瓶颈传递 3D token。
2）机器人 scaling 出现两条新轴：RoboTTT 扩的是可压缩的时间上下文，Humanoid BFM 扩的是 rollout × 行为多样性 × 架构协同；相比单纯加参数，更关注闭环经验和行为覆盖。
3）世界模型开始从生成质量竞赛转向决策吞吐：DriftWorld 的核心指标是单次前向、30+ fps 和 action-search 效率，说明“能否实时多想几步”正在取代单纯视频逼真度。
4）不确定性和分布式自治被显式建模：TVB 输出候选 BEV 分布，MIND-CAVs 处理多车冲突意图。下一步值得跟踪的共同问题是校准、安全约束、通信失效和真实道路/真机泛化。
