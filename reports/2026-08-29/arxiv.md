# arXiv 自动驾驶、机器人与具身智能晨报｜2026-08-29

## 检索状态

截至北京时间 2026-08-29 06:00，arXiv Atom API 多次连接被远端重置，无法可靠取得 8 月 26–28 日提交清单。本期不虚构“当日新稿”，以下为公开索引中可追溯、且未在本仓库近两期作为主条目的近期研究线索；提交日期和实验数字待接口恢复后补核。

## 自动驾驶与导航

### Senna: Bridging Large Vision-Language Models and End-to-End Autonomous Driving
- 链接：[公开索引](https://doi.org/10.1007/s11263-026-03002-y)；公开日期 2026-08-25。
- 问题：将 VLM 场景理解稳定转为闭环驾驶动作。
- 机制与创新：把语言视觉语义作为端到端策略条件，连接解释、感知和轨迹生成。
- 实验/价值：索引确认主题，数值待原文核验；适合检验语言推理是否真正改善闭环安全。
- 局限：需核查是否使用特权地图、闭环延迟和跨城市泛化。

### TopV-Nav: Unlocking the Top-View Spatial Reasoning Potential of MLLM for Zero-Shot Object Navigation
- 链接：[公开索引](https://doi.org/10.1007/s11263-026-02996-9)；公开日期 2026-08-25。
- 问题：第一视角 MLLM 在遮挡和长程空间关系上容易漂移。
- 机制与创新：引入俯视空间表征辅助零样本目标导航。
- 实验/价值：公开记录确认题目；关注其空间接口能否减少地图记忆负担。
- 局限：俯视信息可能是特权输入，真实机器人证据待补。

## 机器人与具身智能

### TENDASSIST — DIY Machine Tending Framework for Robotic Assistance
- 链接：[Zenodo 记录](https://doi.org/10.5281/zenodo.22096298)；日期 2026-08-25；Profactor。
- 问题：机床上下料等工业任务集成成本高。
- 机制与创新：以可组合框架封装感知、操作和工艺集成。
- 实验/价值：公开记录确认项目；体现从单点策略到可维护工艺闭环。
- 局限：硬件兼容、安全互锁和失败恢复需技术文档验证。

### Automatic Robotic Assessment and Repair of Fatigue Cracks in Dissimilar Welding Structures
- 链接：[论文索引](https://doi.org/10.1007/s11661-026-08331-8)；日期 2026-08-25；深圳大学。
- 问题：异种材料焊接裂纹检测与修复依赖人工经验。
- 机制与创新：把自动评估、机器人修复和复检串成闭环工艺。
- 实验/价值：索引确认研究方向；对高价值制造的具身闭环有参考意义。
- 局限：传感器、材料泛化和认证证据待全文核查。

### From Harvest to Package: An Autonomous Robot for Integrated Tomato Picking and Bagging
- 链接：[论文索引](https://doi.org/10.35633/inmateh-79-25)；日期 2026-08-25；苏州大学。
- 问题：采摘与包装常被割裂为两个工位。
- 机制与创新：将采摘、转运和装袋集成到同一自治系统。
- 实验/价值：公开索引确认题目；代表户外操作从单任务走向完整作业链。
- 局限：成熟度、遮挡、柔性接触损伤和节拍数据待补。

## 趋势与跟进

近期可核验线索共同指向“语义/空间接口 + 工艺闭环 + 可部署硬件”。由于原始提交清单不可用，本期不更新 arXiv 数量判断；下次运行优先回查 8 月 26–28 日批次并补作者、原始 arXiv 链接和实验表。
