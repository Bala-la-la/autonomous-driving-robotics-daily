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
