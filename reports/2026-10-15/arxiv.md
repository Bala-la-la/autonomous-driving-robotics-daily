# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-15

## 日期与证据口径

北京时间 2026-10-15 检索 [arXiv API](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.RO%20OR%20cat%3Acs.AI%20OR%20cat%3Acs.CV%29%20AND%20submittedDate%3A%5B202610120000%20TO%202610142359%5D&start=0&max_results=100&sortBy=submittedDate&sortOrder=descending)。以下 8 篇均在 **2026-10-13 UTC** 首次提交，是本期新入选论文；实验数值均为作者报告、未经独立复现。“关注价值／局限”为编辑判断。

## 自动驾驶、感知与安全运行时

### 1. AutoAgent0: An Agentic Runtime for Safe Closed-Loop Driving

- **论文／作者／时间**：[arXiv:2610.18866](https://arxiv.org/abs/2610.18866)；Jiageng Liu 等；v1：2026-10-13 17:59 UTC。
- **问题**：端到端驾驶专家单帧规划即使准确，未见场景中的感知误差也会在闭环累积，且同一策略常不能从危险状态恢复。
- **创新与机制**：AutoAgent0 将既有驾驶专家包在运行时 harness 内：独立检测技能建立场景上下文，规则验证器检查候选轨迹，失败时由 Recovery Planning 把动作原语组合为备选方案，并依据验证反馈迭代。
- **实验与关键结果**：在 Fail2Drive 和 NavSafe-∞ 的长尾／安全关键场景中，作者报告相对单一驾驶专家提升闭环鲁棒性；摘要未公布统一百分比，需查正文中的失败类型与干预代价分解。
- **关注价值／局限**：把安全改造成可插拔的执行期监督，因而可复用于多个底座模型；规则覆盖、独立检测器同源错误、恢复搜索时延和规则与真实交通法规不一致，仍可能成为新的失效面。

### 2. RadarGSOcc: Doppler-Aware 3D Semantic Occupancy Prediction Using 4D Radar Tensor with Geometric-Semantic Feature Extraction

- **论文／作者／时间**：[arXiv:2610.18686](https://arxiv.org/abs/2610.18686)；Christofel Rio Goenawan 等；v1：2026-10-13 16:40 UTC。
- **问题**：相机在暗光、LiDAR 在恶劣天气会退化；4D 雷达更稳健却稀疏，雷达 tensor 的计算又昂贵。
- **创新与机制**：RadarGSOcc 将 4D 雷达的几何与语义特征分支提取，以可变形注意力做几何细化并显式利用 Doppler；同时给出 K-Radar 3DSemOcc 基准及无逐帧真值恶劣天气下的 EBKL 代理指标。
- **实验与关键结果**：在 51.2 m、15 类预测上达到 **38.2% IoU、7.6% mIoU、25.5% weighted mIoU**；后者较 RadarOcc **21.9% 提升 17%（相对）**，且参数和计算更低，但 car 精度有取舍。
- **关注价值／局限**：为天气鲁棒占据建模补上运动线索与可复现数据基准；EBKL 是代理而非碰撞风险，稀疏雷达对弱小静态物体、跨雷达硬件与融合延迟的边界还需闭环验证。

## 机器人／具身智能

### 3. LoopWAM: Closed-Loop Generalist Policy Improvement from Deployment Rollouts

- **论文／作者／时间**：[arXiv:2610.18873](https://arxiv.org/abs/2610.18873)；Wenxuan Guo、Yingping Liang、Zhaoguo Wang 等；v1：2026-10-13 17:59 UTC。
- **问题**：部署 rollout 混有成功、次优和失败；全盘模仿会强化坏动作，筛掉失败又会丢掉接触后果证据。
- **创新与机制**：LoopWAM 用依赖数据来源的噪声采样统一行为学习与 action-conditioned world modeling，保留全质量视频监督，再以 quality steering 和质量加权的动作模仿调节策略；视频 token 与动作 token 在并行去噪中交互。
- **实验与关键结果**：RoboChallenge Table30-V2 三轮部署—训练从 **23.67% 升至 43.33%（+19.7 点）**；RoboTwin 2.0 平均 **94.5%**、RoboCasa365 **49.5%**；衬衫折叠两轮从 **13.20%** 到 **55.56%**。
- **关注价值／局限**：把失败轨迹从“噪声”转成可受控的学习信号，契合真实机器人持续改进；多轮收益是否能覆盖罕见危险失败、质量标签如何防止奖励投机、真实采集成本和灾难性回归仍须报告。

### 4. ChunkAct: Action Chunking for Agentic Robotics

- **论文／作者／时间**：[arXiv:2610.18874](https://arxiv.org/abs/2610.18874)；Bingxin Xu 等；v1：2026-10-13 17:59 UTC。
- **问题**：Agentic robotics 每个 primitive 都让 LLM 重新读取完整历史并推理，费用随 primitive 数增长，即使子目标确定后动作往往是固定套路。
- **创新与机制**：在线时一次 LLM 调用启动一串自主执行的 primitive，仅失败才回到规划；离线把记忆编译为这些 chunk，测试时常规执行不再检索记忆，规划器只处理真正需要决策的节点。
- **实验与关键结果**：在 LIBERO-Pro，作者称相对当时 agentic-robotics 最优方法成功率提高 **5.0 点**，LLM 调用少 **2.9×**、输入 token 少 **4.4×**、输出 token 少 **2.3×**。
- **关注价值／局限**：将 Skill／记忆变为可预测延迟的执行单元，适合板载或受预算约束的系统；chunk 的前置条件、执行中环境突变与失败检测的漏报，决定了“少调用”是否会牺牲安全恢复。

### 5. EgoExplorer: A Vision-Motion-Touch Observatory for Human Loco-Manipulation In Situ

- **论文／作者／时间**：[arXiv:2610.18872](https://arxiv.org/abs/2610.18872)；Yunsong Zhou 等；v1：2026-10-13 17:59 UTC。
- **问题**：人形机器人学习既要看到行走、姿态和物体交互如何联动，又需要可扩展、轻量的真实环境采集；现有数据常只覆盖其中一部分。
- **创新与机制**：EgoExplorer 用可穿戴设备采集 100 小时职业活动，将第一视角视频、重建全身运动、手指关节、触觉与步骤描述对齐；Calibrate-Complete-Constrain 先固定个体／传感器安装偏差，再由时间先验补全观测不到的关节并施加多层一致性约束。
- **实验与关键结果**：对 tracker-fitted 参考，作者报告身体点误差较最强基线降低 **71.9%**，手部稳定和接触估计也改善，并给出人形重定向与仿真全身控制的初步研究。
- **关注价值／局限**：为人形“走过去再操作”的连贯数据提供多模态证据；重建标注并非真值，职业人群与任务覆盖、隐私治理、触觉校准漂移及从人到机器人形态映射仍需审计。

### 6. Interaction Latents as Actions for Contact-Rich Manipulation

- **论文／作者／时间**：[arXiv:2610.18855](https://arxiv.org/abs/2610.18855)；Yuhang Zheng 等；v1：2026-10-13 17:59 UTC。
- **问题**：多数策略将动作仅表示为轨迹，触觉只是输入或辅助预测，无法把接触时序和施力本身变成可生成、可比较的动作目标。
- **创新与机制**：ILA 以视觉条件的动作—触觉联合重建学习可解码 interaction latent，用时序隐式解码器同时表达运动、接触和力；该 latent 可作为 flow-matching 的目标，也能用触觉条件专家参考做离线加权改善与失败修正。
- **实验与关键结果**：跨三类策略家族、四项真机任务，平均成功率相对触觉条件的直接动作基线提高 **21.0–36.5 个百分点**。
- **关注价值／局限**：将“怎样接触”提升为策略可迁移的 action interface，而不是额外传感通道；latent 可解释性、不同末端／材料的解码稳定性和高速碰撞时的力安全约束尚未由平均成功率证明。

### 7. ForceWAM: Decoupling Future and Response Learning from Demo and Play Data for Contact-Rich Manipulation

- **论文／作者／时间**：[arXiv:2610.18852](https://arxiv.org/abs/2610.18852)；Zijun Xu 等；v1：2026-10-13 17:58 UTC。
- **问题**：专家演示会告诉机器人任务应如何完成，却很少覆盖“不同动作会产生怎样的力响应”；无目标 play 则相反。
- **创新与机制**：ForceWAM 的世界模型从成功演示预测未来视频与六维力／矩，独立 inverse dynamics model 同时由任务与 play 数据学习，将视觉—wrench future 映射为动作；部署时 IDM 用新鲜 wrench 反馈在两次世界模型更新之间反应式执行。
- **实验与关键结果**：在真机力控滑动、带／不带扰动的翻盒与套环任务上，作者报告 **85–95%** 平均成功；加入任务无关 play 比只用演示提高 **15–45 点**。
- **关注价值／局限**：清晰分离“任务期望的未来”与“局部接触响应”，让非任务 play 有可解释用途；力传感器噪声、接触材料转移、IDM 对分布外 wrench 的安全退化与多步模型误差仍待检验。

### 8. EmbodiedEvo: Self-improving Coding Agents for Physical Intelligence

- **论文／作者／时间**：[arXiv:2610.18867](https://arxiv.org/abs/2610.18867)；Wenyi Li 等；v1：2026-10-13 17:59 UTC。
- **问题**：VLA 将观测直接映射为动作不易复用与审计；把 SWE 式“检查—改代码—执行—反馈”搬进物理世界又会遇到持续失败与经验遗忘。
- **创新与机制**：EmbodiedEvo 让 coding agent 在一个 Playground 场景的反馈中沉淀可复用 Skills 与 Lessons，再冻结该 harness 用于新场景；代码既是控制表示，也是修改和验证工作区。
- **实验与关键结果**：RoboDojo-Sim 平均分 **44.48**、成功率 **37.82%**，作者称超过已验证结果；Astra 经验使 Sol／Luna 较无经验提高 **8.86／5.50 点**，与原始交互历史相近的任务表现下执行成本低 **53.0%**。
- **关注价值／局限**：可读代码与经验资产有利于复现和跨模型迁移；结果主要在仿真，细粒度接触仍困难，代码执行的权限、沙箱、技能错误累积及真机动作确认必须成为系统一部分。

## 趋势总结

- **安全从模型属性变为运行时合同**：AutoAgent0 用独立感知、规则检查和恢复形成闭环，RadarGSOcc 用 Doppler 与代理指标补足退化感知；下一步应报告每个守卫的延迟、误报和未拦截风险。
- **世界模型开始利用“坏数据”和接触后果**：LoopWAM 保留混合质量 rollout，ILA／ForceWAM 将力与接触写入动作表示或未来预测；核心评测不应只看成功率，还要看错误接触的严重度与复原成本。
- **Agent 化机器人走向编译与可复用经验**：ChunkAct 将记忆编译为 action chunk，EmbodiedEvo 将反馈写进 Skills／Lessons；效率收益取决于前置条件、权限边界和失败时能否可靠回退。
