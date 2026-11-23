# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪 arXiv 研究与 GitHub 开源趋势。


## 最新一期｜2026-11-24

- [arXiv 独立报告](reports/2026-11-24/arxiv.md)
- [GitHub Trending 独立报告](reports/2026-11-24/github-trending.md)
- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-24

## 日期与证据口径

检索截至北京时间 2026-11-24 06:00。本期采用最新可用的 **2026-11-20 UTC v1** 提交（周末后首个可检索批次），并非将其冒充为 11 月 24 日当日投稿；全部 **7** 篇均未出现在 11 月 21—23 日报告。题目、作者、提交时间、方法与数值来自 arXiv API、摘要页；机构未在可核验元数据中完整披露时不推测。性能数字均为作者报告，未经独立复现。

## 自动驾驶／移动自治

### 1. [Generalist Action Critic: Harnessing Frontier Models in Autonomous Driving](https://arxiv.org/abs/2611.27804)

- **作者／机构／提交：** Yun Yan、Shizhi Hu、Zhichao Li 等；机构未完整披露；v1，2026-11-20 16:32 UTC。
- **问题：** 专用驾驶规划器能生成可执行轨迹，但在少见危险场景中会选错候选；直接把大模型微调成动作输出又昂贵且难验证。
- **创新与机制：** 提出零训练的 **GAC** 推理 harness：专用规划器生成并初选多条轨迹，冻结的前沿模型读取相机图、空间叠加层、驾驶原则与受控上下文，只负责保留或重选候选，而不直接控制车辆。
- **实验与关键结果：** 在 HUGSIM，作者报告 DrivoR 的 HD-Score 达 **43.2**，相对三个规划器最高提升 **32.1%**；NAVSIM v1 中纠正 **52.13%** 可纠正的不安全选择，而原本高质量选择引入新失败仅 **0.67%**。
- **关注价值：** 是把通用推理接到安全关键系统的一种更窄接口：模型的作用、输入与输出都可审计，且保留专用控制器的实时执行边界。
- **局限／跟进：** 候选集若未含安全轨迹，critic 无法创造解；闭环仿真增益也不能替代实车时延、视觉误读和大模型服务失效下的安全论证。

### 2. [Interactive Semi-Parametric On-Track Learning for Vehicle Dynamics in Autonomous Racing](https://arxiv.org/abs/2611.27932)

- **作者／机构／提交：** Jungbin Kim、Youngim Nam、Cheolhyeon Kwon；机构未完整披露；v1，2026-11-20 18:08 UTC。
- **问题：** 极限工况下，纯物理模型漏掉轮胎/路面残差，纯数据残差又难解释；两者分别更新会互相改变学习目标。
- **创新与机制：** 用共享预测误差交替学习名义模型物理参数与数据残差；每次迭代只有在不增加共同目标时接受，从而给出单调不增、收敛的更新门。
- **实验与关键结果：** 相比名义模型，一步横向速度／横摆角速度预测误差在仿真下降 **90.0%／81.6%**，实车下降 **54.0%／59.4%**；作者称数值和硬件试验均优于对照。
- **关注价值：** 对赛车、自动泊车和高动态越野控制，提供“可解释参数 + 残差”的在线校准路径，而非一次性黑盒替代。
- **局限／跟进：** 结果主要是一阶预测误差，尚需报告闭环圈速、碰撞/越界尾部风险和在轮胎突变、雨雪等非平稳条件下的更新安全性。

## 机器人／具身智能

### 3. [Task2Hand: A Contact-Grounded Skill for Parametric Dexterous-Hand Morphology Design](https://arxiv.org/abs/2611.27967)

- **作者／机构／提交：** Haoyang Wang、Weibo Gao、Zhengxiong Li、Lingfeng Tao；机构未完整披露；v1，2026-11-20 18:48 UTC。
- **问题：** 灵巧手设计要反复处理几何、URDF/MJCF、碰撞、抓取初始化与策略训练，生成式设计容易把昂贵训练浪费在早期就不可行的候选上。
- **创新与机制：** **Task2Hand** 把功能说明变为参数化手模型，并按成本排序通过接触、动力学、学习三类 gate；每个 gate 留存证据，失败时只修改有界参数组并从最早阻塞点重跑，关键取舍交由人类确认。
- **实验与关键结果：** 生成的 4 指、16 驱动 DoF SAGE Hand 在六棱柱任务 **45.6% vs. LEAP 37.3%**、双色圆柱 **70.8% vs. 51.6%**；稠密仿真触觉将圆柱掉落率降逾一半。受控迭代中，Skill 路径保持 **164/165** 次有效捕获，对照仅 **14/165**。
- **关注价值：** 将 Agent 从“生成 CAD”推进到带回归守卫、可追溯设计资产的具身协同流程，适合把仿真训练预算投入真正有前景的本体。
- **局限／跟进：** 结果依赖匹配的仿真协议；真实制造公差、耐久、驱动成本和触觉 sim-to-real 偏差尚未验证。

