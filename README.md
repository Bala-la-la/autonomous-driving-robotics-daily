# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-11-26

- [arXiv 独立报告](reports/2026-11-26/arxiv.md)
- [GitHub Trending 独立报告](reports/2026-11-26/github-trending.md)
- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-26

## 日期与证据口径

检索截至北京时间 2026-11-26 06:00。本期精选 **2026-11-24 UTC v1** 的 7 篇投稿；不是 11 月 26 日当日投稿，且未出现在 11 月 25 日报告。题目、作者、提交时间、方法和数值来自 arXiv 摘要/API；摘要无法完整核验机构归属，故不臆测。所有结果均为作者报告，尚未独立复现。

## 自动驾驶／移动自治

### 1. [Benchmarking Evidence Sufficiency in Vision-Language Models for Autonomous Driving](https://arxiv.org/abs/2611.32964)

- **作者／机构／提交：** Nhat Ha Nguyen、Sudipta Chowdhury、Lokesh Das 等；机构未完整披露；v1，2026-11-24 17:01 UTC。
- **问题：** 驾驶 VLM 即使答对或定位到相关目标，也可能没有足够视觉证据；现有评测把 grounding 和可回答性分开，掩盖“应当拒答”的风险。
- **创新与机制：** **DriveAnswer** 构造 20,151 个问题、七类推理任务的强／弱证据配对：保持场景事实和正确语义答案不变，只改变观测是否支持作答；联合计分回答、弱证据 abstain 与完整 grounding。
- **实验与关键结果：** 最强 zero-shot 的强证据准确率为 **67.31%**，但只有 **21.55%** 配对问题同时做到答对／拒答／完整定位；受控适配后 Gemma-4-12B 的联合能力为 **63.29%**，约为 zero-shot 的三倍。
- **关注价值：** 让驾驶模型的“不知道”成为可测接口，能直接服务遮挡、远距、低照等 ODD 下的降级策略设计。
- **局限／跟进：** benchmark 的配对操作未等同真实传感器失效；还应量化拒答如何接入规划器、误拒成本、跨相机/天气泛化及闭环安全收益。

### 2. [MemAnchorWorld: A Sparse World Model with Horizon-Conditioned Memory Retrieval for Autonomous Driving](https://arxiv.org/abs/2611.32745)

- **作者／机构／提交：** Xinyang Jia、Yuqi Zhang、Jiakai Wang 等；机构未完整披露；v1，2026-11-24 14:56 UTC。
- **问题：** 稀疏 4D occupancy 世界模型将历史压进递推 scene state，远期预测会累积几何和语义误差。
- **创新与机制：** **MemAnchorWorld** 按预测时域、信息有效年龄和语义兼容性做分层双路检索：query 级筛候选、point 级取 memory anchors；再用任务和时域共同门控的 residual adapter 分别修正语义、占据置信度和空间位置。
- **实验与关键结果：** Occ3D-nuScenes 的 1--3 秒平均 mIoU **13.55%**、IoU **22.84%**，作者称两项均为 SOTA。
- **关注价值：** 它把“何段历史实际影响哪个未来时刻”显式化，便于审计记忆过期、错检索和规划代价，而不只是扩大 latent state。
- **局限／跟进：** 需比较显式检索的车端延迟、记忆污染和地图变化下的错误回滚；占据 IoU 改善也不能替代碰撞与控制闭环验证。

### 3. [GeoVLDrive: Geometry-Grounded Vision-Language Reasoning for Autonomous Driving](https://arxiv.org/abs/2611.32510)

- **作者／机构／提交：** JiaHui Huang、Songyan Zhang、Hanbing Li 等；机构未完整披露；v1，2026-11-24 12:41 UTC。
- **问题：** 驾驶 VLA 从通用 VLM 继承语义知识，但理由通常未被 3D 结构与时间变化约束。
- **创新与机制：** 多层 3D foundation features 经 gated cross-attention 注入 VLM；结构化 latent CoT 分别监督未来几何、关键体运动与 meta-action，action expert 据此提议并以场景交互 score tokens 排序轨迹；同时发布 NAVSIM 3DQA。
- **实验与关键结果：** NAVSIM v1 **91.8 PDMS**、v2 **90.9 EPDMS**；NAVSIM 3DQA **89.2%**，较微调 Qwen3-VL-2B 高 **4.6** 点；LingoQA Lingo-Judge **68.6%**。
- **关注价值：** 将几何理由、候选动作和排序依据分离，是检查自然语言／视觉推理是否真正影响控制的较强中间接口。
- **局限／跟进：** 需防止 latent CoT 成为不可验证标签；应报告3D基础模型误差、雨雾／标定漂移、候选遗漏和端到端 p95 延迟。

