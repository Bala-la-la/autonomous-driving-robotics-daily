# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-11-16

- [arXiv 独立报告](reports/2026-11-16/arxiv.md)
- [GitHub Trending 独立报告](reports/2026-11-16/github-trending.md)
- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-16

## 日期与证据口径

检索截至北京时间 2026-11-16 06:00。最新相关 v1 仍为 **2026-11-12 UTC**；周末无更晚常规批次。以下与 11 月 10—15 日归档去重后的七篇均为 **11 月 12 日投稿，不是 11 月 16 日新稿**；作者、时间、方法和数值来自 arXiv 元数据及摘要。

## 自动驾驶／移动自治

### 1. [Memory-Efficient Parallel Policy Learning for Collapse-Reactive Retreat via Hybrid Terrain Modeling](https://arxiv.org/abs/2611.16337)

- **作者／提交：** Yuki Kadokawa 等 5 位作者；v1，2026-11-12 05:58 UTC。
- **问题、创新与机制：** 大规模 RL 中共享塌陷地形会发生环境互扰，复制刚体地形则耗显存。Hybrid Terrain 对可塌区用虚拟接触力，State-Multiplexed Contact Model 共享几何却保存每环境独立塌陷状态，策略用本体感觉同时学习行走与失支撑撤退。
- **实验／价值／局限：** 相同显存下并行环境超过刚体块方案 **100 倍**、收敛超过 **50 倍**更快，并报告 sim-to-sim 与真机撤退。虚拟力仍可能漏掉土体延迟、滚动、埋陷和传感误差；需公开误触发、时延和不可撤回动作代价。

### 2. [MotionSkill: From Bipedal Motion Video to Control across Embodiments](https://arxiv.org/abs/2611.16346)

- **作者／提交：** Philip Niu、Xiaofeng Han、Sylvie Pan、Yang Wang；v1，2026-11-12 06:04 UTC。
- **问题、创新与机制：** 单目视频不直接给不同机器人可执行关节命令。方法恢复带时序参考，在公共坐标对齐根部／关键点，保留肢体方向并以 IK 满足长度、限位与闭链，再用残差策略按实测状态校正接触命令。
- **实验／价值／局限：** 十种双足机器人 MuJoCo 实验的原视频完成率 **98%**，上半身遮挡一秒为 **26%**。它分离了视频资产、形态映射和控制，但仍限仿真步行，须测真实尺度、跌倒恢复和跨硬件安全。

## 机器人／具身智能

### 3. [I See What You Want: Decoding Hierarchical Operator Intent from Visual Teleoperation History](https://arxiv.org/abs/2611.16419)

- **作者／提交：** Xiangyi Jia 等 6 位作者；v1，2026-11-12 07:30 UTC。
- **问题、创新与机制：** 以遥操视觉历史同时预测原子动作与高层任务。VI AMO 含 6,600 episode、13,653 个动作和 9,702 个任务标注，VIM 将预测任务交给 VLA 做可审计中途接管。
- **实验／价值／局限：** VIM 留出集动作／任务相似度 **0.825／0.821**，GPT-4o 为 0.563／0.470；真机接管据称减少人工遥操 **34.6%**。相似度不等于错误接管风险，需报告拒绝／澄清、时延和安全停止率。

### 4. [BlinkMimic: Training a Humanoid Motion Tracker in Minutes on a Single GPU](https://arxiv.org/abs/2611.16422)

- **作者／提交：** Fuyi Chen；v1，2026-11-12 07:31 UTC。
- **问题、创新与机制：** 将跟踪训练时间拆为每轮成本、拟合迭代与最后失败消除；采用进度衰减步长、部署失败重置和 GPU graph capture。
- **实验／价值／局限：** 模拟 Unitree G1 上，一张 RTX 4090 为 40 条 LAFAN1 clip 训练单一策略需 **3.4 分钟**。时间成为可复核指标，但尚未证明接触丰富真机技能或不同硬件下的尾部成本。

### 5. [Remember What Changes the Odds: Critic-Gated Event Memory for Long-Horizon Manipulation](https://arxiv.org/abs/2611.16386)

- **作者／提交：** Xuanzhuo Liu 等 4 位作者；v1，2026-11-12 06:55 UTC。
- **问题、创新与机制：** CGEM 不按事件外观、而按其对最终成功概率的改变选择记忆；critic 写入进展／失败记录，并在子任务完成后删除失败记录。
- **实验／价值／局限：** 十子任务诊断环境中成功率 **88.0%**，36 步窗口和运动学事件记忆均为 0.0%，删除失败记录后为 **1.7%**。需测 critic 误校准、真机时延和罕见事故召回。

## 交叉方向：空间状态／长期自治

### 6. [Spatial Foundry: A Multimodal Dataset for Spatial Intelligence](https://arxiv.org/abs/2611.17318)

- **作者／提交：** Ethan Lin、Yang Song；v1，2026-11-12 18:58 UTC。
- **问题、创新与机制：** 用共同坐标连接跨视角几何、对象与变化状态；**5,280** 个可编辑住宅场景提供户型图、RGB、米制深度、点云、网格、3D 框、轨迹和视频。
- **实验／价值／局限：** 摘要未给统一闭环排行榜；它有助区分记住外观和跟踪状态，但合成住宅不覆盖真实噪声、人群与杂乱，需定义状态变化泛化和地图污染基线。