### 4. [Non-penetrating World Models](https://arxiv.org/abs/2611.27963)

- **作者／机构／提交：** Yuhang Dai、Yinwei Wu、Ziyue Lin 等；机构未完整披露；v1，2026-11-20 18:44 UTC。
- **问题：** 交互视频世界模型会让物体穿过障碍，造成看似合理但物理不可能的 roll-out，直接削弱其用于规划与训练的价值。
- **创新与机制：** 建立 **NoPeBench**，并以冻结 DiT 隐状态上的轻量预测头读出候选动作是否会穿透；对不安全动作选择最能保留原意图的安全替换，形成 **NoPeWorld**。
- **实验与关键结果：** 六个视频世界模型平均物理违规率由 **74%** 降至 **16%**；作者报告可零样本迁移到开放域图像、第三人称视角和移动障碍，并开放代码、基准和权重。
- **关注价值：** 显示通用生成模型的内部表征可能已经含有物理违规线索，先加读出/门控层可比重训整个世界模型更实际。
- **局限／跟进：** “不穿透”只是物理正确性的一个维度；摩擦、稳定性、遮挡下的碰撞和替换动作的长期可达性仍需闭环机器人验证。

### 5. [What Must a Model Tell a Planner? Outcome Interfaces for Risk-Aware Planning After Robot Damage](https://arxiv.org/abs/2611.27939)

- **作者／机构／提交：** Hassan Iqbal、Krishna Kumar；机构未完整披露；v1，2026-11-20 18:12 UTC。
- **问题：** 机器人受损后，固定惩罚的端到端策略无法随着任务风险阈值改变路线；规划器需要的是可组合后果，而不是单一“该怎么走”。
- **创新与机制：** 比较决策策略、固定罚项策略、预测可行性/时间的 outcome model 与预测成功概率/时间并沿路径组合的 **capability contract**；全部使用相同经验、调参和不确定性 guard。
- **实验与关键结果：** 在弱电机、增载或低摩擦的 Go2/H1 仿真中，两个低风险探测即可使 capability contract 对危险地形的排序接近每种危险额外四次试验；在经验不可行路线选择限制 **5%** 时，Go2 拒绝任务由约 **32%** 降至 **7–8%**，H1 由 **57%** 降至 **35–36%**。
- **关注价值：** 将世界模型输出设计为规划可消费的风险—时间契约，支持同一经验库下按不同任务安全要求重规划。
- **局限／跟进：** 仅覆盖仿真 Go2/H1 与若干损伤类型；真实损伤诊断、传感失真和探索过程中的物理安全成本尚未纳入。

### 6. [EvoTER: Evolving Embodied Agents via Tool-Use Experience and Reflection](https://arxiv.org/abs/2611.27797)

- **作者／机构／提交：** Yingting Zhou、Yuyin Zhou、Yongliang Wang 等；机构未完整披露；v1，2026-11-20 16:28 UTC。
- **问题：** 长程具身 Agent 的局部修复或记忆总结未必改善完整任务，也难安全吸收新工具和失败经验。
- **创新与机制：** 不更新模型参数的三角色演化环：Explorer 记录工具轨迹，Diagnoser 从成败中提炼选工具、算参数、后置检查和恢复 Skill，Validator 仅在新 session 的完整任务成功率提升时保留修订。
- **实验与关键结果：** 仿真完整任务成功率由 **53.60%** 升至 **80.40%**；作者报告实物实验中继续演化让长程任务由 **20%** 升至 **80–100%**，并能吸收仿真后新增工具能力。
- **关注价值：** 强调经验库应以新会话的端到端收益验收，而不是以一次局部补丁或语言反思的流畅度验收。
- **局限／跟进：** 小规模真实任务的 80–100% 需要明确样本数、失败代价与跨环境复现；Skill 迭代也会带来权限膨胀和错误经验污染，须有版本回滚与人工审批。

## 交叉方向：边缘感知与移动平台

### 7. [Real-time neuromorphic audio and vision perception for autonomous robotic applications](https://arxiv.org/abs/2611.27953)

