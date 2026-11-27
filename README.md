# 自动驾驶、机器人与开源趋势日报


## 最新一期｜2026-11-28

- [arXiv 独立报告](reports/2026-11-28/arxiv.md)
- [GitHub Trending 独立报告](reports/2026-11-28/github-trending.md)
- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-28

## 日期与证据口径

检索截至北京时间 2026-11-28 06:00。常规 arXiv 最新相关批次仍为 **2026-11-25 UTC v1**；本期从该批次补选 6 篇、均未出现在 11 月 25--27 日报告，因此明确属于回溯而非当日新稿。题目、作者、时间、方法与数值来自 arXiv API 摘要；未能完整核验单位时不臆测。所有性能为作者报告，尚未独立复现。

## 自动驾驶／移动自治

### 1. [Towards Closing the Performance Gap in Cross-Modal Place Recognition](https://arxiv.org/abs/2611.34877)

- **作者／机构／提交：** Ofer Idan、Dan Badur、Yoli Shavit 等；机构未完整披露；v1，2026-11-25 18:38 UTC。
- **问题：** 用自然语言在带地理标注的图像库中定位，适于语言导航；现有视觉—语言检索难区分相似地点，显著落后纯视觉 place recognition。
- **创新与机制：** CrossPlace 先将 DINOv2-B/14 与逐步微调的 BGE-Large 做全局召回，再以轻量 token 级 cross-attention 重排候选；论文系统分解视觉 token 密度、文本编码器容量和任务微调的贡献。
- **实验与关键结果：** 在既有及新增城市级、恶劣天气/照明测试上，相对既有跨模态方法有双位数 Recall@1 提升，并缩小到单模态 VPR 的差距；摘要未披露统一绝对数值。
- **关注价值：** 它把语言描述变为可检索的空间锚点，可为车辆/机器人在无实时视觉查询、需要解释目标地标时提供候选重定位接口。
- **局限／跟进：** 地理标注库与文本描述的时效、歧义和隐私不在 Recall@1 中；应报告闭环导航收益、候选错误的安全回退、跨城市/语言漂移和端侧延迟。

### 2. [One Ocean, Many Tasks: A Data-Grounded Simulation Suite and Benchmark for Marine Robotics](https://arxiv.org/abs/2611.34925)

- **作者／机构／提交：** Shuaijun Liu、Qifu Wen、Xingwei Chen 等；机构未完整披露；v1，2026-11-25 18:58 UTC。
- **问题：** 海洋机器人仿真通常在视觉逼真、吞吐和真实海流/潮汐之间取舍，导致不同导航、巡检和多艇工作流难以比较。
- **创新与机制：** OneOcean 用统一时空海洋环境产品融合水深、数据驱动海流/潮汐及可选污染场；建立从定点、航线、扫描、管线巡检到 2--10 艘协同巡逻/围控/清污的任务阶梯，并固定 run manifest 与度量。
- **实验与关键结果：** 覆盖 3--6 DoF，在不同场景/难度中比较启发式、行为克隆与 LLM planner，揭示它们在数据驱动扰动下的取舍；摘要未给可横比的单一胜率。
- **关注价值：** 将“海况”从背景贴图提升为可复现的动态扰动，适合把规划、控制、能耗和多主体通信放入同一评测记录。
- **局限／跟进：** 再分析海洋数据不保证局地突发流、传感故障和执行器退化一致；需公开数据时间覆盖、sim-to-sea 偏差、通信丢包与真实水池/海试闭环。

## 机器人／具身智能

### 3. [FineDex: Bridging Fine-Grained Human-Object Interaction Generation to Dexterous Humanoid Manipulation](https://arxiv.org/abs/2611.34884)

- **作者／机构／提交：** Yujia Zeng、Yuxin Chen、Yuzhen Song 等；机构未完整披露；v1，2026-11-25 18:40 UTC。
- **问题：** 灵巧操作常把五指简化成夹爪，或复制单个示范，难以表达“哪只手、哪根手指、以何种接触”以及将生成动作落到物理执行。
- **创新与机制：** FineDex 按手、手指和关节物接触的细粒度文本条件生成人体—手—物协同运动；将生成交互当作先验，在物理 digital twin 中由 agent 练习可行接触策略，并在测试时适配而非逐实例重训。
- **实验与关键结果：** 作者报告 HOI 生成质量、细粒度可控性和灵巧成功率均优于比较方法，并在真实灵巧人形机器人上完成部署；摘要未提供统一绝对成功率。
- **关注价值：** 将人类意图、接触先验和物理可执行性拆成可审计层，有助于定位失败来自生成、接触规划还是控制。
- **局限／跟进：** 数字孪生中的摩擦、手部标定和接触力误差会累积；应披露手指级碰撞/滑落、适配试次、真实对象分布与不可逆动作的安全策略。

