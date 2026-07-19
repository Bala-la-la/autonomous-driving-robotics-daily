arXiv 自动驾驶与机器人晨报｜2026-06-04

说明：截至 2026-06-04 早间，本轮优先检索最近一批可稳定访问的高相关新稿，重点落在 2026-05-01 至 2026-05-28；未强行凑“当天刚挂出但信息不足”的条目。以下按“自动驾驶”“机器人/具身智能”“交叉方向”分组，共 7 篇。

一、自动驾驶

1) Fast-dDrive: Efficient Block-Diffusion VLM for Autonomous Driving
arXiv: https://arxiv.org/abs/2605.23163
日期：arXiv 聚合页显示 2026-05-25；HF 提交页显示 2026-05-28
作者/机构：Kewei Zhang, Jin Wang, Sensen Gao, Chengyue Wu, Yulong Cao, Songyang Han, Boris Ivanovic, Langechuan Liu, Marco Pavone, Song Han, Daquan Zhou, Enze Xie；NVIDIA
要解决的问题：端到端自动驾驶 VLA 一直卡在两头都不够好：自回归方案推理慢、容易曝光偏差；全序列扩散又难复用 KV cache，且会破坏“先感知后规划”的因果结构。
核心创新点：把驾驶输出视作结构化语义块，而不是一长串等价 token。作者提出 block-diffusion VLA，在块内双向细化、块间严格因果，既保留扩散式全局修正能力，又不打乱规划顺序。
方法机制/模型结构：一是把 JSON 式输出里的结构 token 冻结成 scaffold；二是做 section-aware training，把安全相关规划段落训练权重拉高；三是提出 Scaffold Speculative Decoding；四是在测试时从共享前缀 KV cache 分叉 N 条随机轨迹再平均，低成本抑制方差。
实验设置和关键结果：摘要与聚合页给出的核心结果是，在自动驾驶 agent 上重写了 speed-accuracy frontier；集成 SGLang 后，相比自回归基线吞吐提升 12 倍，同时保持 AR 级质量。
为什么值得关注：这不是单纯“更大模型”路线，而是在生成机制层面重构驾驶 VLA 的推理形式，直接对应车端部署最敏感的延迟与稳定性。
可能局限/后续点：当前公开信息更强调系统效率，闭环安全指标、不同算力平台表现、复杂长尾 corner case 收益还需要看完整论文和后续复现。

2) Sensor2Sensor: Cross-Embodiment Sensor Conversion for Autonomous Driving
arXiv: https://arxiv.org/abs/2605.22809
日期：arXiv 聚合页显示 2026-05-21；HF 提交页显示 2026-05-22
作者/机构：Jiahao Wang, Bo Sun, Yijing Bai, Vincent Casser, Songyou Peng, Zehao Zhu, Meng-Li Shih, Xander Masotto, Shih-Yang Su, Kanaad V Parvate, Tiancheng Ge, Linn Bieske, Dragomir Anguelov, Mingxing Tan, Chiyu Max Jiang；Google
要解决的问题：真实 AV 车队日志高保真但规模、地域和长尾覆盖有限；互联网行车视频极多，却不是 ADS 可直接消费的多模态传感器格式。
核心创新点：把“野生 dashcam 视频”转换成“AV 可用的多相机 + LiDAR 传感器包”，相当于把开放互联网视频转译成自动驾驶训练/验证资产。
方法机制/模型结构：先把真实 AV logs 通过 4D Gaussian Splatting 重建并渲染成 dashcam 风格视频，用这一步制造近似配对数据；再用 diffusion 架构学习从单目 dashcam 到多模态传感器套件的生成映射。
实验设置和关键结果：作者做了生成保真度与真实性评估，并展示了把互联网/行车记录仪中的复杂场景转成 realistic multi-modal data format 的可行性。摘要虽未给出具体数值，但明确定位在“训练与验证数据扩容”。
为什么值得关注：如果这条路线成立，自动驾驶数据不再被自有车队规模硬约束，外部视频将有机会变成长尾场景补充层，尤其适合风险回放、仿真回灌和验证集扩展。
可能局限/后续点：生成式传感器转换的误差会不会误导下游评测，是最大风险；需要特别关注几何一致性、时序一致性和稀有交通参与者的保真度。

