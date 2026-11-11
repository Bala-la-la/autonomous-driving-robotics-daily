# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪最新 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-11-12

- [arXiv 独立报告](reports/2026-11-12/arxiv.md)

- [GitHub Trending 独立报告](reports/2026-11-12/github-trending.md)

- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-12

## 日期与证据口径

截至北京时间 2026-11-12 06:00，arXiv API 在 `cs.RO`、`cs.CV`、`cs.AI` 的最新相关 v1 批次为 **2026-11-10 UTC**。以下七篇均为该日新提交，并已同 11 月 10—11 日报告去重；作者、时间、方法与数字均来自 arXiv 元数据和摘要。未能从元数据可靠核验机构时不作推断；摘要数字不等于开放环境安全保证。

## 自动驾驶／移动自治

### 1. [ForeseeDrive: Future-Token Conditioning for Anticipatory Generative Driving](https://arxiv.org/abs/2611.14286)

- **作者／机构／提交：** Shaokai Wu、Xunchu Zhou、Pinzhi Wang、Bo Dong、Yuting Hu 等；arXiv 未列可核验机构；v1 2026-11-10 16:27 UTC。
- **问题与创新：** 生成式驾驶规划即使能采样多条轨迹，后置打分器也无法补回候选集中缺失的规避动作。ForeseeDrive 在候选轨迹生成前，以未来演化 token 直接条件化轨迹几何。
- **机制／结构：** 从日志中的参与者运动、占据变化、路线交互和 TTC 裕度提取 query-indexed token；部署时由当前上下文预测同一 token 空间。零 token 门控残差与 candidate-preservation loss 限制无必要漂移，TTC-margin guard 专门约束安全边界附近的翻转。
- **实验与关键结果：** 摘要报告 NAVSIM navtest 89.2 PDMS、nuScenes 验证平均 L2 0.41 m 与碰撞率 0.05%、Bench2Drive 76.50 driving score；受控诊断显示零 token 时精确 no-op，但 oracle-best 和 TTC 边界仍有局部失败。
- **关注价值：** 把“未来”从事后评分信号前移成可部署的生成接口，针对候选覆盖不足这一闭环规划弱点。
- **局限／跟进：** token 由日志监督，可能继承数据覆盖偏差；需报告实时延迟、极端交互/OOD、候选多样性及真实车端风险收益。

### 2. [HiPFuse: Real-Time LiDAR Semantic Segmentation for Robotic Perception on Edge Devices](https://arxiv.org/abs/2611.14025)

- **作者／机构／提交：** Haiyang Wu、George Vosselman、Ville Lehtola；arXiv 未列可核验机构；v1 2026-11-10 12:57 UTC。
- **问题与创新：** 常规 BEV 聚合会混合一列中不同高度、不同语义的点，边缘设备又受算力限制。HiPFuse 用点特征与按高度分区的 BEV 特征跨尺度交换，兼顾垂直细节和大范围语境。
- **机制／结构：** 固定高度 assignment 保持垂直聚合组，辅助监督初始 BEV；双尺度 BEV context 再加入粗网格上下文，输入仅需一帧 LiDAR。
- **实验与关键结果：** SemanticKITTI/MCD 分别 63.7%/62.5% mIoU，在 Jetson AGX Orin 达 14.2/22.4 FPS；替换固定机器人系统中的语义前端后，两个室外序列平均 ATE RMSE 降 10.6%，SemanticKITTI 接受闭环召回升 8.7 个百分点。
- **关注价值：** 把语义分割指标接到定位/回环后果，且速度超过 10 Hz 扫描率，是感知—长期自治接口的实用证据。
- **局限／跟进：** 数据集与天气/传感器域偏移、Jetson 端到端尾延迟、动态交通参与者及真实车辆闭环安全仍待验证。

## 机器人／具身智能

### 3. [Is Your Robot's Memory Just a Clock? Temporal Shortcuts in Memory-Augmented VLA Policies](https://arxiv.org/abs/2611.14488)

- **作者／机构／提交：** Chubin Zhang、Bo An；arXiv 未列可核验机构；v1 2026-11-10 18:47 UTC。
- **问题与创新：** 许多 memory-VLA 均匀采样历史帧并编码时刻，可能把“时间经过”误作“任务已推进”。论文定义 phantom progress，并隔离其来自记忆索引而非机器人中断本身的因果来源。
- **机制／结构：** 在 RoboMME 计数任务中插入暂停/手腕 fidget 的无效事件，并单独缩放时间戳或移除记忆帧；提出按事件而非时钟索引 memory 的修复方向。
- **实验与关键结果：** 一个任务成功数由 47/50 降至 16/50，另一任务由 44/50 降至 10/50；移除对应记忆帧可恢复。仅去掉时间编码仍无效，而 event indexing 无需重训即可恢复至少一半损失。
- **关注价值：** 为“长历史”提出更精确的失败测试：状态记忆应代表发生了什么，而非固定速率示范中的隐式进度。
- **局限／跟进：** 仅覆盖特定计数任务和已发布设计；应测试视觉停顿、异步执行、任务切换、真实硬件时延与事件检测错漏。

