# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪最新 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-11-13

- [arXiv 独立报告](reports/2026-11-13/arxiv.md)

- [GitHub Trending 独立报告](reports/2026-11-13/github-trending.md)

- [分类趋势总结](CATEGORY_SUMMARY.md)

## 内容标准

每期 arXiv 报告按方向精选并说明问题、创新、机制、实验、价值和局限；GitHub 报告区分可核验元数据与编辑推断。归档位于 [`reports/`](reports/)。

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-14

## 日期与证据口径

检索截至北京时间 2026-11-14 06:00。arXiv `cs.RO`、`cs.AI` 等检索中最新相关 v1 批次为 **2026-11-12 UTC**；本期回溯该批并与 11 月 10—13 日归档去重，以下七篇均为 **11 月 12 日新投稿，并非 11 月 14 日新稿**。作者、时间、方法与数值均据 arXiv 元数据和摘要；没有可可靠核验的机构信息时不臆测，摘要的实验描述不构成真实世界安全保证。

## 自动驾驶／移动自治

### 1. [ProtoVis-Nav: Prototypical Visual Imagination for Visual-Spatial Aligned UAV Navigation](https://arxiv.org/abs/2611.17330)

- **作者／机构／提交：** Guangyuan Sui、Yunzhong Hou、Chi Harold Liu；arXiv 元数据未列可核验机构；v1，2026-11-12 18:59 UTC。
- **问题与创新：** 无人机语言导航中，三维运动的小偏差会转为碰撞或航点偏差；现有方法往往直接由语言—图像预测 waypoint，缺少对执行后局部视觉的检验。ProtoVis-Nav 先“想象”目标位置的局部视觉表征，再据此输出动作。
- **机制／结构：** 模型预测一组视觉 feature prototype，以线性组合估计下一意图位置的目标区域特征；这些预测 prototype 作为动作生成上下文，使视觉条件和 waypoint 对齐。
- **实验与关键结果：** 摘要称大量实验相对基线有显著提升，但未提供可由摘要复核的成功率、碰撞率、延迟或场景数。
- **关注价值：** 把语言导航中的未来状态从隐式 token 变为可检查的视觉中间目标，适合与安全过滤、重规划连接。
- **局限／跟进：** prototype 是否在光照、动态障碍、深度误差下仍可靠尚未量化；需报告真实飞行失败类型、计算预算和闭环碰撞率。

### 2. [UAV-Flow++: A Unified Suite for Benchmarking and Learning Language-Guided UAV Flight](https://arxiv.org/abs/2611.17163)

- **作者／机构／提交：** Donglin Yang 等 9 位作者；arXiv 元数据未列可核验机构；v1，2026-11-12 17:39 UTC。
- **问题与创新：** 语言引导飞行多偏向长距离路径，忽略“绕过物体、贴近某物”等短程连续动作。论文提出 Flying-on-a-Word（Flow），将简短指令、第一视角与动力学状态映射为连续飞行动作。
- **机制／结构：** UAV-Flow 含 30,692 条真实专家轨迹、八类动作，以及含 10,109 条轨迹和任务验收条件的仿真环境；FlowVLA 先混合真机/仿真模仿预训练，再用根据 group reward 分布强化高回报序列的 Tail-Aware GRPO 后训练。
- **实验与关键结果：** 在 273 个留出仿真 episode，预训练 FlowVLA 平均成功率 75.58%，较最强基线高 6.72 个百分点；TGRPO 后为 93.16%。作者还报告室内外实体机可执行物体相对指令。
- **关注价值：** 数据、连续控制、验收条件和真机演示放在同一套基准，补足 VLM/VLA 只验证路线语义、不验证近距离飞行动作的缺口。
- **局限／跟进：** 273 个 episode 与八类动作的覆盖仍有限；需独立测量 sim-to-real 退化、风扰、时延、视觉遮挡和尾部碰撞风险。

## 机器人／具身智能

### 3. [HEIR: Harness Egocentric Intent for Human-Robot Interactions](https://arxiv.org/abs/2611.17238)

- **作者／机构／提交：** Yichi Zhang 等 14 位作者；arXiv 元数据未列可核验机构；v1，2026-11-12 18:25 UTC。
- **问题与创新：** 服务机器人不仅要听懂话，还要结合人的视线和第一视角意图，把连续请求分解为导航—操作子任务。HEIR 为此提供保留跨 episode 连续性的自然家庭交互资源。
- **机制／结构：** 每段数据对齐人类语音、实测 gaze、第一视角视频、机器人观测和遥操作 nav-manip 轨迹，并附人工标注，用于意图 grounding、规划和完成度研究。
- **实验与关键结果：** 作者进行了离线的人本上下文消融和真机任务完成测试；摘要未披露数据规模、各任务成功率或统计显著性。
- **关注价值：** 将“用户究竟指向什么、希望机器人接着做什么”保留为与动作同等重要的训练信号，适合研究长任务的澄清与恢复。
- **局限／跟进：** 家庭采集的参与者、对象及隐私边界会决定泛化性；需公开跨用户/跨房屋划分、标注一致性、失败恢复与安全接近策略。

