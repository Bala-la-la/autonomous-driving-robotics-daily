# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪最新 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-10-25

- [arXiv 独立报告](reports/2026-10-25/arxiv.md)
- [GitHub Trending 独立报告](reports/2026-10-25/github-trending.md)
- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-25

## 日期与证据口径

截至北京时间 2026-10-25 06:17，相关 arXiv 查询最新批次是 10 月 23 日公布、v1 于 10 月 22 日 UTC 提交的周五批次；周末没有新的相关日更。复查 10 月 23 日 UTC 之后的 autonomous driving、robotics、embodied、manipulation、navigation、SLAM、VLA 等主题未发现可替代的新稿。本期明确回溯至 10 月 22 日 v1，选取 7 篇且不与前一期重复的论文。作者、题名和时间依据 arXiv API；机构只在论文首页可核实时列出。数据仅按论文实际评测范围转述，不把离线指标当作部署安全证明。

## 自动驾驶

### 1. [To Route or to Adapt? Multi-Expert Diffusion Planners in Unseen Regions](https://arxiv.org/abs/2610.31095)

- **作者／机构／提交时间：** Yun Li、Ehsan Javanmardi、Simon Thompson、Jiachen Gong、Qunli Zhang、Zifan Zeng、Shiming Liu、Peng Wang、Yidu Zhang、Manabu Tsukada；东京大学、TIER IV、华为；v1 提交于 2026-10-22 11:06:48 UTC。
- **问题与创新：** 面向训练分布之外的新区域，扩散式轨迹规划器究竟只需从现有专家中选路由，还是必须更新规划器本身？作者把这个工程取舍做成直接对照，而不是把专家选择或测试时适配单独包装成新方法。
- **机制／结构：** 被测规划器有共享 adapter 和按 ODD 划分的专家 adapter。论文比较 8 种测试时专家路由方案、oracle 路由，以及用目标区域奖励微调；联合回放目标区域与旧训练场景，以降低灾难性遗忘。
- **实验与关键结果：** 在 3 张真实留出地图上，8 种路由都没有优于所有场景固定使用同一专家的默认策略；即使 oracle 每个场景选最佳专家，平均侧向偏差也只改善 0.9 m。只用 20 个目标区域场景做奖励微调并联合回放后，匹配评估切片的车队平均偏差由 12.4 m 降到 6.9 m。nuPlan 上开环偏差同样改善，但闭环成绩下降；另有两个测试时适配基线以退化轨迹换得表面上的低偏差。
- **关注价值：** 结果给出了一个实用边界：专家路由无法凭空补出训练中没有的区域经验，小量目标域训练可能带来更明显的开环收益，但侧向误差并不等于安全或闭环驾驶质量。
- **局限／跟进：** 实地留出地图只有 3 张，微调数据也很少；nuPlan 的开环改善伴随闭环退化。后续应报告更多区域、交通参与者交互、安全事件分项、目标域数据成本和回放对旧 ODD 的实际保留效果。

## 机器人／具身智能

### 2. [Progress Probes P²: Lightweight Runtime Monitoring for Vision-Language-Action Models](https://arxiv.org/abs/2610.31613)

- **作者／机构／提交时间：** Atiksh Bhardwaj、Edward W. Duan、Junwon Seo、Prithwish Dan、Wei-Chiu Ma、Andrea Bajcsy、Preston Culbertson；Carnegie Mellon University、Cornell University；v1 提交于 2026-10-22 17:40:19 UTC。
- **问题与创新：** VLA 在真实操作中会停滞或偏离任务，常见监控器依赖额外 VLM 或失败标注，增加推理成本并要求难采集的数据。P² 检验策略自身的内部激活是否已经编码了足够的任务进展信息。
- **机制／结构：** 用成功演示给每个时刻标注归一化任务进度，并训练线性 probe 从 π0.5 内部激活解码进度；运行时将预测进度与成功轨迹的预期进度比较，落后或偏离时发出异常信号。监控复用策略前向计算已经产生的激活，不需失败样本或外部基础模型。
- **实验与关键结果：** 在 6 项 VLABench 模拟任务和 6 项真实操作任务上，AUROC 分别为 0.788 和 0.780；论文报告其故障检测可与或优于 VLM 监控器及需要失败数据的方法。该结果是检测任务执行偏离，不是直接提升机械臂完成率。
- **关注价值：** 将轻量、可学习的运行时监控嵌入 VLA 本身，为策略提供低额外计算的“是否还在推进任务”信号。
- **局限／跟进：** 评测依赖成功示范定义的进度轨迹，当前只测 π0.5 与有限任务；策略可能朝错误目标持续前进而仍显示有进度。应补充跨本体、不同任务分解、误报漏报成本以及监控触发后暂停／恢复的闭环评测。