## 机器人／具身智能

### 4. [OmniAct: One Policy, One Million Embodiments](https://arxiv.org/abs/2611.33158)

- **作者／机构／提交：** Xiang Fan、Yuheng Wang、Jiayuan Yan 等；机构未完整披露；v1，2026-11-24 18:59 UTC。
- **问题：** 共享动作空间能迁移任务知识，却难表达不同关节、自由度和连通性应如何改变操作策略。
- **创新与机制：** 用连接关节位置、运动轴和视觉观测的运动学图条件化策略；flow matching 为各节点预测相对关节运动。训练端程序化设计、物理筛选 **100 万** robot embodiments，并生成其仿真轨迹。
- **实验与关键结果：** 2,000 个 embodiment-scene held-out episode 成功率 **63.0%**，pi 0.5 为 **17.8%**、最强 baseline 为 **57.9%**；作者称在未见真机上接近 MolmoAct2 的两倍成功率。
- **关注价值：** 把跨本体泛化锚定到可检查的运动学条件，而不是仅靠统一 action token；适合评估硬件变化何时需要重新采集。
- **局限／跟进：** “百万形态”仍是合成分布；须披露真机数量、任务和统计区间，并测试标定偏差、关节限位、接触／动力学失配和安全停止。

### 5. [PyRUA-Dex: Learning Programmatic Policies for Dexterous Bimanual Manipulation with Coding Agents](https://arxiv.org/abs/2611.33144)

- **作者／机构／提交：** Feixiang Ruan、Guodong Lv、Kewei Zhang 等；机构未完整披露；v1，2026-11-24 18:56 UTC。
- **问题：** 灵巧双手的高质量示范稀缺：视频重定向不精确、遥操缺力反馈、外骨骼扩展困难。
- **创新与机制：** 多个 coding agents 并行探索 skill 与组合方式，distilling agent 将成功尝试压成任务库和一个程序策略；随后通过随机布局 refinement 改善鲁棒性与执行效率，无需示范训练。
- **实验与关键结果：** Bench2Dex **72.9**、完全随机化 DexJoCo **81.0%**，作者称均领先已训练策略；双 22-DoF 真机上可学钢琴、书法等，谱面到新曲最短约 **30 分钟**。
- **关注价值：** 将 agent 的代码探索产物变成可检查、可组合的控制程序，为示范稀缺任务提供不同于端到端模仿的迭代路径。
- **局限／跟进：** 成功程序的搜索成本、碰撞／超力失败、权限边界和真机试错预算仍未由摘要说明；应公开程序审查、stop rule 与跨任务复用失败率。

### 6. [iWAM: Efficient Action Prediction from World Models without Explicit Future Prediction](https://arxiv.org/abs/2611.33141)

- **作者／机构／提交：** Vansh Kapoor、Max Sobol Mark、Sreyas Venkataraman 等；机构未完整披露；v1，2026-11-24 18:56 UTC。
- **问题：** WAM 依赖视频模型生成未来来选动作，但逐帧高分辨率想象太慢，难用于实时控制。
- **创新与机制：** 利用 flow-matching 的可逆动力学把训练未来反演到噪声；学习 bidirectional flow map 摊销生成计算。推理时从 prior 采 latent，仅一次 video-backbone forward 的中间特征条件化策略，不显式渲染未来帧。
- **实验与关键结果：** 作者报告在仿真及真机上恢复 WAM 的泛化收益，同时显著降低推理开销；摘要未列统一绝对成功率、帧率或硬件配置。
- **关注价值：** 清楚区分“预测图像”和“保留动作判别信息”，是让世界模型进入快控制回路的实用方向。
- **局限／跟进：** 缺少摘要级成本与安全数字；应报告 p50/p95 时延、latent 不确定性、反事实失败例和相对显式预测的接触风险。

## 交叉方向：SLAM／长期空间智能

### 7. [GOLD-SLAM: Gaussian-splatting Omnidirectional LiDAR-Depth SLAM](https://arxiv.org/abs/2611.32335)

- **作者／机构／提交：** Weicong Zhang、Yuan Huang、Yu Zheng 等；机构未完整披露；v1，2026-11-24 10:20 UTC。
- **问题：** 全景相机近球面覆盖与 LiDAR 有限视场不匹配，使依赖 LiDAR 深度先验的全景 3DGS SLAM 出现无深度区域和增量浮点伪影。
- **创新与机制：** 在球面域跟踪／建图，用无 LiDAR 覆盖区的视觉特征改善位姿；**DAEP**（Depth-Aware Map Extension and Pruning）扩展新表面并清理浮点。作者采集 UAV **WHOLE** 数据集，覆盖弱几何、高动态、全景、低照等。
- **实验与关键结果：** 相较全景 baseline，平均 PSNR 提升 **5.56--9.10 dB**、Depth-L1 降 **71.9--83.9%**；Jetson Orin NX 16 GB 配置可在线运行，但牺牲重建质量。
- **关注价值：** 直接面向空中平台的全向观测与端侧资源，补充长期空间状态不仅要更密，也要说明观测盲区如何处理。
- **局限／跟进：** 渲染／Depth-L1 不能代替跨日重定位、回环和避障表现；应公布高动态遮挡、LiDAR失配、内存增长和嵌入式 p95 的退化曲线。

