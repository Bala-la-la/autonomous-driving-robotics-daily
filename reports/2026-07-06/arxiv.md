arXiv 自动驾驶与机器人晨报｜2026-07-06

说明：按北京时间 2026-07-06 早晨检索。由于周末与美国假期窗口，当前能稳定检索到的最新高相关 arXiv 提交/更新主要集中在 2026-07-02 UTC 与 2026-07-01 UTC；本期覆盖最近 3-5 天内最值得关注的 7 篇论文。

【自动驾驶】
1. Drive-JEPA: Video JEPA Meets Multimodal Trajectory Distillation for End-to-End Driving
链接：https://arxiv.org/abs/2601.22032
作者/机构：Linhan Wang, Zichong Yang, Chen Bai, Guoxiang Zhang, Xiaotong Liu, Xiaoyin Zheng, Xiao-Xiao Long, Chang-Tien Lu, Cheng Lu；机构未在 arXiv 摘要页明确列出
时间：首次提交 2026-01-29，最新更新 2026-07-02
要解决的问题：端到端驾驶近两年大量引入视频自监督预训练，但“看懂场景”并没有稳定转化成“更会规划”；同时真实驾驶数据通常只给出单一人类轨迹，难以学到多模态、安全且可恢复的驾驶行为。
核心创新点：把 V-JEPA 这种视频联合嵌入预测架构真正拉到驾驶规划里，不只学视觉表征，还通过多模态轨迹蒸馏把“可能但没被人类演示过”的候选轨迹灌进规划器；用 momentum-aware 的候选选择机制抑制不稳定或冒险轨迹。
方法/结构：先用大规模驾驶视频预训练 ViT 编码器，得到更偏预测式的时空表示；再接一个 proposal-centric planner，把仿真器生成的多样轨迹与人类轨迹一起蒸馏进 transformer 解码器；训练时显式对齐轨迹规划目标，而不是只做通用视频预测。
实验与结果：在 NAVSIM 上，单用 V-JEPA 表征配简单 transformer decoder，就比此前 perception-free 方法高 3 PDMS；完整 Drive-JEPA 在 v1 上做到 93.3 PDMS、在 v2 上做到 87.8 EPDMS，摘要称为新的 SOTA。
为什么值得关注：这篇不是单纯“再做一个更大 backbone”，而是在自动驾驶里把 world-model 风格的预测表征和多轨迹监督真正耦合起来，说明预训练要想转化为闭环收益，关键不是视觉模型越大越好，而是要把规划歧义一起建模。
可能局限/后续点：摘要没有展开仿真候选与真实分布的偏差控制，也没有说明极端 corner case 下的安全边界；后续要看其在闭环真实车、长尾交互与失配导航条件下是否仍能保持优势。

2. Open-Weather Robust 3D Detection via Dual-Critic Diffusion Alignment
链接：https://arxiv.org/abs/2607.01983
作者/机构：Shuyao Li, Chuanxing Geng, Heyang Sun, Qiang Zhou, Jingjing Gu；机构未在 arXiv 摘要页明确列出
时间：提交/更新于 2026-07-02
要解决的问题：恶劣天气下的 3D 检测一直受“闭世界天气假设”限制，很多方法默认训练和测试天气类型、强度一致；现实里雨雾雪组合、甚至同为降雨但粒度不同，都会让 LiDAR 退化模式完全变形。
核心创新点：不再显式学习“天气标签到补偿策略”的映射，而是学习把退化 LiDAR 特征拉回“晴天干净特征流形”；用双 critic 同时约束目标级判别性与整体分布一致性。
方法/结构：提出 DCDA。主干是 4D radar 条件化 diffusion，对退化 LiDAR 特征逐步去噪；critic 1 是 detection-guided critic，借助预训练晴天检测器保证语义与定位不丢；critic 2 是 weather adversarial critic，逼近干净天气特征分布。整个框架不要求成对天气样本，也不依赖显式天气标签。
实验与结果：论文额外构造了 held-out type-severity 组合的 open-weather benchmark，用来专门考察“没见过的天气类型/强度”；摘要给出结论是对未见天气有稳定泛化优势，但未在摘要中列出具体数值。
为什么值得关注：自动驾驶鲁棒性研究正在从“多加几种天气做数据增强”转向“把退化感知恢复到任务可用特征空间”，这比做天气分类更贴近量产系统需求；4D radar 在这里承担的不是简单补模态，而是作为跨天气 anchor。
可能局限/后续点：扩散式特征校正可能增加时延与算力成本；若 radar 本身噪声很大，双 critic 是否仍稳定还要看正文实验。值得继续跟踪其对实时栈、BEV 检测器和端到端驾驶器的迁移效果。