3) Learning A Unified Risk Map for Autonomous Driving in Partially Observable Environments
arXiv: https://arxiv.org/abs/2605.22189
日期：arXiv 聚合页显示 2026-05-21；HF 提交页显示 2026-05-29
作者/机构：Jie Jia, Yaofeng Su, Zeyu Bao, Yun Hong, Bingzhao Gao, Zhongxue Gan, Wenchao Ding；Fudan University
要解决的问题：遮挡场景下，自动驾驶很容易低估“没看见但可能存在”的风险；现有方法往往不是过度保守，就是在高遮挡下预测不准。
核心创新点：把 traffic flow risk 和 collision risk 统一进一个时空 risk map，而不是只做可达域风险或只做轨迹预测；并引入 diffusion-based adversarial scenario generation，专门补齐遮挡交互稀缺样本。
方法机制/模型结构：先做 unified spatiotemporal modeling 建模遮挡风险，再用生成模型补充 realistic yet adversarial occluded interactions，最后把统一风险图直接送入 partial observability 下的 risk-aware planning。
实验设置和关键结果：在 Waymo Open Motion Dataset 上，相比最强 occlusion-aware baseline，minimum time-to-collision 提升 0.78 倍，average time-to-collision 提升 1.67 倍。
为什么值得关注：这篇不是只追求轨迹误差更小，而是把“看不见的危险怎么量化”显式化，和真实部署里的保守性/效率平衡直接相关。
可能局限/后续点：风险图一旦被 planner 强依赖，误报与漏报的代价会被放大；后续值得跟踪它在 closed-loop planner、城市复杂交互和多车协同中的稳定性。

二、机器人/具身智能

4) Qwen-VLA: Unifying Vision-Language-Action Modeling across Tasks, Environments, and Robot Embodiments
arXiv: https://arxiv.org/abs/2605.30280
日期：arXiv 聚合页显示 2026-05-28；HF 提交页显示 2026-05-29
作者/机构：Qiuyue Wang 等；Qwen
要解决的问题：具身智能长期被“按任务分模型、按本体分模型、按环境分模型”切碎，操作、导航、轨迹预测之间知识无法共享。
核心创新点：尝试把 manipulation、navigation、trajectory prediction 都压进同一个 VLA 统一框架，并通过 embodiment-aware prompt conditioning 处理不同机器人本体与控制接口。
方法机制/模型结构：基于 Qwen 的视觉语言主干，向下接一个 DiT-based action decoder；训练时混合机器人操作轨迹、人类第一视角演示、仿真数据、VLN 数据、轨迹监督和辅助视觉语言数据；再用文本式 robot description 显式标注当前 embodiment 和 control convention。
实验设置和关键结果：在 manipulation、navigation、trajectory-centric benchmarks 上，作者报告了稳定的多任务性能和 OOD 泛化，尤其覆盖场景布局、背景、光照、物体配置和机器人本体变化。
为什么值得关注：这篇的价值不只在分数，而是在回答“VLA 是否能成为跨任务具身统一接口”这个关键问题；如果成立，会减少数据和模型资产继续碎片化。
可能局限/后续点：统一模型通常会面临 token 预算、动作空间对齐和任务负迁移问题；后续要看它在长时序操作与真实机器人闭环鲁棒性上能否维持优势。

5) HumanEgo: Zero-Shot Robot Learning from Minutes of Human Egocentric Videos
arXiv: https://arxiv.org/abs/2605.24934
日期：arXiv 聚合页显示 2026-05-24
作者/机构：Zhi Wang, Botao He, Kelin Yu, Seungjae Lee, Ruohan Gao, Furong Huang, Yiannis Aloimonos；页面未显式给出机构
要解决的问题：人类第一视角视频里有大量便宜、自然的操作演示，但人和机器人的视觉外观、运动学和执行器差异很大，直接迁移通常失败。
核心创新点：不是把人类视频硬对齐到机器人动作，而是先提升到 entity-level hand-object interaction 表示，再训练 flow matching policy，并用 dense auxiliary objectives 放大每条轨迹的监督密度。
方法机制/模型结构：核心桥接手段有三层：一层是 hand-object interaction 的实体级抽象，二层是 robot-data-free 的策略学习，三层是密集辅助目标让短时长人类视频也能产生足够训练信号。
实验设置和关键结果：只用每个任务 30 分钟人类视频，4 个真实任务平均成功率 92.5%；只用 15 分钟也有 75%；对比同时间预算的机器人遥操作数据，性能高 41%；还能零样本迁移到新机器人、新相机和新环境。
为什么值得关注：这是“少量人类视频直达机器人技能”的强信号，意味着高成本机器人示教未必总是首选数据源。
可能局限/后续点：目前更像中短程 manipulation transfer 的强证明；复杂接触、双臂协作、精密插装和失败恢复策略能否同样迁移，仍需验证。