## 趋势总结

- **把“不确定／无证据”变成控制前的显式门。** DriveAnswer 的拒答能力、MemAnchorWorld 的时域检索、GeoVLDrive 的结构化几何理由都让模型说明依据何在；下一步必须验证这些门是否真实降低闭环风险。
- **具身规模化的焦点正从单一主干移向结构接口。** OmniAct 的运动学图、PyRUA-Dex 的程序技能库、iWAM 的一次前向动作特征分别连接形态、探索产物和计算预算；应共同报告试错伤害、尾延迟和可回滚性。
- **空间表征向全向、资源受限和可清理状态发展。** GOLD-SLAM 的覆盖补偿／地图修剪有助于 UAV 在线运行，但长期自治仍需跨时证据、内存上界和错误回环隔离。

# GitHub 开源趋势晨报｜2026-11-26

## 时间与证据口径

检索于北京时间 2026-11-26 06:00。GitHub 当日 Trending 页面可访问，但高位 Agent／Skills 项目与 11 月 21--25 日已报道项目高度重合；为避免重复，本期从 **GitHub Search API 的 2026-11-19 至 25 新建仓库**中选择 6 项，并用 Repository API 复核当前 stars、forks、语言、许可证、创建时间与描述。下表“增量依据”是**创建至查询时的累计 stars**，绝非官方 `stars today`；走红原因均是编辑推断。

| 项目 | 当前 stars | 增量依据 | 语言／类别 |
| --- | ---: | --- | --- |
| iamajmeena/neonclipping | 2,621 | 11-19 创建至查询 | Python／本地视频生产力 |
| os6/nospeaker | 1,876 | 11-22 创建至查询 | Swift／macOS 无障碍／硬件交互 |
| leanprover-community/riemann-hypothesis | 1,212 | 11-20 创建至查询 | Lean／形式化数学 |
| deterministic-machines/deslop-please | 1,049 | 11-22 创建至查询 | Rust／开发工具 |
| qianyiai/kurocat | 949 | 11-21 创建至查询 | TypeScript／桌面生产力 |
| danielwh2/sprite-stacking | 902 | 11-20 创建至查询 | HTML／Agent Skill／创作工具 |

## 精选项目

### 1. [iamajmeena/neonclipping](https://github.com/iamajmeena/neonclipping)

- **确认信息：** Repository API：**2,621** stars、165 forks，Python、AGPL-3.0，2026-11-19 创建。项目自述为本地开源 clipping engine：输入链接，借助音频、YouTube captions 和本地 LLM 生成带字幕的 9:16 短片。
- **用途：** 将长视频转换为竖版、带字幕的候选片段，适合媒体剪辑工作流原型。
- **走红原因（推断）／适合人群：** 把视频切片、字幕和本地模型放在一个可自托管流程中，正好回应创作团队对成本和素材隐私的需求；适合有明确来源授权的内容团队和开发者。
- **采用提醒：** 必须核对视频／字幕权利、平台条款、模型与 AGPL 网络分发义务；先测误剪、字幕幻觉、GPU 资源和对敏感素材的留存策略。

### 2. [os6/nospeaker](https://github.com/os6/nospeaker)

- **确认信息：** Repository API：**1,876** stars、98 forks，Swift、MIT，2026-11-22 创建。项目让 MacBook trackpad 的 haptic motor 发声。
- **用途：** 探索 macOS 触觉执行器作为音频／反馈输出的交互与无障碍实验。
- **走红原因（推断）／适合人群：** 将现有硬件转成出人意料的系统能力，且 demo 直观、代码体量小，容易吸引系统开发者与交互创作者。
- **采用提醒：** 这不是常规扬声器替代；需验证设备兼容性、功耗／发热、用户舒适性、系统权限和对关键输入设备的干扰。

### 3. [leanprover-community/riemann-hypothesis](https://github.com/leanprover-community/riemann-hypothesis)