3. Comprehensive Robustness Analysis of LiDAR-based 3D Object Detection in Autonomous Driving
链接：https://arxiv.org/abs/2607.02074
作者/机构：Adwait Chandorkar, Kai Krink, Yerdana Maulenbay, Hasan Tercan, Tobias Meisen；机构未在 arXiv 摘要页明确列出
时间：提交/更新于 2026-07-02
要解决的问题：LiDAR-only 3D 检测近年精度涨得很快，但对抗鲁棒性评测明显滞后，已有工作多停留在旧模型，而且常常只看 mAP，忽略点云结构和预测行为层面的脆弱性。
核心创新点：把鲁棒性评测从单一精度指标，扩展成“结构因素 + 预测因素”的整体框架。结构上看点云密度与定位扰动，预测上看误分类、框定位误差以及与自车距离相关的脆弱性。
方法/结构：针对近期和旧版 SOTA LiDAR 检测器施加专门设计的 adversarial attacks，再用五类指标横向分析不同架构脆弱性，尤其比较 voxel-based、pillar-based、anchor-based 与 non-anchor-based 检测器。
实验与结果：摘要中的关键发现很明确：高容量 voxel-based 检测器比 pillar-based 更容易受结构化坐标扰动影响；non-anchor-based 检测器表现出更差的对抗鲁棒性；总体上“新模型并没有比老模型安全多少”。
为什么值得关注：这类工作虽然不直接提新模型，但对自动驾驶落地更重要。行业里常见现象是精度榜单持续刷新，安全性却缺少同步评估；这篇给了一个更像真实部署审计的鲁棒性视角。
可能局限/后续点：摘要没有给出涉及的数据集与攻击预算细节；后续要看是否覆盖多传感器融合检测器，以及这些发现能否反向指导鲁棒训练而不是停留在诊断。

4. CommonRoad-Game: A Human-in-the-Loop Simulation Framework for Autonomous Driving
链接：https://arxiv.org/abs/2607.01382
作者/机构：Yunfei Bi, Youran Wang；机构未在 arXiv 摘要页明确列出
时间：提交于 2026-07-01
要解决的问题：很多运动规划器只在回放数据或无真人参与的仿真里验证，难以评估在人车互动中的稳定性、效率与可解释行为；现有人在环平台又往往偏重、难迭代，且和主流自动驾驶研究生态割裂。
核心创新点：把人在环交互、轻量级仿真和 CommonRoad 生态整合到一个框架里，重点不是“逼真画面”，而是可重复地测试 motion planner 与真人驾驶者互动时的时序一致性和行为反馈。
方法/结构：采用多线程架构和稳健同步机制，把 simulation time 与 wall-clock time 对齐，确保人驾车和自动驾驶车的交互具备确定性；同时提供 scenario generation 模块，把人在环实验日志回灌成可复现测试用例。
实验与结果：摘要称其实现了稳定的时序同步、可扩展的多智能体仿真，并可无缝接入 CommonRoad-compatible motion planner；源码已公开到 GitHub，利于后续复现实验基准。
为什么值得关注：闭环自动驾驶评测正在从“静态 benchmark 打榜”转向“交互系统测试”。这篇虽然不是 perception/planning 模型创新，但它补的是评测基础设施短板，尤其适合研究规划、博弈与人机共驾。
可能局限/后续点：轻量架构通常会牺牲部分传感器和物理细节；后续值得看其是否支持更复杂 V2X、行人/骑行者行为建模，以及与 learned planner 的大规模批量回放闭环。