### 3. [Humanoid Mobility via Attention-based Contacts](https://arxiv.org/abs/2610.31608)

- **作者／机构／提交时间：** Junzhe He、Kehan Wen、Chong Zhang、Clemens Schwarke、Zewei Zhang、Kaixian Qu、Siyuan Hu、Matthias Müller、Vladlen Koltun、Marco Hutter；ETH Zurich、National University of Singapore、Apple、ETH AI Center、NVIDIA；v1 提交于 2026-10-22 17:37:36 UTC。
- **问题与创新：** 仅靠强化学习奖励探索很难学到协调的全身接触动作；直接跟踪人类／机器人参考动作虽自然，却受限于训练轨迹覆盖。本文把“何时、何处、用身体哪一部分接触环境”作为感知到动作之间的中间接口。
- **机制／结构：** 三阶段训练：先从参考动作训练全身接触跟踪器，再用显式注意力接触规划器从地形图、机器人本体状态和目标预测未来接触，最后通过接触条件化的强化学习微调并把成功 rollout 回流给规划器。部署时只用机载观测，不输入参考动作。
- **实验与关键结果：** Unitree G1 真机演示包括楼梯、梯子和箱体攀爬、坐下与起身、稀疏／组合地形穿越；还展示了摔倒、起身失败和攀爬卡住后的自主恢复。论文的真机证据以行为展示为主，没有给出可跨场景比较的总体成功率。
- **关注价值：** 联系动作先验与环境适应的不是完整轨迹，而是更稀疏、几何明确的接触计划；同一策略可以根据目标与地形组合不同全身行为。
- **局限／跟进：** 全局导航不在研究范围内，部分非结构化地形使用人工中间 waypoint；实机验证集中在 Unitree G1。需要报告重复试验成功率、失败恢复代价、感知延迟和跨本体迁移，而不能仅凭演示推断通用人形能力。

### 4. [AstroBench: Benchmarking Free-Floating Capture and Space Robotic Manipulation](https://arxiv.org/abs/2610.31064)

- **作者／机构／提交时间：** Zizhe Wang、Jia Deng、Xin Lu、Zehao Jia、Yi Huang、Yao Zhu；Astroup Lab、哈尔滨工业大学北京研究院；v1 提交于 2026-10-22 10:42:38 UTC。
- **问题与创新：** 在轨捕获的物体会自由平移、旋转，且接触会改变其运动，和桌面上被支撑的物体差异很大。AstroBench 把自由漂浮捕获和后续空间站操作纳入可扩展 benchmark，而不是把桌面抓取成功率外推到微重力。
- **机制／结构：** 基准包含 2 个固定基座机械臂工作单元、9 种任务定义和 29 种任务—目标组合；覆盖 4 类初始运动、MELFI 样本存储，以及基于 Robotic Refueling Mission 的盖帽与捕获螺钉操作。还提供 8,414 个经元数据筛选的 Objaverse 物体、5 种舱内视觉背景和版本化任务说明。
- **实验与关键结果：** 冻结的 π0.5 DROID 关节位置策略在 20 种物体上静止目标捕获 2/200、运动目标 4/200；另一次独立实验中，针对立方体训练的 ACT 在静止目标捕获 8/10、运动目标 6/10。两组实验配置与分母不同，不能直接比较算法优劣。
- **关注价值：** 提供了显式考虑目标动量与接触后运动变化的开放测试床，结果也量化显示通用桌面策略直接迁移的困难。
- **局限／跟进：** 低 π0.5 捕获数只说明被测 checkpoint 在这些配置下迁移不佳；cube-specific ACT 试验规模小。固定基座工作单元不等于在轨微重力，仍需验证视觉延迟、目标自旋估计、抓取后稳定和真实硬件约束。

