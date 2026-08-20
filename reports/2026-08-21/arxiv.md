# arXiv 自动驾驶、机器人与具身智能晨报｜2026-08-21

说明：截至北京时间 2026-08-21 06:00，最新相关批次为 2026-08-19 UTC。

## 自动驾驶

### DA-WAM: Decision-Aligned Future Latents for Driving World Models

链接：https://arxiv.org/abs/2608.19085。问题：驾驶世界模型预测的视觉逼真度与决策价值不一致。机制：以规划/控制目标约束未来潜变量，使生成表征对动作后果更敏感。实验：论文报告在闭环驾驶指标和未来状态预测上优于通用视频预测基线。关注价值：把世界模型训练从“像素准确”转向“决策对齐”。局限/跟进：需核对跨城市、长时域和感知失效下的稳定性。

### USR-Drive: Unified Driving Scene Representation via Joint Denoising of 3D Gaussians and Boxes

链接：https://arxiv.org/abs/2608.19036。问题：3D Gaussian 与目标框通常分开建模，难共享场景几何。机制：联合去噪学习静态/动态实体的统一场景表示。实验：在 3D 检测、场景重建与预测任务上报告竞争力，强调跨任务共享。关注价值：为生成式 3D 场景模型连接感知和规划。局限/跟进：动态遮挡、算力和真实闭环收益仍需实车验证。

## 机器人／具身智能

### PartialBiGrasp: Inferring Hidden Local Geometry for Bimanual Grasping from Partial Views

链接：https://arxiv.org/abs/2608.19188。问题：双臂抓取常只能看到物体局部，遮挡导致接触点不可靠。机制：从部分观测推断隐藏局部几何，再联合生成双手抓取。实验：在双臂抓取基准与实物测试中改善成功率和遮挡场景鲁棒性。关注价值：直接针对双手协作最常见的几何缺失。局限/跟进：复杂柔性物体和受限视角泛化待验证。

### ADEPT: Accelerating Dexterity via Pre-Training and Post-Training using Reinforcement Learning

链接：https://arxiv.org/abs/2608.19182。问题：灵巧操作需要大量示范，训练成本高。机制：先用大规模预训练获得通用动作先验，再以强化学习后训练适配任务。实验：在多项灵巧操作任务上以更少交互达到更高成功率。关注价值：展示“预训练+后训练”向手部操作迁移的可行路径。局限/跟进：奖励设计、真实机器人安全和跨手型迁移仍是瓶颈。

### RoboEdit: Turning Human Manipulation Videos into Scalable Robot Experience

链接：https://arxiv.org/abs/2608.18948。问题：机器人数据采集昂贵，人类视频与机器人动作存在形态鸿沟。机制：编辑人类操作视频并提取可迁移的时序经验，生成规模化训练样本。实验：在多个操作任务中提升策略学习效率。关注价值：扩大廉价视频数据在机器人学习中的作用。局限/跟进：视频到动作的因果对齐和接触动力学仍需真实闭环验证。

### Dream2Reward: Transition-Alignment Reward Models from Positive Demonstrations for Robotic Manipulation

链接：https://arxiv.org/abs/2608.18787。问题：只有成功示范时，如何构造可靠奖励。机制：学习与示范状态转移对齐的奖励模型，减少手工奖励工程。实验：在操作任务中改善稀疏奖励下的策略优化。关注价值：让世界模型/示范数据直接服务于奖励学习。局限/跟进：负例缺失可能造成奖励投机，需要安全约束。

## 交叉方向：长期自治与高效推理

### LT-Mem: Volatility-Aware Spatio-Temporal Memory for Lifelong Scene Understanding

链接：https://arxiv.org/abs/2608.19059。问题：长期运行系统既要记住稳定结构，也要快速更新变化区域。机制：按场景波动性分配时空记忆更新频率。实验：长期场景理解与变化检测优于固定窗口记忆。关注价值：为机器人和车辆的终身地图提供资源感知机制。局限/跟进：极端季节变化、错误记忆累积和存储上限需评估。

### Algorithm-Architecture Co-Design for Efficient VLA Inference via Speculative Inference and Verification

链接：https://arxiv.org/abs/2608.15636。问题：VLA 自回归推理延迟高，难满足机器人实时性。机制：推测生成候选动作，再由验证器筛选，并联合硬件架构优化。实验：报告在保持任务性能的同时降低推理延迟。关注价值：把模型算法和部署硬件作为一个系统优化。局限/跟进：动作分布外时验证开销、不同芯片可移植性待测。

趋势总结：新一批工作共同把“可用性”前移到表示、记忆、奖励和推理接口：驾驶世界模型强调决策对齐，机器人借助部分几何与视频经验扩大数据，长期自治关注波动感知记忆，VLA 则以推测-验证压低闭环延迟。下一步应优先看真实机器人闭环、失败恢复和跨平台复现。
