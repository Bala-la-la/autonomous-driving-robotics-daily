GitHub Star 飙升项目速览｜2026-07-14

说明：本部分优先参考近 7 天 Trendshift 周榜/项目趋势页判断“升温”，再用 GitHub API 补当前 star、语言和仓库说明。文中“确认信息”来自 GitHub API 或 Trendshift 页面；“推断原因”是基于榜单位置、项目方向和近期更新频率做的判断。

1. MadsLorentzen/ai-job-search
链接：https://github.com/MadsLorentzen/ai-job-search
确认信息：21,871 stars，TypeScript；Trendshift 显示本周约 +4.2k stars。项目是一个本地运行的 AI 求职代理框架，可自动评估岗位、定制简历/求职信、辅助面试准备。
推断原因：求职是非常强的刚需场景，而“fork 后自己掌控数据与流程”正好踩中近期用户对 agent 可控性的偏好。
适合谁关注：做 agent 产品、个人自动化、AI 工作流模板的人。

2. firecrawl/firecrawl
链接：https://github.com/firecrawl/firecrawl
确认信息：150,388 stars，TypeScript；Trendshift 周榜显示本周约 +5.0k stars。项目提供大规模网页搜索、抓取与交互 API，是很多 agent 数据入口和 RAG 管线的底层组件。
推断原因：Agent 和浏览器自动化继续升温，社区开始更重视“稳定抓网页”这种基础设施，而不是只看上层 demo。
适合谁关注：做数据采集、RAG、web agent、开发平台基础设施的人。

3. iOfficeAI/OfficeCLI
链接：https://github.com/iOfficeAI/OfficeCLI
确认信息：16,067 stars，C#；Trendshift 当前周榜高位项目，GitHub Trending 历史页显示其在 2026-06-21 曾冲到全语言第 1。项目提供无需安装 Office 的单二进制 CLI，可供 AI agents 读写 Word/Excel/PowerPoint。
推断原因：AI agent 真正进入办公流后，社区不再满足“能生成文档”，而是需要稳定、可自动化、可嵌入工作流的 Office 原语。
适合谁关注：做办公自动化、文档 agent、企业内工具的人。

4. stablyai/orca
链接：https://github.com/stablyai/orca
确认信息：18,149 stars，TypeScript；Trendshift 项目页显示其在 2026-07-14 进入 GitHub Trending 前列。Orca 是面向并行 coding agents 的 ADE，可在桌面和移动端运行多代理协作。
推断原因：社区热点正从“单个 coding agent”转向“agent fleet orchestration”，Orca 把 IDE/ADE 这一新入口产品化了。
适合谁关注：做编码代理、开发者工具、多人/多代理协同编排的人。

5. Graphify-Labs/graphify
链接：https://github.com/Graphify-Labs/graphify
确认信息：84,558 stars，Python；Trendshift 项目页显示其在 2026-07-13 首次进入 GitHub Trending 前列。项目把代码、SQL、文档、图片、视频等资产转成可查询知识图谱，服务于 Claude Code、Codex 等助手。
推断原因：代码库上下文越来越长，单纯 embedding 检索开始不够用，知识图谱型上下文组织重新受欢迎。
适合谁关注：做 codebase intelligence、GraphRAG、开发者知识管理的人。

6. langchain-ai/openwiki
链接：https://github.com/langchain-ai/openwiki
确认信息：10,913 stars，TypeScript；仓库创建于 2026-06-22，近一天仍在持续更新。项目是一个 CLI，用来为代码库自动生成并维护 agent 文档。
升温依据：Trendshift 月榜和近周趋势页持续收录，说明它不是短时灌星；但公开摘要未给出精确近 7 天增量，因此这里不把涨幅写成确认值。
推断原因：随着更多团队把 agent 接入真实仓库，“给 agent 写文档”正在成为新的工程卫生。
适合谁关注：维护中大型代码库、想提升 agent 上手速度的团队。

7. TencentCloud/CubeSandbox
链接：https://github.com/TencentCloud/CubeSandbox
确认信息：9,973 stars，Rust；项目定位是面向 AI agents 的即时、并发、安全、轻量 sandbox。仓库近一天仍有代码更新。
升温依据：Trendshift 项目趋势页显示它近期上过 GitHub Trending，但当前公开摘要未稳定给出最近 7 天精确增量。
推断原因：agent 真正落地后，执行隔离、并发调度和安全沙箱从“平台细节”变成主卖点。
适合谁关注：做 agent runtime、云执行环境、安全基础设施的人。

8. kyutai-labs/pocket-tts
链接：https://github.com/kyutai-labs/pocket-tts
确认信息：7,500 stars，Python；Trendshift 项目页显示其在 2026-07-07 冲到 GitHub Trending 前列。项目主打“CPU 也能跑、够小够轻”的 TTS。
推断原因：端侧 AI 继续升温，社区对“小模型 + 本地可运行 + 低资源占用”的声音能力需求明显增加。
适合谁关注：做语音助手、边缘设备、机器人语音交互的人。

【简短总结】
1. 社区偏好明显从“单点大模型演示”转向“agent 基础设施 + 工作流原语 + 上下文工程”。
2. 办公自动化、网页抓取、代码库文档化、知识图谱和安全沙箱这几类项目持续升温，说明大家开始补 agent 落地链路里的脏活累活。
3. 另一条明显趋势是端侧与轻量化：像 pocket-tts 这类 CPU 友好项目仍然有较强传播力，说明“能在本地跑”依旧是社区重要偏好。