# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-12

## 日期与证据口径

截至北京时间 2026-11-12 06:00，arXiv API 在 `cs.RO`、`cs.CV`、`cs.AI` 的最新相关 v1 批次为 **2026-11-10 UTC**。以下七篇均为该日新提交，并已同 11 月 10—11 日报告去重；作者、时间、方法与数字均来自 arXiv 元数据和摘要。未能从元数据可靠核验机构时不作推断；摘要数字不等于开放环境安全保证。

## 自动驾驶／移动自治

### 1. [ForeseeDrive: Future-Token Conditioning for Anticipatory Generative Driving](https://arxiv.org/abs/2611.14286)

- **作者／机构／提交：** Shaokai Wu、Xunchu Zhou、Pinzhi Wang、Bo Dong、Yuting Hu 等；arXiv 未列可核验机构；v1 2026-11-10 16:27 UTC。
- **问题与创新：** 生成式驾驶规划即使能采样多条轨迹，后置打分器也无法补回候选集中缺失的规避动作。ForeseeDrive 在候选轨迹生成前，以未来演化 token 直接条件化轨迹几何。
- **机制／结构：** 从日志中的参与者运动、占据变化、路线交互和 TTC 裕度提取 query-indexed token；部署时由当前上下文预测同一 token 空间。零 token 门控残差与 candidate-preservation loss 限制无必要漂移，TTC-margin guard 专门约束安全边界附近的翻转。
- **实验与关键结果：** 摘要报告 NAVSIM navtest 89.2 PDMS、nuScenes 验证平均 L2 0.41 m 与碰撞率 0.05%、Bench2Drive 76.50 driving score；受控诊断显示零 token 时精确 no-op，但 oracle-best 和 TTC 边界仍有局部失败。
- **关注价值：** 把“未来”从事后评分信号前移成可部署的生成接口，针对候选覆盖不足这一闭环规划弱点。
- **局限／跟进：** token 由日志监督，可能继承数据覆盖偏差；需报告实时延迟、极端交互/OOD、候选多样性及真实车端风险收益。

### 2. [HiPFuse: Real-Time LiDAR Semantic Segmentation for Robotic Perception on Edge Devices](https://arxiv.org/abs/2611.14025)

- **作者／机构／提交：** Haiyang Wu、George Vosselman、Ville Lehtola；arXiv 未列可核验机构；v1 2026-11-10 12:57 UTC。
- **问题与创新：** 常规 BEV 聚合会混合一列中不同高度、不同语义的点，边缘设备又受算力限制。HiPFuse 用点特征与按高度分区的 BEV 特征跨尺度交换，兼顾垂直细节和大范围语境。
- **机制／结构：** 固定高度 assignment 保持垂直聚合组，辅助监督初始 BEV；双尺度 BEV context 再加入粗网格上下文，输入仅需一帧 LiDAR。
- **实验与关键结果：** SemanticKITTI/MCD 分别 63.7%/62.5% mIoU，在 Jetson AGX Orin 达 14.2/22.4 FPS；替换固定机器人系统中的语义前端后，两个室外序列平均 ATE RMSE 降 10.6%，SemanticKITTI 接受闭环召回升 8.7 个百分点。
- **关注价值：** 把语义分割指标接到定位/回环后果，且速度超过 10 Hz 扫描率，是感知—长期自治接口的实用证据。
- **局限／跟进：** 数据集与天气/传感器域偏移、Jetson 端到端尾延迟、动态交通参与者及真实车辆闭环安全仍待验证。

## 机器人／具身智能

### 3. [Is Your Robot's Memory Just a Clock? Temporal Shortcuts in Memory-Augmented VLA Policies](https://arxiv.org/abs/2611.14488)

- **作者／机构／提交：** Chubin Zhang、Bo An；arXiv 未列可核验机构；v1 2026-11-10 18:47 UTC。
- **问题与创新：** 许多 memory-VLA 均匀采样历史帧并编码时刻，可能把“时间经过”误作“任务已推进”。论文定义 phantom progress，并隔离其来自记忆索引而非机器人中断本身的因果来源。
- **机制／结构：** 在 RoboMME 计数任务中插入暂停/手腕 fidget 的无效事件，并单独缩放时间戳或移除记忆帧；提出按事件而非时钟索引 memory 的修复方向。
- **实验与关键结果：** 一个任务成功数由 47/50 降至 16/50，另一任务由 44/50 降至 10/50；移除对应记忆帧可恢复。仅去掉时间编码仍无效，而 event indexing 无需重训即可恢复至少一半损失。
- **关注价值：** 为“长历史”提出更精确的失败测试：状态记忆应代表发生了什么，而非固定速率示范中的隐式进度。
- **局限／跟进：** 仅覆盖特定计数任务和已发布设计；应测试视觉停顿、异步执行、任务切换、真实硬件时延与事件检测错漏。

### 4. [One Policy for 100 Household Tasks: Our Solution for the 2026 BEHAVIOR Challenge](https://arxiv.org/abs/2611.14432)

