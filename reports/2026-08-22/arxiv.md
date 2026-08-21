# arXiv 自动驾驶、机器人与具身智能晨报｜2026-08-22

说明：截至北京时间 2026-08-22 06:00，采用 2026-08-20 UTC 最新相关提交；作者与结果依据 arXiv 摘要，未将摘要外推断写成事实。

## 自动驾驶

### DART-S: Reachability-Audited Active-Suspension Preconditioning for Off-Road Vehicle Jumps

链接：https://arxiv.org/abs/2608.20275。作者/机构：以论文页面为准。问题：越野车辆起跳时的姿态误差在空中受轮胎角动量预算限制，难以补救。机制：在起跳坡面利用主动悬架预调姿态，并用可达性审计判断空中控制是否可行。实验：摘要报告在越野跳跃控制中改善可达姿态与落地稳定性。关注价值：把车辆底盘执行器和安全可达集接入极限驾驶规划。局限/跟进：需核验真实车辆、不同地形和感知延迟下的闭环结果。

### Multi-Agent Orchestration with the Common-Sense Reasoning Capabilities of LLMs for Autonomous Driving

链接：https://arxiv.org/abs/2608.20129。问题：自动驾驶多模块决策在复杂交互中缺少可组合的常识推理。机制：以 LLM 编排多 Agent 分工，协调场景理解、预测与规划。实验：摘要指向多智能体驾驶任务评估。关注价值：探索把高层交互推理变成可审计的 Agent 协议。局限/跟进：实时性、幻觉和安全边界必须通过闭环实车验证。

## 机器人／具身智能

### DreamHand: Repurposing Video Diffusion Models for Occlusion-Robust Egocentric 3D Hand Motion Recovery

链接：https://arxiv.org/abs/2608.20308。作者：Yufei Liu 等。问题：第一视角视频中双手频繁被物体遮挡或出画，难恢复度量 3D 轨迹。机制：将视频扩散模型改作确定性 clean-latent 几何编码器，配合双向时空解码器和射线相机求解。实验：五个 egocentric 基准上，ARCTIC MPJPE-p 降 30%、HOT3D 降 40%；纳入出画手时提升 46–61%。关注价值：把日常人类视频转成机器人操作数据。局限/跟进：离线方法与真实在线控制的时延、跨相机泛化仍待验证。

### DECOWAM: Decoupled Whole-Body World-Action Model for Legged Mobile Manipulation

链接：https://arxiv.org/abs/2608.20114。问题：腿式移动操作同时处理全身运动与接触动作，统一模型易受控制频率和本体耦合影响。机制：解耦 whole-body 世界预测与动作生成接口。实验：摘要报告面向腿式移动操作的世界—动作建模。关注价值：为移动操作提供可复用的预测/控制分层。局限/跟进：需关注真机接触稳定、长时误差与跨本体迁移。

### RoMAN-Flow: Taming Autoregressive Normalizing Flows for Offline Reinforcement Learning in Robotic Manipulation

链接：https://arxiv.org/abs/2608.20208。问题：离线机器人强化学习受数据分布和动作多峰性限制。机制：以自回归 normalizing flow 建模动作分布，提升离线策略表达。实验：在机器人操作离线 RL 任务上评估策略质量。关注价值：为示范数据有限时的连续动作生成提供概率接口。局限/跟进：数据覆盖、真实部署安全和 OOD 动作抑制仍需量化。

### CoToGrasp: Contact-Topology-Conditioned Dexterous Grasp Synthesis via Canonical Workspace Learning

链接：https://arxiv.org/abs/2608.19776。问题：灵巧抓取的接触拓扑变化大，直接回归姿态泛化差。机制：学习规范化工作空间，并以接触拓扑条件生成抓取。实验：摘要报告面向灵巧抓取合成。关注价值：把接触关系作为显式中间变量，利于可解释规划。局限/跟进：柔性物体、触觉噪声及真机成功率需进一步验证。

## 交叉方向：导航与可验证规划

### Video2DoorTraversal: Push Door Traversal via Simulated Door Twins

链接：https://arxiv.org/abs/2608.20251。问题：推门穿越涉及门体动力学、视觉遮挡和接触策略，真实数据昂贵。机制：构建可交互的 simulated door twin 生成训练与测试场景。实验：在推门穿越任务上验证策略。关注价值：展示面向接触任务的数字孪生数据闭环。局限/跟进：仿真门铰链摩擦、材质差异和真实迁移是关键。

### Evidence-Gated Task and Motion Planning with Vision-Language Models

链接：https://arxiv.org/abs/2608.20084。问题：VLM 生成的任务计划可能缺少几何或可执行证据。机制：在任务—运动规划之间加入 evidence gate，只有满足视觉证据才推进动作。实验：摘要报告面向 VLM 任务与运动规划。关注价值：将“看起来合理”转成可核验前置条件。局限/跟进：证据误检、长链恢复和实时开销需在动态环境测试。

趋势总结：本批工作把“接触与可达性”推到接口层：车辆用可达性审计管理极限动作，机器人用 clean-latent、接触拓扑和解耦 WAM 组织数据与控制，导航则以数字孪生和证据门降低执行风险。下一步应重点追踪真机闭环、失败恢复和跨本体复现。