### 4. [HOG-WAM: Improving Visual Robustness through Future Gradient Prediction](https://arxiv.org/abs/2611.34811)

- **作者／机构／提交：** Boxuan Dong、Yupeng Qian、Ying Wu 等；机构未完整披露；v1，2026-11-25 17:59 UTC。
- **问题：** world-action model 以 RGB 预测未来及动作，观察噪声或腐蚀会直接污染控制表征。
- **创新与机制：** HOG-WAM 从示范图像导出未来 HOG 结构监督；训练期以辅助 HOG DiT 对 RGB feature 做非对称注意力，推理时去掉该模块，保留 FastWAM 的 RGB-to-action 架构和成本。
- **实验与关键结果：** RoboTwin-Plus 混合噪声成功率 **78.86→82.86%**；LIBERO Plus 总体 **74.49→75.26%**、传感噪声 **74.14→78.89%**；四项 Franka 任务平均 clean/noisy 成功率 **40→59%**、**17→24%**。
- **关注价值：** 以不增加部署模块的结构监督增强动作表征，是在既有 VLA/WAM 栈上降低视觉脆弱性的实用路径。
- **局限／跟进：** HOG 对低纹理、反光和遮挡未必稳定，且合成 corruption 不能代替相机曝光/同步/标定故障；需要 p95 延迟、真实传感扰动与接触任务回退数据。

### 5. [Nav4Manip: From Navigation to Dexterous Mobile Manipulation through Co-Evolution](https://arxiv.org/abs/2611.34655)

- **作者／机构／提交：** Yusen Feng、Zixi Kang、Zhijun Yin 等；机构未完整披露；v1，2026-11-25 16:29 UTC。
- **问题：** 到达米级目标并不意味着底座位置和朝向足以操作；导航与操作分训也无法让前者从后者失败中修正。
- **创新与机制：** Nav4Manip-N 学长程导航和 manipulation-aware affordance，并经多任务 co-tuning、拒绝采样微调、RLAIF 迭代；Nav4Manip-M 为下游灵巧操作训练 WAM。Nav-N-Manip benchmark/Pairs 把导航—操作 rollout 与 affordance 监督配对。
- **实验与关键结果：** 作者称在公开 VLN 与 Nav-N-Manip 上达 SOTA，并在真实环境完成多样灵巧移动操作；摘要未给统一数值，不能据此比较真实成功率。
- **关注价值：** 把操作反馈反哺“最后一米”导航，使移动底座的精度、可达性和任务完成不再被割裂评估。
- **局限／跟进：** 需报告导航失败/操作失败各自占比、重定位次数、回退动作和真实长时段碰撞率；RLAIF 的偏好来源与安全边界也应公开。

## 交叉方向：SLAM／3D／世界模型

### 6. [Motion Beyond Pixels: Learning Future Visual Representations for Object-Centric Dynamics](https://arxiv.org/abs/2611.34644)

- **作者／机构／提交：** Chengzhi Zhao、Juelin Li、Zhennan Wang 等；机构未完整披露；v1，2026-11-25 16:24 UTC。
- **问题：** 以 RGB 重建训练的具身世界模型，不一定保留物体级语义与几何运动所需状态。
- **创新与机制：** MotionRep 以 DINO-VAE 压缩时序/通道特征；统一 diffusion transformer 在图像、物体 query point 与语言条件下联合预测未来 DINO 表征和 3D object flow，并用非对称噪声日程让视觉流先于 flow 收敛。
- **实验与关键结果：** 在仿真及真实操作基准上，作者报告相对 pixel baseline 有更佳 3D object-flow 精度和未见场景泛化，推理仅 3 个 denoising step；摘要未列绝对指标。
- **关注价值：** 用“可解释的语义表征 + 3D 流”取代单纯像素未来，可能成为规划/抓取前的紧凑对象动态接口。
- **局限／跟进：** DINO 特征并非物理状态真值，flow 误差如何影响动作尚未量化；应增加遮挡、接触、相机外参漂移、闭环规划收益与计算内存上界。