【机器人 / 具身智能】
5. VT-WAM: Visual-Tactile World Action Model for Contact-Rich Manipulation
链接：https://arxiv.org/abs/2607.02503
作者/机构：Shuai Tian, Yupeng Zheng, Yuhang Zheng, Songen Gu, Yujie Zang, Yuxing Qin, Weize Li, Haoran Li, Wenchao Ding, Dongbin Zhao；机构未在 arXiv 摘要页明确列出
时间：提交/更新于 2026-07-02
要解决的问题：接触丰富操作里，决定成败的往往是形变、压力、滑移和摩擦，这些信号既稀疏又常常视觉不可见。现有视觉-触觉策略通常只是把触觉拼到动作头里，却很少显式建模触觉随动作演化的动态。
核心创新点：提出 Visual-Tactile World Action Model，把未来视觉预测、未来触觉形变预测和动作生成放到统一 flow matching 框架里联合学；强调“先理解接触动力学，再决定动作”，而不是把触觉当额外 token。
方法/结构：两块设计最关键。其一是 Asymmetric Mixture-of-Transformers attention，用首帧视觉锚点对齐时序触觉动态；其二是 contact-gated AVTAG，让动作 query 在接触阶段更强依赖触觉证据，从而减少“看着对、摸着错”的动作。
实验与结果：在 6 个真实接触丰富操作任务上，VT-WAM 平均成功率 71.67%，比 Fast-WAM 高 26.67%，比 OmniVTLA 高 35.84%。消融显示：显式建模触觉形变动态、以及接触阶段的触觉引导，二者都不可缺。
为什么值得关注：具身模型近半年一个明显趋势，是从“纯视觉 VLA”往“多感知闭环控制”升级。这篇把 world model、触觉和动作生成联成一体，说明高难操作真正缺的不是更大语义模型，而是可预测的接触状态演化。
可能局限/后续点：多模态时序建模的训练成本和传感器标定复杂度都不低；后续要看任务迁移时是否依赖特定触觉硬件，以及对长时序装配/变形体操作的收益是否还能维持。

6. Learning to Move Before Learning to Do: Task-Agnostic pretraining for VLAs
链接：https://arxiv.org/abs/2607.02466
作者/机构：Junhao Shi, Siyin Wang, Xiaopeng Yu, Li Ji, Jingjing Gong, Xipeng Qiu；机构未在 arXiv 摘要页明确列出
时间：提交/更新于 2026-07-02
要解决的问题：VLA 的根本瓶颈仍是高质量专家演示太贵。论文提出一个很直接的判断：机器人学习里“怎么动”与“做什么”被长期混在一起训练，而语言监督其实只对后者必要。
核心创新点：提出 Decomposition Hypothesis，并据此设计 Task-Agnostic Pretraining (TAP) 两阶段范式。先用廉价、无标签的交互轨迹学 motor prior，再用少量带语言的专家数据做语义对齐。
方法/结构：第一阶段用 inverse dynamics 自监督，从 off-task 轨迹与 autonomous play 中学习身体运动规律；第二阶段只做轻量级语言 grounding。也就是说，先把物理可行动作空间学扎实，再让语言去选择其中哪种动作。
实验与结果：在 SIMPLER benchmark 上，TAP 用远少于 100 万条专家轨迹的标注量，表现却能匹配同级别大模型，并比标准 behavior cloning 高 10% 绝对值；在真实 WidowX 平台上，遇到相机扰动时仍保有 25% 成功率，而 internet-scale baseline 降到 0%。
为什么值得关注：这篇对 VLA 训练路线的批判很到位。它暗示“具身 scaling”未必先靠更大的互联网语料，而可能先靠把无标签机器人交互数据利用起来，这对低成本扩展机器人能力尤其关键。
可能局限/后续点：inverse dynamics 学到的 motor prior 能否覆盖复杂双臂、移动操作和长时序任务，还有待验证；另外 TAP 与更强 world model 或 reasoning supervision 结合后能否进一步放大收益，值得跟进。

