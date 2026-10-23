# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-24

## 日期与证据口径

截至北京时间 2026-10-24 06:20，arXiv API 的相关检索结果最新为 2026-10-22 UTC 提交批次；对 2026-10-23 UTC 以 robot、embodied、manipulation、navigation、SLAM、VLA、world-action、LiDAR、autonomous driving 等关键词和日期范围复查，返回 0 篇。故本期明确回溯至 10 月 22 日 v1 批次，选取 8 篇非重复研究。v1 时间、作者和摘要以 arXiv API 为准；机构来自论文首页，未确认时不推测。论文结论只按其报告的实验范围表述。

## 自动驾驶与自主系统

### 1. [Measuring the Reasoning-Action Coupling in Driving Vision-Language-Action Models through Counterfactuals](https://arxiv.org/abs/2610.30953)

- **作者／机构／提交时间：** Gabriel Manalu、Saad Wazir、Thao Do、Seongah Kim、Hyeontaek Hwang、Tolcha Yalew Kidane、Daeyoung Kim；KAIST 计算机学院；v1 提交于 2026-10-22 09:04:06 UTC。
- **问题与创新：** 驾驶 VLA 以文字说明动作理由，容易被误当成轨迹的忠实解释。本文不以文字是否合理作判断，而用因果干预直接测试推理内容是否改变动作、被提及的视觉原因变化后动作是否跟随。
- **机制／结构：** 在四种驾驶 VLA 上分别修改模型生成的推理文本，并以保留语义的改写和相机输入置空作对照；另从视频帧中反事实移除模型提到的关键对象，再检查新推理与轨迹是否一致。
- **实验与关键结果：** 在 DriveLM 与 PhysicalAI-AV 上，语义改写对轨迹的影响通常小于置空相机输入。移除对象后，模型的理由会更新，但轨迹不总是执行更新后的理由。AutoVLA 在 DriveLM 上有 187/202 个明确左右决策与轨迹方向相符，在 PhysicalAI-AV 为 66/74（89.2%）；Alpamayo-1.5 在 DriveLM 仅 71/155 个样本相符。
- **关注价值：** 把驾驶 VLA 的“可解释性”从语言质量转为可干预的行为一致性，揭示自然语言理由可能只是在事后描述，而非轨迹的有效因果依据。
- **局限／跟进：** 这是离线数据集与经筛选反事实样本上的机制评测，不是驾驶正确性或道路安全基准；对象移除还依赖图像编辑和人工核查。后续应把同类干预接入闭环仿真，测试轨迹重规划、交通参与者互动和真实道路行为。

### 2. [RaSFNet: Ray-aligned and Scan-aware Fusion Network for LiDAR Semantic Segmentation](https://arxiv.org/abs/2610.31186)

- **作者／机构／提交时间：** Chuang Chen；四川大学视觉合成科学国家重点实验室；v1 提交于 2026-10-22 12:35:29 UTC。论文列出的代码地址当前返回 HTTP 404，GitHub 仓库搜索未找到公开匹配项，本期不将其视作可用代码资源。
- **问题与创新：** 投影式点云分割会把不同深度的点压进同一视锥单元，局部卷积也难捕捉跨 LiDAR 扫描区域关系；二维邻近并不意味着三维邻近。RaSFNet 将传感器射线几何与扫描顺序显式写入点—视锥融合。
- **机制／结构：** RAGDE 用射线坐标和多频 Fourier 特征区分单个视锥中的点分布；STAM 按方位角采样顺序组织视锥特征，并以 Mamba 建模长程扫描上下文；RCPFF 用共享距离约束点特征和投影特征的交换，减少跨深度混合。
- **实验与关键结果：** 在 SemanticKITTI 与 nuScenes 验证集分别报告 70.2% 和 77.7% mIoU。距离分段结果显示，50–60 m 区域 mIoU 为 25.4%，接近该区间对比方法最高的 26.0%；消融中去除三个模块都会降低两套数据上的 mIoU/mAcc。
- **关注价值：** 将 LiDAR 的采样物理过程与二维投影网络对齐，方法直接面向自动驾驶和移动机器人常见的远距稀疏点云问题。
- **局限／跟进：** 目前证据是两套验证集上的分割指标，论文未据此证明闭环驾驶收益；仍需报告不同雷达线束/扫描模式、恶劣天气、运行延迟和远距小目标的稳定性。

