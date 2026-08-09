# arXiv 自动驾驶与机器人晨报｜2026-08-10

说明：截至北京时间 2026-08-10 06:00，周末后尚无新的常规 arXiv 批次。本期明确回溯 2026-08-05 至 2026-08-06 UTC 提交，并避开上一期已选论文；作者和实验数字以摘要可核验内容为准。

## 自动驾驶

### 1. Talk2Sensors: 3D Visual Grounding in Autonomous Driving via Sensor-Adaptive Physical Cue Matching
- 链接：https://arxiv.org/abs/2608.04568
- 作者／机构：Runwei Guan、Di Tian、Ningwei Ouyang 等；机构未在摘要页披露；提交：2026-08-05。
- 问题：户外 3D 指代需要按语言查询灵活调用相机纹理、LiDAR 几何和 4D 雷达运动信息，现有方法常局限于单一模态。
- 创新与机制：发布含 8,682 条语言指令、20,558 个指代对象的 Talk2Sensors；TSFormer 先用语言路由采样各传感器，再以稀疏保持的模态仲裁细化位置，避免稠密模态淹没关键稀疏信号。
- 实验与价值：相对最强基线提升 8.05 mAP，并在单目 Mono3DRefer 上达到 53.05% Acc@0.5；为车载语言交互和可解释多传感器检索提供基准。
- 局限／跟进：需核验恶劣天气、传感器失准、长尾指令和实时延迟；语言标注规模仍小于常规感知数据集。

### 2. Adaptive-WAM: Quality-Guided Early-Exit Planning from Intermediate Video-Diffusion Features
- 链接：https://arxiv.org/abs/2608.06008
- 作者／机构：Sining Ang、Yuguang Yang、Yan Wang；机构未披露；提交：2026-08-06。
- 问题：驾驶世界动作模型继承视频扩散的多步去噪与解码成本，但部署最终只需要轨迹。
- 创新与机制：在 Wan2.2-5B 的多个 DiT 层挂接轨迹头，以轻量质量评分器决定是否早退；复用缓存隐藏状态，跳过未来视频生成、CFG 循环和 VAE 解码。
- 实验与价值：NAVSIM 自适应单轨迹达到 90.8 PDMS，固定多候选版本 92.6 PDMS；nuScenes 零微调为 0.88 m L2、0.08% 碰撞率。A100 平均 170 ms，比全深度 320 ms 降低约 47%。
- 局限／跟进：170 ms 仍限制高频闭环；质量评分失校准可能在困难场景过早退出，需真实道路与尾部风险验证。

## 机器人／具身智能

### 3. MobileWAM: Bridging World Action Models to Mobile Manipulation with Chain-of-Foresight
- 链接：https://arxiv.org/abs/2608.04657
- 作者／机构：Zehua Fan、Junjie He、Wenxuan Song 等；机构未披露；提交：2026-08-05。
- 问题：现有 WAM 多限于桌面机械臂，移动操作需要同时处理场景级运动、底盘和全身操作。
- 创新与机制：以联合注意力融合视频扩散骨干和轻量动作专家，并用共享／移动／操作三专家按动作意图路由；Chain-of-Foresight 在训练时逐段预测未来潜变量，部署时丢弃生成链，仅保留策略成本。
- 实验与价值：在 ManiSkill-HAB 超过对比移动操作策略，并迁移到真实 ARX Lift2；训练期未来监督不增加部署生成开销，适合长时移动操作。
- 局限／跟进：摘要未给具体增益和控制频率；需检查真实狭窄空间、移动接触耦合和视频先验失配。

### 4. JoyAI-RA 0.5: Scaling Robot Manipulation Learning via Dual Action Alignment
- 链接：https://arxiv.org/abs/2608.05674
- 作者／机构：JoyAI-RA Team；提交：2026-08-06。
- 问题：人类第一视角视频、仿真和真机数据的动作标签缺失或不兼容，直接混合会产生负迁移。
- 创新与机制：隐式动作对齐从视觉变化推断潜动作，让无标签数据训练世界动力学；显式对齐用规范动作表征和相机坐标系分块末端动作统一可靠轨迹，再以双层强化学习兼顾任务适配与基础策略更新。
- 实验与价值：在 AgiBot 真机基准覆盖已见任务和未见变化；得分随人类第一视角预训练数据增加持续上升，尚未出现平台期，支持将弱标注人类视频作为主要扩展轴。
- 局限／跟进：摘要未披露绝对分数和数据规模；需要审计动作推断误差、数据许可、跨相机标定及负迁移边界。