### 4. [XBot-Omni: An Omni-Modal Model for Embodied Understanding and Interaction](https://arxiv.org/abs/2611.17160)

- **作者／机构／提交：** Kerui Gu 等 13 位作者；arXiv 元数据未列可核验机构；v1，2026-11-12 17:38 UTC。
- **问题与创新：** 具身交互不止理解多模态输入，还要以语言、语音、身体和面部动作表达意图。XBot-Omni 将 Omni 模型扩展为 Thinker—Talker—Actor，其中 Actor 是专门的流式具身输出部件。
- **机制／结构：** Thinker 处理文本、图像、音频和视频，Talker 与 Actor 直接使用其原生表征，生成语音和协调肢体表达，避免分段转换造成信息损失。
- **实验与关键结果：** 作者报告在七个通用和机器人中心视频基准上有较强理解能力，并验证协调动作／语音生成；摘要未给出分数、主观评分协议或端到端延迟。
- **关注价值：** 把“能解释”扩展到“能用非语言行为传达状态”，对协作、陪护与远程操作界面有价值。
- **局限／跟进：** 自然动作不等于安全动作；需要独立评估接触约束、动作可执行性、延迟、文化/用户偏好和故障时的可预测降级。

### 5. [FORGE: Force-Aware Multi-Granularity Control for Efficient Humanoid Loco-Manipulation](https://arxiv.org/abs/2611.17142)

- **作者／机构／提交：** Liangjun Xing 等 11 位作者；arXiv 元数据未列可核验机构；v1，2026-11-12 17:30 UTC。
- **问题与创新：** 人形移动操作常靠昂贵全身遥操演示和腕部力传感器。FORGE 以速度、落脚、腕位姿到可选力条件的粗到细命令控制，训练不需要全身人体轨迹或关节参考。
- **机制／结构：** 部署只输入骨盆相对的稀疏双腕姿态、粗运动命令和可选期望腕载荷；动量观测器加学习校正由本体感觉与低层 PD 力矩重建低频腕等效力，虚拟目标环据此修正腕目标，冻结 locomotion prior 以残差稳定全身。
- **实验与关键结果：** 摘要覆盖统一控制稳定性、任务空间跟踪、等效力估计、推箱持续接触和跨载荷 squat-and-lift diffusion-policy 执行，但未给出统一成功率或力误差数值。
- **关注价值：** 在减少演示与传感器负担的同时，显式处理力，提供面向现有 humanoid 硬件的工程折中。
- **局限／跟进：** 等效力不是直接六维腕力；需在动态接触、滑移、多接触、不同手臂刚度和长期安全恢复上对比真实 F/T 传感器。

### 6. [SALA: Semantically Aligned Latent Actions Enable Dual-Axis Scaling of Embodied Foundation Models](https://arxiv.org/abs/2611.17110)

- **作者／机构／提交：** Jiachun Jin、Zetong Zhou、Haonan Wang、Xiao Yang、Jun Zhu、Zhijie Deng；arXiv 元数据未列可核验机构；v1，2026-11-12 17:04 UTC。
- **问题与创新：** 从人类第一视角视频学 latent action 时，重建训练易按外观聚类，难以对齐人和机器人的同义动作。SALA 不需配对数据，以两端 clip 的语言描述建立语义对应。
- **机制／结构：** 将未配对人类／机器人片段的语言相似度转成软邻域结构，把人类 latent action 拉向语义相关机器人 latent；机器人动作重建保持控制可落地，共享动作空间同时监督人类视频预训练和机器人任务后训练。
- **实验与关键结果：** 摘要称增加通用人类视频会持续降低下游机器人动作预测误差，增加任务相关人类视频会明显提高真机成功率，但未披露规模—收益曲线和绝对成功率。
- **关注价值：** 给“人类视频能否扩展机器人数据”一个更明确的对齐接口，避免只扩大视频量而让动作语义漂移。
- **局限／跟进：** 语言相似不保证动力学或接触相似；应检验跨形态、遮挡、错误字幕、罕见动作及人—机动作可达性失配。

## 交叉方向：SLAM／长期自治

### 7. [CT-SGAL-LIO: Causal Continuous Time Refinement of Discrete LiDAR Inertial Odometry](https://arxiv.org/abs/2611.16918)