- **确认信息：** Repository API：**1,212** stars、486 forks，Lean，许可证字段为 `NOASSERTION`，2026-11-20 创建。仓库自述为对 2026-11-20 Riemann Hypothesis 形式化工作的社区清理。
- **用途：** 用 Lean 组织可机器检查的数学定义、引理和证明工件，供形式化验证研究／社区协作。
- **走红原因（推断）／适合人群：** 重大数学事件与可复查 proof assistant 工件结合，显著降低旁观者进入和复核的门槛；适合 Lean 学习者、形式化数学研究者。
- **采用提醒：** star 与 PR 活跃度不构成定理正确性证明；应以指定 Lean／mathlib 版本完整编译，核实证明边界、依赖信任链与缺失许可证。

### 4. [deterministic-machines/deslop-please](https://github.com/deterministic-machines/deslop-please)

- **确认信息：** Repository API：**1,049** stars、49 forks，Rust、MIT，2026-11-22 创建；简介为“Bring (back) sanity to your code”。
- **用途：** 面向代码质量／可维护性问题的 Rust 工具项目；具体规则与执行模型应以仓库文档和版本化配置为准。
- **走红原因（推断）／适合人群：** 在 AI 辅助编码扩张后，开发者愈发需要将风格、复杂度和可读性拉回可执行规则；适合愿意在 CI 中试验严格检查的团队。
- **采用提醒：** 简短定位不足以说明误报率或自动修复安全性；先在只报告模式跑基线，固定版本，并审阅对生成代码、monorepo 和 CI 时延的影响。

### 5. [qianyiai/kurocat](https://github.com/qianyiai/kurocat)

- **确认信息：** Repository API：**949** stars、146 forks，TypeScript、MIT，2026-11-21 创建。Tauri v2 + Rust + MCP 的跨平台透明置顶打字宠物／OBS overlay，项目列出 Win、Mac、Linux、Android 等目标。
- **用途：** 为直播、桌面陪伴或输入可视化提供轻量的本地 overlay，也展示了 MCP 接入桌面小应用的模式。
- **走红原因（推断）／适合人群：** 可见的互动产物、跨平台交付与 AI 定制入口结合，契合独立开发与创作者对低门槛桌面体验的偏好。
- **采用提醒：** overlay、输入监测和 MCP 都可能触及键盘数据及系统权限；应核查输入过滤、秘密遮蔽、插件来源、网络访问和 OBS 场景隔离。

### 6. [danielwh2/sprite-stacking](https://github.com/danielwh2/sprite-stacking)

- **确认信息：** Repository API：**902** stars、73 forks，HTML、MIT，2026-11-20 创建。项目将四个像素画视图生成可旋转的伪 3D sprite，并声明支持 Claude Code、Codex、Cursor、OpenCode、Gemini CLI 与 Pi。
- **用途：** 把特定像素艺术制作规范封装为 Agent 可调用 Skill，用于游戏、交互页面和动画资产生成。
- **走红原因（推断）／适合人群：** 结果视觉化、输入约束明确，正是小而专的 Skill 易被复制、改造和嵌入创作流水线的类型；适合独立游戏开发者与前端创作者。
- **采用提醒：** 生成资产仍需检查原创性、许可证、风格一致性、透明通道／分辨率和无障碍替代文本；不要将一个 Skill 的演示效果外推为通用视觉生产能力。

## 技术趋势与社区偏好

- **“可交付的本地工件”比抽象 Agent 框架更醒目。** 本地剪辑、桌面 overlay、像素资产和代码约束都直接产出可见或可合入的结果；这也是近期 Trending 中 Skills／生产力项目反复出现的原因之一。
- **可验证性正在横跨不同层次。** Lean 形式化追求机器检查，代码工具追求可执行约束，创作工具则需要来源和构建可追溯；热度不能替代复现、权限或许可证审计。
- **近期样本不代表日榜增量。** 本期以创建至查询的累计 stars 作为确认增长证据，并刻意不把它写成 `stars today`；官方 Trending 的当日排序可证明可见度，但不能倒推出上述仓库的精确日增长。

## 证据链接

- [GitHub Search API：近 7 天创建且 stars 大于 20](https://api.github.com/search/repositories?q=created%3A%3E2026-11-18%20stars%3A%3E20&sort=stars&order=desc&per_page=50)：候选发现和创建窗口。
- [GitHub Trending 日榜](https://github.com/trending?since=daily)：当日可见度背景；本期未将其排序当作项目日增量。
- 每项当前 metadata 以对应项目的 [GitHub Repository API](https://docs.github.com/rest/repos/repos#get-a-repository) 复核为准。

## 内容标准与归档

每期 arXiv 按问题、创新、机制、实验、价值和局限选篇；GitHub 区分可核验元数据与编辑推断。历史文件位于 [`reports/`](reports/)，跨期判断见 [分类趋势总结](CATEGORY_SUMMARY.md)。