### 3. [ProTrav: Probabilistic Traversability with Elevation Uncertainty Propagation for Risk-aware Off-road Navigation](https://arxiv.org/abs/2610.30839)

- **作者／机构／提交时间：** Chuanlin Zuo、Miloš Prágr、Arun Kumar Singh、Mohammad Loni、Reza Ghabcheloo；Tampere University、University of Tartu、Volvo Autonomous Solutions；v1 提交于 2026-10-22 07:08:09 UTC。
- **问题与创新：** 越野导航常先用平均高程计算坡度、粗糙度等几何量，再事后膨胀成本；这会丢失空间相关性，也无法正确传播非线性特征中的高程不确定性。ProTrav 将不确定性从地图一直传播到规划代价。
- **机制／结构：** 稀疏变分高斯过程构造连续概率高程场；函数空间采样保留相邻位置的相关性，并对每个地形实现重新计算几何和可通行代价；再将基于均值与标准差的 UCB 风险项接入 MPPI。
- **实验与关键结果：** 仿真山地与负障碍 cliff 场景中，论文报告各地形成功率超过 90%，而确定性基线低于 40%；cliff 案例的单项表格显示 ProTrav 成功率为 80–90%，RRT*/MPPI 对照为 0–20%。另在搭载 Livox Mid-360 和 Jetson AGX Orin 的四轮机器人上完成松土土堆、斜坡和约 125 m waypoint 序列部署；土堆目标 3 次重复试验均到达。
- **关注价值：** 将“地图不确定性”转化成控制器可直接使用的风险代价，而不是仅给感知模块输出置信度；对自动驾驶越野和野外机器人都适用。
- **局限／跟进：** 真实部署规模有限；几何特征无法区分松土与坚实地面，论文中一项因松土摩擦不足的运行由监督者停止。作者还指出概率代价会随观测变化而波动，需改进时间一致性并融合视觉语义。

## 机器人／具身智能

### 4. [DiffDreamer: Coupling World Models with Differentiable Simulation for Agile Quadrotor Control](https://arxiv.org/abs/2610.31617)

- **作者／机构／提交时间：** Fanxing Li、Yuxiang Huang、Shengyang Wang、Fangyu Sun、Shuyu Wu、Tianbao Zhang、Dexin Zuo、Yan Yufei、Danping Zou、Wenxian Yu；v1 提交于 2026-10-22 17:41:13 UTC。作者机构未从可核对首页确认。
- **问题与创新：** 单一 learned rollout 同时建模外部运动和飞行器刚体动力学，会将世界模型偏差传入高速控制；纯可微模拟又难处理移动目标和离散过门奖励。DiffDreamer 将环境预测和本体动力学拆开优化，再让两种 rollout 共享同一动作序列。
- **机制／结构：** RSSM 世界模型预测带历史信息的外部状态，微分模拟器传播显式飞行器状态；critic 路径处理不可微任务奖励，模拟器路径提供可微运动奖励。相对目标／里程计状态帮助学习跟踪移动目标。
- **实验与关键结果：** 仿真中跟踪目标平均距离误差为 0.381 m，低于 Elastic Tracker 的 0.793 m、BPTT 的 0.835 m 和 DreamerV3 的 1.003 m。动态门赛在最大门速 1.0/1.5/2.0 m/s 下，512 步内平均通过 16/12/8 道门；MPC 为 12/4/1。作者还在定制四旋翼上做了 proof-of-concept 真机飞行，Orin NX 机载策略频率超过 100 Hz。
- **关注价值：** 提供一种把可学习的外部世界预测与可微的本体物理模型组合起来的训练结构，兼顾移动目标不确定性和高速控制梯度。
- **局限／跟进：** 真机证据是经系统辨识校准的单一自定义平台验证，尚非广泛跨机型或户外泛化；仿真目标轨迹和物理参数范围也较受控。应补充动态扰动、传感器延迟和长时飞行安全评估。