### 4. [One Policy for 100 Household Tasks: Our Solution for the 2026 BEHAVIOR Challenge](https://arxiv.org/abs/2611.14432)

- **作者／机构／提交：** Ilia Larchenko、Gleb Zarin、Atindra Nair、Keerti Manney、Vitaly Kleban 等；arXiv 未列可核验机构；v1 2026-11-10 18:06 UTC。
- **问题与创新：** 长程家居任务常需每任务策略或昂贵评测。该方案以单个基于 π₀.₅ 的 VLA 覆盖 100 个 OmniGibson 任务，并将训练阶段、动作空间、采样与可恢复评测基础设施组合优化。
- **机制／结构：** 用演示 skill annotation 构造语义阶段，按相似旧任务 warm-start 新任务/阶段嵌入；21 维动作匹配遥操作控制，使用方差缩减多样本 flow matching 和按噪声—算力模型选 expert sample 数。14 个任务另由带观测/运动工具的 coding agent 处理。
- **实验与关键结果：** 50 个共享任务 Q 从 0.260 升至 0.371，100 任务总体 Q 0.392；公开提交 Q 0.446、完整任务成功率 27.3%。作者另报 agent 处理的 14 项平均 Q 0.639，学习策略为 0.108；二者并非同一评测设置，不能直接泛化比较。
- **关注价值：** 将统一策略、任务阶段与可恢复诊断合到规模化基准运行链，展示训练预算和评测基础设施同样决定具身结果。
- **局限／跟进：** 结果以模拟器为主，且部分 agent 成绩未进入公开提交；需公开任务逐项方差、推理/云成本、失败恢复和真机迁移。

### 5. [DexSeed: Expanding Human Hand-Object Interactions into Robot Demonstrations for Dexterous Policy Learning](https://arxiv.org/abs/2611.14092)

- **作者／机构／提交：** Huaijin Pi、Zehong Shen、Yong Wang、Kechun Xu、Changpeng Wang 等；arXiv 未列可核验机构；v1 2026-11-10 13:52 UTC。
- **问题与创新：** 灵巧 VLA 依赖昂贵遥操作数据；人手—物数据丰富却难直接转成可执行机器人轨迹。DexSeed 从人类交互扩增出保持抓取关系、可在物理中执行的机器人示范。
- **机制／结构：** 按 grasp mode 和共享语言描述组织源序列，InteractionMesh retargeting 与手臂轨迹增强适配不同手、物体和放置位置；RL 手指控制器生成可执行 rollout，将成功渲染观测与动作用于 VLA 微调。
- **实验与关键结果：** 作者报告相对基线更好的接触保真与全臂执行可靠性；仅用生成示范微调的 VLA 可在真机执行语言指定抓取。摘要未给统一成功率、对象数或 sim-to-real 置信区间。
- **关注价值：** 把人体交互数据转化为可执行、带视觉和动作的训练资产，有望缓解灵巧遥操作的瓶颈。
- **局限／跟进：** retargeting、接触模型和 RL rollout 可能筛掉最难样本；需评估未见手型/物料、遮挡、触觉缺失及生成数据偏差。

### 6. [LaST0.5: A Generalist World Action Model with Interaction-Centric Latent Reasoning](https://arxiv.org/abs/2611.14048)

- **作者／机构／提交：** Xuheng Zhang、Yiming Zhang、Jialin Gao、Hao Chen、Jiaming Liu 等；arXiv 未列可核验机构；v1 2026-11-10 13:15 UTC。
- **问题与创新：** 全局 world-model 表征未必保留机器人—物体局部接触信息，直接转给动作会造成表示目标错配。LaST0.5 在世界预测与动作生成间插入 interaction-centric physical latent。
- **机制／结构：** 在 Mixture-of-Transformers 中以 latent expert 连接 world expert 与 action expert；视觉交互线索监督局部物理推理，并联预测未来表征和 progress value，用 progress consistency 调节执行/未来重采样。预训练数据超 14k 小时。
- **实验与关键结果：** 摘要报告 LIBERO 99.5%，十个 RLBench 任务超过先前 SOTA，并给出长程与灵巧真实操作演示；完整基线、任务分布和真机成功率仍须在正文核验。
- **关注价值：** 不是只增加预测容量，而是把“局部交互”设为可学习中间接口，回应世界模型到控制的错配。
- **局限／跟进：** progress 值误判会触发错误重采样；需报告动作延迟、接触突变、未见工具和跨机器人收益，以及 14k 小时数据的质量/授权构成。

