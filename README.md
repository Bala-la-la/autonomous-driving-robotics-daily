# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪最新 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-11-10

- [arXiv 独立报告](reports/2026-11-10/arxiv.md)

- [GitHub Trending 独立报告](reports/2026-11-10/github-trending.md)

- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-10

## 日期与证据口径

截至北京时间 2026-11-10 06:00，arXiv API 在 cs.RO、cs.CV、cs.AI 与 eess.SY 中最新可见的相关 v1 批次为 **2026-11-06 UTC**；周末后尚无更晚常规批次，故本期明确回溯该日，并非将旧稿称为 11 月 10 日新稿。作者、时间和实验数字均以 arXiv 摘要/元数据为准；API 未给可核验机构时不推断，摘要指标不等同真实道路或生产部署保证。

## 自动驾驶／移动自治

### 1. [Scenario Orchestration for Closed-loop Policy Evaluation of Autonomous Driving](https://arxiv.org/abs/2611.09888)

- **作者／机构／提交时间：** Frieda Rong、Zhaoyue Wang、Veer Kapadia、Vishaka Rajani、Aren A. Babikian、Xujie Si、Mahsa Golchoubian、Raquel Urtasun、Igor Gilitschenski；arXiv 未列可核验机构；v1 于 2026-11-06 18:58 UTC。
- **问题与创新：** 预先脚本化的交通参与者在 ego 闭环响应后往往不再形成原定交互；单纯 learned actor 又未必能稳定实现测试意图。该工作将“情景是否真正发生”与“ego 是否失败”分开判定。
- **机制／结构：** orchestrator 持续观察联合交通状态，对非 ego 车辆做重定时、重路由和角色重新分配；每步解受约束优化，既维持目标交互，又限制干预并保持交通可行。
- **实验与关键结果：** 在 CARLA 多类场景及多种驾驶策略中，作者报告比脚本式和 learned actor 基线更可靠地实现目标交互，尤其能抵抗初值和 ego 行为变化；摘要未给出绝对成功率。
- **关注价值：** 让闭环评测能区分“没测到预定危险”与“策略应对失败”，提高测试可复现性和失败归因质量。
- **局限／跟进：** 证据限于 CARLA；需要公开干预幅度、对其他交通参与者的自然性影响、动态约束失效与真实地图/交通规则下的迁移结果。

### 2. [EGT: Execution-Grounded Traversability through Learned Closed-Loop Trajectory Distributions](https://arxiv.org/abs/2611.09270)

- **作者／机构／提交时间：** Chinmay Mundane、Amith Manoharan、Arun Kumar Singh；arXiv 未列可核验机构；v1 于 2026-11-06 10:26 UTC。
- **问题与创新：** 逐点 roll/pitch 或力角裕度会忽略低层控制修正与地形扰动，因而对越野路径既误拒安全路径也可能放行风险路径。EGT 改估计“特定车—控制器组合完成整条路径”的概率。
- **机制／结构：** 以多分辨率地形特征、车体姿态和轮地接触先验为条件，用 latent flow matching 预测闭环轨迹分布；在 receding-horizon sampling planner 中以该分布评价候选路径。
- **实验与关键结果：** 650 个未见仿真地形中，安全路径误拒降至 2.2%（对照为 11.4%–39.5%），危险路径误接受 7.7%；规划器失败率较两组基线低 24–42 与 30–44 个百分点，且有仿真训、户外零样本实测。
- **关注价值：** 将可通行性从静态几何阈值推进到包含控制器的闭环风险接口，适合检查地图质量之外的执行后果。
- **局限／跟进：** 实测规模、气候/速度覆盖和失效案例仍未在摘要中量化；需测试传感噪声、轮胎/载荷变化、罕见地表及概率校准。

## 机器人／具身智能

### 3. [On Agentic Manipulation Policies](https://arxiv.org/abs/2611.09892)

- **作者／机构／提交时间：** Chen Chen、Omid Bagherieh、Naveen Nikamanth Appiah Balaji 等 13 人；arXiv 未列可核验机构；v1 于 2026-11-06 18:59 UTC。
- **问题与创新：** 专项 VLA/WAM 通常依赖示范和任务训练；作者检验通用 AI 模型能否在执行中直接指挥机械臂，并给出可跨单臂、双臂、移动操作复用的 AMP1 harness。
- **机制／结构：** harness 不预置抓取、推拉或放置技能，Agent 按观测迭代出动作策略，可搜索遮挡物、把物体当工具和校准相机；可选跨 episode persistent memory 记录经验。
- **实验与关键结果：** RoboLab-120 零样本成功率 85.6%，对比所列 VLA/WAM 的 49.2%/42.9%；12 个任务、3 个机器人共 108 次真机试验成功 104 次。加记忆后 RoboDojo 双臂任务失败率相对零样本低 4.6 倍。
- **关注价值：** 将泛化能力、工具使用和记忆放到同一可运行接口，直接挑战“每类操作须专训”的假设。
- **局限／跟进：** 摘要未展开模型调用成本、控制频率、失败安全和真实任务分布；104/108 试验不等同开放环境可靠性，需独立复现并审计记忆污染与外部工具权限。

