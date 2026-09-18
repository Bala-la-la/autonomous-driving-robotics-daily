# arXiv 自动驾驶、机器人与具身智能晨报｜2026-09-17

## 检索状态

截至北京时间 2026-09-17 06:00，最新可核验相关批次为 2026-09-16 UTC；以下选入该批次中与自动驾驶、机器人操作、导航、控制和长期自治直接相关的 10 篇论文。提交日期按 arXiv UTC 元数据记录。

## 自动驾驶与实时 VLA

1. [FIVE-VLA: Fast and EffectIVE Autonomous Driving with Recurrent Action Memory](https://arxiv.org/abs/2609.18623v1)

   - **问题与机制**：驾驶 VLA 面临高分辨率视觉成本高、参数量大和缺少时间记忆的问题。FIVE-VLA 使用高分辨率高效视觉编码、循环动作记忆和紧凑策略接口，目标是保留历史动作信息并降低推理负担。
   - **关注价值**：把驾驶 VLA 的实时性与时序记忆放在同一设计中，适合追踪其闭环延迟、长时稳定性和端侧部署代价。
   - **局限**：摘要未覆盖所有硬件、天气和长尾交互；离线轨迹指标不能替代真实道路安全验证。

2. [VLA-ULAP: Interleaving Cloud VLA Calls with Ultra-Lightweight Local Action Prediction at the Edge](https://arxiv.org/abs/2609.18663v1)

   - **问题与机制**：大模型 VLA 的远程调用存在功耗、带宽和延迟问题。VLA-ULAP 用约 7.4M 参数的本地动作预测器结合当前视觉、本体感知和已执行动作，在云端 VLA 调用之间提供快速动作。
   - **关注价值**：这是“云端慢推理 + 边缘快控制”的明确系统接口，关键不只是平均成功率，还包括突发风险时本地分支是否会及时接管。
   - **局限**：远程调用失败、分布外场景和本地预测器错误累积仍需真实网络与传感器退化实验。

## 机器人学习与操作

3. [PointZero: 3D Point Track Completion for Learning Transferable 3D Dynamics](https://arxiv.org/abs/2609.19142v1)

   - **问题与机制**：动作标注限制了机器人世界模型使用网络视频。PointZero 以 RGB-D 观测和稀疏 3D 轨迹为输入，预训练所有点的未来轨迹，再后训练为动作条件动力学和模仿策略；作者报告 290 万合成帧，覆盖刚体、关节和可变形物体。
   - **实验与关注价值**：后训练后在 PGND 3D dynamics 和 7 个模拟/真实操作任务中取得竞争力，说明“先学 3D 动力学、后接机器人动作”可能扩大无机器人数据的利用范围。
   - **局限**：合成动力学先验能否覆盖真实接触、遮挡和材料变化仍是主要风险；应核查数据与 checkpoint 的复现实验。

4. [In-Context Robot Learning with VLM Agents](https://arxiv.org/abs/2609.19138v1)

   - **问题与机制**：有限示范无法覆盖机器人部署时遇到的所有任务。该工作让 VLM Agent 在上下文中读取观察、示范和执行反馈，并据此适配陌生环境，而不是只依赖固定策略。
   - **关注价值**：将 in-context learning 从语言任务推进到机器人部署，重点应看它能否用少量现场证据修正动作，而不是仅生成合理解释。
   - **局限**：VLM 的错误记忆、工具调用延迟和动作安全边界可能让上下文适配变成风险放大器。

5. [Dreaming the Sound of Contact: Leveraging Video and Audio Generation for Zero-Shot Force-Aware Manipulation and Data Generation](https://arxiv.org/abs/2609.19137v1)

   - **问题与机制**：视频生成通常提供运动外观，却缺少接触力信息。该工作利用生成视频和音频线索塑造有界、随时间变化的目标力曲线，用于零样本力感知操作和数据生成。
   - **关注价值**：把音频作为接触状态的廉价补充观测，可能降低对昂贵力传感器标注的依赖；但真正的价值取决于力曲线是否与材料、速度和接触几何一致。
   - **局限**：音频与力的映射高度依赖环境声学和物体材质，生成数据的物理真实性需要独立实机审计。

6. [Track, Articulate, Act: Generating Articulation from Casual Human Videos](https://arxiv.org/abs/2609.19119v1)

   - **问题与机制**：人类视频包含手如何引起门、抽屉、柜体等关节物体运动的因果证据，但难以直接用于机器人。该工作从随手拍视频中恢复物体关节结构与运动，再生成可供操作策略使用的 articulation 表示。
   - **关注价值**：它把“看见人类操作”转成可执行的物体运动先验，连接互联网视频与机器人数据扩展。
   - **局限**：单目视频的遮挡、深度尺度和未观测接触力会影响关节估计；从人手动作到特定机械臂仍需动力学适配。

7. [KINO: A Keyframe Interface for VLM Planning and Whole-Body Control in Humanoid Loco-Manipulation](https://arxiv.org/abs/2609.18869v1)

   - **问题与机制**：人形移动操作同时要求语义规划、全身姿态和物体位姿协调。KINO 以运动 keyframe 作为 VLM 规划与 RL 控制之间的中间接口，每个 keyframe 指定全身与相关物体目标姿态。
   - **关注价值**：相比直接输出关节或低层动作，keyframe 提供了可检查、可重规划的系统边界，值得关注其在不同身高、负载和接触任务上的迁移。
   - **局限**：关键帧离散化可能遗漏连续接触与平衡约束；高层目标可行不代表低层控制能稳定执行。

## 控制、安全与导航

8. [ElastiQP: An Always-Feasible QP Solver for Constrained Robot Control](https://arxiv.org/abs/2609.19080v1)

   - **问题与机制**：约束增多时 QP 控制器可能瞬时不可行，导致控制器无动作可执行。ElastiQP 通过弹性化约束，让求解器在冲突时仍返回可执行结果，并显式暴露约束违约程度。
   - **关注价值**：安全控制的工程难点常是“没有可执行输出”，而不是名义最优解；always-feasible 接口便于与学习策略、CBF 和故障恢复组合。
   - **局限**：可行不等于安全，软约束优先级和违约上界必须经过物理系统标定，不能只报告求解成功率。

9. [AdaGeoVLN: Selective Geometry Across Representation Depth and Navigation Time for Vision-Language Navigation](https://arxiv.org/abs/2609.18789v1)

   - **问题与机制**：VLN 需要同时利用视觉语义、几何层级和历史空间证据。AdaGeoVLN 选择性读取 geometry foundation model 的不同深度表示，并按导航时间流式保留几何信息。
   - **关注价值**：它把“用多少几何、保留多久”变成策略变量，有望减少长时导航中的上下文膨胀与空间漂移。
   - **局限**：benchmark 中的几何先验可能高于真实传感器质量；动态障碍、定位误差和跨建筑泛化需要额外验证。

10. [PASSAGE: Scaling Scene-Aligned Motion Learning for Perceptive Humanoid Traversal in Cluttered Environments](https://arxiv.org/abs/2609.18732v1)

   - **问题与机制**：人形机器人需要从感知中选择跨越、挤过、下蹲等通过行为，但手工运动库和任务特定奖励难以覆盖复杂障碍。PASSAGE 采用感知条件 planner-tracker，将场景对齐运动学习用于杂乱环境穿越。
   - **关注价值**：把可通过性从静态碰撞检测提升为与身体动作、场景几何共同决定的运动选择，适合观察真机失效与恢复成本。
   - **局限**：场景对齐误差、落脚点不确定性和受扰平衡仍是部署瓶颈；复杂人群环境中的安全证据尚不足。

## 趋势总结

- **实时性开始成为 VLA 的接口问题**：FIVE-VLA 通过循环动作记忆降低时序成本，VLA-ULAP 进一步把云端语义调用和本地快动作拆成双层控制路径。
- **无机器人数据的价值依赖可执行中间表示**：PointZero 使用 3D 点轨迹，Track-Articulate-Act 使用关节结构，Dreaming the Sound of Contact 则尝试用音频补足接触力；共同问题是中间表示是否真的改善闭环动作。
- **人形系统正在显式化规划—控制边界**：KINO 的 keyframe、PASSAGE 的 scene-aligned motion 和 ElastiQP 的 always-feasible 求解器都把可检查、可恢复的运行时接口置于单一策略之前。
- **下一步核查重点**：真实硬件延迟、传感器退化、接触安全、长时误差累积，以及失败后是否能返回可执行且可审计的动作。