6) MolmoAct2: Action Reasoning Models for Real-world Deployment
arXiv: https://arxiv.org/abs/2605.02881
日期：arXiv 聚合页显示 2026-05-04；HF 提交页显示 2026-05-05
作者/机构：Haoquan Fang, Jiafei Duan 等；Ai2
要解决的问题：开源 VLA 往往要么依赖昂贵硬件，要么推理太慢，要么 reasoning 加强后失去实时部署价值。
核心创新点：沿五个方向系统补齐“开源可部署”短板，包括专门的 embodied reasoning 主干 MolmoER、新数据集、新 action tokenizer、连续动作专家和自适应深度推理。
方法机制/模型结构：MolmoER 用 330 万样本做 specialize-then-rehearse 训练；数据侧加入 720 小时遥操作双臂轨迹等新数据；OpenFAST 做跨五种 embodiment 的开放 action tokenizer；结构上把 flow-matching continuous-action expert 通过 per-layer KV-cache conditioning 接到离散 token VLM 上；MolmoThink 只对变化区域重预测 depth token 以降延迟。
实验设置和关键结果：作者称这是“目前最广泛的开源 VLA 实证”之一，覆盖 7 个仿真与真实 benchmark；MolmoAct2 超过 Pi-0.5 等强基线，MolmoER 在 13 个 embodied-reasoning benchmark 上超过 GPT-5 与 Gemini Robotics ER-1.5。
为什么值得关注：这篇把“开源具身模型”从 demo 级往 deployment-grade 推进了一步，尤其是动作 tokenizer、KV-cache 条件化和低时延 reasoning 设计都非常工程化。
可能局限/后续点：论文声称的基准覆盖广，但不同平台上的控制频率、执行失败模式和长期可靠性仍需独立复核；另一个关注点是数据规模扩大后是否会快速逼近闭源系统上限。

三、交叉方向

7) The DAWN of World-Action Interactive Models
arXiv: https://arxiv.org/abs/2605.11550
日期：arXiv 聚合页显示 2026-05-12；HF 提交页显示 2026-05-14
作者/机构：Hongbo Lu, Liang Yao, Chenghao He, Haoyu Wang, Xiang Gu, Xianfei Li, Wenlong Liao, Tao He, Pai Peng；COWARobot
要解决的问题：传统 world model 常把“世界演化预测”和“动作生成”分成并行支路，或 rigid predict-then-plan，忽略两者本来就是相互依赖的。
核心创新点：提出 World-Action Interactive Models（WAIMs）视角，在自动驾驶里用 DAWN 做实例化，让 action generation 与 world evolution recursive refinement，而不是先后硬切。
方法机制/模型结构：DAWN 不做整段像素级未来展开，而是做一小段显式 latent rollout，足以支撑长时规划；本质上是用更轻量的可交互 latent dynamics，维持“动作影响世界、世界反过来约束动作”的耦合。
实验设置和关键结果：公开摘要给出的结论是，在多个自动驾驶 benchmark 上拿到强 planning performance，并且安全相关结果更优。
为什么值得关注：这篇代表一个明显方向变化，即从“先看世界、再出轨迹”转向“世界-动作联合生成”；这个思想同样可能迁移到机器人操作和多步导航。
可能局限/后续点：目前外部摘要对具体 benchmark 和绝对数值披露不多；真正价值要看长时 rollout 漂移、反事实交互质量，以及是否能扩展到更复杂多体交互。

四、趋势总结

1. 自动驾驶方向最明显的新意，不是再堆单模块精度，而是把“生成式世界建模 + 风险建模 + 可部署推理”合并成闭环系统设计。Fast-dDrive 和 DAWN 都在试图同时解决规划质量与车端推理速度，说明研究重点正从“能不能做端到端”转向“能不能实时、稳定、可因果地做端到端”。
2. 数据路线也在明显变化。Sensor2Sensor 代表把开放世界视频资产化，Unified Risk Map 代表用生成模型专门补长尾遮挡风险，说明社区不再满足于被动收集车队日志，而是开始主动制造可训练、可验证、可对抗的数据分布。
3. 机器人/具身方向则在走“统一模型 + 便宜数据 + 真机后训练”三线并进。Qwen-VLA 要统一任务和本体，HumanEgo 试图摆脱高成本机器人示教，MolmoAct2 则把开源模型往真实部署推。
4. 和以往相比，最近一批论文一个很鲜明的差别是：大家不再满足于把 perception、reasoning、action 串起来，而是更强调 action-aware perception、world-action coupling、deployment-time efficiency、post-deployment learning。这比过去单纯追逐 benchmark SOTA 更接近真实系统工程。
5. 值得继续跟踪的后续问题包括：生成式中间表示是否足够可信、统一 VLA 是否会被多任务负迁移拖累、低成本数据替代机器人示教的边界在哪里，以及 closed-loop 安全指标是否能稳定复现到真车/真机。