### 4. [Grasp-TAGS: Task-Aware Grasp Selection via Critic Distillation for Prehensile Loco-Manipulation](https://arxiv.org/abs/2611.09864)

- **作者／机构／提交时间：** Xun Tu、Minghao Zou、Karthik Desingh；arXiv 未列可核验机构；v1 于 2026-11-06 18:44 UTC。
- **问题与创新：** 几何上稳定的抓取会造成截然不同的后续搬运/放置结果，固定初始抓取掩盖了这一差异。工作把长程任务回报蒸馏成接触前即可用的抓取效用评分器。
- **机制／结构：** 跨多个初始抓取训练统一 PPO policy；将 critic 蒸馏为仅看候选抓取配置和目标的轻量 grasp-utility network，推理时先挑最高下游效用抓取再运行主策略。
- **实验与关键结果：** 大物体重排平均成功率 89.84%，优于最强单抓取策略的 79.87%（+9.97 点），并降低所有评估物体的末端朝向误差。
- **关注价值：** 把接触前选择与接触后长程后果连起来，可作为移动操作中更便宜的任务条件化入口。
- **局限／跟进：** PPO 价值估计和候选抓取集可能共同限制泛化；应验证视觉噪声、未知物体、抓取检测失败、真机接触力与不同底盘动力学。

### 5. [MDF++: Visuo-Tactile World Action Model with End-to-end Representation Learning](https://arxiv.org/abs/2611.09293)

- **作者／机构／提交时间：** Zixuan Huang、Jinhao Yu、Zachary Charlick、Dmitry Berenson；arXiv 未列可核验机构；v1 于 2026-11-06 10:47 UTC。
- **问题与创新：** 许多 WAM 固定重建式预训练 encoder，表示未必服务于控制；直接端到端联合训练又会 feature collapse。MDF++ 以视觉—触觉相关性学习物理且控制相关的 latent。
- **机制／结构：** 扩散式 WAM 同时建模动作和未来观测；多任务训练将跨模态预测作为表示学习约束，避免 naive joint training 的坍塌。
- **实验与关键结果：** 在含真实 bolt screwing、nut mating 的接触丰富任务中，作者报告相对 frozen representation WAM 最高提升 50%。
- **关注价值：** 触觉不再只是策略附加输入，而成为世界动作表示本身的训练信号，适合精细接触和失败预判。
- **局限／跟进：** “最高 50%”未说明任务切片、绝对成功率和方差；需测试触觉传感漂移/缺失、模态不同步、推理延迟及跨硬件迁移。

### 6. [SURE: Spatiotemporal Uncertainty Representation for Efficient Vision-Language-Action Learning](https://arxiv.org/abs/2611.09684)

- **作者／机构／提交时间：** Jingye Zhang、Choo Sin Wai、Dake Zhong、Zhifang Liu、Yuhong Zhang、Siyao Xiao、Guorui Song；arXiv 未列可核验机构；v1 于 2026-11-06 16:32 UTC。
- **问题与创新：** 同一操作可由邻近动作或不同时速完成，逐点模仿把示范轨迹错误视为唯一真值。SURE 显式建模空间和时间两类动作不确定性，以减少示范需求。
- **机制／结构：** 轻量转置卷积概率 decoder 用相邻 action bin 相关性表达空间不确定性；Soft-DTW 将预测 action chunk 与示范作局部时间对齐。
- **实验与关键结果：** 在 LIBERO、RoboTwin 2.0 和真机操作中，作者报告仅用 10% 示范数据或 20% 训练步数即可达到或超过基线 VLA 的成功率。
- **关注价值：** 提供一种区分“合理轨迹多解”与“策略偏离”的训练口径，有望降低采集数据时对单一操作者姿态/节奏的过拟合。
- **局限／跟进：** 摘要未给不同任务的绝对数字和计算开销；对高风险接触、多峰但差异显著的动作及目标移动时，宽分布可能反而掩盖错误，需做校准和安全消融。

## 交叉方向：形态与全身接触

### 7. [Autonomous Whole-body Loco-manipulation Using a Snake Robot](https://arxiv.org/abs/2611.09777)