### 7. [LiveGeo: Benchmarking Geographic Agents in Continuously Evolving Worlds](https://arxiv.org/abs/2611.17267)

- **作者／提交：** Pengcheng Zhou 等 9 位作者；v1，2026-11-12 18:45 UTC。
- **问题、创新与机制：** GeoWorld 让 agent 主动取证、验证旧证据是否过期、按更新状态修订计划，并保留可核验历史。
- **实验／价值／局限：** 作者称静态强表现不保证动态可靠，摘要无具体分数。它是车队／机器人外部世界状态压力测试原型，仍需验证更新延迟、错误源、工具不可用和安全关键校准。

## 趋势总结

塌陷恢复、遥操交接、成功概率驱动记忆与可更新空间状态，都让“状态变化后怎么办”成为一等对象。后续应将平均成功率与状态过期、错误接管、恢复延迟、模拟—真实偏移及不可逆动作代价一起报告。

# GitHub 开源趋势晨报｜2026-11-16

## 时间与证据口径

排名与 `+N/日` 来自第三方镜像的 **2026-11-15 UTC** 日榜（采集于 21:07 UTC），`gained` 并非本次总 star 相减。当前 metadata 经 GitHub Repository API 复核；镜像非 GitHub 官方，走红原因和趋势均为编辑推断。排除了 11 月 14—15 日已选项目。

### 1. [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills)

- **数据：** **9,244 stars**；第 3、**+248/日**；TypeScript；Apache-2.0。[API](https://api.github.com/repos/google-labs-code/stitch-skills)／[日榜](https://githubtrending.today/api/archive/2026-11-15.json)。
- **用途／原因／适合：** Stitch MCP 的开放标准 Agent Skills 库；能力正在成为可版本化、跨 agent 分发的工作流资产。适合设计生成 agent 平台团队；先审计网络／文件写入、服务条款、版本锁定和产物版权。

### 2. [ggml-org/ggml](https://github.com/ggml-org/ggml)

- **数据：** **15,883 stars**；第 8、**+53/日**；C++；MIT。[API](https://api.github.com/repos/ggml-org/ggml)／[日榜](https://githubtrending.today/api/archive/2026-11-15.json)。
- **用途／原因／适合：** 机器学习 tensor library，显示社区持续关注本地／跨硬件推理底层。适合系统工程师；以目标模型、量化、后端、吞吐、显存、数值一致性和更新策略实测。

### 3. [NVIDIA/SkillEvaluator](https://github.com/NVIDIA/SkillEvaluator)

- **数据：** **1,598 stars**；第 12、**+205/日**；Python；Apache-2.0。[API](https://api.github.com/repos/NVIDIA/SkillEvaluator)／[日榜](https://githubtrending.today/api/archive/2026-11-15.json)。
- **用途／原因／适合：** Skill 质量门、语义重叠、合成评测和在线行为评估；Skill 目录增长后，真实增益测量成为独立需求。适合内部 catalog 团队；隔离工具权限并审计 evaluator／合成数据偏差。

### 4. [elementalsouls/Claude-BugHunter](https://github.com/elementalsouls/Claude-BugHunter)

- **数据：** **6,323 stars**；第 9、**+221/日**；Python；MIT。[API](https://api.github.com/repos/elementalsouls/Claude-BugHunter)／[日榜](https://githubtrending.today/api/archive/2026-11-15.json)。
- **用途／原因／适合：** 82 项 Skills、15 个命令的 bug hunting／红队 bundle，显示公开漏洞模式被转成审计工作流。仅适合明确授权的安全人员和隔离环境；审计命令、依赖、凭据、日志与披露流程。

### 5. [GoogleChrome/modern-web-guidance-src](https://github.com/GoogleChrome/modern-web-guidance-src)

- **数据：** **7,031 stars**；第 10、**+1,220/日**；TypeScript；Apache-2.0。[API](https://api.github.com/repos/GoogleChrome/modern-web-guidance-src)／[日榜](https://githubtrending.today/api/archive/2026-11-15.json)。
- **用途／原因／适合：** 为 coding agent 保持 Web 最佳实践更新的 guidance 源码；工程规则源码化更可审查、更新和复用。适合前端平台团队；按自身浏览器、框架与可访问性要求验收。

## 技术趋势与社区偏好

能力资产（Stitch）、质量门（SkillEvaluator）、执行底座（ggml）、授权安全工作流（BugHunter）和工程规范（modern-web-guidance）形成完整链条。热度表明 Agent 生态正转向可安装、可评估、可约束的运行面；采用前仍须审计写权限、供应链、数据留存、许可证与人工审批。

## 内容标准与归档

每期 arXiv 报告按方向说明问题、创新、机制、实验、价值和局限；GitHub 报告区分可核验元数据与编辑推断。历史文件位于 [`reports/`](reports/)，跨期判断见 [分类趋势总结](CATEGORY_SUMMARY.md)。
