arXiv 自动驾驶与机器人晨报｜2026-06-23

时间说明：本期优先覆盖 arXiv 于 2026-06-22（UTC）最新提交/更新的高相关论文；本次无需回退到更早 3-5 天窗口。

一、自动驾驶
1. SparseWorld: Enhancing End-to-End Autonomous Driving via World Models with Sparse Scene Representation
链接：https://arxiv.org/abs/2605.24354
作者：Ruoyu Wang, Jingke Wang, Yukai Ma, Yuehao Huang, Shuangming Lei, Guanglin Xu, Aixue Ye, Yong Liu
时间：2026-06-22 更新 v2（初版 2026-05-23）
问题/痛点：现有驾驶世界模型多依赖稠密场景表示，算力开销大、冗余信息多，难以高效服务端到端规划。
核心创新：提出 SparseWorld，只预测“关键布局”而不是完整稠密未来场景，把世界模型从重建导向转为决策导向。
方法机制：先用 Sparse Dreamer 在潜空间里自回归预测未来地图元素与周边交通体，再把这些稀疏未来实例回馈给运动预测与轨迹规划模块，通过时空联合注意力建模未来交互。
实验与结果：在 nuScenes 开环规划指标上达到 SOTA，碰撞率仅 0.05%；在 Bench2Drive 闭环规划上也显著优于基线。
为什么值得关注：这条路线说明“世界模型不一定越全越好”，稀疏但任务相关的未来表征，可能更适合量产级自动驾驶栈。
局限/跟进：摘要未给出推理时延和不同稀疏度配置下的收益曲线；后续值得关注其在更长尾城市路况和多传感器设置上的稳定性。

2. UECP: Uncertainty-Enhanced Collaborative Perception
链接：https://arxiv.org/abs/2606.23046
作者：Kang Yang, Tianci Bu, Peng Wang, Deying Li, Wen Jie, Yongcai Wang
时间：2026-06-22 提交 v1
问题/痛点：车路协同/多车协同感知里，如何判断“哪个参与体的信息更可靠”一直是难点；很多方法直接学 confidence map，但它和检测头耦合，容易把检测误差再放大。
核心创新：把“置信度”换成由 LiDAR 点密度直接监督的 uncertainty map，让贡献权重来自物理证据而不是检测器自说自话。
方法机制：围绕 UAPF（Uncertainty-Aware Pyramid Fusion）设计粗到细融合，包括 UWD（不确定性感知下采样）和 UGRF（不确定性引导残差融合），在多尺度上保高质量信息、抑制噪声传播。
实验与结果：摘要给出的结论是，在真实数据集上，UECP 在效果和鲁棒性上都优于现有 SOTA；虽然未公开具体数字，但明确强调了把 uncertainty 深度嵌入融合流程带来的收益。
为什么值得关注：协同感知近两年从“拼更多视角”转向“拼更可信的视角”，这篇工作把物理可解释性直接放进融合权重，是很实用的工程方向。
局限/跟进：摘要没有列出具体 benchmark 名称与增益幅度；后续可跟进其代码和补充材料，看在低带宽通信、异构传感器和极端遮挡下是否仍稳。

3. A Generative Model for Closed-Loop Microsimulation of Signalized Intersections
链接：https://arxiv.org/abs/2606.23588
作者：Yash Ranjan, Rahul Sengupta, Anand Rangarajan, Sanjay Ranka
时间：2026-06-22 提交 v1
问题/痛点：传统交通微观仿真依赖手工行为模型，能拟合总体流量，但刻画不好真实路口中车辆间的异质交互；而纯轨迹预测模型又常在闭环运行时发散。
核心创新：提出 Enactor，把“可闭环运行”的生成式 actor-centric 路口仿真做成一套统一架构，兼顾行为多样性与长期稳定性。
方法机制：以车辆为预测主体、行人为上下文；采用相对路口中心的极坐标表示动态参与体与车道折线，再用时空分离注意力 Transformer 预测每个 actor 下一步运动分布；训练时引入 closed-loop curriculum，让模型习惯吃自己的预测。
实验与结果：在两个路口几何上的 4000 秒仿真中，Enactor 对 travel time 的 KL divergence 比近期 Transformer 基线低一个数量级以上，速度分布误差也明显更低；红灯闯灯次数较同基线降低一个数量级以上；在真实路口鱼眼相机数据上也优于 constant-velocity baseline。
为什么值得关注：这类闭环微观生成模型，对自动驾驶仿真、信控评估、数字孪生交通都是高价值基础设施，不只是学术上的轨迹预测改进。
局限/跟进：当前只预测车辆、不预测行人；后续若要服务更复杂城市自动驾驶测试，行人与非机动车的闭环行为建模仍是关键缺口。