- **作者／机构／提交：** Guillem Fustier-Castillo、Ruben Ribes-Serrano、Javier Naranjo-Alcazar 等；机构未完整披露；v1，2026-11-20 18:27 UTC。
- **问题：** 神经形态感知多停留在离线基准，少有被整合进可行动移动机器人的端到端运行证据。
- **创新与机制：** 四轮 rover 将 Jetson 上的 PANNs 音频、Xylo Audio 2 上 SNN 音频与事件相机 + SpikeYOLO 锥桶检测容器化为 ROS 2 服务，并由可配置 action dispatcher 将类别映射为机器人行为。
- **实验与关键结果：** 原型演示了主机只配置并读取 Xylo 输出时的片上音频分类，以及声类反应与锥桶检测共同闭环；论文定位为系统集成可行性报告，摘要未给出统一能耗、端到端延迟或任务成功率对照。
- **关注价值：** 将“低功耗模型”落到传感器、芯片、ROS 服务和行为调度的完整接口，对受限算力巡检/救援平台有工程参考。
- **局限／跟进：** 仍是概念验证；需与 GPU-only 基线对比 p95 延迟、能耗、噪声鲁棒性和多传感器冲突处理，才能判断神经形态链路的实际收益。

## 趋势总结

- **运行时 gate 正成为具身系统的共同骨架：** GAC 复核候选轨迹、NoPeWorld 拦截穿透动作、Task2Hand 早停不可行设计、EvoTER 仅接受整任务增益；研究重点正从“一次生成最好答案”转到何时拒绝、替换或回滚。
- **世界模型的价值取决于输出接口：** 损伤机器人研究要求输出可组合的风险—时间契约，NoPeWorld 则从冻结生成器读出安全信号；对下游规划有用的不是更逼真视频本身，而是可校准、可验证的后果预测。
- **实物自治需补齐端侧证据：** 赛车半参数更新和神经形态 rover 都把模型放回硬件回路，但下一步必须并报闭环安全、尾延迟、能耗与故障退化，而非只给预测误差或演示视频。

# GitHub 开源趋势晨报｜2026-11-24

## 时间与证据口径