### 5. [OpenTac: An Open Ecosystem for Customizable, Scalable, and Transferable 3D Tactile Sensing](https://arxiv.org/abs/2610.31661)

- **作者／机构／提交时间：** Ariel Slepyan、Geeta Chandra Raju Bethala、Jiafeng Gu、Anagha Rajendra Dangle、Yinzhe Zhou、Hongyuan Fu、Jade Sim、Tuhin Basu、Xinyi Yin、Md Faizal Karim、Gregory Hager、Homanga Bharadhwaj、Anand Bhattad、Krishna Murthy Jatavallabhula、Nitish V. Thakor；Johns Hopkins University、MIT；v1 提交于 2026-10-22 17:59:06 UTC。
- **问题与创新：** 触觉皮肤往往难按机器人表面定制，也难在多种本体之间复用。OpenTac 同时提供可生成制造文件的传感器设计工具、可变形电阻式触觉皮肤、仿真、跨传感器迁移和自适应读出。
- **机制／结构：** 结构化 bump 将切向力转成不同 taxel 的空间压力差，编码剪切方向；共模响应估计法向力。统一 manifest 描述表面几何、taxel、布线和 bump，贯穿 CAD、仿真与采集。自适应采样仅读取预测的接触区域，以空间完整性换取更新频率。
- **实验与关键结果：** 团队设计并制造 30 多种传感器，在四种真实机器人本体上测试接触反馈控制与操作策略学习。对三轴参考力传感器的估计 R² 为 0.95/0.93/0.96，RMSE 为 0.11/0.16/0.15 N；1024-taxel 皮肤在每次读取 16 个 taxel 时达到 1,286 Hz，相比 67 Hz 全阵列扫描提升 19.2 倍。
- **关注价值：** 让触觉硬件从固定零件转为可由目标机器人几何驱动设计的开放工具链，并展示高频部分读出如何服务接触丰富的控制。
- **局限／跟进：** 作者指出软板不可拉伸，曲面需可展开；电阻式材料有迟滞、漂移和温度依赖。高频采样牺牲空间完整性，当前跨传感器迁移主要评估法向接触形状，尚不能证明完整策略的 sim-to-real 迁移。

### 6. [FocusVLA: Future-Intent Guided Dynamic View Routing for Vision-Language-Action Models](https://arxiv.org/abs/2610.31423)

- **作者／机构／提交时间：** Huixin Xu、Ziya Yu、Peng Li；南京软件技术研究院、中国科学院软件研究所、中国科学院大学、南京邮电大学、河海大学；v1 提交于 2026-10-22 15:25:02 UTC。
- **问题与创新：** 多视角 VLA 常沿用静态融合权重；机械臂早期形成的腕部相机依赖会延续到需要全局规划的阶段。FocusVLA 将未来交互意图作为视角选择的条件，使相机依赖随操作阶段变化。
- **机制／结构：** Future Intent Bridge 从多模态观测和动作历史预测未来操作阶段，生成逐动作步的路由权重，在全局视角和腕部/局部视角特征之间动态分配；可插入现有 VLA，不改视觉编码器、语言模型或动作主干。
- **实验与关键结果：** RoboTwin 2.0 全部 50 项任务上，平均成功率比最强 π0.5 基线高 10.10 个百分点；6 项真机操作任务的成功率从 π0.5 的 71.7% 升至 85.0%，增加 13.3 个百分点。视角遮挡实验也显示静态基线在规划阶段仍过度依赖局部视图。
- **关注价值：** 说明阶段感知不一定要靠更大主干或重写动作模型；将未来意图转换为观察路由即可针对多视角利用率做轻量适配。
- **局限／跟进：** 论文把“未来意图”作为进度表征，作者指出还可加入显式子目标或对象交互状态；跨本体、不同相机布局和更复杂真机环境仍需验证。