- **作者／机构／提交时间：** Adarsh Salagame、Henry Noyes、Haroon Hublikar、Alireza Ramezani；arXiv 未列可核验机构；v1 于 2026-11-06 17:38 UTC。
- **问题与创新：** 蛇形机器人的身体同时用于推进和推物，无法像轮腿平台那样把移动与操作拆分。论文让 COBRA 任意身体段参与接触，在侧绕行中自主推物至目标。
- **机制／结构：** Moreau–Jean time-stepping contact-implicit dynamics 统一机器人—地面、机器人—物体、物体—地面接触；几何规划器和 nominal P controller 引导全阶动力学轨迹优化。
- **实验与关键结果：** 作者在多种配置上进行硬件验证，并给出简化轨迹优化的仿真接触解析；摘要未列成功率、路径误差或计算时间。
- **关注价值：** 展示“身体即末端执行器”的规划接口，适合研究受限空间和分布式接触中的形态—控制耦合。
- **局限／跟进：** 缺少摘要级量化比较；需报告接触估计误差、地面摩擦变化、碰撞恢复、实时优化时延和对非规则物体的泛化。

## 趋势总结

本期共同主题是把“执行后果”前移到系统接口：驾驶测试动态维持目标交互，越野规划预测控制器实际会跑出的轨迹；操作则分别将 Agent 运行、接触前抓取价值、视觉—触觉表示和示范多解性纳入决策。它们的可迁移性仍应由真实硬件尾延迟、状态/记忆校准、传感缺失与失败回退来检验，而不是只看仿真成功率或摘要中最高增益。
# GitHub 开源趋势晨报｜2026-11-10

## 时间与证据口径

检索于北京时间 2026-11-10 06:00。采用第三方镜像保存的 **2026-11-09 GitHub Trending 日榜**（采集时间 2026-11-09 22:01 UTC）；“日增”是镜像记录的 Trending `gained`，并非当前总 star 的差值。当前 stars、语言、许可证和描述均由 GitHub Repository API 在本次检索时复核。镜像并非 GitHub 官方服务；“走红原因”和趋势判断均为编辑推断，star 不代表安全、质量、真实安装量或生产采用。

## 精选项目

### 1. [anthropics/skills](https://github.com/anthropics/skills)