## 交叉方向：世界模型与安全执行

### 7. [LEASH: Stay Safe in Agentic Robotics](https://arxiv.org/abs/2611.14115)

- **作者／机构／提交：** Qinfeng Zhu、Weiguang Zhao、Ke Sun、Xihao Guo、Yunxi Jiang 等；arXiv 未列可核验机构；v1 2026-11-10 14:06 UTC。
- **问题与创新：** 以基础模型直接控制机器人会把提示注入、计划修复与不可逆执行风险并入同一闭环，但现有评测覆盖有限。RoboRisk 以五类风险建立仿真+实体评测，LEASH 在任务、动作和 commit 三层设置安全 gate。
- **机制／结构：** 92 个仿真任务、13 个实体任务覆盖拒绝、计划修复、执行期危险、注入和序列记忆；共享安全策略的 decision model 在视觉上下文中审核任务、每个动作和不可逆操作。
- **实验与关键结果：** 摘要称六个基础模型普遍出现高 harm rate；LEASH 在仿真和实体机器人中降低伤害，同时大体保留完成率且增加较少时间/token 开销，但未给统一 harm、成功率和置信区间。
- **关注价值：** 将“机器人 Agent 安全”从文本对齐推进为按执行时刻、不可逆性与视觉上下文分层审查的系统接口。
- **局限／跟进：** gate 本身会错判或成为延迟瓶颈；需独立复现攻击集、披露拒绝/误放行权衡，并验证断网、传感失效及人类紧急接管。

## 趋势总结

11 月 10 日的新稿将“预测”进一步压缩成可审计的执行接口：ForeseeDrive 在候选生成前写入未来条件，HiPFuse 将语义收益连到定位，LaST0.5/Only memory 研究分别约束交互状态与事件进度，DexSeed 让数据先满足可执行性，LEASH 则为不可逆动作增加门控。共同的下一步不是再叠一层 latent 或 Agent，而是分别报告状态是否正确、何时失效、门控/重采样是否及时，以及在真实扰动下能否安全降级。

# GitHub 开源趋势晨报｜2026-11-12

## 时间与证据口径

检索于北京时间 2026-11-12 06:00。Trending 增量取自第三方镜像保存的 **2026-11-11 UTC 日榜**（采集 2026-11-11 21:07 UTC）；`+N/日` 是镜像记录的 GitHub Trending `gained`，不是本次总 star 的相减值。当前 star、语言、许可证和用途以本次 GitHub Repository API 复核为准；镜像不是 GitHub 官方服务。项目“走红原因”及趋势结论均为编辑推断，star 不证明质量、安全或生产采用。

## 精选项目

### 1. [meta/astryx](https://github.com/meta/astryx)

- **数据：** API 当前 **24,810 stars**；11 月 11 日日榜第 1、**+2,842/日**；TypeScript；MIT。证据：[Repository API](https://api.github.com/repos/meta/astryx)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 可高度定制、面向 Agent 的开源 design system。
- **走红原因（推断）：** 团队希望 Agent 产出的 UI 能落回 design token 与组件约束，热度反映“可编辑工件”而非只生成页面的需求延续。
- **适合人群：** 维护前端设计系统的团队；应先检查无障碍、主题、版本迁移与生成输出的审阅流程。

### 2. [GoogleChrome/modern-web-guidance-src](https://github.com/GoogleChrome/modern-web-guidance-src)

- **数据：** API 当前 **1,682 stars**；日榜第 3、**+133/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/GoogleChrome/modern-web-guidance-src)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 仓库自述为空；从仓库名和组织可确认其为 Chrome 团队发布的现代 Web guidance 源码，具体 Agent 集成范围须以 README/版本文档为准。
- **走红原因（推断）：** 面向 Agent 的 Web 开发需要可靠、可版本控制的技术指导来源，官方组织发布降低了资料来源的不确定性。
- **适合人群：** 构建 Web 工程规范或辅助编码上下文的团队；勿把组织归属当作完整兼容性/安全保证，须逐版本核验内容和许可。

### 3. [shadcn/improve](https://github.com/shadcn/improve)

