# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪最新 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-11-11

- [arXiv 独立报告](reports/2026-11-11/arxiv.md)

- [GitHub Trending 独立报告](reports/2026-11-11/github-trending.md)

- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-11

## 日期与证据口径

截至北京时间 2026-11-11 06:00，arXiv API 在 cs.RO、cs.CV、cs.AI、eess.SY 的最新相关 v1 批次为 **2026-11-09 UTC**。以下均为该日新提交，并与 11 月 10 日已报道条目去重；作者、时间、方法与数字来自 arXiv 元数据和摘要。未能从元数据可靠核验机构时不作推断；摘要中的实验数字不等于真实开放环境保证。

## 自动驾驶／移动自治

### 1. [SAM-VTP: Video Memory and Measured Geometry for Continuous Traversability Segmentation](https://arxiv.org/abs/2611.12099)

- **作者／机构／提交：** Lucas Hoefs、Hui Xie、Senjian An、Fangyi Zhang；arXiv 未列可核验机构；v1 2026-11-09 09:18 UTC。
- **问题与创新：** 逐帧视觉可通行性易闪烁，外观也不足以代表坡度、粗糙度和高度。SAM-VTP 将 SAM2 视频记忆与实测深度几何并入连续（非二元）可通行评分。
- **机制／结构：** 持久 video-memory 编码前序观测；由深度计算坡度、粗糙度、高度并融合图像特征；离线管线以几何与语义先验生成每像素 [0,1] 监督，无需机器人部署或人工像素标注。
- **实验与关键结果：** TartanGround 上 fuzzy Jaccard 0.908→0.924、IoU 0.854→0.886，帧间闪烁降 31%；两处野外闭环试验使用同一规划器，摘要未给完整成功率。
- **关注价值：** 将时序一致、可测几何和规划输入连成接口，比单张语义掩码更接近可审计越野自治。
- **局限／跟进：** 深度误差、雨雾/强光、地图更新延迟和未见地表仍可能破坏评分；应公开闭环碰撞、保守拒绝与实时资源曲线。

### 2. [Certified Zonotopic Reachability Analysis for Trajectory Tracking on Lie Groups](https://arxiv.org/abs/2611.12767)

- **作者／机构／提交：** Yanliang Huang、Peng Xie、Zhen Zhang、Zhuoqi Zeng、Amr Alanwar；arXiv 未列可核验机构；v1 2026-11-09 17:40 UTC。
- **问题与创新：** 飞行/航天器沿障碍附近轨迹行驶时，单一不变椭球或区间常过度保守。该工作在 Lie algebra 误差坐标内构造连续时间、可证明覆盖所有跟踪误差的 zonotope tube。
- **机制／结构：** 利用 group-affine 系统参考输入下的线性误差部分；以 zonotope 传播，并闭式包络 inverse right Jacobian 对扰动的影响，保留无输入分量带来的非线性余项。
- **实验与关键结果：** 作者报告所得 tube 更紧且在所测案例中可认证；摘要未给统一的体积缩减、运行时间或真机安全增益。
- **关注价值：** 为移动机器人规划提供“执行偏差上界”而非只给名义轨迹，适合接入风险约束与安全走廊。
- **局限／跟进：** 依赖扰动界、动力学模型与状态估计；需要比较保守度—算力权衡，并在传感延迟、模型失配和在线重规划下验证。

## 机器人／具身智能

### 3. [World In-Context Learning for Agentic Robot Manipulation](https://arxiv.org/abs/2611.12885)

- **作者／机构／提交：** Heng Fang、Zehui Guo、Yuehan Zhang、Mingyang Du、Dingkang Liang、Xiang Bai；arXiv 未列可核验机构；v1 2026-11-09 18:59 UTC。
- **问题与创新：** 训练策略把技能固化在权重和采集分布中；跨场景演示又缺少当前世界的反馈。WICL 让冻结模型在模拟世界 rehearsal，将反馈写入上下文任务记忆而非更新参数。
- **机制／结构：** RoboScript 从单个演示抽取语义步骤与对象角色，在模拟器反复试做，冻结 Task Memory 后在新场景部署；数据隔离要求每项部署输入在真机可获得。
- **实验与关键结果：** RoboTwin 2.0 的 50 个任务平均成功率 83.4%；摘要称优于对照，但完整对照、仿真—真机比例和成本需读全文核验。
- **关注价值：** 把“经验”变成可查看、可替换的上下文资产，可能降低每个新任务重新训练的成本。
- **局限／跟进：** 模拟 rehearsal 的错误会写进记忆；需报告记忆长度/推理时延、失败回滚、现实随机性与恶意/错误演示的隔离效果。

