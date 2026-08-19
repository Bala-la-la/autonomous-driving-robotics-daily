# arXiv 自动驾驶、机器人与具身智能晨报｜2026-08-20

说明：截至北京时间 2026-08-20 06:00，检索到的最新相关批次为 2026-08-18 UTC（arXiv 页面提交/更新时间）；以下为当日新稿，作者机构以 arXiv 元数据为准。

## 自动驾驶

### Plug-and-Play Traffic Element Awareness for End-to-End Autonomous Driving

链接：https://arxiv.org/abs/2608.18035。问题：端到端驾驶通常只建模车辆、行人，交通灯和标志的结构化影响缺少系统评估。机制：给多个公开驾驶集补充交通元素标注，并设计几乎不改网络的 plug-and-play 信号注入，覆盖感知-预测-规划、视觉语言和端到端范式。实验：跨范式比较交通元素增强前后闭环/离线指标，摘要强调统一基础设施与低集成成本，具体增益需以论文表格复核。关注价值：把“规则性视觉线索”从数据缺口变成可插拔变量。局限/跟进：摘要未给出完整数据规模、闭环事故率；需检查标注一致性和跨城市泛化。

### Stability Control for Real World Testing in Autonomous Racing

链接：https://arxiv.org/abs/2608.17779。问题：极限工况下轮胎滑移和外部扰动会使常规运动控制失稳。机制：电子稳定控制 ESC、滑移控制 SC、反打方向 CS 组成安全层，动态修正转向与制动命令。实验：仿真加全尺寸实车验证，报告在临界场景保持稳定并扩大可行运行域；实现开源于 https://github.com/TUMFTM/tam-stability-control。关注价值：将学习/优化控制器与可审计稳定屏障组合。局限/跟进：尚未看到不同路面、延迟和感知故障的统计；应关注与学习型规划器的接口。

## 机器人／具身智能

### Hydra-0: Action Flow for Generalist World Modeling and Control

链接：https://arxiv.org/abs/2608.18077。问题：不同本体、任务和视频骨干的动作表示不统一。机制：把机器人动作表示为像素运动的 action flow，训练共享世界模型，并从目标物体流反推可执行机器人运动。实验：相对 action-conditioned baseline，机器人运动误差降低 90.4%、物体运动误差降低 60.2%；RoboLab 回放与参考成功率相关系数 r=0.96，并展示零样本组合和低数据适配。关注价值：提供跨本体、跨人类视频的控制接口。局限/跟进：开环视频指标与真实闭环差距仍大，动作流遮挡/接触建模待验证。

### PRISM: Precision and contact-rich Real-world Industrial Skill Dataset with Multimodal sensing

链接：https://arxiv.org/abs/2608.17962。问题：现有数据集偏短时、低接触 pick-and-place，缺少工业装配中的力、触觉和机械约束。机制：25+ 类任务、5000+ 轨迹、45 小时遥操作，提供同步多视角 RGB-D、力/矩、触觉和机器人状态。实验：作为接触丰富操作的真实基准和训练底座；项目页 https://tengbo-yu.github.io/PRISM/。关注价值：推动 VLA 从“看懂并抓取”转向精密接触控制。局限/跟进：遥操作分布不等于自主策略分布，需跨工厂、跨末端执行器评估。

### CompCPZ: Preserving Multi-Modal Intent in Language-Guided Robot Manipulation

链接：https://arxiv.org/abs/2608.17717。问题：含“或”条件的指令被压成单一几何均值，导致语义上两边都不满足。机制：沿语言解析树递归组合约束多项式 zonotope，并用无分布假设 conformal coverage 保留多模态可行集，运行时间低于毫秒级。实验：ManiSkill3 闭环基准相对多类凸集、峰值解码器和零样本 VLA 获得 1900/1918 配对胜利；无需重调迁移到 Unitree Go2 实机平面试验。关注价值：把语言歧义显式传给规划器，而不是让策略平均化。局限/跟进：复杂三维接触和长时组合的集合膨胀仍需测量。

### LIBERO-VIFO: Benchmarking the Capability and Safety of Visual Cue Following in Vision-Language-Action Models

链接：https://arxiv.org/abs/2608.17600。问题：VLA 能否只跟随获授权视觉提示、拒绝未授权提示尚不清楚。机制：八类视觉 cue、四种协议，分别测试理解/授权执行，以及语言冲突或无语言时的未授权跟随。实验：评测七个 VLA，发现理解不稳定地转化为执行，但模型可在无语言时执行 cue 指示任务，暴露 prompt injection 式风险。关注价值：将视觉提示当作权限边界测试，而非单纯成功率。局限/跟进：主要是基准环境；需要真实遮挡、恶意标记和动作前确认策略。

### HODAgent: Towards On-Demand, Responsive Humanoids for Physical World Human Interaction

链接：https://arxiv.org/abs/2608.17584。问题：服务型人形机器人执行中会收到新请求，必须暂停、修订并核验结果。机制：半双工 System-2 架构由 Env-Interactor、Planner、Executor、分层 Memory 维护任务状态，并用统一接口连接模拟和 Unitree G1。实验：164 个交互案例，两个 VLM 的联合成功率 84.8%/91.5%；实机原子、复合、完整任务通过率 92%/72%/63.3%，多项基准提升 0.7–9.0 个百分点。关注价值：把“可打断、可修订、可闭环验收”作为人形 Agent 的系统指标。局限/跟进：完整长任务仍明显掉点，记忆错误和执行延迟需要更细分归因。

## 交叉方向：边缘自治与安全

### Jetson-ORB-SLAM3: Accuracy-Preserving GPU Implementation for Edge Computing Devices

链接：https://arxiv.org/abs/2608.17874。问题：边缘 GPU 加速 ORB-SLAM 常以近似检测器换速度，改变轨迹。机制：Jetson Orin Nano 上复现 CPU ORB，前端 GPU、后端建图优化 CPU，并用 TensorRT 加速回环。实验：关键点 94.7% 完全一致、描述子 bit 一致率 99.9%；EuRoC 四种配置 MAE 差异小于 0.10 cm，并在 TUM-VI、KITTI 复核。关注价值：为低功耗长期自治提供可复现的“加速不改语义”路径。局限/跟进：功耗、热 throttling、动态场景和多传感器融合仍待报告。

趋势总结：本批次呈现三条线索：驾驶系统把交通规则和稳定性下沉为可插拔安全层；机器人策略用 action flow、集合表示和多模态触觉数据连接跨本体泛化；VLA/人形 Agent 的评价从最终成功率扩展到授权、可打断、结果核验与边缘可复现性。下一步应优先追踪真实闭环、分布外扰动和权限失败率，而不是只看离线平均分。