- **作者／机构／提交：** Nam Tran、Thu Tran、Toan Nguyen、William J. Beksi、Tuan Dang；arXiv 元数据未列可核验机构；v1，2026-11-12 15:07 UTC。
- **问题与创新：** 离散 LiDAR—IMU 估计虽然全局准，传播／校正交替仍会让短时姿态跳动；从原始传感器重建连续轨迹又增加优化延迟。CT-SGAL-LIO 在不改估计器的前提下，对其 SGal(3) posterior 做因果连续时间细化。
- **机制／结构：** 在有限近期窗口拟合三次轨迹，以固定小滞后在已观测时间区间内插值而非外推，从而保持因果和原估计器的全局性质。
- **实验与关键结果：** GRAND-TOUR、MCD、GEODE 共 17 序列中短时误差改善；GRAND-TOUR RTE 最高改善 70%，GEODE 七条序列均改善 9.9–51.1%；19.5 分钟 R-Campus 运行的 posterior jump 降 85.4%，起终间隙仅变化 4.7 mm。
- **关注价值：** 将下游控制真正感受到的短时平滑性，与传统全局漂移指标分开优化，适合高速运动和传感器融合管线。
- **局限／跟进：** 固定滞后会增加控制延迟，三次拟合在异常观测下的鲁棒性未明；应报告 CPU/GPU 开销、快速旋转失效情况及对闭环控制的实际收益。

## 趋势总结

本批工作的共同线索是把具身系统的“未来”和“人”写成显式接口：UAV 通过可想象的目标视觉和可验收的连续动作减少未来失配；HEIR、XBot-Omni、FORGE 和 SALA 分别把人的意图、表达、接触力和跨形态动作语义拆开建模；CT-SGAL-LIO 则把短时连续性作为定位输出的独立质量。下一步应优先关注这些中间接口在真机时延、传感噪声、跨用户／跨形态和恢复场景中是否仍能改善闭环，而不是只报告离线理解或平均成功率。


# GitHub 开源趋势晨报｜2026-11-14

## 时间与证据口径

检索于北京时间 2026-11-14 06:00。排名与 `+N/日` 来自第三方镜像保存的 **2026-11-13 UTC GitHub Trending 日榜**（`collectedAt` 为 2026-11-13 21:07 UTC）；这是镜像记录的 `gained`，不是本次总 star 相减。当前 star、主语言、许可证和自述由 GitHub Repository API 于本次运行复核。镜像不是 GitHub 官方服务；用途为仓库自述可确认信息，走红原因和趋势结论均是编辑推断，star 不证明质量、安全或生产采用。

## 精选项目

### 1. [alibaba/open-code-review](https://github.com/alibaba/open-code-review)

