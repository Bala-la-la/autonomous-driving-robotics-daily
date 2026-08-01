# GitHub 开源趋势晨报｜2026-08-02

说明：查询于 2026-08-02 06:00（Asia/Shanghai）。GitHub Trending HTML 在本次运行中连接超时，因此本期不声称官方 `stars today`；项目来自 GitHub Search 的近 7 日高 Star 候选，当前 Star、创建时间、语言、描述和许可证由 Repository API 核验。“创建以来增量”是创建日至查询时的可确认累计值，不等同 24 小时增量；走红原因均为编辑推断。已排除作弊、账号自动化、描述不清和疑似灌星项目。

## 精选项目

### 1. MoonshotAI/Kimi-K3
- 项目：https://github.com/MoonshotAI/Kimi-K3
- Star：7,817；确认增量：2026-07-27 创建以来 +7,817，较 2026-07-28 本晨报快照 +6,765；语言未标注；类别：开放模型。
- 用途（确认）：Moonshot AI 发布的 Kimi-K3 开放前沿模型项目；Repository API 未给出标准 SPDX 许可证标识。
- 走红原因（推断）：模型发布窗口、开放权重预期与超大 MoE 架构讨论共同推动持续关注；Star 不能替代独立能力和成本评测。
- 适合人群：模型评测、推理系统、中文 Agent 与 MoE 基础设施开发者。

### 2. yc-software/qm
- 项目：https://github.com/yc-software/qm
- Star：4,788；确认增量：2026-07-29 创建以来 +4,788；TypeScript；类别：多 Agent 工作台。
- 用途（确认）：面向工作的多人式 Agent harness，采用 MIT 许可证。
- 走红原因（推断）：社区希望像管理协作团队一样分配、观察和协调多个 Agent，而不仅是并发启动若干命令。
- 适合人群：Agent 编排、软件团队自动化和 TypeScript 平台开发者。

### 3. QwenAudio/qwen-audio-agent
- 项目：https://github.com/QwenAudio/qwen-audio-agent
- Star：1,181；确认增量：2026-07-27 创建以来 +1,181；JavaScript；类别：实时语音 Agent。
- 用途（确认）：让 Agent 持续对话、执行工作并保持在线的实时语音运行时，采用 Apache-2.0 许可证。
- 走红原因（推断）：语音 Agent 的竞争点从一次性 ASR/TTS 调用转向低延迟、可打断、长连接的完整运行时。
- 适合人群：语音助手、实时客服、陪伴式应用和浏览器音频开发者。

### 4. sqliteai/waste
- 项目：https://github.com/sqliteai/waste
- Star：653；确认增量：2026-07-28 创建以来 +653；C；类别：超大模型推理基础设施。
- 用途（确认）：通过从 NVMe 流式读取激活权重，在内存不足时运行 2.78T 参数 Kimi-K3；无依赖、可嵌入，采用 Apache-2.0 许可证。
- 走红原因（推断）：超大稀疏模型发布后，社区立即需要回答“普通硬件能否运行”，存储分层和按需权重流成为可见瓶颈。
- 适合人群：本地推理、存储系统、C 嵌入式运行时与 MoE 性能研究者。

### 5. talivia-group/talivia
- 项目：https://github.com/talivia-group/talivia
- Star：587；确认增量：2026-07-29 创建以来 +587；TypeScript；类别：自托管产品分析。
- 用途（确认）：面向创始人的收入优先分析平台，集成 Web 分析、Session Replay、收入归因和客户收入数据，采用 MIT 许可证。
- 走红原因（推断）：开源分析工具从单纯页面访问统计转向把行为直接连接到收入，同时满足自托管与数据控制需求。
- 适合人群：SaaS 创始人、增长团队、产品分析工程师和自托管用户。

### 6. wassgha/rescript
- 项目：https://github.com/wassgha/rescript
- Star：499；确认增量：2026-07-26 创建以来 +499；TypeScript；类别：浏览器音视频生产力。
- 用途（确认）：在浏览器中按文字稿编辑音频和视频；Repository API 未给出标准 SPDX 许可证标识。
- 走红原因（推断）：文字稿作为剪辑接口降低了非专业用户的时间轴操作成本，也容易接入转写和生成式编辑能力。
- 适合人群：播客、访谈、课程视频、内容团队和 Web 媒体工具开发者。

### 7. deerwork-ai/deer-workflow
- 项目：https://github.com/deerwork-ai/deer-workflow
- Star：374；确认增量：2026-07-26 创建以来 +374；TypeScript；类别：Agent 工作流运行时。
- 用途（确认）：以 TypeScript 保持图工作流编排，并把语义任务委派给可替换 Agent 运行时，采用 MIT 许可证。
- 走红原因（推断）：把确定性控制流与可替换的模型执行层分离，有助于测试、迁移供应商和约束生产行为。
- 适合人群：生产 Agent、工作流平台、模型路由和需要可审计编排的团队。

### 8. microsoft/skill-recorder
- 项目：https://github.com/microsoft/skill-recorder
- Star：307；确认增量：2026-07-29 创建以来 +307；TypeScript；类别：Agent Skill 工具。
- 用途（确认）：微软维护的 Skill Recorder 仓库，采用 MIT 许可证；Repository API 暂未提供更详细描述。
- 走红原因（推断）：把人类操作或成熟工作流录制为可复用 Skill，回应了 Agent 能力资产化和低门槛流程捕获需求。
- 适合人群：Skill 生态、企业流程自动化、Agent 培训和可复用工作流工具开发者。

## 技术趋势与社区偏好
1. Agent 工程继续分层：多 Agent 工作台负责协作界面，图运行时负责确定性编排，Skill Recorder 负责沉淀可复用流程。
2. 实时语音正成为独立运行时问题，重点从模型单项能力转向打断、持续会话、工具执行和延迟管理。
3. 超大 MoE 模型带动存储感知推理，NVMe 流式权重说明社区愿意用速度换取“在现有硬件上可运行”。
4. 浏览器生产力与自托管业务软件保持增长，社区同时奖励 AI 基础设施和能直接完成剪辑、分析等具体工作的开源产品。
5. 本期因 Trending 页面不可达，所有增量判断均保持较长时间窗；下一期应优先恢复官方日榜快照，避免把创建以来累计误读为单日热度。