### 4. [SWAM: Scaling World Action Models with Cross-Modal Alignment](https://arxiv.org/abs/2611.12870)

- **作者／机构／提交：** Yu Zhou、Xinyuan Xia、Xuankun Yang、Yinghao Yang、Wendi Chen、Bowen Liu、Jianhan Ma、Weicheng Duan、Jun Lv、Cewu Lu、Yanwei Li；arXiv 未列可核验机构；v1 2026-11-09 18:55 UTC。
- **问题与创新：** WAM 加入动作监督后可能损坏原有语言—视频对齐；论文系统研究语言—视频、语言—视频—动作监督及其混合的配方，而非只扩大网络。
- **机制／结构：** 汇集约 4.7 万小时通用/第一视角视频、UMI 与机器人示范；考察标注质量、数据混合、联合训练及结构设计，以保持语言视频能力并扩展到 action modeling。
- **实验与关键结果：** 摘要报告固定训练预算下，混合第一视角与 UMI 示范带来更强 WAM；未列统一绝对成功率/长时预测误差，不能将“规模”直接当控制收益。
- **关注价值：** 将数据类型和跨模态对齐视为可消融设计变量，为大规模具身数据配方提供更实用的研究路径。
- **局限／跟进：** 数据授权、动作时间同步、数据分布泄漏和真实接触任务的因果贡献需独立审计；应报告算力、模型尺寸和失败样例。

### 5. [Learning Heterogeneous Tactile Representation for General Dexterous Manipulation](https://arxiv.org/abs/2611.12806)

- **作者／机构／提交：** Bing Han、Yichuan Peng、Haoyu Dong、Yuanmeng Hu、Yongyi Jia、Fangjing Wang 等；arXiv 未列可核验机构；v1 2026-11-09 18:12 UTC。
- **问题与创新：** 压阻、磁性、视觉触觉传感器的物理与格式不同，策略难以复用。LingBot-Touch 学习跨传感器统一触觉 token，并作为 diffusion policy、π₀.₅、LingBot-VLA 的即插即用输入。
- **机制／结构：** 以异构触觉数据训练基础表征并预留新传感器扩展路径；用 token 与视觉/动作模型融合，服务精细接触操控。
- **实验与关键结果：** 摘要称在仿真及多硬件真机上持续提升灵巧操作，但未给绝对成功率、传感器间掉点和方差。
- **关注价值：** 若能跨硬件成立，触觉数据不再被单一传感器锁定，可更好支持接触状态估计和策略迁移。
- **局限／跟进：** 需要验证传感器饱和、漂移、缺失、安装姿态变化和跨厂商新传感器的零样本表现。

### 6. [Benchmarking Real-World Robotic Manipulation through Stochastic Challenges](https://arxiv.org/abs/2611.12804)

- **作者／机构／提交：** Elias Gläßer、Gülhan Şikaroğlu、Pavlo Kupyn、Marc Pollefeys、Zuria Bauer、Hermann Blum；arXiv 未列可核验机构；v1 2026-11-09 18:10 UTC。
- **问题与创新：** 静态数据集不能覆盖交互，仿真又难涵盖真实复杂性。论文提出可复现实景上的随机挑战：样本来自同一分布，但保持隐藏测试般的意外性。
- **机制／结构：** 在可复制真实场景中随机采样任务，按跨实验室成功率比较不同平台；实现了移动操作 benchmark，并在两个实验室比较两台机器人。
- **实验与关键结果：** 论文展示跨机器人、跨实验室的分布式成功率比较；摘要未给样本量、置信区间与平台差异的完整数字。
- **关注价值：** 以可重放现实随机性补齐“单次真机 demo”与纯仿真之间的证据断层。
- **局限／跟进：** 任务分布和场景搭建仍会决定结论；应发布生成协议、故障定义、统计功效、传感/执行器版本及跨地点复现实验。

## 交叉方向：世界模型与长期空间状态

### 7. [Compass 1: Towards Open-World and Persistent Embodied Navigation from Monocular RGB Videos](https://arxiv.org/abs/2611.12087)

- **作者／机构／提交：** Hai Zhang、Siqi Liang、Yanjun Guo、Shoufeng Zhang、Yunhao Wang 等；arXiv 未列可核验机构；v1 2026-11-09 09:04 UTC。
- **问题与创新：** 开放世界导航通常只能利用少量最近帧，长时执行易丢失空间与任务阶段。Compass 1 用单目 RGB 视频同时连接语言理解、视频生成和可回溯历史。
- **机制／结构：** 在不改底层架构下引入 History Representation：稀疏关键帧加显式 History Representation Map；再以任务阶段 grounding、探索一致性、时空目标检索三类 VQA 监督训练使用历史，并建立 500+ 小时真实交互数据。
- **实验与关键结果：** 摘要称历史可回溯近 2 分钟；未列逐基准成功率、地图漂移和真实自主闭环安全数字。
- **关注价值：** 明确把“记住什么、如何检索”做成状态接口，适用于长走廊、物体移动和重复访问任务。
- **局限／跟进：** 单目尺度/遮挡、历史错误累积、视频生成幻觉与检索延迟仍是核心风险；需在动态人群和跨天场景报告失败恢复。

