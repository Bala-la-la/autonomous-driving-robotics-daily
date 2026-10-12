# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪最新 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-10-13

- [arXiv 独立报告](reports/2026-10-13/arxiv.md)

- [GitHub Trending 独立报告](reports/2026-10-13/github-trending.md)

- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-13

## 日期与证据口径

北京时间 2026-10-13 检索 [arXiv API](https://export.arxiv.org/api/query?search_query=cat%3Acs.RO%20OR%20cat%3Acs.AI%20OR%20cat%3Acs.CV&start=0&max_results=100&sortBy=submittedDate&sortOrder=descending)。周末后可取得的最新相关常规批次为 **2026-10-09 UTC**；以下 7 篇均为该日新提交，明确作为回溯，**不是 10 月 13 日新稿**。实验数值均为作者报告、未经独立复现；“关注价值／局限”是编辑判断。

## 自动驾驶、规划与长期自治

### 1. SimVTA: Simulation-Grounded Video-Trajectory Alignment for Driving World Action Models

- **论文／作者／时间**：[arXiv:2610.13781](https://arxiv.org/abs/2610.13781)；Changhui Jing、Haochen Tian、Hongchen Li、Hao Zhao 等；v1：2026-10-09 16:01 UTC。
- **问题**：驾驶世界动作模型在 RL 后训练时会探索日志中不存在的候选轨迹，因而没有与这些轨迹匹配的未来视频监督。
- **创新与机制**：SimVTA 在 3D Gaussian Splatting 重建的真实场景中，以 World Engine 等模拟器渲染高奖励候选轨迹的未来视频；按预测误差优先分配有限渲染预算，并以 GRPO 轨迹优化和 flow-matching 视频损失共同更新表征。
- **实验与关键结果**：作者报告 NAVSIM v1 PDMS 从 **86.2 升至 91.3（+5.1）**，NAVSIM v2 为 **88.2 EPDMS**，HUGSIM 闭环平均 HD-Score 为 **38.8**；推理时不调用模拟器。
- **关注价值／局限**：将“探索到的驾驶动作”重新接回可视未来证据，适合闭环后训练；收益依赖重建、渲染与奖励是否覆盖长尾交互，仿真视频误差仍可能反向塑形策略。

### 2. When LiDAR Fades, Radar Takes Over: LiDAR Reliability-Aware Adaptive Localization Under Airborne Obscurants

- **论文／作者／时间**：[arXiv:2610.13788](https://arxiv.org/abs/2610.13788)；Moumita Mukherjee、Avijit Banerjee、Anton Koval、George Nikolakopoulos；v1：2026-10-09 16:04 UTC。
- **问题**：烟尘等空气遮挡会使 LiDAR-inertial odometry 在 GNSS 拒止地下环境中突然失效，而雷达往往更耐受。
- **创新与机制**：以仅在健康运行数据上训练的滑窗 LSTM autoencoder 建模空间、跨模态、几何／运动、强度与测量新鲜度特征；异常分数生成 LiDAR 可靠度，并在 LIO 与 radar-inertial odometry 间切换定位权。
- **实验与关键结果**：作者在真实地下隧道的正常与浓烟地面机器人数据中展示退化检测、模态切换和严重退化下持续输出；特征族消融显示，在该浓烟场景中较精简的表示反而改善定位。
- **关注价值／局限**：把传感器失效检测直接连接到冗余定位执行；目前未给出跨粉尘类型、速度、雷达干扰及切换误报代价的广泛定量安全边界。

## 机器人／具身智能

### 3. Splat2Act: From Captured Scenes to Personalized VLA Manipulation

- **论文／作者／时间**：[arXiv:2610.13945](https://arxiv.org/abs/2610.13945)；Xiaomeng Ye、Krishna Jaganathan、Gyubeum Lim、Zsolt Kira 等；v1：2026-10-09 17:59 UTC。
- **问题**：通用 VLA 在用户家居／办公室中面对私人物品与布局常失效，逐场景采集真机示范成本很高。
- **创新与机制**：仅用手持手机扫描和物体图像构建含碰撞几何的建筑级 3DGS 数字孪生，自动找容器、生成抓取任务，并以特权模拟 oracle 合成示范；两阶段微调先适应公共资产、再适应用户物体与摆放。
- **实验与关键结果**：101 个扫描校园环境（中位可通行面积 **104.87 m²**）产生 852 个容器与逾 **68,000** 条示范；作者报告目标场景聚合抓取成功率 **62.5%**，Stretch 3 的 12 任务真机子集为 **63.9%**，仿真为 **66.7%**。
- **关注价值／局限**：把场景个性化从人工遥操移到可复用采集—仿真管线；scan 质量、物体物理参数、动态家居环境与 12 项真机任务外的泛化仍需检验。

### 4. Noise Space Learning for VLA Adaptation

- **论文／作者／时间**：[arXiv:2610.13943](https://arxiv.org/abs/2610.13943)；Junjie Lu、Chuheng Zhang、Yucen Wang、Li Zhao 等；v1：2026-10-09 17:58 UTC。
- **问题**：把预训练 flow-matching VLA 适配到具体任务时，直接调模型既消耗机器人交互与算力，也难维持部署安全约束。
- **创新与机制**：冻结 VLA 主干，只学习上下文条件化的噪声分布；以该“噪声接口”承载 PPO、SAC、AWR 等不同学习算法，并给出信息论分析解释适配效率。
- **实验与关键结果**：在 LIBERO、RoboTwin 和 4 个真机操作任务、不同交互／算力／执行限制下比较多个 NSL 变体，作者给出按资源与部署条件选算法的经验建议；摘要未披露统一单一百分比增益。
- **关注价值／局限**：为低风险、小预算在线适配提供比全参微调更窄的改动面；噪声空间的可控性不等于动作安全，真实失败恢复、OOD 目标和长期遗忘需单独报告。

### 5. Chronos Policy: Learning Robot Policies on Physical Time

- **论文／作者／时间**：[arXiv:2610.13929](https://arxiv.org/abs/2610.13929)；Changhao Wang、Jaden Clark、Shuran Song；v1：2026-10-09 17:55 UTC。
- **问题**：将感知—控制压到固定频率 token 序列，会在传感异步、动作延迟或推理时延变化时失真。
- **创新与机制**：把观测采集时刻与目标动作执行时刻显式条件化进 diffusion transformer；比较 timestamp embedding 与 time-aware RoPE，并在训练中随机化观测采样和 action chunk 起点。
- **实验与关键结果**：作者称 time-aware RoPE 更稳健；在仿真与真机动态、多传感任务上优于固定时间网格，同时在准静态任务保持标称表现并提升时序变化鲁棒性。
- **关注价值／局限**：时间戳可成为多速率机器人系统的标准策略接口；摘要未给出任务级幅度，硬件时钟同步误差和极端网络抖动下的退化曲线仍是部署关键。

### 6. BT-Agent: Deploying Onboard Robot Agents with Behavior Trees and Multi-Fidelity Evaluation

- **论文／作者／时间**：[arXiv:2610.13862](https://arxiv.org/abs/2610.13862)；Fabio Hübel、Adam Lilja、Yue Yin、Claire Tomlin、Marco Pavone 等；v1：2026-10-09 17:08 UTC。
- **问题**：移动机器人上的语言 Agent 既要在有限板载资源内决策，也必须在导航异常时即时停止，不能等下一轮模型推理。
- **创新与机制**：LLM 负责任务层决策，预定义行为树技能负责前置条件、执行与结构化失败反馈；建立 161 任务多保真评测，文本全量筛选、Habitat 对 39 项做具身验证。
- **实验与关键结果**：9B 模型在四足机器人上完成 5 类任务；文本评测吞吐是仿真的 **10.9×**，相对最强 Act/ReAct 基线，4B／9B 时最大成功率约提升 **10／5 个百分点**。
- **关注价值／局限**：把高层 Agent 与可即时拦截的本地控制合同分开，利于安全审计；行为树技能覆盖决定上限，文本到仿真的筛选可能漏掉视觉、运动与接触失败。

## 交叉方向：3D／导航

### 7. HorizonNav: Geometry-Guided Video Diffusion for Anticipatory 3D Robot Navigation

- **论文／作者／时间**：[arXiv:2610.13849](https://arxiv.org/abs/2610.13849)；Hajira Amjad、Valerii Serpiva、Viacheslav Liubimov、Dzmitry Tsetserukou 等；v1：2026-10-09 16:57 UTC。
- **问题**：仅由单张 RGB 想象未见空间时，视频扩散的时间连贯并不保证深度与碰撞几何一致，规划会把生成幻觉当可通行区域。
- **创新与机制**：VLM 将文本目标转为视频扩散提示，再用 ORB-SLAM3 相机位姿、Video Depth Anything 深度和三角化地标作 geometry-guided depth alignment，最后在想象 3D 空间中运行 RRT。
- **实验与关键结果**：19 场景中可规划场景从 P20 的 **13/19** 到 P81 的 **15/19**，成功 RRT 从 **62/90** 到 **75/90**；25 条可评轨迹中 6 条违反重建碰撞约束，RRT 修复其中 5 条，15 条走廊重建平均地标误差约 **0.30 m**。
- **关注价值／局限**：没有 LiDAR 时仍主动暴露可行性与碰撞失败，而非只展示视频；其安全性受视频先验、单目尺度和静态走廊评估限制，不能作为真实避障保证。

## 趋势总结

- **世界模型开始接收“轨迹对齐的证据”而非只生成好看的未来**：SimVTA 将高奖励动作配回模拟视频，HorizonNav 则把生成视频再压回多视几何约束；两者都应按罕见风险和重建误差审计。
- **部署接口正在显式化为可靠度、时间与技能合同**：LiDAR／雷达切换、Chronos 的物理时间编码、BT-Agent 的行为树守卫，共同把不可控隐状态拆为可监测、可中止的运行时变量。
- **个性化与适配强调少改主干、少采真机**：Splat2Act 用捕获场景合成数据，NSL 冻结 VLA 改造噪声分布；下一步不是只比较成功率，而是核验动态环境、OOD 和失败恢复的成本。

# GitHub 开源趋势晨报｜2026-10-13

## 时间与证据口径

北京时间 2026-10-13，GitHub Trending 页面请求超时，故本期**不声称官方 `stars today` 或 24 小时增量**。改以 [GitHub Search API](https://api.github.com/search/repositories?q=created%3A%3E%3D2026-10-06&sort=stars&order=desc) 和逐仓库 [Repository API](https://docs.github.com/rest/repos/repos#get-a-repository) 核对 2026-10-06 至 10-08 创建项目；“增量”均为**创建至本次查询的当前 stars**，不是日增量。星数、创建时间、语言、许可证和描述为确认信息；走红原因与适合人群为编辑推断。

| 项目 | 当前 stars | 增量依据 | 语言／类别 |
| --- | ---: | --- | --- |
| openai/math | 14,403 | 创建至查询 | Lean／形式化数学 |
| storytold/wordcraft | 8,944 | 创建至查询 | Rust／本地文档编辑 |
| storytold/cadcraft | 3,407 | 创建至查询 | Rust／CAD 工具 |
| zhongerxin/iPhone-use | 3,347 | 创建至查询 | Python／设备自动化 |
| noahdunnagan/fsearch | 1,961 | 创建至查询 | Rust／本地搜索 |
| HelixDB/helix-foundry | 1,331 | 创建至查询 | TypeScript／数据工作台 |
| pingdotgg/ts-rust | 1,120 | 创建至查询 | Rust／开发基础设施 |
| bherbruck/solidcraft | 1,048 | 创建至查询 | Rust／参数化 CAD／MCP |

### 1. openai/math

- **确认信息**：[仓库](https://github.com/openai/math)／[API](https://api.github.com/repos/openai/math)：2026-10-06 创建，14,403 stars，Lean、Apache-2.0。
- **用途**：提供可复现、机器检查的形式化数学工作基础。
- **走红原因（推断）／适合人群**：随着模型推理进入高价值技术流程，社区会偏好可验证的证明工件；适合研究者、形式化方法与 AI 评测开发者。应先确认数据来源、证明审查流程与自身 Lean 工具链兼容性。

### 2. storytold/wordcraft

- **确认信息**：[仓库](https://github.com/storytold/wordcraft)／[API](https://api.github.com/repos/storytold/wordcraft)：2026-10-07 创建，8,944 stars，Rust、Apache-2.0；自述为纯 Rust 的 Microsoft Word clean-room 重实现。
- **用途**：在本地生成、编辑和处理文档工件。
- **走红原因（推断）／适合人群**：Agent 需要能继续编辑、校验和版本管理的文档表面，而不是一次性导出；适合桌面软件、企业文档流和自动化开发者。复杂 DOCX 保真、宏／外链安全和协作模型仍须压测。

### 3. storytold/cadcraft

- **确认信息**：[仓库](https://github.com/storytold/cadcraft)／[API](https://api.github.com/repos/storytold/cadcraft)：2026-10-07 创建，3,407 stars，Rust、Apache-2.0；自述为 AutoCAD 风格的 CAD／制图应用。
- **用途**：为二维制图与 CAD 编辑提供本地开源底座。
- **走红原因（推断）／适合人群**：可编辑的工程工件正从文档扩展到空间设计；适合 maker、CAD 工具开发者及需审计图纸生成链的团队。DWG/DXF 互操作、几何内核正确性与许可证兼容是采用前检查项。

### 4. zhongerxin/iPhone-use

- **确认信息**：[仓库](https://github.com/zhongerxin/iPhone-use)／[API](https://api.github.com/repos/zhongerxin/iPhone-use)：2026-10-06 创建，3,347 stars，Python、MIT；描述为通过 USB 让 Codex 操作真实 iPhone，含引导安装、App 自动化、实时屏幕和截图回退。
- **用途**：把受控的真实移动设备纳入 Agent 自动化与测试循环。
- **走红原因（推断）／适合人群**：computer-use 的价值从浏览器扩展到实际设备；适合移动端测试、个人自动化和研究原型。必须在隔离测试设备运行，审阅 USB 信任、隐私数据、App 权限和误触操作边界。

### 5. noahdunnagan/fsearch

- **确认信息**：[仓库](https://github.com/noahdunnagan/fsearch)／[API](https://api.github.com/repos/noahdunnagan/fsearch)：2026-10-08 创建，1,961 stars，Rust、MIT；自述为 macOS 全盘搜索，支持模糊名称、容错和索引内容 grep，宣称 8M 文件约 1 ms 查询。
- **用途**：为本地资料、代码和文件系统提供低延迟检索入口。
- **走红原因（推断）／适合人群**：个人 Agent 的上下文基础层需要先能可靠定位原始资料；适合研究、工程与资料密集用户。应评估索引范围、敏感目录排除、后台资源占用和删除后索引清理。

### 6. HelixDB/helix-foundry

- **确认信息**：[仓库](https://github.com/HelixDB/helix-foundry)／[API](https://api.github.com/repos/HelixDB/helix-foundry)：2026-10-07 创建，1,331 stars，TypeScript、Apache-2.0；描述为基于 HelixDB 与 DuckDB 的本地优先数据工作台，将公司数据连接为 ontology。
- **用途**：把异构业务数据组织为可查询的本地语义工作区。
- **走红原因（推断）／适合人群**：Agent 落地正从聊天记忆转向可治理的数据语义层；适合数据平台、分析与知识工程团队。需验证连接器权限、血缘、访问控制与本体维护成本。

### 7. pingdotgg/ts-rust

- **确认信息**：[仓库](https://github.com/pingdotgg/ts-rust)／[API](https://api.github.com/repos/pingdotgg/ts-rust)：2026-10-07 创建，1,120 stars，Rust、MIT；描述为 TypeScript 7 编译器（`tsc`）的实验性 Rust 移植。
- **用途**：探索更高效、可并发的 TypeScript 编译基础设施。
- **走红原因（推断）／适合人群**：大型 Agent 代码改动会放大编译与反馈时间，开发者偏好更快的工具链；适合编译器研究、构建系统和大型 TS 项目维护者。实验性质意味着语义兼容、插件生态和生产稳定性不能默认成立。

### 8. bherbruck/solidcraft

- **确认信息**：[仓库](https://github.com/bherbruck/solidcraft)／[API](https://api.github.com/repos/bherbruck/solidcraft)：2026-10-07 创建，1,048 stars，Rust、Apache-2.0；自述为桌面、Web 与 MCP 自动化皆可用的开源参数化 3D CAD。
- **用途**：将参数化建模暴露给人类设计者及 MCP 驱动的自动化流程。
- **走红原因（推断）／适合人群**：与 CadCraft 一起表明 Agent 工件面正在进入几何设计，且开始以 MCP 提供结构化操作入口；适合硬件原型、生成式设计和机器人场景资产团队。应隔离自动生成模型，并校验尺寸、公差、导出格式和物理可制造性。

## 技术趋势与社区偏好

- **“可验证”从代码测试扩展到数学与工程工件**：openai/math、CAD 与文档重实现共同说明，社区正追逐可继续编辑、检查与版本化的高价值成果，而不只是生成文本。
- **本地优先的上下文层继续下沉**：fsearch 提供文件检索，helix-foundry 提供语义数据工作台；敏感数据接入的权限、索引边界和删除传播成为默认评估项。
- **Agent 正触达真实设备和实体设计**：iPhone-use 与 SolidCraft 把执行范围扩到手机、三维模型和 MCP；这提高可交付性，也要求测试设备隔离、动作确认及工程验算。
- **基础设施偏好效率与兼容性并重**：ts-rust 的快速增长反映开发者对构建反馈的持续压力，但实验性项目应先以兼容测试而非 star 数判断可用性。

## 历史归档

报告按 [reports/](reports/) 下的 `YYYY-MM-DD/` 保存，保留每日 arXiv 与 GitHub Trending 独立文件。

## 内容标准

- arXiv 报告明确提交日期、问题、机制、实验、关注价值、局限与回溯日期。
- GitHub 报告区分 Trending 页面确认、仓库元数据与编辑推断，排除营销、攻击、账号自动化和疑似灌星项目。
- README 最新一期展示本次两份报告正文；跨期判断维护于 [CATEGORY_SUMMARY.md](CATEGORY_SUMMARY.md)。