### 5. XEWorld: Can Action-Conditioned World Models Generalize to Unseen Robot Embodiments?
- 链接：https://arxiv.org/abs/2608.05799
- 作者／机构：Yixiang Chen、Jiabing Yang、Yuan Xu 等；机构未披露；提交：2026-08-06。
- 问题：只在训练机器人上评测世界模型，无法区分其学到物理动力学还是记住外观模式。
- 创新与机制：构造物理场景保持一致、仅留出机器人本体的受控测试床，分别检验数值关节动作、像素动作和时空对齐提示的零样本与少样本迁移。
- 实验与价值：系统分析显示现有模型主要按视觉相似性而非运动学相似性泛化；零样本需要强空间锚定，少样本恢复新外观又会遗忘旧本体，为跨本体 WAM 提供更严格诊断。
- 局限／跟进：结论依赖所选架构与受控场景；需扩展到接触、可变相机、真实机器人和长期动力学偏差。

### 6. SkillMemo: Expert-guided Skill Memory Framework for Compositional Embodied Manipulation
- 链接：https://arxiv.org/abs/2608.05970
- 作者／机构：Changyuan Wang、Chubin Zhang、Zhenyu Wu 等；机构未披露；提交：2026-08-06。
- 问题：轨迹数据稀缺使 DP/VLA 难以发现可复用技能结构，并在未见组合任务中泛化。
- 创新与机制：MoE 门控隐式切分长时示范为原子技能，将紧凑表示写入动态情景记忆；推理时检索相关技能并与当前门控分布融合，作为动作预测先验。
- 实验与价值：可同时增强 DP 与 VLA 骨干，在仿真和真机组合任务中报告优于 π0.5，并显示未见任务配置泛化能力。
- 局限／跟进：需核验对专家划分偏差、记忆规模、检索延迟和错误技能召回的敏感性。

## 交叉方向：具身安全

### 7. Hijacking Robots with a Piece of Paper: A Systematic Study of Physical Prompt Injection in VLM-Controlled Robots
- 链接：https://arxiv.org/abs/2608.05715
- 作者／机构：S. Samarakoon、M. V. J. Muthugala、W. K. R. Sachinthana、M. R. Elara；提交：2026-08-06。
- 问题：场景中的人类可读文字会进入 VLM 规划栈，形成视觉侧间接提示注入。
- 创新与机制：定义标牌诱导、任务重定义、权威冒充和冲突注入四类攻击，在三种布局与三种指令精度下进行 5,670 次试验，并比较提示防御、两阶段核验和文字遮蔽。
- 实验与价值：GPT-4o、Gemini 2.5 Flash、Qwen3-VL-32B 的攻击成功率分别为 27.0%、29.4%、5.0%；两阶段核验降低 85%–100%，文字遮蔽在该基准为 100%。
- 局限／跟进：遮蔽会损害必须读取标签的任务；基准集中于分拣，尚需移动机器人、动态攻击、OCR 绕过和端到端安全策略验证。

## 趋势总结
1. 世界动作模型正把“未来预测”留在训练阶段，把中间特征、质量早退和轻量动作专家留给部署，算力开始按决策难度动态分配。
2. 跨数据与跨本体扩展暴露出统一动作空间不足：隐式／显式双对齐、像素动作锚定和本体专属执行接口成为关键。
3. 机器人记忆从保存观测推进到检索原子技能；是否能稳定组合、避免错误召回将决定长时任务价值。
4. 多模态驾驶感知与 VLM 机器人同时面临接口安全问题：前者要防模态淹没，后者要把场景文字视作不可信输入。