## 交叉方向：世界动作模型与多机器人协调

### 7. [UniFlowWAM: A Unified World-Action Model with Visual Semantics and 4D Geometry](https://arxiv.org/abs/2610.30991)

- **作者／机构／提交时间：** Jialin Tian、Zhuofan Li、Xinkai Wang、Bokai Lin、Chenyi Wang、Xinyu Zhan、Cewu Lu、Lixin Yang；上海交通大学 MVIG、上海创新研究院、Noematrix；v1 提交于 2026-10-22 09:35:56 UTC。
- **问题与创新：** 机器人演示含视觉与动作，却没有直接描述动作间场景几何如何变化。UniFlowWAM 将场景级 3D flow 从辅助预测头提升为和视觉、动作并列的第三模态，使世界动作模型同时学习语义和 4D 几何。
- **机制／结构：** 扩散 Transformer 为视觉、动作和 3D flow 各设专家，并用联合注意力交换信息；十种目标配置让同一模型在输入/输出/缺省角色间组合，既可作策略，也能预测前向/逆向动力学与场景流。
- **实验与关键结果：** RoboCasa-GR1 成功率由不带 flow 的基座 52.1% 提升至 56.4%；LIBERO 保持 98.1%，LIBERO-Plus 零样本成功率 87.7%；四项双臂真机操作平均 87.0%，强基线为 68.5%。
- **关注价值：** 把“动作导致怎样的空间变化”纳入策略本身，可统一机器人操作中的未来预测、几何表征与控制。
- **局限／跟进：** 3D flow 由 Track4World 生成伪标签，存在时间不连续；flow 中训练约 1,200 小时，远少于基座的 EI-30k 预训练。后续需扩大联合预训练、量化跟踪误差并检查跨相机/本体迁移。

### 8. [Dispersive Tree Agreements for Multi-Robot Coordination](https://arxiv.org/abs/2610.31540)

- **作者／机构／提交时间：** Shashank A. Deshpande、Blake T. Edwards、Jonathan P. How；MIT 航空航天系；v1 提交于 2026-10-22 16:48:09 UTC。
- **问题与创新：** 多机器人联合轨迹优化常在集中式离线最优与分布式实时安全之间取舍。WarpWeaver 将联合问题改写为各机器人局部前向搜索树上的异步协商，争取在实时预算内得到近优解。
- **机制／结构：** 对可微平坦系统构造分散控制树，以局部整数约束近似机器人间耦合；机器人通过分布式列生成协商共享空间的使用“租金”，以 receding horizon 异步推进。协商静止时可验证近优性，时间到限时可提交当前协议。
- **实验与关键结果：** Dynobench 仿真中，总旅行时间相对集中式离线规划最多降低 22%，相对分布式实时基线最多降低 37%；图连通任务成功率接近任务专用规划器的两倍。六台机器人各自在机载计算机上规划，展示了真实运行实现。
- **关注价值：** 把多机器人协调从“一次性全局求解”变为可协商、可中断、可提交的实时过程，适合通信不稳定且机器人需分布式决策的场景。
- **局限／跟进：** 作者指出，紧密耦合约束（如刚性编队）会令局部树上的整数松弛变弱，不适合所有协调问题；需继续研究非平坦系统、强约束队形与通信延迟下的质量保证。

## 趋势总结

本批材料把“可解释、可导航、可操作”进一步落实为可干预的状态接口：驾驶 VLA 的自然语言理由必须接受反事实检验；越野地图把高程不确定性传入轨迹风险；触觉剪切、动态视角与 3D scene flow 则分别补足接触、阶段和几何变化。控制端同时出现两个结构化方向：Differentiable simulation 为本体动力学提供梯度，分布式树协商为多机器人提供时限内协议。共通缺口是评测覆盖仍小于真实部署空间，尤其是材料/传感变化、跨平台迁移、最坏延迟和闭环失败恢复。
