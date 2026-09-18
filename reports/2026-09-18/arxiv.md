# arXiv 自动驾驶、机器人与具身智能晨报｜2026-09-18

## 检索状态

截至北京时间 2026-09-18 06:00，最新可核验的相关批次为 2026-09-17 UTC；以下选入 11 篇与自动驾驶、机器人操作、VLA 实时性、控制安全和长期自治直接相关的论文。论文提交日期按 arXiv UTC 元数据记录，摘要中的实验数字保留作者报告口径。

## 自动驾驶与系统验证

1. [OPTED: On-Policy Fine-Tuning for End-to-End Driving using a Render-Free Teacher](https://arxiv.org/abs/2609.20756v1)

   - **问题与机制**：端到端驾驶策略用人类数据做开环行为克隆时，闭环误差会把车辆带出训练分布；直接对传感器策略做强化学习又需要昂贵仿真。OPTED 先在 HD map 和 bounding box 等特权向量输入上训练 RL teacher，再用 teacher 在闭环中监督预训练的相机策略。
   - **实验与关注价值**：在 AlpaSim 和真实驾驶日志的 3D Gaussian 重建上，TransFuser 与 VaVAM 的 driving score 分别提升 1.6 倍和 9.5 倍；作者报告相较直接 RL 后训练约少用三个数量级的仿真交互。它把后训练的主要问题从“再采更多人类数据”转为“如何用可计算的 teacher 提供闭环方向”。
   - **局限**：特权 teacher 与相机 student 的差距、重建仿真的物理真实性和长尾交通参与者仍会影响安全收益；分数提升不等于真实道路风险下降。

2. [MILER: Semantic Mid-Level Representation for Sim-to-Real Reinforcement Learning in Unstructured Autonomous Driving](https://arxiv.org/abs/2609.20747v1)

   - **问题与机制**：非结构化道路的 sim-to-real 强依赖感知、动力学和控制接口的一致性。MILER 在离线阶段用语义中层表示模拟器训练 RL 策略，部署时用相机与 LiDAR 经 BEVFusion 生成同构的语义 BEV，再通过 trajectory alignment 把策略迁移到真实车辆。
   - **实验与关注价值**：作者在两辆车、3.0 km 测试赛道上无人工干预行驶 17.3 km，覆盖障碍物、发夹弯、最高 33.6 km/h 和越野路段；完整软件栈运行于 Jetson AGX Orin。它把中层语义接口作为 sim-to-real 的可审计边界，而不是让模拟器直接预测真实传感器像素。
   - **局限**：17.3 km 的路线与车辆覆盖仍有限；BEVFusion 误差、语义表示缺失和轨迹对齐规则在更复杂道路上的稳健性需要独立验证。

3. [VAST: V2X/Dynamic Map-Aware Autonomous Driving Systems Validation Toolchain](https://arxiv.org/abs/2609.19681v1)

   - **问题与机制**：协同驾驶系统同时包含车辆、基础设施传感器、边缘 Dynamic Map 和车端栈，单一模块 benchmark 难以覆盖接口失效。VAST 把 Scenic、Scenario Simulator v2、AWSIM、Autoware 与 SIM-LDM 接起来，统一场景生成、动态地图注入以及 TTC、PET、碰撞和超时指标。
   - **实验与关注价值**：在遮挡路口，受 Lanelet2 约束的采样把 edge-case 发现率从 40.0% 提到 80.0%，平均发现时间从 259.7 s 降到 110.4 s；加入 Dynamic Map 后碰撞率从 78.0% 降到 40.0%。价值在于把协同驾驶的互操作和验证成本本身变成研究对象。
   - **局限**：仿真链路的传感器、通信和重启开销未必代表真实车路云系统；碰撞率受场景分布影响，不能直接外推道路安全。

## 机器人 VLA、记忆与安全执行

4. [Coding Agents with an Obstacle-Aware Harness for Safe Robot Manipulation](https://arxiv.org/abs/2609.20822v1)

   - **问题与机制**：让 coding agent 直接写机器人控制程序时，模型即使在推理轨迹中提到障碍物，也可能把完成目标置于避障约束之上。SafeHarness 将任务拆成路线阶段与接触阶段：先把物体 grounding 为包围盒，规划并验证 waypoint 路线，必要时重规划，再选择不碰障碍的接触位置。
   - **实验与关注价值**：SafeHarness 达到 71.9% task success 和 87.5% collision avoidance，相比此前最佳结果分别提高 6.5 和 27.0 个百分点；相比无 harness 的同一 agent，两个数字分别是 2.3 倍和 1.5 倍。它直接证明“提示里写了安全要求”不等于执行层拥有安全优先级。
   - **局限**：包围盒近似、路线验证和接触位置选择仍依赖准确几何与执行误差模型；实验任务中的障碍约束不能覆盖动态人类和柔性接触。

5. [Workspace Models: Lightweight Robotic Memory via Saliency-Driven Supervision](https://arxiv.org/abs/2609.20820v1)

   - **问题与机制**：完整历史会让策略学到伪相关，而部署时每次调用 VLM 压缩历史又太慢。Workspace Models 在训练期让 VLM 找出当前任务真正需要的历史信息，再通过 set-reconstruction decoder loss 蒸馏成轻量 workspace token，部署时直接查询该 latent memory。
   - **实验与关注价值**：论文在仿真和硬件上都验证了 workspace token 可替代原始观察解决需要长期记忆的任务，并报告它不仅更轻量，策略性能也更好。方向上的关键变化是把“记忆选择”从运行时 VLM 调用转成可部署的策略输入。
   - **局限**：训练期 saliency 判断错误会把关键历史压掉；跨任务、跨本体和长期在线更新的记忆污染仍未由摘要中的结果解决。

6. [StageGuard: Learning Stage Transitions for Long-Horizon Robot Tasks via Agentic Distillation](https://arxiv.org/abs/2609.20791v1)

   - **问题与机制**：层级机器人控制需要判断当前 skill 何时完成并切换到下一个子任务，但手工 completion checker 难以覆盖真实执行。StageGuard 用 teacher VLM 对示范轨迹生成带结构化解释的阶段完成信号，再蒸馏轻量 student VLM 做低延迟在线监控，并接入层级控制闭环。
   - **实验与关注价值**：论文在两个 benchmark 的阶段转换预测、BEHAVIOR-1K 闭环任务以及真实机器人上报告显著改进。它把“阶段边界”从任务脚本中的静态规则提升为可以训练、解释和审计的运行时状态。
   - **局限**：teacher 解释可能把 benchmark 语言模式带入 student；阶段误判会造成过早切换或重复执行，仍需报告恢复成本和安全边界。

7. [GeoAAC: Geometry-Based Adaptive Action Chunking from Denoising Trajectories in VLA Policies](https://arxiv.org/abs/2609.20776v1)

   - **问题与机制**：固定 action horizon 无法同时适应自由空间快速移动和接触阶段高频反馈。GeoAAC 从 flow-matching 去噪轨迹的 prefix 几何变化估计当前动作预测可靠性，在一次生成内按阶段自适应选择 chunk 长度，不需要额外训练。
   - **实验与关注价值**：在 GR00T N1.5、π0.5、LIBERO、LIBERO-Pro、RoboCasa365 和真实操作任务上，相比固定 horizon 最多提升 8.7 个百分点；真实平均成功率从 53.3% 提到 74.4%。它把实时性控制变成模型内部置信度与反馈频率的联动问题。
   - **局限**：去噪轨迹几何与实际动作风险的相关性可能随模型、任务和传感器改变；单次生成的 horizon 选择仍需在突发接触与严重延迟下验证。

8. [Agile-WAM: An Agile Tactile World Action Model for Contact-Rich Robot Control](https://arxiv.org/abs/2609.20761v1)

   - **问题与机制**：大生成式 backbone 能建模接触物理，但推理太慢，不适合高频控制。Agile-WAM 将视觉与触觉编码到共享 latent，直接用 vision-tactile-to-action flow matching 同时预测动作块和未来视觉／触觉 latent，并利用视觉慢变化、触觉接触突变的不同时间尺度做 multi-horizon supervision。
   - **实验与关注价值**：在 9 个模拟和 5 个真实接触操作任务上超过最强 baseline；真实实验报告整体成功率相对提升 29.4%，推理延迟为 11.9 ms。重点不只是融合触觉，而是为触觉旁路保留足够高的控制频率。
   - **局限**：触觉传感器标定、磨损与材质迁移会改变 latent；低延迟模型是否在未见接触模式下保持安全，需要比平均成功率更细的失败分析。

9. [SkipVLA: Skipping VLA Steps with Classical Planning for Fast Robot Manipulation](https://arxiv.org/abs/2609.20648v1)

   - **问题与机制**：VLA 在长时任务中每个时刻都运行会产生不必要的延迟和能耗，而经典规划器能快速处理自由空间却缺少语义和接触技能。SkipVLA 让运动规划器处理无接触段，只在抓取、放置等接触丰富阶段调用 VLA，并复用冻结的视觉语言 backbone 预测目标位姿。
   - **实验与关注价值**：用三个 VLA 在 13 个 LIBERO 任务和真实 6-DoF YAM 抓取任务上评估，报告任务完成最多加速 2.5 倍、能耗显著下降，同时保持相同任务成功率。它给“大模型控制全部时间步”提供了一个清晰的系统级替代接口。
   - **局限**：自由空间与接触阶段的切分依赖可靠几何和目标位姿；真实场景中的接触前异常、规划失败和回退策略仍需覆盖。

10. [MoWAM: Explicit Future Motion Prediction for Efficient World Action Models](https://arxiv.org/abs/2609.20709v1)

   - **问题与机制**：WAM 若在推理时生成未来视频，计算成本高；完全去掉未来监督又会使未来动力学只隐含在 observation feature 中。MoWAM 用紧凑的未来运动表示替代完整视频生成，训练期联合预测 motion 与 action，并用 task-progress verifier 从多个 motion-action 候选中选择。
   - **实验与关注价值**：在 LIBERO、LIBERO-Plus 和真实操作任务上报告较强的分布内性能、更好的分布外鲁棒性和更高的真实成功率；候选采样增多时性能继续提升。它把 inference-time scaling 从视频采样转成更小的运动候选搜索。
   - **局限**：紧凑运动是否覆盖不可逆形变、遮挡和接触后果取决于表示设计；候选数量、验证器偏差和控制延迟之间的折中需要明确预算。

## SLAM 与长期自治

11. [EliGSiR: Continual RGB-D Mapping with Gaussian Splatting under Bounded Compute](https://arxiv.org/abs/2609.20348v1)

   - **问题与机制**：传统 3D Gaussian Splatting 假设观测集固定且可以长时间优化，而在线建图必须不断吸收新观测、保留旧区域并受限于计算预算。EliGSiR 用地图状态驱动视角调度、按负载调整监督分辨率，并只在重复 RGB-D 证据显示缺失时扩充几何容量。
   - **实验与关注价值**：在 Replica、TUM RGB-D、ScanNet++ 和真实 RGB-D 序列上评估；在 TUM fr3/long_office_household 上以相同真值位姿达到 21.52 dB，对比 SplaTAM 的 19.42 dB；配合实时 ORB-SLAM3 位姿时达到 23.02 dB，用时 155.5 s。
   - **局限**：结果对位姿质量、RGB-D 传感器和场景重复观测依赖明显；动态对象、长期回环和真正低算力平台上的持续运行仍是部署风险。

## 趋势总结

- **驾驶后训练开始显式拆分 teacher、student 与验证工具链**：OPTED 用特权 teacher 解决闭环探索成本，MILER 用语义中层表示承接 sim-to-real，VAST 则把车路云互操作和 edge-case 发现纳入统一验证。
- **VLA 实时性从“换更小模型”转为“减少不必要的调用”**：GeoAAC 调 action horizon，SkipVLA 跳过自由空间 VLA 步骤，MoWAM 用未来运动候选替代未来视频生成。
- **具身安全的重点从最终成功率前移到过程状态**：SafeHarness 约束路线与接触，StageGuard 识别阶段边界，Workspace token 把长期记忆压成可部署状态，Agile-WAM 则把触觉突变保留在高频控制通道。
- **下一步核查重点**：闭环真实道路和真机中的误差恢复、传感器退化下的 memory／horizon 选择、验证工具链的场景覆盖，以及长期地图在动态环境中的证据保留。