## 趋势总结

- **移动自治的交接面被前移。** CrossPlace、OneOcean 与 Nav4Manip 都把“到达”拆为检索、环境扰动、最终操作可达性；未来报告应同时给候选错误、控制尾延迟和任务终止证据。
- **具身模型的中间表征更强调结构而非像素。** FineDex 的手指/接触、HOG-WAM 的未来边缘、MotionRep 的 DINO+3D flow 都让控制依赖的状态可单独验证。
- **真实部署仍是短板。** 多数摘要只报相对提升或定性真机展示；摩擦、传感同步、长程重试、失败恢复和人工接管仍需独立统计。


# GitHub 开源趋势晨报｜2026-11-28

## 时间与证据口径

检索于北京时间 2026-11-28 06:00。官方 GitHub Trending 页面本次请求超时，因此**不宣称官方 `stars today`**。以下项目均由 GitHub Search 以创建日期 2026-11-21 至 11-25、按 stars 排序发现，再用 Repository API 复核当前 stars、forks、语言、许可证、创建/更新时间和描述；“增量依据”是从创建至本次查询的可确认累积增长（不等于 24 小时增量），走红原因均为编辑推断。

| 项目 | 当前 stars | 增量依据 | 语言／类别 |
| --- | ---: | --- | --- |
| [EL4CTEO/fast-anything](https://github.com/EL4CTEO/fast-anything) | 4,440 | 11-21 创建至查询累计 | Rust／性能优化 Agent |
| [nexu-io/opengame](https://github.com/nexu-io/opengame) | 2,176 | 11-25 创建至查询累计 | TypeScript／Agent 游戏创作 |
| [alesha-pro/llm.asm](https://github.com/alesha-pro/llm.asm) | 2,131 | 11-25 创建至查询累计 | Assembly／端侧推理教育 |
| [qianyiai/KuroCat](https://github.com/qianyiai/KuroCat) | 1,757 | 11-21 创建至查询累计 | TypeScript／桌面生产力 |
| [sybil-solutions/skill-distill](https://github.com/sybil-solutions/skill-distill) | 997 | 11-21 创建至查询累计 | Python／Skills 工程 |
| [xikhar/papercraft](https://github.com/xikhar/papercraft) | 930 | 11-21 创建至查询累计 | JavaScript／创作 Skill |

## 精选项目

### 1. [EL4CTEO/fast-anything](https://github.com/EL4CTEO/fast-anything)

- **确认信息：** Repository API：**4,440** stars、318 forks，Rust、MIT；2026-11-21 创建，11-27 更新。项目主张只将 profile 发现的热点 5% 迁到 Rust，并让 coding agent 证明新旧实现行为相同，覆盖 Python、JS/TS、Java、Go 等。
- **用途：** 为既有应用选择性做性能剖析、热点重写和等价性验证，而不是全量重写。
- **走红原因（推断）／适合人群：** 它把 Agent 编码从“产出更多代码”转为有性能边界和验证要求的改造流程；适合维护多语言遗留系统、愿意先建立 benchmark 的工程团队。
- **采用提醒：** 自动迁移不能保证语义、并发、FFI 和异常行为等价；应锁定基准/测试、保留人工 code review 与可回滚变更。

### 2. [nexu-io/opengame](https://github.com/nexu-io/opengame)

- **确认信息：** **2,176** stars、355 forks，TypeScript、Apache-2.0；2026-11-25 创建。自述为面向 AI agent 的 Unity/Unreal 式游戏创作平台，可协调 20+ coding agent 并发布 3D/小游戏至多个平台。
- **用途：** 将代码 Agent、游戏模板、构建和多渠道发布连接成创作流水线。
- **走红原因（推断）／适合人群：** “Agent 直接交付可玩的工件”传播性强，且把多 Agent 协作落到具体媒介；适合 game jam、教育和原型团队。
- **采用提醒：** 多平台发布涉及账号、素材版权、未成年人内容和构建供应链；先隔离凭据、审查发布审批和第三方资源许可。

### 3. [alesha-pro/llm.asm](https://github.com/alesha-pro/llm.asm)

- **确认信息：** **2,131** stars、324 forks，Assembly、MIT；2026-11-25 创建。项目包含 12 KB Qwen3-0.6B inference、22 KB 可启动 bare-metal OS 与 32 KB Mini-GPT trainer，均为 x86-64 NASM、无 C/libc/依赖。
- **用途：** 用极小、可读的底层实现学习推理运行时、启动链与训练的资源约束。
- **走红原因（推断）／适合人群：** 在大模型栈日益复杂时，极简实现能帮助开发者理解真正的内存/指令成本；适合系统研究、教育和实验性端侧开发。
- **采用提醒：** 小体积 demo 不代表通用模型性能或安全；裸机代码应在隔离虚拟机/专用硬件上测试，且不要把实验模型用于敏感推理。

### 4. [qianyiai/KuroCat](https://github.com/qianyiai/KuroCat)

- **确认信息：** **1,757** stars、248 forks，TypeScript、MIT；2026-11-21 创建。自述为跨 Win/macOS/Linux/Android 的 3D/2D desktop typing cat 与 AI coding companion，采用 Tauri v2、Rust、MCP，可接 Claude/Codex/DeepSeek/OBS。
- **用途：** 提供可视化桌面陪伴/状态展示，并连接 coding-agent 与 OBS 等本地工具。
- **走红原因（推断）／适合人群：** 它把抽象的 Agent 运行状态变成可见、可分享的桌面交互，覆盖创作者与开发者的轻量生产力场景。
- **采用提醒：** MCP 和桌面集成可能触及本地文件、窗口和 token；需检查每个 server 的权限、网络出口和会话保存策略。

### 5. [sybil-solutions/skill-distill](https://github.com/sybil-solutions/skill-distill)

- **确认信息：** **997** stars、85 forks，Python、MIT；2026-11-21 创建。项目目标是把高质量 Claude Code/Codex 会话蒸馏为开放权重模型可复现任务的 skill。
- **用途：** 将一次性 agent 操作整理为可复用技能资产，服务后续模型或团队工作流。
- **走红原因（推断）／适合人群：** Skill 从提示词转向可积累操作知识是当前 Agent 工程热点；适合有重复工程流程、希望降低昂贵模型调用的团队。
- **采用提醒：** 会话可能含 secrets、私人代码和错误操作；蒸馏前应脱敏、固定输入/工具版本、添加评测与人工审批，避免把偶然成功固化为规范。

### 6. [xikhar/papercraft](https://github.com/xikhar/papercraft)

- **确认信息：** **930** stars、102 forks，JavaScript、MIT；2026-11-21 创建。它是一个用于制作 pop-up papercraft 风格游戏、交互场景、网页和动画的 Agent skill。
- **用途：** 为网页/互动内容提供可重复调用的视觉风格和实现约束。
- **走红原因（推断）／适合人群：** 社区正偏好能直接产生区别化、可见成品的 Skills；适合创意编码、教学和原型演示。
- **采用提醒：** 风格 skill 不等于无版权风险或无障碍合格；需审查素材来源、bundle 体积、移动端性能与生成代码的安全性。

## 技术趋势与社区偏好

- **Agent 工程转向“可验证的改造”。** fast-anything 的性能/等价性约束与 skill-distill 的经验复用，都要求把一次运行变成可测试资产，而非只追求自动化产出。
- **可交付工件仍是强驱动力。** opengame、KuroCat、papercraft 将 Agent 能力落到游戏、桌面交互和网页视觉，社区更愿意传播可直接体验的产物。
- **本地可控与底层透明度回潮。** llm.asm 的热度显示，在云端 Agent 扩张之外，开发者仍关注资源上限、可解释实现和离线实验；这不免除权限、发布和供应链审计。

## 证据链接

- [GitHub Trending 日榜](https://github.com/trending?since=daily)：本次页面连接超时，未用其数值。
- [GitHub Search API](https://docs.github.com/rest/search/search#search-repositories) 与 [Repository API](https://docs.github.com/rest/repos/repos#get-a-repository)：用于发现和复核本期当前 metadata；创建至查询累计 stars 仅作近期增长下界。


## 内容标准与归档

每期 arXiv 按问题、创新、机制、实验、价值和局限选篇；GitHub 区分可核验元数据与编辑推断。历史文件位于 [`reports/`](reports/)，跨期判断见 [分类趋势总结](CATEGORY_SUMMARY.md)。