检索于北京时间 2026-11-24 06:00。日榜排名与 `+N/日` 来自 [githubtrending.today](https://githubtrending.today/api/archive/2026-11-23.json) 保存的 **2026-11-23 UTC** 日榜（`collectedAt` 2026-11-23 21:07 UTC）；这是采集窗口内的增星，并非本地轮询差值。当前 stars、forks、语言、许可证、创建／更新时间与项目描述来自本次 [GitHub Repository API](https://docs.github.com/rest/repos/repos#get-a-repository) 复核。排除了过去数期已选和明显面向漏洞利用/红队操作的高热项目；“走红原因”为编辑推断。

| 项目 | 当前 stars | 榜单增量依据 | 语言／类别 |
| --- | ---: | --- | --- |
| HKUDS/CLI-Anything | 63,532 | 日榜第 3，+783/日 | Python／软件 CLI 化与 Agent 执行 |
| firecrawl/firecrawl | 207,822 | 日榜第 6，+920/日 | TypeScript／网页数据与 Agent 检索基础设施 |
| openvinotoolkit/openvino | 12,268 | 日榜第 8，+183/日 | C++／边缘 AI 推理 |
| cathrynlavery/diagram-design | 70,899 | 日榜第 9，+624/日 | HTML／设计工件 Skill |
| Tracer-Cloud/opensre | 14,784 | 日榜第 13，+438/日 | Python／CI/CD SRE Agent |
| toeverything/AFFiNE | 77,336 | 日榜第 14，+593/日 | TypeScript／本地优先知识工作 |

## 精选项目

### 1. [HKUDS/CLI-Anything](https://github.com/HKUDS/CLI-Anything)

- **确认信息：** Repository API：**63,532** stars、5,772 forks，Python、Apache-2.0，创建于 2026-03-08；11 月 23 日日榜第 **3**、**+783/日**。项目目标是将图形软件转为 Agent 可调用的 CLI，并链接 CLI-Hub。
- **用途：** 为 Agent 把原本依赖 GUI 的软件能力暴露为脚本化、可编排命令接口。
- **走红原因（推断）／适合人群：** Agent 从代码生成扩展到操控现有软件时，CLI 是最易记录、测试和串联的执行面；适合构建本地工作流、桌面自动化与可复现设计/媒体流水线的开发者。
- **采用提醒：** GUI 软件的副作用仍需文件隔离、dry-run、命令 allowlist 和产物校验；“能调用”不代表默认安全或幂等。

### 2. [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)

- **确认信息：** Repository API：**207,822** stars、10,861 forks，TypeScript、AGPL-3.0，创建于 2024-04-15；日榜第 **6**、**+920/日**。仓库自述为 Agent 数据基础设施，提供搜索、抓取及 550+ 数据提供方的统一 API。
- **用途：** 为 RAG、研究 Agent 和数据采集工作流提供网页获取、清洗与访问层。
- **走红原因（推断）／适合人群：** 真实业务 Agent 的瓶颈常是新鲜、可引用的外部数据，而不是再换一个模型；适合需要网页检索/抽取管线的产品与数据平台团队。
- **采用提醒：** AGPL-3.0 对服务化集成有合规影响；同时需处理站点 robots/条款、速率限制、个人数据、提示注入与抓取结果溯源。

### 3. [openvinotoolkit/openvino](https://github.com/openvinotoolkit/openvino)

- **确认信息：** Repository API：**12,268** stars、3,678 forks，C++、Apache-2.0，创建于 2018-10-15；日榜第 **8**、**+183/日**。OpenVINO 是优化并部署 AI 推理的开源工具包。
- **用途：** 在 Intel CPU、GPU、NPU 等硬件上做模型转换、图优化和部署，服务视觉、语音与边缘 Agent。
- **走红原因（推断）／适合人群：** 随着多模态与本地 Agent 落地，成本、隐私和尾延迟促使团队重新关注推理部署底座；适合边缘 AI、机器人和平台工程团队。
- **采用提醒：** 性能需按目标芯片、模型版本和真实 batch/上下文长度实测，不能由单一吞吐 benchmark 外推；也应准备驱动和算子回退路径。

### 4. [cathrynlavery/diagram-design](https://github.com/cathrynlavery/diagram-design)

- **确认信息：** Repository API：**70,899** stars、4,745 forks，HTML、MIT，创建于 2026-04-16；日榜第 **9**、**+624/日**。自述提供面向 Claude Code、Codex、Copilot、Cursor 等的编辑式图表设计，覆盖 **52** 种图表类型，输出自包含 HTML + SVG。
- **用途：** 让编码 Agent 产出可继续编辑、可嵌入文档或网站的架构图、流程图和叙事图形。
- **走红原因（推断）／适合人群：** 社区正在偏好“可交付工件”而非一段提示词：结构化 SVG/HTML 更便于版本控制、审阅和品牌化；适合产品、解决方案和技术写作团队。
- **采用提醒：** 生成图应经过事实、可访问性（文字替代、色彩对比）与品牌规范审阅；不要把视觉整洁误认为架构正确。

### 5. [Tracer-Cloud/opensre](https://github.com/Tracer-Cloud/opensre)

- **确认信息：** Repository API：**14,784** stars、1,987 forks，Python、Apache-2.0，创建于 2026-01-13；日榜第 **13**、**+438/日**。仓库定位为开源 CI/CD 可靠性 Agent。
- **用途：** 辅助排查构建、测试和部署流程故障，并把运维诊断接入交付流水线。
- **走红原因（推断）／适合人群：** 代码生成提速后，CI 失败、发布回滚与环境差异成为团队新瓶颈；能读取日志并参与排障的 Agent 贴近实际交付价值。
- **采用提醒：** CI/CD 是高权限执行面：应强制只读诊断优先、生产变更审批、短期凭据、命令审计和网络/密钥隔离，不能把自动建议直接升级为自动发布。

### 6. [toeverything/AFFiNE](https://github.com/toeverything/AFFiNE)

- **确认信息：** Repository API：**77,336** stars、5,662 forks，TypeScript，许可证字段为 `NOASSERTION`，创建于 2022-07-31；日榜第 **14**、**+593/日**。项目自述是隐私优先、可定制的开源知识库，融合规划、整理与创作。
- **用途：** 提供本地优先的文档、白板与知识组织环境，可作为个人或团队知识工作基座。
- **走红原因（推断）／适合人群：** 生成式工作流促使用户希望把资料、画布与计划放在可导出、可控的空间中；适合重视本地数据控制与可定制知识管理的个人/团队。
- **采用提醒：** API 的 `NOASSERTION` 不可当作已确认开源许可，部署/二次分发前需核对仓库实际许可文本、同步/备份设置和团队数据 ACL。

## 技术趋势与社区偏好

- **Agent 栈由“会调用”走向受约束执行：** CLI-Anything、OpenSRE 与 Firecrawl 分别占据软件操作、发布可靠性和外部数据入口；社区兴趣已经覆盖完整执行链，但高权限命令、网页不可信内容和生产变更必须有最小权限与可回放证据。
- **可编辑工件和本地部署同时升温：** diagram-design 将图形变为版本化 HTML/SVG，AFFiNE 提供可控知识空间，OpenVINO 指向端侧推理。热度反映对可交付、可迁移、可控制资产的偏好，不能替代许可证、硬件兼容性和数据治理核验。

## 证据链接

- [GitHub Trending 2026-11-23 日榜归档](https://githubtrending.today/api/archive/2026-11-23.json)：排名、快照总 star 与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：第三方快照口径。
- 各项目的当前 metadata 以上述项目链接对应的 GitHub Repository API 为准；走红原因和趋势为编辑推断。

## 内容标准与归档

每期 arXiv 按问题、创新、机制、实验、价值和局限选篇；GitHub 区分可核验元数据与编辑推断。历史文件位于 [`reports/`](reports/)，跨期判断见 [分类趋势总结](CATEGORY_SUMMARY.md)。
