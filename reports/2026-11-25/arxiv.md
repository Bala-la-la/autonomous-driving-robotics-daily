# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-25

## 日期与证据口径

检索截至北京时间 2026-11-25 06:02。本期精选 **2026-11-23 UTC v1** 投稿的 7 篇论文；这是周日提交批次，明确不是 11 月 25 日当日投稿，且未出现在 11 月 21—24 日报告。题目、作者、时间、方法与数值均来自 arXiv 摘要/API；机构未能由该元数据完整核验时不臆测。所有性能数字均为作者报告，尚未独立复现。

## 自动驾驶／移动自治

### 1. [Pruning Autonomous Driving VLAs: What to Preserve for Reasoning and Action](https://arxiv.org/abs/2611.31240)

- **作者／机构／提交：** Seongchan Kim、Soowon Son、Sangoh Kim 等；机构未完整披露；v1，2026-11-23 18:59 UTC。
- **问题：** 带 CoT 的驾驶 VLA 同时做场景推理与轨迹生成，显存和算力昂贵；直接按单一重要性剪枝容易保住动作却损失推理，或反之。
- **创新与机制：** 提出 **MoOP**：用推理与轨迹两目标的 Taylor importance 联合排序 VLM 结构，并跨去噪步骤聚合 action expert 的 MLP channel 重要性，选定固定子集；不依赖剪枝后微调。
- **实验与关键结果：** 在 Alpamayo-1.5-10B 上，24.0% 总参数削减时保留 **94.0%** 的 dense LingoQA 分数；39.4% 削减（含移除 93.75% expert MLP channels）仍保持有竞争力的闭环表现，端到端推理 **1.37×** 加速、峰值显存降低 **36.6%**。
- **关注价值：** 把部署约束细化到“保留何种能力”的可测接口，为车端 VLA 的预算—推理—控制权衡提供可复核路径。
- **局限／跟进：** 仍主要是特定 backbone 与基准上的结构重要性；需报告不同硬件、长尾 ODD、量化叠加及剪枝后不安全理由/轨迹的尾部退化。

### 2. [CoSel: Cooperation as Selection for End-to-End Driving](https://arxiv.org/abs/2611.30918)

- **作者／机构／提交：** Yiping Li、Haohua Que、Zhipeng Bao、Wenjie Zhao、Qianwen Li；机构未完整披露；v1，2026-11-23 16:10 UTC。
- **问题：** V2X/路侧共享信息真正改变驾驶决策的样本很稀少，把其直接注入端到端规划器会让学习信号不足且干预原因难追溯。
- **创新与机制：** **CoSel** 保持 ego-only planner 不变，由独立 cooperative predictor 融合自车、RSU 与 CAV 观测来预测周边体，再逐条评估 planner 候选：原选择仍安全则保留，否则取最近安全替代；每次干预关联触发它的共享证据。
- **实验与关键结果：** V2Xverse 闭环 driving score **70.7**，比最佳比较协同方法高 **7.5**；MDrive 平均 **85.8**。72 个 ego 检测缺失场景中碰撞从 **17→19**，对照从 **19→32**。
- **关注价值：** 将协同感知收束为可审计“候选选择层”，既避免重训主规划器，又便于检查共享数据何时实际影响控制。
- **局限／跟进：** 安全上限受候选轨迹覆盖和预测校准限制；真实 V2X 的时钟偏移、通信延迟/攻击、RSU 失效与冲突证据的降级策略仍待闭环实测。

### 3. [Coordinating Perception and Planning for Test-Time Adaptation in End-to-End Driving under Distribution Shifts](https://arxiv.org/abs/2611.30739)

- **作者／机构／提交：** Shiyu Fang、Yiming Cui、Qihang Huang 等；机构未完整披露；v1，2026-11-23 14:18 UTC。
- **问题：** 驾驶 TTA 若只最小化感知熵，未必改善规划；持续在线更新还会发生参数漂移。
- **创新与机制：** **P2-TTA** 联合感知熵与从实际 ego motion 得到的回溯式时间规划一致性；以 EMA teacher 约束更新，并拒绝会增大历史 planning loss 的候选更新，作为 plug-and-play 模块接入多种端到端模型。
- **实验与关键结果：** 在严重分布偏移下，平均仅更新 **0.11‰** 参数、适配耗时 **19.9 ms**，作者报告 L2、collision rate、PDMS 分别恢复 **36.4%／30.0%／9.3%**；在 UniAD 比较中获最高 L2 与碰撞恢复。
- **关注价值：** 将“是否值得更新”从感知代理指标连接到已执行轨迹的规划后果，适合研究安全更新门与运行时回滚。
- **局限／跟进：** 历史一致性不能保证未来安全；19.9 ms 未包含完整车端队列和传感同步，仍需测试突变天气、误定位、灾难性遗忘与人工冻结阈值。

## 机器人／具身智能

### 4. [ACAP: Asynchronous Coding Agents for Efficient Robot Control](https://arxiv.org/abs/2611.31205)

- **作者／机构／提交：** Zexin He、Rui Li、Yushi Lan、Chengkai Jin、Zhi Hou、Xingang Pan；机构未完整披露；v1，2026-11-23 18:52 UTC。
- **问题：** 单一 coding agent 控制整台机器人会将可并行的臂、夹爪、底盘/躯干工作串行化；完全固定的分工又无法处理物理耦合。
- **创新与机制：** **ACAP** 将持续 agent 分配给可配置控制组，允许异步推理与执行；hyper-agent 负责依赖、任务分派及 lead/member 控制权动态分配，在独立工作和紧耦合操作间切换。
- **实验与关键结果：** 覆盖 25 个任务/平台设置的 **72** 次真机 rollout 中，相比单 agent Direct Policy，task-balanced time cost 降 **28.2%**；另有 **90** 次 rollout 研究中，六项任务均低于 Direct 的 30 分钟封顶平均时间。
- **关注价值：** 为多臂、移动操作等具身多 agent 系统提供按物理依赖划分的并发边界，而非只按对话角色分工。
- **局限／跟进：** 时间成本不替代安全与成功率；应公开冲突/抢占日志、通信和锁等待尾延迟、hyper-agent 单点失效，以及在接触事故时的硬实时停机链路。