- **数据：** API 当前 **190,839 stars**；11 月 9 日日榜第 1、**+1,052/日**；Python；API 许可证字段 `NOASSERTION`。证据：[Repository API](https://api.github.com/repos/anthropics/skills)、[日榜快照](https://githubtrending.today/api/archive/2026-11-09.json)。
- **确认用途：** 仓库描述为公开 Agent Skills 仓库；提供可被 Agent 使用的任务说明与资源组织方式。
- **走红原因（推断）：** 把可复用流程作为可检查、可安装的资产，正好满足团队将“提示经验”沉淀为工程接口的需求；日增不证明单个 Skill 的安全性或效果。
- **适合人群：** 想规范化 Agent 工作流的开发团队；采用前逐条审阅指令、脚本、网络访问和许可证，避免将仓库热度当作执行授权。

### 2. [meta/astryx](https://github.com/meta/astryx)

- **数据：** API 当前 **19,759 stars**；11 月 9 日日榜第 2、**+3,324/日**；TypeScript；MIT。证据：[Repository API](https://api.github.com/repos/meta/astryx)、[日榜快照](https://githubtrending.today/api/archive/2026-11-09.json)。
- **确认用途：** 仓库描述为可高度定制、agent-ready 的开源 design system。
- **走红原因（推断）：** 设计系统把生成式界面从一次性截图拉回 token、组件和约束，可让人和 Agent 在同一可编辑界面层协作；高日增仍需要观察 API 稳定性与真实产品采用。
- **适合人群：** 维护前端组件库、希望在受控设计令牌下使用 Agent 的设计工程团队；先评估现有组件、主题和无障碍标准的兼容性。

### 3. [google-deepmind/mujoco](https://github.com/google-deepmind/mujoco)

- **数据：** API 当前 **16,870 stars**；11 月 9 日日榜第 4、**+579/日**；C++；Apache-2.0。证据：[Repository API](https://api.github.com/repos/google-deepmind/mujoco)、[日榜快照](https://githubtrending.today/api/archive/2026-11-09.json)。
- **确认用途：** 通用多关节接触动力学物理模拟器。
- **走红原因（推断）：** 机器人策略、世界模型和 Agent 可执行性验证持续升温，带动可复现实验底座受到关注；榜单不能证明某个任务的 sim-to-real 误差已解决。
- **适合人群：** 机器人研究者、控制/强化学习工程师；应单独校准接触、摩擦、传感与执行器模型，不把模拟成功直接外推到真机。

### 4. [vercel-labs/agent-browser](https://github.com/vercel-labs/agent-browser)

- **数据：** API 当前 **48,402 stars**；11 月 9 日日榜第 7、**+914/日**；Rust；Apache-2.0。证据：[Repository API](https://api.github.com/repos/vercel-labs/agent-browser)、[日榜快照](https://githubtrending.today/api/archive/2026-11-09.json)。
- **确认用途：** 面向 AI Agent 的浏览器自动化 CLI。
- **走红原因（推断）：** CLI 将网页操作装进可脚本化、可组合的 Agent 执行面，适配测试、信息录入和研究工作流；高增长不等于网站条款、验证码和身份权限问题已被解决。
- **适合人群：** 构建受控浏览器测试或内部自动化的开发者；隔离会话、最小化凭据、设置域名 allowlist，并审查每个可写操作的确认机制。

### 5. [anthropics/claude-quickstarts](https://github.com/anthropics/claude-quickstarts)

- **数据：** API 当前 **19,975 stars**；11 月 9 日日榜第 5、**+560/日**；Python；MIT。证据：[Repository API](https://api.github.com/repos/anthropics/claude-quickstarts)、[日榜快照](https://githubtrending.today/api/archive/2026-11-09.json)。
- **确认用途：** 用于快速启动可部署 Claude API 应用的项目集合。
- **走红原因（推断）：** 可运行模板比抽象 API 文档更容易缩短原型到部署的距离；star 不能替代对成本、数据流与版本锁定的工程审查。
- **适合人群：** 需要评估 LLM 应用结构的产品和开发团队；将示例中的密钥管理、限流、日志、内容安全和依赖版本作为上线前必审项。

### 6. [homeassistant-ai/ha-mcp](https://github.com/homeassistant-ai/ha-mcp)

- **数据：** API 当前 **5,891 stars**；11 月 9 日日榜第 10、**+31/日**；Python；MIT。证据：[Repository API](https://api.github.com/repos/homeassistant-ai/ha-mcp)、[日榜快照](https://githubtrending.today/api/archive/2026-11-09.json)。
- **确认用途：** 让 Claude、ChatGPT 等 AI 助手配置和自动化 Home Assistant。
- **走红原因（推断）：** MCP 把自然语言 Agent 接到真实设备与家庭工作流，体现社区从“会回答”走向“能执行”的偏好；较低日增仅表示本期持续入榜，不代表同级爆发。
- **适合人群：** 已有 Home Assistant 环境的极客与自动化开发者；先以只读或低风险实体试验，划分家庭成员权限并避免让模型无审计地控制门锁、报警、能源设备。

### 7. [garrytan/gbrain](https://github.com/garrytan/gbrain)

- **数据：** API 当前 **32,095 stars**；11 月 9 日日榜第 6、**+215/日**；TypeScript；MIT。证据：[Repository API](https://api.github.com/repos/garrytan/gbrain)、[日榜快照](https://githubtrending.today/api/archive/2026-11-09.json)。
- **确认用途：** 仓库描述为面向 OpenClaw/Hermes Agent 的 opinionated “Agent Brain”。
- **走红原因（推断）：** 多轮 Agent 任务开始需要把个人偏好、上下文和操作原则持久化；公开的 brain 模板容易被复制和二次传播。日增不能证明其中记忆内容正确、隔离或适合团队使用。
- **适合人群：** 研究 Agent 长期上下文和个人自动化的开发者；应检查记忆保存位置、敏感信息脱敏、注入防护、更新与删除策略。

## 技术趋势与社区偏好

这份日榜将 Skills、design system、quickstarts、browser CLI、家庭自动化和 Agent memory 放在同一条链上：社区更偏好可复用指令、可编辑工件、可运行模板，以及能进入真实环境的执行接口。MuJoCo 的持续上榜说明物理仿真仍是具身系统的基础设施。对应的工程门槛也更清晰：Skills/模板要审计命令，浏览器与家庭自动化要收紧身份和写权限，持久记忆要有数据生命周期与注入治理；这些结论是样本推断，不由 star 数自动成立。

## 证据链接

- [GitHub Trending 2026-11-09 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-09.json)：含排名、stars 和 `gained` 字段。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：第三方镜像说明其数据来源与统计方式。
- 各项目的用途、语言和许可证以相应 GitHub Repository API/README 为准；“走红原因”均为编辑推断。
## 历史归档

报告按 [reports/](https://github.com/Bala-la-la/autonomous-driving-robotics-daily/tree/main/reports/) 下的 YYYY-MM-DD/ 保存，每天保留 arXiv 与 GitHub 两份独立报告。

## 内容标准

- arXiv 报告明确标注提交日期、问题、机制、实验、关注价值与局限；无新稿时标明回溯日期。
- GitHub 报告区分当前仓库元数据、Trending 增量证据和编辑推断，并注明重复观察与统计窗口。
- README 最新一期直接展示两份报告全文；跨期判断维护于 [CATEGORY_SUMMARY.md](CATEGORY_SUMMARY.md)。
