arXiv 自动驾驶与机器人晨报｜2026-06-17

时间范围：优先覆盖 2026-06-15 最新提交，少量补充 2026-06-14；以下均为已在 arXiv 原文页确认的论文。

【自动驾驶】
1. SurroundNEXO: Ego-Centric Metric Bridging for Spatially Consistent Geometry in Autonomous Driving
URL: https://arxiv.org/abs/2606.16960
作者：Shuai Yuan 等
提交时间：2026-06-15
问题/痛点：环视相机外向布置导致视角重叠很弱，传统多视图几何依赖跨视角对应，难做稳定的度量深度与跨视角一致性。
核心创新：把“跨视角找外观对应”改成“先在自车坐标系里对齐几何射线”。提出 Ego-Ray Positional Encoding，把各相机 token 先映射到可比较的 ego-frame viewing directions，再用稀疏 LiDAR 当尺度锚点，最后按“单视角-局部时空-全局融合”渐进交互。
方法/结构：低重叠多相机 metric depth 框架；核心是 ego-centric geometry + sparse depth anchoring + progressive feature interaction。
实验/结果：在 nuScenes、Waymo、DDAD 上，单视角误差降 33.2%，跨视角一致性提升 10.5%，度量重建质量提升 25.6%；对极稀疏深度提示和未见相机布局也有零样本泛化。
为什么值得看：这是把“弱重叠环视几何”单独拎出来解决，而不是继续堆融合 backbone；对量产车 surround perception、重建和规划前端都更实用。
局限/跟进：当前主打深度与几何一致性，离端到端驾驶闭环收益还有链路距离；后续要看在检测/占据/规划一体化里是否稳定转化。

2. GraphBEV++: Multi-Modal Feature Alignment for Autonomous Driving
URL: https://arxiv.org/abs/2606.16354
作者：Ziying Song 等
提交时间：2026-06-15
问题/痛点：LiDAR-相机标定误差会让 BEV 融合特征错位，但很多工作默认投影后天然对齐，导致长尾噪声下感知和规划一起掉。
核心创新：把“对齐”拆成局部与全局两层。LocalAlign-v2 用图匹配引入邻域感知深度特征修局部错位；GlobalAlign-v2 分成 Deformable 和 Diffusion 两条线，前者显式学 offset，后者用加噪-去噪模拟隐式错位恢复对齐。
方法/结构：兼容 LSS 系和 query-based 系两种 BEV 范式，可接 BEVFusion、BEVFormer，并延伸到 occupancy 与端到端驾驶。
实验/结果：摘要确认其在 nuScenes、Waymo subset、Argoverse2 上取得错位噪声场景下 SOTA，并在 Bench2Drive、NAVSIM 等 open-loop/closed-loop 评测中优于 UniAD、VAD、FusionAD、MomAD、WoTE 等基线。
为什么值得看：近期端到端驾驶论文很多在堆 world model，但这篇回到非常工程本质的问题：跨模态几何对不齐，后面一切都不稳。
局限/跟进：摘要未给具体绝对数值；需要后看论文正文确认在不同标定噪声幅度下的收益曲线，以及额外计算开销。

3. Metis: A Generalizable and Efficient World-Action Model for Autonomous Driving and Urban Navigation
URL: https://arxiv.org/abs/2606.15869
作者：Jingyu Li 等
提交时间：2026-06-14
问题/痛点：现有 world-action model 常把视频生成与动作预测紧耦合，推理时还要显式预测未来观测，导致时延大、分布失配、泛化差。
核心创新：提出解耦式 WAM。用 Mixture-of-Transformers 给“视频生成”和“动作预测”分配专门 expert，同时用 asymmetric attention mask 做联合训练，但在推理时让动作 expert 绕过显式视频生成。
方法/结构：joint training, decoupled inference；目标是兼顾训练一致性、推理效率和跨任务泛化。
实验/结果：在 NAVSIM navhard、navtest、CityWalker 上达到 SOTA，并做了 real-robot deployment，说明不只是仿真里好看。
为什么值得看：这代表 WAM 研究从“能不能统一建模”转到“统一建模后如何把延迟打下来”；对驾驶和城市导航共享一套 world-action 表达也很有启发。
局限/跟进：摘要未披露具体推理加速倍数；后续重点看其在复杂交互场景下是否牺牲未来视觉可解释性。

【机器人/具身智能】
4. T-Rex: Tactile-Reactive Dexterous Manipulation
URL: https://arxiv.org/abs/2606.17055
作者：Dantong Niu 等；摘要页 affiliation 仅显示 Linxi
提交时间：2026-06-15
问题/痛点：现有 VLA 操作模型大多忽略触觉，或只把触觉当静态编码，导致精细受力控制、可变形物体操作始终差一截。
核心创新：同时补三块短板：100 小时 tactile-rich 数据、面向高频触觉的 temporal tactile VQ-VAE、以及 variable-rate Mixture-of-Transformers，让触觉以更高频率进入策略而不破坏原有视觉语言能力。
方法/结构：先用以基础运动原语为中心的数据采集 recipe 降低触觉数据成本，再让 MoT 在多速率输入下整合视觉、语言、触觉。
实验/结果：在 12 个需要精细力控和可变形物体处理的任务上，平均成功率比最强基线高 30% 以上。
为什么值得看：过去一年 manipulation foundation model 的主线是“更大视觉语义模型”，这篇明确表明只靠视觉不够，真正的灵巧操作要把触觉做成第一类模态。
局限/跟进：100 小时对触觉已不小，但离开放世界还远；需要继续看传感器更换、手型变化、跨平台迁移是否稳定。