- **数据：** API 当前 **10,784 stars**；日榜第 4、**+333/日**；主要语言未标注；MIT。证据：[Repository API](https://api.github.com/repos/shadcn/improve)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 以能力较强模型审计代码库、产出计划，再让低成本模型执行该计划。
- **走红原因（推断）：** 将昂贵推理聚焦在规划/审阅、将实施分发给更廉价执行模型，直击 coding agent 的成本与稳定性问题。
- **适合人群：** 有成熟 CI 与代码审阅机制的软件团队；计划必须经过人类/自动测试验证，不能让下游模型获得未审阅的写权限。

### 4. [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)

- **数据：** API 当前 **115,870 stars**；日榜第 5、**+788/日**；JavaScript；MIT。证据：[Repository API](https://api.github.com/repos/addyosmani/agent-skills)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 面向 AI coding agent 的 production-grade engineering skills。
- **走红原因（推断）：** 连续多日上榜说明工程团队在把审阅、设计和交付约束沉淀为版本化资产；这是兴趣信号，不是采用率统计。
- **适合人群：** 使用 coding agent 的应用/平台工程师；把每个 Skill 视作可执行依赖，审阅脚本、网络访问、数据输入、许可并在沙箱测试。

### 5. [vercel-labs/agent-browser](https://github.com/vercel-labs/agent-browser)

- **数据：** API 当前 **49,806 stars**；日榜第 6、**+712/日**；Rust；Apache-2.0。证据：[Repository API](https://api.github.com/repos/vercel-labs/agent-browser)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 面向 AI Agent 的浏览器自动化 CLI。
- **走红原因（推断）：** 结合 Skills/计划型工具的同榜表现，浏览器仍是 Agent 获取信息和落地内部流程的通用执行面。
- **适合人群：** 受控网页测试和内部自动化团队；隔离会话与凭据、设置域名 allowlist，并对支付、发布、删除等写操作设置明确确认。

### 6. [homeassistant-ai/ha-mcp](https://github.com/homeassistant-ai/ha-mcp)

- **数据：** API 当前 **7,284 stars**；日榜第 8、**+640/日**；Python；MIT。证据：[Repository API](https://api.github.com/repos/homeassistant-ai/ha-mcp)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 让 Claude、ChatGPT 等助手配置和自动化 Home Assistant。
- **走红原因（推断）：** MCP 将 Agent 接到真实设备控制面，增长显示对可执行连接器的兴趣延续，并不证明默认配置安全。
- **适合人群：** 已部署 Home Assistant 的自动化开发者；从只读/低风险实体开始，最小化 token 权限，并把门锁、警报、能源类动作置于独立审批。

### 7. [openai/codex-security](https://github.com/openai/codex-security)

- **数据：** API 当前 **11,655 stars**；日榜第 9、**+20/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/openai/codex-security)、[日榜快照](https://githubtrending.today/api/archive/2026-11-11.json)。
- **确认用途：** 用于发现、验证和修复安全漏洞的 Codex Security CLI 与 TypeScript SDK。
- **走红原因（推断）：** 在 Agent 能写代码、操作浏览器和设备的同一榜单中，安全验证工具显示社区开始要求执行链附带审计与修复闭环。
- **适合人群：** 希望把安全检查纳入开发流程的工程/安全团队；先用只读扫描与隔离测试仓库验证误报、范围、数据外传和自动修复审批。

## 技术趋势与社区偏好

本期热点形成“规范—计划—执行—审计”的链条：Modern Web Guidance/Skills 提供可版本化知识，Astryx 提供可编辑 UI 约束，Improve 划分高价规划与低价实施，agent-browser/ha-mcp 打开网页与实体执行面，Codex Security 补上验证。社区偏好显然不止模型能力，而是可复用工作流和可交付产物；相应地，任何安装内容都应先审计供应链、写权限、凭据、数据留存和许可证。

## 证据链接

- [GitHub Trending 2026-11-11 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-11.json)：排名、快照总 star 与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：镜像采集和统计口径。
- 各项目当前元数据以上述 Repository API 为准；走红原因均为编辑推断。

## 历史归档

报告按 [reports/](https://github.com/Bala-la-la/autonomous-driving-robotics-daily/tree/main/reports/) 下的 YYYY-MM-DD/ 保存，每天保留 arXiv 与 GitHub 两份独立报告。

## 内容标准

- arXiv 报告明确标注提交日期、问题、机制、实验、关注价值与局限；无新稿时标明回溯日期。
- GitHub 报告区分当前仓库元数据、Trending 增量证据和编辑推断，并注明重复观察与统计窗口。
- README 最新一期直接展示两份报告全文；跨期判断维护于 [CATEGORY_SUMMARY.md](CATEGORY_SUMMARY.md)。
