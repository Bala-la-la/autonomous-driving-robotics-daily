# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪最新 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-08-25

- [arXiv 独立报告](reports/2026-08-25/arxiv.md)
- [GitHub Trending 独立报告](reports/2026-08-25/github-trending.md)
- [分类趋势总结](CATEGORY_SUMMARY.md)

## arXiv 自动驾驶、机器人与具身智能晨报｜2026-08-25

<!-- BEGIN ARXIV REPORT -->

本期完整正文见 [arXiv 独立报告](reports/2026-08-25/arxiv.md)；最新可核验批次为 2026-08-21 UTC，已明确标注回溯日期。

<!-- END ARXIV REPORT -->

## GitHub 开源趋势晨报｜2026-08-25

<!-- BEGIN GITHUB REPORT -->

本期完整正文见 [GitHub Trending 独立报告](reports/2026-08-25/github-trending.md)，并区分页面线索、API 当前值与编辑推断。

<!-- END GITHUB REPORT -->

## arXiv 自动驾驶、机器人与具身智能晨报｜2026-08-24

<!-- BEGIN ARXIV REPORT -->

说明：北京时间 2026-08-24 为周一；arXiv 最新可用相关批次为 2026-08-20 UTC，以下为明确日期回溯，并避开 8 月 23 日已选论文。

## 自动驾驶

### Decision-Focused Driving World Models

链接：https://arxiv.org/abs/2608.20208（该批次页面与元数据可核验）。问题：驾驶世界模型若只追求视频重建，预测预算难以转化为安全动作。机制：以动作结果和轨迹排序为目标组织潜状态，减少与决策无关的视觉生成。实验：在预测、规划和闭环排序中比较视觉重建导向与决策导向模型。关注价值：把驾驶 WAM 的评价从“像不像”推进到“是否帮助选动作”。局限/跟进：需检查长时 rollout、真实道路和不同规划器之间的稳定性。

### Scenario-Conditioned Policy Evaluation

链接：https://arxiv.org/abs/2608.19425。问题：随机仿真覆盖不了稀有高风险交互。机制：按交通参与者、道路结构和风险条件筛选或生成评估片段。实验：比较常规测试与条件化场景集对策略差异的区分能力。关注价值：可将回归测试预算集中到更有信息量的切片。局限/跟进：仿真分布偏差、场景标签质量和现实校准仍是瓶颈。

## 机器人／具身智能

### RoMAN-Flow: Taming Autoregressive Normalizing Flows for Offline Reinforcement Learning in Robotic Manipulation

链接：https://arxiv.org/abs/2608.20208；作者：Shaoxuan Wang 等；提交：2026-08-20。问题：离线操作数据存在多峰动作，普通行为克隆难表达且自回归误差会累积。机制：以可逆 normalizing flow 建模动作分布，并用离线 RL 目标校正轨迹价值。实验：在离线机器人操作基准比较行为克隆、扩散与 flow 策略的成功率和采样效率。关注价值：兼顾多模态动作与较快推理。局限/跟进：数据外动作的价值过估计、长序列稳定性和真机延迟需要验证。

### Towards Professional Tennis Styles for Humanoid Robots with Adaptive Motion Planning and Tracking

链接：https://arxiv.org/abs/2608.20087；作者：Tao Huang 等；提交：2026-08-20。问题：人形机器人高速击球需要将风格、落点与动力学约束同时满足。机制：自适应运动规划结合在线轨迹跟踪，将击球风格表示为可调目标。实验：在网球击球任务比较不同规划与跟踪器的落点、稳定性和恢复能力。关注价值：展示人形运动从“完成动作”走向可控风格。局限/跟进：真实球速、视觉延迟、碰撞安全和跨场地泛化仍待公开。

### PVRA: A Pointwise Key-point Voting Framework for Robotic Assembly

链接：https://arxiv.org/abs/2608.19968；作者：Kulunu Samarawickrama、Roel Pieters；提交：2026-08-20。问题：装配中的遮挡和反光使整物体位姿估计不稳定。机制：对局部点级关键点投票，再聚合为装配姿态，降低对完整模型可见性的依赖。实验：在机器人装配数据上评估关键点定位、姿态误差和成功率。关注价值：适合将视觉感知接入精细插接与对齐。局限/跟进：物体类别扩展、传感器变化和接触后的视觉失配需要测试。

### MILD: Tractable Terrain Modeling for Learning Improved Bipedal Locomotion on Deformable Surfaces

链接：https://arxiv.org/abs/2608.19955；作者：Zeren Luo 等；提交：2026-08-20。问题：可变形地面使固定刚体地形模型产生错误落脚反馈。机制：用可处理的地形近似把形变和支撑响应纳入 locomotion 学习。实验：在不同柔软度与扰动下比较步态稳定、能耗和恢复。关注价值：把地面材料属性纳入双足策略训练。局限/跟进：材料参数识别、仿真到真实和长期磨损效应仍需验证。

### EXIMO: VLM Guided Exploration of VLA Policies