## 交叉方向：越野导航、跨时段地图与多机器人 SLAM

### 5. [TRACE: Traversability-aware Reactive Navigation via VLM-driven Adaptive Constraints Estimation](https://arxiv.org/abs/2610.30994)

- **作者／机构／提交时间：** Mario A. V. Saucedo、Midhun Edatharam Kunnath、Elias Small、Akash Patel、Shruti Kotpalliwar、Christoforos Kanellakis、George Nikolakopoulos；Luleå University of Technology、KAIST；v1 提交于 2026-10-22 09:37:02 UTC。
- **问题与创新：** 森林里的草、松土、树根与岩石难由坡度或语义类别单独判定能否通过。TRACE 用 VLM 从“已走过的路径”等语言提示中估计可通行性，再把视觉判断转为可供控制器使用的走廊约束。
- **机制／结构：** 正向和负向提示分别生成置信图，经证据融合形成稠密 traversability map；对带标签点云做分位数分箱以抽取左右边界，再用样条或正则化多项式拟合，最后将边界写成 NMPC 的软 barrier 约束。
- **实验与关键结果：** GOOSE 越野数据集上的稳定地面、颗粒地面 IoU 分别为 0.672、0.334；poor foothold、high resistance、obstacle 类分别为 0.071、0.008、0.002。另在瑞典北部的 Husky 真机上测试两条森林道路／徒步路径，覆盖高草、植被、岩石和坡地，展示了沿松散路径平稳穿行；该现场验证主要为定性演示。
- **关注价值：** 将 VLM 的场景语义收敛成连续可行走走廊，再交由传统 NMPC 做动态可行性控制，是从视觉 affordance 到执行约束的一种明确接口。
- **局限／跟进：** 小类 IoU 较低，数据集分类指标并不等同路径安全率；真机试验只有一台机器人和两类路线，未报告广泛的碰撞／成功统计。作者将扩大环境与机器人平台列为后续工作。

### 6. [A Sparse Topometric Graph for Scalable Cross-Session Indoor Navigation](https://arxiv.org/abs/2610.31432)

- **作者／机构／提交时间：** Eun Sun Lee、Minkyun Seo、Gwangtak Bae、Junho Kim、Seunggu Kang、Jaesik Park、Young Min Kim；首尔国立大学；v1 提交于 2026-10-22 15:30:33 UTC。
- **问题与创新：** 跨时段导航会遇到家具移动、视角／传感器改变、地图部分重叠；逐点地图或密集特征地图虽细，却占内存且易受局部相似结构干扰。本文以稀疏拓扑几何图保留可复用的局部三维几何和通道连接关系。
- **机制／结构：** 图节点编码局部几何，按距离加权的边表达可通行连通性；学习式子图匹配同时使用节点描述符与邻域结构，在局部外观重复时通过上下文寻找跨时段对应。目标点指定在旧地图，机器人在新 session 的未知位姿中定位并导航。
- **实验与关键结果：** Gibson 上无噪声里程计成功率 77.14%、SPL 47.71%；加入里程计噪声后成功率 60.00%、SPL 23.64%。在家具增删、移动和替换后的 3D-FRONT 场景，成功率 40.00%、SPL 20.18%。Gibson 参考地图存储约 0.02 MB，对照点云表示为 2.81 MB，约缩小 140 倍。真实办公室的数周间隔、手持 LiDAR 与 iPhone LiDAR 配对数据只作对应关系案例，不是在线机器人闭环部署。
- **关注价值：** 把跨时段复用的核心从高分辨率地图改成稀疏的“局部几何 + 连通性”，同时通过图上下文缓解重复布局造成的错配。
- **局限／跟进：** 评测限于单层室内、二维 top-down 点目标任务；封闭门、走廊阻塞等连通性剧变没有系统测试。真实数据展示也不含机载控制、实时定位和失败恢复。