- **数据：** API 当前 **50,536 stars**；日榜第 1、**+206/日**；Go；Apache-2.0。证据：[Repository API](https://api.github.com/repos/alibaba/open-code-review)、[日榜快照](https://githubtrending.today/api/archive/2026-11-13.json)。
- **确认用途：** 自述为混合式代码审查工具：确定性流水线结合 LLM Agent，提供逐行评论和 NPE、线程安全、XSS、SQL 注入等多语言规则。
- **走红原因（推断）：** Agent 写代码后，团队需要把可预测静态规则与模型判断放进同一个审阅环，而不是只让模型给自然语言建议。
- **适合人群：** 希望把 AI 辅助审阅接入已有 CI 的工程／安全团队；应先用只读、隔离 PR 验证误报、数据出境和自动修复审批。

### 2. [GoogleChrome/modern-web-guidance-src](https://github.com/GoogleChrome/modern-web-guidance-src)

- **数据：** API 当前 **4,705 stars**；日榜第 2、**+1,875/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/GoogleChrome/modern-web-guidance-src)、[日榜快照](https://githubtrending.today/api/archive/2026-11-13.json)。
- **确认用途：** 为 coding agent 保持最新 Web 最佳实践的指导源码。
- **走红原因（推断）：** 前端团队更倾向把规范固化为可版本化、可审查的 Agent 上下文，替代一次性提示词和口头规则。
- **适合人群：** 维护设计／前端工程约束的团队；应按项目技术栈审阅规则版本、浏览器兼容性和许可证。

### 3. [openai/codex-security](https://github.com/openai/codex-security)

- **数据：** API 当前 **13,075 stars**；日榜第 3、**+754/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/openai/codex-security)、[日榜快照](https://githubtrending.today/api/archive/2026-11-13.json)。
- **确认用途：** 用于发现、验证与修复安全漏洞的 Codex Security CLI 和 TypeScript SDK。
- **走红原因（推断）：** 当代码生成进入日常交付，扫描—验证—修复的可追踪闭环成为接入 Agent 的必要安全配套。
- **适合人群：** 有代码审阅和最小权限环境的工程／安全团队；先在隔离仓库验证误报、依赖、数据边界和修复的人工批准点。

### 4. [backnotprop/plannotator](https://github.com/backnotprop/plannotator)

- **数据：** API 当前 **10,403 stars**；日榜第 6、**+100/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/backnotprop/plannotator)、[日榜快照](https://githubtrending.today/api/archive/2026-11-13.json)。
- **确认用途：** 面向 Agent 工作的协作空间，可塑形／决策／规划／批注／审阅代码，并把反馈交回 Agent。
- **走红原因（推断）：** 多人协作的瓶颈从“能否运行 Agent”转到能否在执行前后留下可讨论的计划和反馈工件。
- **适合人群：** 需要团队审阅 Agent 改动的产品、设计与工程团队；应明确工作区、反馈、代码上下文和第三方凭据的访问范围。

### 5. [ChromeDevTools/chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp)

- **数据：** API 当前 **55,418 stars**；日榜第 12、**+145/日**；TypeScript；Apache-2.0。证据：[Repository API](https://api.github.com/repos/ChromeDevTools/chrome-devtools-mcp)、[日榜快照](https://githubtrending.today/api/archive/2026-11-13.json)。
- **确认用途：** 为 coding agent 提供 Chrome DevTools 能力。
- **走红原因（推断）：** 当 Agent 编写 Web 代码时，浏览器中的网络、DOM 和性能证据比静态代码上下文更接近真实故障现场。
- **适合人群：** 需要让 Agent 协助调试前端的开发者；需用专用浏览器 profile，避免暴露登录态、生产数据和可执行下载。

### 6. [louislam/uptime-kuma](https://github.com/louislam/uptime-kuma)

- **数据：** API 当前 **93,811 stars**；日榜第 7、**+61/日**；JavaScript；MIT。证据：[Repository API](https://api.github.com/repos/louislam/uptime-kuma)、[日榜快照](https://githubtrending.today/api/archive/2026-11-13.json)。
- **确认用途：** 自托管监控工具。
- **走红原因（推断）：** Agent 与服务自动化增加后，轻量、可自托管的健康检查仍是最低成本的可观测性入口。
- **适合人群：** 想快速监控内部服务的个人和小团队；应保护通知凭据、监控端点和管理界面，并建立真正的告警响应流程。

### 7. [block/buzz](https://github.com/block/buzz)

- **数据：** API 当前 **37,277 stars**；日榜第 8、**+95/日**；Rust；Apache-2.0。证据：[Repository API](https://api.github.com/repos/block/buzz)、[日榜快照](https://githubtrending.today/api/archive/2026-11-13.json)。
- **确认用途：** 自述为 hive mind communication platform。
- **走红原因（推断）：** 人—人、人—Agent 与多 Agent 的状态协同需要可共享的通信层；“群体协作”类原语正在成为工具生态的独立层。
- **适合人群：** 探索协作式工作流的基础设施团队；上线前应核验身份、消息保留、权限模型和运行成熟度，不能仅按热门度采用。

### 8. [tailscale/tailcat](https://github.com/tailscale/tailcat)

- **数据：** API 当前 **9,405 stars**；日榜第 10、**+324/日**；Go；BSD-3-Clause。证据：[Repository API](https://api.github.com/repos/tailscale/tailcat)、[日榜快照](https://githubtrending.today/api/archive/2026-11-13.json)。
- **确认用途：** 类似 netcat、但通过 Tailscale data plane 而非其 control plane 的工具。
- **走红原因（推断）：** 开发与 Agent 自动化跨机器执行时，简单且可组合的连通性工具仍有吸引力，尤其是已有私有网络的团队。
- **适合人群：** 熟悉网络边界的运维与开发者；需明确 ACL、监听范围、审计和传输数据分类，避免把临时连通性当作访问控制。

## 技术趋势与社区偏好

11 月 13 日日榜显示出一条比“单体 Agent”更完整的工程链：guidance 固化规范，Plannotator 让计划与反馈可协作，DevTools MCP 扩展现场证据，open-code-review 与 Codex Security 建立审查／验证，Uptime Kuma 与 Tailcat 提供运行监测和网络底座。社区热度也覆盖协作通信，但这些工具的真实采用门槛仍是权限、凭据、数据留存、供应链和人工审批，而非 star。

## 证据链接

- [GitHub Trending 2026-11-13 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-13.json)：排名、快照总 star 与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：镜像采集和统计口径。
- 各项目当前元数据以上述 Repository API 为准；走红原因均为编辑推断。