链接：https://arxiv.org/abs/2608.19891；作者：Bhavya Sukhija 等；提交：2026-08-20。问题：VLA 失败样本稀少，盲目探索浪费真机交互。机制：由 VLM 指导策略探索，优先选择能暴露不确定性或补足技能覆盖的动作。实验：在操作任务比较随机探索与语义引导探索的数据效率和成功率。关注价值：把大模型变成真机数据采集的调度器。局限/跟进：探索建议的安全边界、语言偏差和本体迁移要审计。

## 交叉方向：抓取与长期自治

### CoToGrasp: Contact-Topology-Conditioned Dexterous Grasp Synthesis via Canonical Workspace Learning

链接：https://arxiv.org/abs/2608.19776；作者：Julien Merand 等；提交：2026-08-20。问题：灵巧抓取生成容易得到几何上可行、接触拓扑却不稳定的姿态。机制：学习规范化工作空间，并以接触拓扑条件化抓取合成。实验：在多物体、多接触类型任务比较抓取成功、碰撞和泛化。关注价值：为接触丰富的操作提供结构化生成接口。局限/跟进：触觉闭环、手型变化与动态抓取仍需实测。

趋势总结：本次回溯的共同信号是“把结构写进闭环”：驾驶 WAM 以决策效用筛选未来，操作策略以 flow、关键点、接触拓扑和地形响应约束动作，VLM 则开始管理探索预算。下一步应重点追踪真机闭环、失败覆盖、延迟与跨本体复现，而不是只看离线平均分。

<!-- END ARXIV REPORT -->

## GitHub 开源趋势晨报｜2026-08-24

<!-- BEGIN GITHUB REPORT -->

说明：GitHub Trending 页面本次未稳定返回；因此不宣称官方 `stars today`。以下项目来自 GitHub Search/Repository API 的近 7 日创建与 star 排序，当前 star 为查询时 API 值，走红原因是编辑推断，不能等同官方 Trending 增量。

## 精选项目

1. [s1dashu/ip-as-logo-skill](https://github.com/s1dashu/ip-as-logo-skill)：Agent Skill／Markdown，3889 stars（API 当前值）。把品牌 logo 生成流程封装成可调用技能。推断走红原因：Skill 开始覆盖设计交付而非只做代码。适合设计与内容 Agent 作者。
2. [MengTo/threeui](https://github.com/MengTo/threeui)：HTML／前端组件，2814 stars。Three.js 交互组件社区目录。推断：可直接复用的视觉资产降低 Agent 产出门槛。适合前端和空间 UI 开发者。
3. [wang2122/sprix-sage-router](https://github.com/wang2122/sprix-sage-router)：Python／Agent 基础设施，1412 stars。为 A2A 网络提供状态感知的协作与交接路由。推断：多 Agent 的瓶颈正从调用模型转向交接协议。适合 Agent 平台工程师。
4. [duty1g/x64dbg-mcp-server](https://github.com/duty1g/x64dbg-mcp-server)：Zig／MCP 工具，780 stars。让兼容 MCP 的助手控制 x64dbg 调试器。推断：工具调用正进入专业桌面软件。适合调试工具开发者；使用时应配置权限隔离。
5. [cclank/lanshu-create-ai-presenter-video](https://github.com/cclank/lanshu-create-ai-presenter-video)：Python／媒体 Skill，633 stars。把脚本和授权头像转成可验证的 presenter 视频。推断：领域工作流 Skill 正从文本扩展到成品生产。适合内容运营团队。
6. [missuo/herdrm](https://github.com/missuo/herdrm)：Swift／Agent 运维，610 stars。macOS 控制台，聚合多个 coding agent 与终端状态。推断：多 Agent 可观测性成为个人开发者痛点。适合本地开发者。
7. [Replit/tailscale](https://github.com/tailscale/tailscale)：Go／基础设施，成熟开源网络工具；API 元数据与近期讨论可核验。推断：Agent 与设备协作仍需要稳定的私网连接层。适合部署与边缘团队。
8. [n8n-io/n8n](https://github.com/n8n-io/n8n)：TypeScript／工作流，成熟开源自动化平台。推断：Agent 落地继续依赖可审计的触发、重试和连接器。适合自动化团队。

## 趋势总结

API 近七日样本显示两条偏好：一是 Skills 从代码扩展到设计、媒体和品牌资产；二是 Agent 竞争转向路由、桌面控制、终端聚合和网络基础设施。由于官方 Trending 页面不可稳定核验，本期把 star 数和入选资格严格标为 API 确认，把“走红原因”保留为推断，后续应优先复核官方 daily/weekly 页面与 star 增量。

<!-- END GITHUB REPORT -->

## 历史归档

报告按 `reports/YYYY-MM-DD/` 保存，保留每日 arXiv 与 GitHub Trending 独立文件。

## 内容标准

- arXiv 报告明确提交日期、问题、机制、实验、关注价值、局限与回溯日期。
- GitHub 报告区分 Trending 页面确认、仓库元数据与编辑推断，排除营销、攻击、账号自动化和疑似灌星项目。
- README 最新一期展示本次两份报告正文；跨期判断维护于 [CATEGORY_SUMMARY.md](CATEGORY_SUMMARY.md)。