7. WorldSample: Closed-loop Real-robot RL with World Modelling
链接：https://arxiv.org/abs/2607.02431
作者/机构：Yuquan Xue, Le Xu, Zeyi Liu, Zhenyu Wu, Zhengyi Gu, Xinyang Song, Bofang Jia, Ziwei Wang；机构未在 arXiv 摘要页明确列出
时间：提交/更新于 2026-07-02
要解决的问题：真实机器人 RL 的老问题没变：真实 rollout 太贵，每一次交互只看到一条实际发生的 action-outcome 轨迹，探索成本远高于仿真。
核心创新点：不是简单把 world model 生成的数据混进 replay buffer，而是构造一个 real-synthetic loop：真实轨迹驱动后训练 world model 产出更可信 synthetic transition，再通过 Policy-Paced Learning 控制哪些合成样本该在什么时候喂给策略。
方法/结构：先基于真实 rollouts 对 world model 做 post-training，尽量压低视觉 hallucination；再用 PPL 做样本选择和训练调度，在“合成数据带来覆盖提升”和“合成误差导致价值高估”之间找平衡。
实验与结果：在接触丰富和高精度操作任务上，相比 baseline，成功率提高 28%，训练步数减少 59%；world model 的视觉保真度也显著提升，PSNR 提高 19.4dB、SSIM 提高 0.47。
为什么值得关注：很多“world model + real robot RL”工作卡在 hallucination 一关，这篇的价值在于它没有回避假样本污染，而是把“何时信任合成样本”做成训练机制。若正文扎实，这会是现实机器人 RL 很有参考价值的一条路。
可能局限/后续点：摘要未交代任务规模、机器人类型和长时序任务稳定性；对更开放场景、非刚体或强遮挡任务，post-trained world model 是否还能保持高保真，值得继续观察。

【交叉方向】
8. Embodied.cpp: A Portable Inference Runtime of Embodied AI Models on Heterogeneous Robots
链接：https://arxiv.org/abs/2607.02501
作者/机构：Ling Xu, Chuyu Han, Borui Li, Hao Wu, Shiqi Jiang, Ting Cao, Chuanyou Li, Sheng Zhong, Shuai Wang；机构未在 arXiv 摘要页明确列出
时间：提交/更新于 2026-07-02
要解决的问题：VLA 和 WAM 模型在论文里常能跑通，但真正上机器人时往往被 Python 栈、后端依赖、batch-1 延迟和多频率闭环控制卡住；传统 serving runtime 解决的是请求响应，不是 embodied deployment。
核心创新点：提出面向具身模型的通用 C++ runtime，把 VLA/WAM 的共性执行路径抽象为五层架构，从输入适配到部署适配打通，强调多频率、低时延、可扩展 I/O，而不是只追吞吐。
方法/结构：五层分别是 input adapters、sequence builders、backbone execution、head plugins、deployment adapters；同时提供 latency-first fused inference、heterogeneous hardware backend abstraction，以及超出 token I/O 的具身接口。
实验与结果：在 HY-VLA 与 pi0.5 两个 VLA 部署上实现 100.0% 与 91.0% 闭环任务成功率；WAM 基准上把 block memory 从 312.2 MiB 降到 88.1 MiB。
为什么值得关注：具身方向现在已经不缺“会做任务的模型”，更缺“能稳定部署的系统栈”。这篇代表一个很现实的新趋势：论文贡献开始从模型本身转向运行时、编译与边缘部署基础设施。
可能局限/后续点：摘要给出的评测任务还偏有限；后续要看它对更多机器人硬件、更多 VLA/WAM 架构和更严格实时约束的适配广度。

【趋势总结】
1. 自动驾驶侧的增量，正在从“再做一个更高分的 detector/planner”转向“闭环可用性”：Drive-JEPA 把多模态轨迹蒸馏纳入预训练收益转化，DCDA 和 LiDAR 鲁棒性分析则都在正面处理开放天气与安全脆弱性，不再满足于封闭数据集精度。
2. 机器人侧的主线越来越清晰：纯视觉 imitation 已经不够，研究在同步补三块短板。第一块是身体经验的预训练（TAP）；第二块是接触与物理世界动态（VT-WAM、WorldSample）；第三块是部署运行时（Embodied.cpp）。
3. 与以往路线相比，新意在于“系统性耦合”而不是单点堆料。最近这批论文更少强调单一 backbone 更大，更多强调如何把表征、规划、触觉、world model、runtime 和安全评测连成闭环。
4. 接下来值得继续盯的方向：开放天气/开放分布鲁棒检测是否能进入实时车端；触觉驱动的 world-action model 能否扩展到更长时序装配；无标签 robot play 预训练是否会像互联网预训练那样成为 VLA 标配；以及推理 runtime 会不会成为具身模型落地的新竞争层。

信息来源：arXiv API 与论文摘要页，检索时间 2026-07-06 早晨。