二、机器人 / 具身智能
4. AutoDex: An Automated Real-World System for Dexterous Grasping Data Collection
链接：https://arxiv.org/abs/2606.23689
作者：Mingi Choi, Gunhee Kim, Jisoo Kim, Taeksoo Kim, Taeyun Ha, Jongbin Lim, Hanbyul Joo
时间：2026-06-22 提交 v1
问题/痛点：灵巧抓取最缺的不是模型，而是大规模、真实、带物理成败标签的数据；遥操作太慢且有人偏，仿真又不能真正保证接触有效。
核心创新：做了一个“全自动真实世界数据工厂”AutoDex，把候选抓取生成、20 相机感知、执行、成败打标、物体重置串成无人值守闭环。
方法机制：系统先在严重手物遮挡下用稠密多视角定位物体，再执行带碰撞监控的机器人动作，用 lift-and-hold 自动判定成功/失败，并主动重置物体姿态以暴露更多稳定抓取候选；最终形成可检索、可按可行性过滤的抓取数据库。
实验与结果：在 100 个物体、Allegro 与 Inspire 两类手上采到 3593 条真实抓取试验；同样 500 条轨迹的采集任务中，AutoDex 用时 10.3 小时，而遥操作要 49.4 小时，吞吐提升 4.8 倍；基于 AutoDex 验证库检索的抓取成功率 76%，显著高于仅仿真验证的 34%。
为什么值得关注：这不是又一个抓取 policy，而是把“数据基础设施”本身变成研究贡献，尤其适合当前具身学习从模型瓶颈转向数据瓶颈的阶段。
局限/跟进：当前规模仍主要针对抓取而非复杂接触操作；后续值得看它能否扩到 in-hand manipulation、接触丰富装配与更多末端形态。

5. LIBERO-Safety: A Comprehensive Benchmark for Physical and Semantic Safety in Vision-Language-Action Models
链接：https://arxiv.org/abs/2606.23686
作者：Rongxu Cui, Zongzheng Zhang, Jingrui Pang, Haohan Chi, Jinbang Guo, Saining Zhang, Shaoxuan Xie, Xin Jin
时间：2026-06-22 提交 v1
问题/痛点：VLA 模型最近在操作成功率上进展快，但“成功且安全”并不是一回事；目前缺少系统化、可程序化生成的安全 benchmark。
核心创新：提出 LIBERO-Safety，从物理安全和语义安全两侧构建参数化基准，并配套 keypose-driven 数据生成流水线，减少对人工遥操作的依赖。
方法机制：作者程序化生成具有随机性的安全关键场景，构建 19,664 条严格无碰撞示范，并对 8 个 VLA 和 2 个 embodied foundation models 做跨范式评测。
实验与结果：论文最重要的发现不是“谁最好”，而是揭示了 generalization-safety tension：训练多样性更高时，轨迹通常更安全，但任务成功率仍受制于轨迹合成不足和语义对齐失误。
为什么值得关注：具身模型从 demo 走向真实部署，安全 benchmark 会变成基础门槛；这篇文章提供了一个比较像“真实评测制度”的起点。
局限/跟进：摘要没有细列各模型分项排名；后续要看 benchmark 是否覆盖接触力、长时记忆和人机共场景等更难的安全维度。

6. LaST-HD: Learning Latent Physical Reasoning from Scalable Human Data for Robot Manipulation
链接：https://arxiv.org/abs/2606.23685
作者：Jiaming Liu, Yinxi Wang, Chenyang Gu, Siyuan Qian, Xiangju Mi, Hao Chen, Jiawei Chen, Qingpo Wuwu
时间：2026-06-22 提交 v1
问题/痛点：把人手示范迁移给机器人，若只做几何 retargeting，常会在真实物理交互上失效，因为“动作看着像”不等于“动力学意义一致”。
核心创新：提出 LaST-HD，把 human-hand 与 robot demonstration 对齐到共享的 latent reasoning space，不再只模仿手部轨迹，而是学习跨形态共享的物理推理。
方法机制：训练一个基于动作条件的 world model，在未配对的人手与机器人轨迹上合成统一 latent target；再用这个共享前向动力学空间监督 reasoning-before-acting 的 VLA 过程。作者还做了低成本 OOL Glove，用于采高精度人手关键点并作为通用动作监督。
实验与结果：通过 mixed human-robot co-training，LaST-HD 能仅凭人手示范提升对新物体、新场景和新位置的泛化；再加上 human-hand online correction，仅用 20 分钟 OOL glove 数据就能把新环境任务准确率推到 90% 以上。
为什么值得关注：这篇工作代表一个重要转向：具身模仿学习不再只解决“如何 retarget”，而是开始显式学习“跨 embodiment 的物理语义”。
局限/跟进：摘要没有给出与多少现有 retargeting/VLA 基线对比；后续要观察其共享 latent 是否能扩展到双臂协作、柔性物体和高频接触任务。