### 7. [Consistent Distributed Invariant EKF SLAM with Point and Object Features](https://arxiv.org/abs/2610.31221)

- **作者／机构／提交时间：** Mengya Xu、Xianjia Yu、Ha Sier、Shoudong Huang、Tomi Westerlund；论文首页未列可核实机构；v1 提交于 2026-10-22 13:06:44 UTC。
- **问题与创新：** 多机器人重复交换地图会引入未知的估计相关性，协方差交集可避免跟踪这些相关性，但 RI-EKF 中邻居地图与其机器人位姿相关，且误差坐标系不兼容，不能直接融合。Joint-CI 为点特征、对象特征和混合地图给出统一构造。
- **机制／结构：** 接收机器人利用邻居后验与机器人间观测，把对方状态映射成自身误差坐标下、包含机器人—特征及特征—特征相关性的联合估计；再对部分状态执行 CI 融合。分析证明保留全局旋转和平移对应的六个不可观方向，并在本地后验一致的前提下维持一阶协方差一致性。
- **实验与关键结果：** 五机器人对象地图仿真中，Joint-CI 相对本地 RI-EKF 将机器人位置 RMSE 从 54.45 cm 降到 48.78 cm、特征位置 RMSE 从 44.26 cm 降到 34.00 cm；YCB-Video 数据集派生实验也显示误差下降且不确定性保持一致、略保守。通信代价是需要传输完整联合协方差。
- **关注价值：** 说明多机器人地图交换不能只对齐坐标和均值，还必须保留共享机器人位姿与地图要素间的统计关联；这是分布式 SLAM 可审计的一致性条件。
- **局限／跟进：** 五机器人结果为 Monte Carlo 仿真，YCB-Video 是数据集派生实验而非多机器人实机部署；算法假设初始后验一致且特征对应关系已知。应报告带宽／计算随地图规模的增长、间歇通信与错误关联条件下的退化。

## 趋势总结

本批新稿把“泛化和自治”落在几种可观察的中间状态上：驾驶规划需要分清选已有专家与适应新区域的能力边界；VLA 监控可以从策略内部激活读取进度；人形控制以显式接触组织全身动作；野外导航把语义可通行性变为 NMPC 约束；跨 session 图和多机器人 CI 则分别处理空间记忆压缩与估计相关性。共同的下一道门槛不是单个平均指标，而是闭环退化、罕见失败、状态关联、跨平台迁移和真实运行资源能否同时被量化。

# GitHub 开源趋势晨报｜2026-10-25

## 时间与证据口径

截至北京时间 2026-10-25 06:17，Repository API 查询各项目当前 stars、语言、许可证与最近推送时间。日增使用 githubtrending.today 保存的 2026-10-24 GitHub Trending 日榜；7 日增使用该站周榜页面于 2026-10-24 06:58 UTC 读取的 GitHub Trending 周榜数值。榜单增量和 API 当前总星数是不同时间点，报告分别标注，不做同一时刻的数值拼接。用途按仓库说明；走红原因是编辑推断，不代表实际采用率。最近一期已经报道过的项目标为回归观察。

## 精选项目

### 1. [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill)