## 趋势总结

11 月 9 日批次的共同变化是把具身系统的中间状态做成可检查资产：越野评分保留视频记忆和测得几何，导航保留可检索历史，WICL 保留任务记忆，WAM/触觉模型保留跨模态接口，随机挑战保留真实世界的统计不确定性。它们的下一道门槛不是更大摘要数字，而是证明这些状态在传感缺失、时延、仿真偏差、跨硬件与不可逆接触下仍可校准并安全回退。

# GitHub 开源趋势晨报｜2026-11-11

## 时间与证据口径

检索于北京时间 2026-11-11 06:00。Trending 增量取自第三方镜像保存的 **2026-11-10 UTC 日榜**（采集 2026-11-10 21:07 UTC），`+N/日` 是该镜像记录的 GitHub Trending `gained`，不是本次总 star 的相减值。总 star、主要语言、许可证和用途以本次 GitHub Repository API 复核为准；镜像并非 GitHub 官方服务。项目“走红原因”及趋势结论均为编辑推断，star 不证明质量、安全或生产采用。

## 精选项目

### 1. [meta/astryx](https://github.com/meta/astryx)

- **数据：** API 当前 **22,586 stars**；11 月 10 日日榜第 1、**+3,111/日**；TypeScript；MIT。证据：[Repository API](https://api.github.com/repos/meta/astryx)、[日榜快照](https://githubtrending.today/api/archive/2026-11-10.json)。
- **确认用途：** 可高度定制、agent-ready 的开源 design system。
- **走红原因（推断）：** 设计 token 和组件约束让 Agent 生成的界面仍能回到可编辑工件，适合团队将提示输出纳入既有前端规范。
- **适合人群：** 维护组件库的设计工程团队；先核对主题、无障碍、迁移成本和发布版本，勿将“agent-ready”视为自动满足产品规范。

### 2. [anthropics/skills](https://github.com/anthropics/skills)

- **数据：** API 当前 **192,226 stars**；日榜第 2、**+1,676/日**；Python；许可证字段 `NOASSERTION`。证据：[Repository API](https://api.github.com/repos/anthropics/skills)、[日榜快照](https://githubtrending.today/api/archive/2026-11-10.json)。
- **确认用途：** 公开的 Agent Skills 仓库，组织 Agent 可使用的任务指令与资源。
- **走红原因（推断）：** 社区正将个人提示经验转成版本化、可检阅的工作流资产；这和 11 月 9 日持续上榜形成连续观察，而非新的采用率证明。
- **适合人群：** 希望规范 Agent 工作流的团队；每个 Skill 都应审阅脚本、网络权限、数据入口和许可后再安装/执行。

### 3. [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)

- **数据：** API 当前 **115,087 stars**；日榜第 3、**+465/日**；JavaScript；MIT。证据：[Repository API](https://api.github.com/repos/addyosmani/agent-skills)、[日榜快照](https://githubtrending.today/api/archive/2026-11-10.json)。
- **确认用途：** 面向 AI coding agent 的 production-grade engineering skills。
- **走红原因（推断）：** 与通用 Skill 仓库同榜，说明开发者特别需要把代码审阅、设计和交付流程固化为可复用约束，而不只换模型。
- **适合人群：** 使用 coding agent 的应用/平台工程师；将 Skill 当作待测试的工程依赖，结合仓库规范、CI 和最小权限沙箱。

### 4. [google-deepmind/mujoco](https://github.com/google-deepmind/mujoco)

- **数据：** API 当前 **17,313 stars**；日榜第 5、**+453/日**；C++；Apache-2.0。证据：[Repository API](https://api.github.com/repos/google-deepmind/mujoco)、[日榜快照](https://githubtrending.today/api/archive/2026-11-10.json)。
- **确认用途：** 通用多关节接触动力学物理模拟器。
- **走红原因（推断）：** 机器人世界模型、操作基准和控制研究升温，使可复现实验底座再次进入日榜；热度不代表 sim-to-real 已解决。
- **适合人群：** 控制、RL、机器人研究者；单独标定摩擦、接触、传感器和执行器模型，并以真机失效案例检验迁移。

### 5. [homeassistant-ai/ha-mcp](https://github.com/homeassistant-ai/ha-mcp)

- **数据：** API 当前 **6,579 stars**；日榜第 7、**+792/日**；Python；MIT。证据：[Repository API](https://api.github.com/repos/homeassistant-ai/ha-mcp)、[日榜快照](https://githubtrending.today/api/archive/2026-11-10.json)。
- **确认用途：** 让 Claude、ChatGPT 等助手配置和自动化 Home Assistant。
- **走红原因（推断）：** MCP 让 Agent 接到真实设备控制面；11 月 10 日增量提高说明此类执行接口持续受关注，非安全性证据。
- **适合人群：** 已部署 Home Assistant 的自动化开发者；先以只读/低风险实体测试，隔离凭据、配置审批并限制门锁、警报和能源类写操作。

### 6. [vercel-labs/agent-browser](https://github.com/vercel-labs/agent-browser)

- **数据：** API 当前 **49,145 stars**；日榜第 8、**+775/日**；Rust；Apache-2.0。证据：[Repository API](https://api.github.com/repos/vercel-labs/agent-browser)、[日榜快照](https://githubtrending.today/api/archive/2026-11-10.json)。
- **确认用途：** 面向 AI Agent 的浏览器自动化 CLI。
- **走红原因（推断）：** 浏览器成为 Agent 的通用执行面，CLI 的可组合性适配测试、研究和内部录入流程；这不消除站点条款、验证码和身份风险。
- **适合人群：** 建设受控网页测试或内部自动化的团队；隔离会话、最小化凭据、设置域名 allowlist，并为写操作提供显式确认。

### 7. [tokio-rs/topcoat](https://github.com/tokio-rs/topcoat)

- **数据：** API 当前 **6,757 stars**；日榜第 10、**+192/日**；Rust；MIT。证据：[Repository API](https://api.github.com/repos/tokio-rs/topcoat)、[日榜快照](https://githubtrending.today/api/archive/2026-11-10.json)。
- **确认用途：** batteries-included 的 Web 应用构建框架。
- **走红原因（推断）：** Agent 应用不只需要模型调用，也需要可靠的 Web 交付底座；Rust 生态的成套框架因性能与部署可控性获得注意。
- **适合人群：** 希望以 Rust 构建服务端/全栈应用的工程师；评估其成熟度、生态兼容性、安全更新和团队学习成本。

### 8. [ranxianglei/billion-context](https://github.com/ranxianglei/billion-context)

- **数据：** API 当前 **6,258 stars**；日榜第 11、**+374/日**；TypeScript；许可证字段 `NOASSERTION`。证据：[Repository API](https://api.github.com/repos/ranxianglei/billion-context)、[日榜快照](https://githubtrending.today/api/archive/2026-11-10.json)。
- **确认用途：** 自述为面向月级长会话的上下文压缩插件，宣称用较小窗口并节省 token；此为项目自述，未独立复测。
- **走红原因（推断）：** Agent 长任务中上下文成本和连续性是共同痛点，压缩工具因可直接嵌入 workflow 而受关注。
- **适合人群：** 研究长任务 Agent 和记忆策略的开发者；先在无敏感数据的可回放基准测试事实遗漏、检索偏差、数据留存和许可证。

## 技术趋势与社区偏好

本期日榜形成三层组合：Skill 把经验资产化，Astryx/Topcoat 把结果落到可编辑、可部署的产品层，agent-browser 与 ha-mcp 将 Agent 接入浏览器和真实设备，billion-context 处理长任务状态，MuJoCo 则继续支撑具身验证。社区偏好已从“模型能做什么”转为“工作流能否持续执行和交付”。相应地，指令/依赖审计、写权限确认、凭据隔离、记忆删除与许可证核验必须先于 star 数。

## 证据链接

- [GitHub Trending 2026-11-10 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-10.json)：排名、快照总 star 与 `gained`。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：镜像采集和统计口径。
- 各项目当前元数据以上述 Repository API 为准；走红原因均为编辑推断。

## 历史归档

报告按 [reports/](https://github.com/Bala-la-la/autonomous-driving-robotics-daily/tree/main/reports/) 下的 YYYY-MM-DD/ 保存，每天保留 arXiv 与 GitHub 两份独立报告。

## 内容标准

- arXiv 报告明确标注提交日期、问题、机制、实验、关注价值与局限；无新稿时标明回溯日期。
- GitHub 报告区分当前仓库元数据、Trending 增量证据和编辑推断，并注明重复观察与统计窗口。
- README 最新一期直接展示两份报告全文；跨期判断维护于 [CATEGORY_SUMMARY.md](CATEGORY_SUMMARY.md)。