三、交叉方向：感知-动作-记忆
7. KEMO: Event-Driven Keyframe Memory for Long-Horizon Robot Manipulation with VLA Policies
链接：https://arxiv.org/abs/2606.23589
作者：Yihan Zeng, Minghao Ye, Yiyuan Chen, Yide Shentu, Philipp Wu, Zike Yan, Zhongyu Li
时间：2026-06-22 提交 v1
问题/痛点：长程操作里，同样的视觉观察可能出现在不同阶段，单看当前帧不够，动作取决于之前哪些关键步骤已经完成；而现有 memory 要么太密、压缩难，要么只记最近片段，容易忘掉早期关键事件。
核心创新：提出事件驱动的关键帧记忆插件 KEMO，只保留“状态真正发生任务相关变化”的关键时刻。
方法机制：结合机器人运动学与视觉过滤检测事件，把关键帧编码成紧凑的时序 memory token，再通过 cross-attention 与 gated residual fusion 融入当前视觉特征；同时对关键转折点附近样本加更高训练权重。
实验与结果：在多种真实双臂任务上，任务包含 2-6 个评分子阶段、执行时长 28-95 秒不等；相比无记忆基线，KEMO 的总任务成功率提升 23.6%，阶段完成率提升 34.1%。消融显示，事件驱动选帧优于均匀采样和“只看最近帧”。
为什么值得关注：具身长任务最近的关键问题不是再堆更大模型，而是怎样低成本地表示任务进度；KEMO 这类轻量记忆模块很可能比全历史压缩更实用。
局限/跟进：事件检测仍依赖运动学和视觉启发式；如果任务事件更隐式、更语义化，是否还能稳定抽到真正关键帧，需要进一步验证。

8. dVLA-RL: Reinforcement Learning over Denoising Trajectories for Discrete Diffusion Vision-Language-Action Models
链接：https://arxiv.org/abs/2606.23623
作者：Yuhao Wu, Yitian Liu, Weijie Shen, Mishuo Han, Wenjie Xu, Haotian Liang, Zhongshan Liu, Yinan Mao
时间：2026-06-22 提交 v1
问题/痛点：离散扩散 VLA 把视觉、语言、动作统一到离散 token 空间，很有吸引力，但此前基本停留在 SFT；一旦要上 RL，最终动作边缘概率不可 tractable，训练目标不好定义。
核心创新：把 denoising 过程本身视作 MDP，不优化最终动作边缘概率，而优化整条生成路径的联合概率，从而把 RL 真正接到 dVLA 上。
方法机制：将逐步去噪转移写成 step-wise path probability，并提出统一步数调度策略，按任务复杂度分配不同 denoising steps，在成功率和计算效率之间做任务级平衡。
实验与结果：在 LIBERO 上达到 99.7% 成功率；在 RoboTwin 2.0 上相比 SFT 基线提升 30.6%，同时与强势的 World-Action Model 基线保持竞争力。
为什么值得关注：这是“生成式动作模型 + RL”结合的一个强信号，说明未来具身策略优化不一定走传统 policy gradient 形态，也可能发生在生成轨迹空间。
局限/跟进：摘要没展开不同任务复杂度下的步数调度开销；后续可关注其训练稳定性、样本效率，以及是否能迁移到真实机器人闭环微调。

四、趋势总结
1. 自动驾驶侧，世界模型开始从“高保真场景重建”转向“对规划最有用的稀疏未来表示”，SparseWorld 是典型信号。
2. 多车/多体感知继续强调“证据质量”而不是“简单融合更多视角”，UECP 这类 uncertainty-as-physics-evidence 路线更偏工程可落地。
3. 机器人侧的主线非常明确：数据基础设施（AutoDex）、安全评测（LIBERO-Safety）、跨 embodiment 物理推理（LaST-HD）和长程记忆（KEMO）同时升温，说明社区已从“先做一个能动的通用策略”进入“把策略做稳、做长、做可部署”的阶段。
4. 与过去偏单任务 imitation learning 的路线相比，今天这批论文的新意在于更强调系统化闭环：闭环数据采集、闭环安全评测、闭环记忆更新、闭环 RL 优化，而不是只在静态离线数据上追一次性成功率。