- **数据：** API 约于 10 月 25 日 06:17 查询为 **44,363 stars**；GitHub Trending 10 月 24 日日榜 **+2,716/日**，该日快照约 42.6k stars。JavaScript；MIT；Agent 安全审计 Skill。证据：[Repository API](https://api.github.com/repos/cloudflare/security-audit-skill)、[10/24 日榜存档](https://githubtrending.today/archive/2026-10-24/)。10 月 21 日已有报道，本期是明显回归观察。
- **确认用途：** Cloudflare 仓库描述为面向 coding agent 的多阶段安全审计 skill，目标是产出可机读、可独立验证的 findings。
- **走红原因（推断）：** Agent 进入代码库后，开发者更关注安全结论是否有复现证据，而非只得到自然语言建议；本期日榜增长本身不能说明漏洞发现质量。
- **适合人群：** 将 coding agent 纳入审计流程的 AppSec 团队；应检查执行权限、验证步骤和误报，不把 skill 输出等同于安全认证。Repository API 显示最近推送时间为 9 月 14 日，stars 激增不代表项目代码近期同步更新。

### 2. [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins)

- **数据：** API 约于 10 月 25 日 06:17 查询为 **32,603 stars**；GitHub Trending 10 月 24 日日榜 **+635/日**，当日快照约 32.4k stars。Python；Apache-2.0；知识工作插件。证据：[Repository API](https://api.github.com/repos/anthropics/knowledge-work-plugins)、[10/24 日榜存档](https://githubtrending.today/archive/2026-10-24/)。10 月 21 日已有报道，本期记录其再次进入日榜。
- **确认用途：** Anthropic 的开源仓库，主要面向 Claude Cowork 知识工作者，以可复用插件封装工作流程与领域能力。
- **走红原因（推断）：** 社区关注点从通用模型能力继续移向可直接安装的角色化工作流；日榜回升没有独立证据指向某一功能发布。
- **适合人群：** 已采用 Claude Cowork、希望试用预组装知识工作流程的个人与团队；企业接入前需检查连接器的数据范围、产品依赖和插件更新策略。

### 3. [OpenBMB/VoxCPM](https://github.com/OpenBMB/VoxCPM)

- **数据：** API 约于 10 月 25 日 06:17 查询为 **40,515 stars**；GitHub Trending 10 月 24 日日榜 **+150/日**，当日快照约 40.4k stars。Python；Apache-2.0；多语言语音生成。证据：[Repository API](https://api.github.com/repos/OpenBMB/VoxCPM)、[10/24 日榜存档](https://githubtrending.today/archive/2026-10-24/)。9 月 14 日曾报道；本期是回归观察。
- **确认用途：** 仓库当前描述聚焦 VoxCPM2：无 tokenizer 的多语言 TTS、声音设计与语音克隆。
- **走红原因（推断）：** 可控语音生成与较开放的模型工作流持续吸引本地创作和语音 Agent 开发者；本次榜单不能证明某个模型版本造成了星增。
- **适合人群：** 语音应用、创作工具和多模态 Agent 开发者；上线前应分别核实模型权重、训练数据、声音克隆授权、推理成本和商用条款。

### 4. [pollen-robotics/microduck](https://github.com/pollen-robotics/microduck)

- **数据：** Repository API 约于 10 月 25 日 06:17 查询为 **10,935 stars**，Rust、Apache-2.0。Trend.ondo 的 10 月 24 日页面称其首次进入记录到的 Trending 日榜、排名 #7，当日页面记为 10,819 stars；两快照相差 **+116**，但页面没有精确采集时刻，故这不是严格的 24 小时增量。该第三方排名与 githubtrending.today 的 10 月 24 日八项日榜存档不一致，本文只把它作为第三方观察，不当作已交叉确认的官方排名。证据：[Repository API](https://api.github.com/repos/pollen-robotics/microduck)、[Trend.ondo 10/24 项目页](https://trend.ondo.sh/github/r/pollen-robotics--microduck/en.html)。
- **确认用途：** Pollen Robotics 的小型双足鸭机器人控制固件，仓库说明包含用强化学习策略驱动舵机的控制环、嵌入式守护进程和更新机制。
- **走红原因（推断）：** 可观看、可操作的小型实体机器人把强化学习从抽象模型带回具体硬件，较易形成直观演示和开发者传播；不能据此推断实际硬件部署量。
- **适合人群：** 嵌入式机器人、运动控制和机器人教育开发者；复现前要核对 BOM、电机／电池安全、策略兼容性及固件更新路径。

### 5. [cursor/plugins](https://github.com/cursor/plugins)

- **数据：** API 约于 10 月 25 日 06:17 查询为 **13,906 stars**；GitHub Trending 周榜于 10 月 24 日 06:58 UTC 显示 **+1,946/7 天**，该快照约 13.8k stars。TypeScript；插件规范与官方插件目录；Repository API 未给出 SPDX 许可证标识。证据：[Repository API](https://api.github.com/repos/cursor/plugins)、[GitHub Trending 周榜快照](https://githubtrending.today/weekly/)。10 月 19 日曾报道，当前属于回升观察。
- **确认用途：** 仓库提供 Cursor 插件规范和官方插件示例／目录。
- **走红原因（推断）：** Agent 编辑器把工具与工作流打包为可发现、可维护的插件，降低每个团队各自配置的成本；增长并不等同插件之间已经形成可移植标准。
- **适合人群：** Cursor 用户与希望封装团队工作流的开发者；先检查插件调用的 MCP／命令权限、兼容性及仓库和插件各自的授权条件。

### 6. [Comfy-Org/ComfyUI](https://github.com/Comfy-Org/ComfyUI)

- **数据：** API 约于 10 月 25 日 06:17 查询为 **142,618 stars**；GitHub Trending 周榜于 10 月 24 日 06:58 UTC 显示 **+4,531/7 天**，该快照约 142.4k stars。Python；GPL-3.0；扩散模型工作流界面与后端。证据：[Repository API](https://api.github.com/repos/Comfy-Org/ComfyUI)、[GitHub Trending 周榜快照](https://githubtrending.today/weekly/)。10 月 21 日已报道，本期为持续热度观察。
- **确认用途：** 提供基于节点图的模块化扩散模型 GUI、API 和推理后端。
- **走红原因（推断）：** 节点图能把生成流程显式化、保存和重复执行，适合复杂图像／视频生成链；周增量不能说明所有 custom node 都经过安全审核。
- **适合人群：** 生成式媒体创作者、模型工程师和本地工作流维护者；需分别审查第三方节点代码、模型权重的授权与硬件资源开销。

### 7. [HKUDS/CLI-Anything](https://github.com/HKUDS/CLI-Anything)

- **数据：** API 约于 10 月 25 日 06:17 查询为 **56,845 stars**；GitHub Trending 周榜于 10 月 24 日 06:58 UTC 显示 **+3,303/7 天**，该快照约 56.7k stars。Python；Apache-2.0；Agent 软件接口与生产力工具。证据：[Repository API](https://api.github.com/repos/HKUDS/CLI-Anything)、[GitHub Trending 周榜快照](https://githubtrending.today/weekly/)。10 月 19 日及更早已有报道，本期只记录它再次回升。
- **确认用途：** 项目目标是为各类软件提供 Agent 可调用的 CLI 接口，把原本依赖 GUI 的操作纳入命令行／自动化流程。
- **走红原因（推断）：** Agent 能力的瓶颈逐渐从文本生成转为对既有软件执行可检查操作；可测试的 CLI 比仅依赖视觉点击更适合组合自动化。
- **适合人群：** 希望将桌面或创作软件接入 Agent 工作流的工程团队；按具体目标软件审查命令覆盖、数据破坏副作用、测试质量和维护状态，不应把“支持 Agent”当成已验证可靠。

## 技术趋势与社区偏好

本期榜单延续 Agent 能力资产化：审计 Skill、知识工作插件、编辑器插件与软件 CLI 都把可重复工作流变成仓库内容；增长最明显的日榜项目之一是安全审计 Skill。ComfyUI 与 VoxCPM 代表图像／视频与语音的本地生成工具持续有关注，microduck 则提供一个实体机器人方向的新观察。以上是榜单样本中的社区偏好推断，不等于使用量或质量背书。

本期没有选入 Trend.ondo 周榜异常领先的 morluto/rea：其页面显示 7 天增加 73,160 stars，远超第二名；仅凭这个差距和当前公开资料，不足以确认增长来源或判断星标真实性，因此不纳入质量精选，也不对其作灌星定性。

## 历史归档

报告按 [reports/](https://github.com/Bala-la-la/autonomous-driving-robotics-daily/tree/main/reports/) 下的 YYYY-MM-DD/ 保存，每天保留 arXiv 与 GitHub 两份独立报告。

## 内容标准

- arXiv 报告明确标注提交日期、问题、机制、实验、关注价值与局限；无新稿时标明回溯日期。
- GitHub 报告区分当前仓库元数据、Trending 增量证据和编辑推断，并注明重复观察与统计窗口。
- README 最新一期直接展示两份报告全文；跨期判断维护于 [CATEGORY_SUMMARY.md](CATEGORY_SUMMARY.md)。
