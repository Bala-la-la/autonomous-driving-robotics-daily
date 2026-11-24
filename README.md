# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-11-25

- [arXiv 独立报告](reports/2026-11-25/arxiv.md)
- [GitHub Trending 独立报告](reports/2026-11-25/github-trending.md)
- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-11-25

本期精选 2026-11-23 UTC v1（不是 11 月 25 日当日投稿）。数字均为作者报告；详尽问题、机制、实验和局限见上方独立报告。

## 自动驾驶／移动自治

### 1. [MoOP：Pruning Autonomous Driving VLAs](https://arxiv.org/abs/2611.31240)

Seongchan Kim 等提出以推理/轨迹双目标 Taylor importance 剪枝驾驶 VLA，并跨去噪步保留稳定 MLP channel。39.4% 参数削减仍有竞争性闭环表现，推理 1.37× 加速、峰值显存降 36.6%；长尾 ODD、量化和不安全尾部仍待审计。

### 2. [CoSel：Cooperation as Selection](https://arxiv.org/abs/2611.30918)

Yiping Li 等让独立协同预测器使用 ego/RSU/CAV 证据，仅在风险显露时重选 ego planner 候选。V2Xverse score 70.7（高 7.5 点）；缺失 ego 检测下碰撞 17→19、对照 19→32。候选覆盖与通信失效是边界。

### 3. [P2-TTA：协调感知与规划适配](https://arxiv.org/abs/2611.30739)

Shiyu Fang 等用感知熵、回溯规划一致性、EMA teacher 和历史 loss 拒绝门稳定在线更新。平均更新 0.11‰ 参数、适配 19.9 ms；L2/碰撞/PDMS 恢复 36.4%/30.0%/9.3%，但历史一致性不等于未来安全。

## 机器人／具身智能

### 4. [ACAP：异步 Coding Agents](https://arxiv.org/abs/2611.31205)

Zexin He 等以 persistent agents 并行控制机器人部件，hyper-agent 管物理依赖和控制权。72 次真机 rollout 的时间成本降 28.2%；还需公开冲突、尾延迟、停机与成功率。

### 5. [WeaveVLA：3D Relational Grounding](https://arxiv.org/abs/2611.31126)

Zien Wang 等用稀疏关系图和跨观测 edge state 条件化 VLA。LIBERO-Plus 74.9→82.0%、85.7→87.8%；真机标准/OOD 55.6→70.0%、33.3→53.3%。需验证标定、遮挡和深度误差。

### 6. [Real2Worlds2Real](https://arxiv.org/abs/2611.31098)

Jinzhong Gu 等从视觉和文字构建 twin/digital cousins，以 rollout 反馈改进并沉淀 Skills。作者称多样世界、数据和复用提升迁移，但摘要未给统一绝对指标；物理偏差、资产许可和真机预算仍关键。

## 交叉方向：长期导航

### 7. [GlanceNav](https://arxiv.org/abs/2611.30900)

Anh Dao 等用固定大小流式记忆和反事实回退归因偏航。4B 模型 R2R-CE/RxR-CE 达 71.9%/73.6%，单步 104 ms；还应报告长期错误记忆、真实传感失配和 p95 延迟。

## arXiv 趋势总结

协同和在线更新正收紧为可拒绝、可追溯的运行时层；效率来自能力重要性、物理依赖、关系状态和固定记忆结构。Real2Sim2Real 的关键资产转向可验证流程。

# GitHub 开源趋势晨报｜2026-11-25

11 月 24 日第三方日榜头部已在前几期报道，首位还带红队/漏洞定位，故本期改用 GitHub Search API 选 11 月 18—24 日创建的新仓库。以下 stars 为创建至本次查询的累计值，不是官方日增；元数据由 Repository API 复核，走红原因均为推断。

### 1. [EL4CTEO/fast-anything](https://github.com/EL4CTEO/fast-anything)

3,573 stars，Rust，MIT，11-21 创建。先 profile 再将少量热点交给 Agent 改写 Rust 并验证等价；适合渐进性能改造，需验证异常、并发、数值与 ABI，使用 feature flag 回滚。

### 2. [sybil-solutions/skill-distill](https://github.com/sybil-solutions/skill-distill)

699 stars，Python，MIT，11-21 创建。将成功 coding-agent session 蒸馏为本地模型 Skill；适合内部知识沉淀，前提是脱敏、许可审查和独立复现。

### 3. [w01fb0ss/PiBot](https://github.com/w01fb0ss/PiBot)

557 stars，TypeScript，Apache-2.0，11-21 创建。本地优先多 Agent、computer use、浏览器、MCP 与审批工作台；应设沙箱、审批、allowlist、秘密隔离和动作审计。

### 4. [Developing-Gamer/agent-sim](https://github.com/Developing-Gamer/agent-sim)

538 stars，Rust，Apache-2.0，11-21 创建。Linux 上面向 Agent 的 iOS simulator layer；应核对 SDK/许可、模拟覆盖、真机差异和敏感数据。

### 5. [sous-labs/songe](https://github.com/sous-labs/songe)

595 stars，Python，Apache-2.0，11-20 创建。利用闲置算力训练本地模型；先用非敏感任务验证隔离、功耗/热管理、恢复能力、权重许可与 checkpoint 完整性。

### 6. [lukendeasy/open-diagram](https://github.com/lukendeasy/open-diagram)

386 stars，Python，MIT，11-18 创建。可自检布局的架构图代码构件，输出版本化 SVG；布局正确不保证架构语义正确，仍需来源、无障碍和敏感拓扑审查。

## GitHub 趋势总结

新样本围绕“测量—生成—验证—复用”：profile 后改写、成功轨迹蒸馏、可重置模拟器和可版本化图表都将 Agent 放进可测环境。本地优先不自动降低权限、数据、权重许可和硬件风险。

## 内容标准与归档

每期 arXiv 按问题、创新、机制、实验、价值和局限选篇；GitHub 区分可核验元数据与编辑推断。历史文件位于 [`reports/`](reports/)，跨期判断见 [分类趋势总结](CATEGORY_SUMMARY.md)。