5. Human Universal Grasping
URL: https://arxiv.org/abs/2606.17054
作者：Kevin Yuanbo Wu, Tianxing Zhou, Isaac Tu, Billy Yan, Irmak Guzey, David Fouhey, Dandan Shan, Lerrel Pinto
提交时间：2026-06-15
问题/痛点：多指抓取长期卡在“机器人数据少、泛化差”；作者直接追问，最天然的大规模抓取数据源其实是人类每天的抓取行为。
核心创新：提出 HUG flow-matching 抓取生成模型，并配套 1M-HUGs 数据集：100 万帧、27.8 小时、6707 个物体实例、41 栋建筑中的日常人类抓取。模型从单张 RGB-D 图像直接输出腕部平移、旋转与 MANO 手姿。
方法/结构：RGB+Depth 融合建模自然人类抓取分布，随后把人手抓取重定向到不同机器人手，实现 zero-shot grasping。
实验/结果：新建 HUG-Bench，含 90 个未见物体；真实世界用其中 30 个测试物体、多个双目相机、多个机器人手和家庭环境评估，较 SOTA 抓取基线提升 +23% 与 +34%。
为什么值得看：它把“人类演示”从动作序列 imitation 扩展到“抓取分布本身”，而且把数据采集入口降到智能眼镜，规模化潜力很强。
局限/跟进：抓取成功不等于后续操作成功；后面值得看与 manipulation policy、接触序列规划如何联动。

6. Geometric Action Model for Robot Policy Learning
URL: https://arxiv.org/abs/2606.17046
作者：Jisang Han 等
提交时间：2026-06-15
问题/痛点：泛化机器人策略虽受益于基础模型，但很多 VLA/WAM 仍主要在 2D 图像或 2D latent 上工作，对接触密集任务所需的 3D 几何理解仍然是隐式的。
核心创新：直接复用 pretrained geometric foundation model 作为统一底座。GAM 在中间层把 GFM 切开：浅层做观测编码，中间插入 causal future predictor 预测未来几何 token，再把结果送回后半段 GFM 完成特征传播与动作解码。
方法/结构：一个 backbone 同时承担 perception、future geometry prediction、action decoding，靠最小结构改动把几何先验转成语言条件世界建模。
实验/结果：摘要确认其在仿真和真实机器人 manipulation 基准上，相比 foundation-model 级基线更准、更稳、更快、更轻。
为什么值得看：这条路线与纯 VLM/VLA 堆语义不同，强调“几何基础模型才是操作的共享底座”，很可能影响下一批 manipulation policy 设计。
局限/跟进：摘要未列具体 benchmark 和绝对提升；需要后看对遮挡、接触不确定性、长时序任务的稳定性。

【交叉方向】
7. Qwen-RobotWorld Technical Report: Unifying Embodied World Modeling through Language-Conditioned Video Generation
URL: https://arxiv.org/abs/2606.17030
作者：Jie Zhang 等
提交时间：2026-06-15
问题/痛点：驾驶、操作、室内导航往往各有各的 world model 与动作接口，难共享数据、评测和规划信号。
核心创新：把自然语言定义为统一动作接口，直接做 language-conditioned video world model；既能预测具身未来视觉轨迹，又能服务数据合成、虚拟评测和语言引导规划。三大关键部件是：60 层 Double-Stream MMDiT + MLLM Action Encoding、8.6M 视频文本/2 亿帧的 EWK 数据、General+Expert Progressive Curriculum 两阶段训练。
方法/结构：冻结 Qwen2.5-VL 语义，与 video-VAE latent 通过层级 joint attention 耦合；先学通用视觉先验，再注入具身专长。
实验/结果：摘要确认其在 EWMBench、DreamGen Bench 排名第 1，在 WorldModelBench、PBench 上超过所有开源模型；在 RoboTwin-IF 上零样本泛化和多视角一致性也较强。
为什么值得看：这是少见同时覆盖 robotic manipulation、autonomous driving、indoor navigation、human-to-robot transfer 的统一 world model，明显在推“跨 embodiment 共享世界模型”。
局限/跟进：目前是技术报告，工程规模很大但真实闭环控制收益还需更多独立验证；后面要看生成质量与可控性怎样转化成控制收益。

【趋势总结】
1. 最近两天最明显的动向，是“世界模型继续升温，但研究重心从单纯生成未来，转向几何一致性、低时延推理和跨 embodiment 统一接口”。SurroundNEXO、Metis、Qwen-RobotWorld 是三条很典型的线。
2. 自动驾驶这批论文比过去更少谈单点检测指标，更多把深度、BEV 对齐、长时规划和仿真闭环绑定在一起，说明社区正在从“感知模块最优”转向“系统级闭环稳健性”。
3. 机器人方向的变化更鲜明：触觉重新进入主线，且不再只是附加传感器，而是被当作高频主模态；同时几何 foundation model 与人类大规模抓取数据，正在成为替代纯 2D VLA 的新抓手。
4. 与以往“更大 VLM + 更多视频”相比，这批工作的新意在于更强调物理接触、度量几何、数据采集机制和推理效率，路线明显更靠近真实部署。
