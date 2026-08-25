# arXiv 自动驾驶、机器人与具身智能晨报｜2026-08-26

说明：截至北京时间 2026-08-26 06:00，最新可核验相关批次为 2026-08-24 UTC；以下按提交日期精选，未将旧稿冒充当日新增。

## 自动驾驶、长期自治与交叉方向

### GeoWAM: Visual Geometry World Action Models for Autonomous Driving
- 链接：https://arxiv.org/abs/2608.23486；提交：2026-08-24；作者/机构：摘要页列示作者。
- 问题：像素空间 WAM 把几何、运动、纹理和光照纠缠，难以直接服务驾驶动作。
- 创新/机制：改为预测未来点云几何，并由几何条件动作头预测 ego 轨迹，联合编码空间结构与时间演化。
- 实验/结果：在开环与闭环评测中，相比图像未来预测基线取得更强驾驶策略；摘要未给出统一数值表。
- 关注价值：把“未来长什么样”转成“未来空间如何变化”，更贴近规划接口。
- 局限/跟进：点云遮挡、传感器缺失、长时 rollout 和真实道路泛化仍需验证。

### MomADv2: Reliable Temporal Memory for End-to-End Autonomous Driving
- 链接：https://arxiv.org/abs/2608.23405；提交：2026-08-24。
- 问题：驾驶指令改变后，旧规划记忆可能变成误导并累积局部轨迹误差。
- 机制：选择性状态空间记忆按时间连续性和指令一致性筛选历史查询，再用 flow-matching residual refiner 修正轨迹。
- 实验/结果：在 NAVSIM、Bench2Drive 闭环及 nuScenes 开环评测中，6 秒规划平均碰撞率较 MomAD 降低 15.6%。
- 关注价值：将长时记忆“可用性”显式化，并把残差修正接入闭环。
- 局限/跟进：记忆门控对分布外指令、传感器丢帧和更长时域的稳定性待测。

### MIVIFI: Bridging Perspective and Fisheye Domains for Training Multi-View Fisheye Image Generation Models
- 链接：https://arxiv.org/abs/2608.23140；提交：2026-08-24。
- 问题：环视鱼眼数据稀缺，真实长尾天气和交通参与者难以覆盖。
- 机制：用体素语义表征条件生成，并以等距投影连接 KITTI-360 鱼眼与 nuScenes 透视域，支持增删演员和天气/光照编辑。
- 实验/结果：定量与视觉实验显示跨域策略改善鱼眼多视角生成与稀有场景操控；摘要未公布单一主指标。
- 关注价值：为环视感知和极端场景回归测试提供可控数据源。
- 局限/跟进：生成分布与真实摄像头噪声、闭环安全收益和仿真偏差需校准。

## 机器人／具身智能

### Act with Intent: Distilling Behavior Intent for Vision-Language-Action Models
- 链接：https://arxiv.org/abs/2608.23478；提交：2026-08-24。
- 问题：行为克隆只监督“做了什么”，没有显式表示指令下的局部目标。
- 机制：冻结教师 VLM 从观测、指令、粗动作和执行视频提炼行为意图，在动作解码器中间层组织动作预测。
- 实验/结果：GR00T-N1.7 在 SimplerEnv-Bridge 由 64.3% 升至 84.7%，RoboCasa 由 64.1% 升至 70.3%；真机平均成功率 62.0%→68.7%。
- 关注价值：将“意图—进展—动作”变成可诊断中间变量，改善长时任务。
- 局限/跟进：教师偏差、意图泄漏和跨本体迁移仍需独立验证。

### Pointing-VLA: Typed Spatial Grounding Interfaces for Vision-Language-Action Manipulation
- 链接：https://arxiv.org/abs/2608.23138；提交：2026-08-24。
- 问题：文本坐标或不透明 action token 使空间推理到控制的接口脆弱且慢。
- 机制：用 typed hidden-state heads 直接预测点、对象功能热图和视觉轨迹，并为 PICK/PLACE 规定阶段化执行契约。
- 实验/结果：Bridge/WidowX 平均 72.9%；接入 π0.5 后真机成功率 52.7%→80.7%，控制器时间降低逾 20 倍，解码速度提升约 6.7–6.9 倍。
- 关注价值：可检查、低延迟的空间读出比“把几何写成文字”更适合机器人。
- 局限/跟进：复杂接触、遮挡和多步纠错的 typed schema 仍需扩展。

### ROS2SmolVLA: Enabling Small Vision-Language-Action Models for Lightweight Robots
- 链接：https://arxiv.org/abs/2608.23320；提交：2026-08-24。
- 问题：大 VLA 难以在工业现场本地运行，合规、隐私和硬件成本阻碍落地。
- 机制：将 SmolVLA 接入 ROS 2 与 Universal Robots，提供可复用的本地推理和控制接口。
- 实验/结果：在 UR10e pick-and-place 任务验证功能，并给出工业级部署指南；摘要未提供完整成功率表。
- 关注价值：小模型、ROS 2 和现成机械臂的组合降低从论文到车间的门槛。
- 局限/跟进：多任务扩展、实时性、异常恢复和安全认证仍待评估。

## 趋势总结

1. WAM 正从像素预测转向几何、意图和结构化行为接口，评价重点随之靠近规划与控制闭环。
2. VLA 的中间层越来越“有类型”：意图、空间点、角色和阶段状态被设计成可验证契约。
3. 端侧部署与数据效率并行推进；下一步应关注真实延迟、故障恢复、跨本体复现和长期安全收益。