### 5. [WeaveVLA: 3D Relational Grounding for Vision-Language-Action Models](https://arxiv.org/abs/2611.31126)

- **作者／机构／提交：** Zien Wang、Yuhao Pan、Yunfeng Fan 等；机构未完整披露；v1，2026-11-23 17:59 UTC。
- **问题：** VLA 往往把物体—夹爪相对 3D 关系隐含在视觉 token 内，观察变化后难保持可操作的空间关系。
- **创新与机制：** **WeaveVLA** 以任务条件稀疏 GNN 编码物体、夹爪与参考物的相对 3D 关系；pair-specific recurrent edge state 跨观测累计证据，learned-query readout 生成紧凑关系 token，同时以几何重建辅助目标维持结构。
- **实验与关键结果：** 在两种 backbone 上 LIBERO 平均成功率均超过 **98%**；LIBERO-Plus 从 **74.9→82.0%**、**85.7→87.8%**。三项真机任务的平均成功率从 **55.6→70.0%**，OOD 扰动从 **33.3→53.3%**。
- **关注价值：** 显式关系状态是让视觉语言策略能够诊断“哪段几何关系漂移”的中间接口，有助于和抓取可达性、碰撞检查结合。
- **局限／跟进：** 3D 关系依赖深度/位姿质量；需报告遮挡、柔性物、物体密集与跨相机标定误差下的关系污染，以及 token 对控制时延的代价。

### 6. [Real2Worlds2Real: Scaling Self-Improving Agentic Real2Sim2Real for Robot Manipulation](https://arxiv.org/abs/2611.31098)

- **作者／机构／提交：** Jinzhong Gu、Jiakai Chen、Xinyi Cao 等；机构未完整披露；v1，2026-11-23 17:39 UTC。
- **问题：** 真机交互昂贵；从有限视觉观测构造可用 digital twin，并扩展到多任务、多物理变化的仿真，通常要大量人工建模和反复修正。
- **创新与机制：** 框架让 tool-orchestration harness 从任务文字和视觉观察构建 twin，再生成可物理执行的 digital cousins；根据视觉与 rollout 反馈回访几何/物理决策，并编排数据生成、策略学习与细化，把已验证流程蒸馏为可复用 Skills。
- **实验与关键结果：** 作者报告世界保真度、真机策略迁移会随 world diversity 与交互数据量增加而改善，Skill reuse 继续提升建模效率与长程任务成功；摘要未披露统一的绝对成功率/样本数。
- **关注价值：** 重点不只是自动造场景，而是将“构建—仿真—策略—真机反馈”闭成可积累技能的证据链。
- **局限／跟进：** 缺少摘要级统一量化细节；digital cousin 的域外物理、生成资产许可、仿真漏洞利用和真机验证预算都应在完整论文/代码中审计。

## 交叉方向：长期导航

### 7. [GlanceNav: Efficient Vision-and-Language Navigation with Streaming Memory and Counterfactual Rewind](https://arxiv.org/abs/2611.30900)

- **作者／机构／提交：** Anh Dao、Quan-Dung Pham、Danh Vinh Le 等；机构未完整披露；v1，2026-11-23 16:02 UTC。
- **问题：** VLN MLLM 常在每一步重编码历史帧，成本随轨迹拉长；整段回报也难指出哪一步导致偏航。
- **创新与机制：** 混合 MLLM 的 Gated DeltaNet 维护全程 recurrent state，attention 只保留短窗口和按状态变化选出的少量关键帧，做到每步固定成本；**CoRe** 从偏航轨迹回退到最接近目标处，专家修正少量动作，以结果变化归因。
- **实验与关键结果：** 仅用 R2R-CE/RxR-CE 训练、RL 阶段 1,000 条指令时，4B 模型在 val-unseen 达 **71.9%／73.6%** success；R2R-CE 比无外部数据的最强单 RGB 先前方法高 **9.1** 点，单步 **104 ms**。
- **关注价值：** 将长期空间记忆、计算上界和可定位的反事实纠错合并，适合端侧导航和持续学习的资源预算讨论。
- **局限／跟进：** success 与平均步时不足以说明记忆是否可靠；应公布最长轨迹、错误 keyframe 保留、回退探索安全性、真实机器人传感失配和 p95 时延。

## 趋势总结

- **“更新/协同”正在被收紧为可拒绝的运行时层：** CoSel 只重选候选，P2-TTA 拒绝增大历史规划损失的更新；这比把新信息直接写进主策略更利于追溯，但候选覆盖和历史指标本身仍须校准。
- **具身 Agent 的效率开始来自结构，而非单纯模型压缩：** MoOP 明确分开推理/动作重要性，ACAP 按物理依赖并发，WeaveVLA 保留关系状态，GlanceNav 约束记忆大小。后续比较应共同报告端到端 p95、碰撞/失败尾部与硬件预算。
- **Real2Sim2Real 的核心资产转向可验证流程：** Real2Worlds2Real 把场景构建、rollout 和技能复用串起来；真实迁移仍需要对生成环境偏差、证据版本和高代价失败明确设门。