- **作者／机构／提交：** Ilia Larchenko、Gleb Zarin、Atindra Nair、Keerti Manney、Vitaly Kleban 等；arXiv 未列可核验机构；v1 2026-11-10 18:06 UTC。
- **问题与创新：** 长程家居任务常需每任务策略或昂贵评测。该方案以单个基于 π₀.₅ 的 VLA 覆盖 100 个 OmniGibson 任务，并将训练阶段、动作空间、采样与可恢复评测基础设施组合优化。
- **机制／结构：** 用演示 skill annotation 构造语义阶段，按相似旧任务 warm-start 新任务/阶段嵌入；21 维动作匹配遥操作控制，使用方差缩减多样本 flow matching 和按噪声—算力模型选 expert sample 数。14 个任务另由带观测/运动工具的 coding agent 处理。
- **实验与关键结果：** 50 个共享任务 Q 从 0.260 升至 0.371，100 任务总体 Q 0.392；公开提交 Q 0.446、完整任务成功率 27.3%。作者另报 agent 处理的 14 项平均 Q 0.639，学习策略为 0.108；二者并非同一评测设置，不能直接泛化比较。
- **关注价值：** 将统一策略、任务阶段与可恢复诊断合到规模化基准运行链，展示训练预算和评测基础设施同样决定具身结果。
- **局限／跟进：** 结果以模拟器为主，且部分 agent 成绩未进入公开提交；需公开任务逐项方差、推理/云成本、失败恢复和真机迁移。

### 5. [DexSeed: Expanding Human Hand-Object Interactions into Robot Demonstrations for Dexterous Policy Learning](https://arxiv.org/abs/2611.14092)

- **作者／机构／提交：** Huaijin Pi、Zehong Shen、Yong Wang、Kechun Xu、Changpeng Wang 等；arXiv 未列可核验机构；v1 2026-11-10 13:52 UTC。
- **问题与创新：** 灵巧 VLA 依赖昂贵遥操作数据；人手—物数据丰富却难直接转成可执行机器人轨迹。DexSeed 从人类交互扩增出保持抓取关系、可在物理中执行的机器人示范。
- **机制／结构：** 按 grasp mode 和共享语言描述组织源序列，InteractionMesh retargeting 与手臂轨迹增强适配不同手、物体和放置位置；RL 手指控制器生成可执行 rollout，将成功渲染观测与动作用于 VLA 微调。
- **实验与关键结果：** 作者报告相对基线更好的接触保真与全臂执行可靠性；仅用生成示范微调的 VLA 可在真机执行语言指定抓取。摘要未给统一成功率、对象数或 sim-to-real 置信区间。
- **关注价值：** 把人体交互数据转化为可执行、带视觉和动作的训练资产，有望缓解灵巧遥操作的瓶颈。
- **局限／跟进：** retargeting、接触模型和 RL rollout 可能筛掉最难样本；需评估未见手型/物料、遮挡、触觉缺失及生成数据偏差。

### 6. [LaST0.5: A Generalist World Action Model with Interaction-Centric Latent Reasoning](https://arxiv.org/abs/2611.14048)

- **作者／机构／提交：** Xuheng Zhang、Yiming Zhang、Jialin Gao、Hao Chen、Jiaming Liu 等；arXiv 未列可核验机构；v1 2026-11-10 13:15 UTC。
- **问题与创新：** 全局 world-model 表征未必保留机器人—物体局部接触信息，直接转给动作会造成表示目标错配。LaST0.5 在世界预测与动作生成间插入 interaction-centric physical latent。
- **机制／结构：** 在 Mixture-of-Transformers 中以 latent expert 连接 world expert 与 action expert；视觉交互线索监督局部物理推理，并联预测未来表征和 progress value，用 progress consistency 调节执行/未来重采样。预训练数据超 14k 小时。
- **实验与关键结果：** 摘要报告 LIBERO 99.5%，十个 RLBench 任务超过先前 SOTA，并给出长程与灵巧真实操作演示；完整基线、任务分布和真机成功率仍须在正文核验。
- **关注价值：** 不是只增加预测容量，而是把“局部交互”设为可学习中间接口，回应世界模型到控制的错配。
- **局限／跟进：** progress 值误判会触发错误重采样；需报告动作延迟、接触突变、未见工具和跨机器人收益，以及 14k 小时数据的质量/授权构成。

## 交叉方向：世界模型与安全执行

### 7. [LEASH: Stay Safe in Agentic Robotics](https://arxiv.org/abs/2611.14115)

- **作者／机构／提交：** Qinfeng Zhu、Weiguang Zhao、Ke Sun、Xihao Guo、Yunxi Jiang 等；arXiv 未列可核验机构；v1 2026-11-10 14:06 UTC。
- **问题与创新：** 以基础模型直接控制机器人会把提示注入、计划修复与不可逆执行风险并入同一闭环，但现有评测覆盖有限。RoboRisk 以五类风险建立仿真+实体评测，LEASH 在任务、动作和 commit 三层设置安全 gate。
- **机制／结构：** 92 个仿真任务、13 个实体任务覆盖拒绝、计划修复、执行期危险、注入和序列记忆；共享安全策略的 decision model 在视觉上下文中审核任务、每个动作和不可逆操作。
- **实验与关键结果：** 摘要称六个基础模型普遍出现高 harm rate；LEASH 在仿真和实体机器人中降低伤害，同时大体保留完成率且增加较少时间/token 开销，但未给统一 harm、成功率和置信区间。
- **关注价值：** 将“机器人 Agent 安全”从文本对齐推进为按执行时刻、不可逆性与视觉上下文分层审查的系统接口。
- **局限／跟进：** gate 本身会错判或成为延迟瓶颈；需独立复现攻击集、披露拒绝/误放行权衡，并验证断网、传感失效及人类紧急接管。

## 趋势总结

11 月 10 日的新稿将“预测”进一步压缩成可审计的执行接口：ForeseeDrive 在候选生成前写入未来条件，HiPFuse 将语义收益连到定位，LaST0.5/Only memory 研究分别约束交互状态与事件进度，DexSeed 让数据先满足可执行性，LEASH 则为不可逆动作增加门控。共同的下一步不是再叠一层 latent 或 Agent，而是分别报告状态是否正确、何时失效、门控/重采样是否及时，以及在真实扰动下能否安全降级。
