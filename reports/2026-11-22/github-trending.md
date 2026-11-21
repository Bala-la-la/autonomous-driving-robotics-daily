# GitHub 开源趋势晨报｜2026-11-22

## 时间与证据口径

检索于北京时间 2026-11-22 06:00。日榜排名与 `+N/日` 来自第三方镜像保存的 **2026-11-21 UTC GitHub Trending 日榜**（`collectedAt` 2026-11-21 21:07 UTC）与同期 GitHub 官方 Trending 页面（全站日榜、周榜及 TypeScript 分区日榜）；`gained` / `stars today` / `stars this week` 为榜单抓取周期内的增星统计，并非两次本地轮询的差值。当前总 star、主语言、许可证、创建时间与仓库自述均经 GitHub Repository API 本次复核。为避免连续重复，排除了昨日（11 月 21 日）已入选的 8 个项目，以及存在红队/漏洞利用敏感标签的高热度榜单条目。文中严格区分**确认信息**与**编辑推断**。

| 项目 | 当前 stars | 榜单增量依据 | 语言／类别 |
| --- | ---: | --- | --- |
| kajisho5/ffmpeg-skill | 9,241 | 周榜第 13，+3,268/周 | Python／Agent 本地媒体技能与 MCP |
| mjmirza/app-store-compliance | 3,337 | 日榜第 12，+724/日 | Shell／合规检查与 Agent Skill |
| jingyaogong/minimind | 68,112 | 日榜第 4，+488/日 | Python／从零训练教学与小模型 |
| zhouxiaoka/autoclip | 12,798 | 日榜第 16，+689/日 | Python／AI 视频剪辑桌面应用 |
| mvanhorn/last30days-skill | 71,947 | 日榜第 10，+566/日（周榜第 5，+3,788/周） | Python／多源趋势研究 Skill |
| google-labs-code/stitch-skills | 11,383 | 日榜第 11，+324/日（周榜第 2，+2,152/周） | TypeScript／开放标准 UI 设计 Skills |
| bendlang/bend | 25,727 | TypeScript 日榜第 5，+58/日 | TypeScript／形式证明与并行语言 |
| nginx/nginx | 32,714 | 日榜第 7，+195/日 | C／Web 服务器与反向代理基础设施 |

## 精选项目

### 1. [kajisho5/ffmpeg-skill](https://github.com/kajisho5/ffmpeg-skill)

- **确认信息：** [Repository API](https://api.github.com/repos/kajisho5/ffmpeg-skill) 当前 **9,241 stars**、835 forks，Python、MIT 协议，创建于 2026-09-03；GitHub 官方周榜第 13、**+3,268/周**。自述提供 42 个 FFmpeg 本地工具、机器可读契约及 MCP 服务器，适配 Claude Code、Cursor 与 Codex，无须云端或 API 密钥，并包含编辑后自检输出机制。
- **用途：** 让编码 Agent 在本地安全调用 FFmpeg 完成剪辑、字幕、画面重框（reframe）、响度规范化与多平台导出。
- **走红原因（推断）／适合人群：** 把容易写错参数的 FFmpeg CLI 封装成带契约和输出自检的 MCP/Skill，直接解决了媒体自动化“调用盲飞”问题；适合多模态工具开发者与内容工程团队。使用前须限制文件系统读写目录，防止路径穿越或误覆写原始素材。

### 2. [mjmirza/app-store-compliance](https://github.com/mjmirza/app-store-compliance)

- **确认信息：** [Repository API](https://api.github.com/repos/mjmirza/app-store-compliance) 当前 **3,337 stars**、208 forks，Shell，创建于 2026-06-06；API 许可证字段为 `NOASSERTION`（仓库 `LICENSE` 文件声明为 OpenRoots Agent License 2.3）。2026-11-21 日榜第 12、**+724/日**。自述整理了 117 条 App Store / Google Play 常见拒审模式与修复、隐私清单与 Data safety 检查、95 个合规截止时间节点及 AI 编码 Agent 专用 Skill。
- **用途：** 作为移动端发版前的自动化合规检查清单与 Agent 可调用审核守卫。
- **走红原因（推断）／适合人群：** 移动应用商店审核规则与 EU AI Act、COPPA 等法规频繁变更，把法务/审核文档转成结构化“pre-submission guard + Agent Skill”切中刚需；适合独立开发者与移动发版团队。须注意非标准许可证（OpenRoots Agent License 2.3）商用限制，并须以苹果/谷歌官方最新审核条款做最终核验，不能将脚本检查等同合规背书。

### 3. [jingyaogong/minimind](https://github.com/jingyaogong/minimind)

- **确认信息：** [Repository API](https://api.github.com/repos/jingyaogong/minimind) 当前 **68,112 stars**、8,902 forks，Python、Apache-2.0 协议，创建于 2024-07-27（近期仍有 PR 合并提交）；2026-11-21 日榜第 4、**+488/日**。自述主打“两小时从 0 训出你的 64M 大模型”，覆盖完整极简训练管线。
- **用途：** 提供从分词、预训练到微调的轻量 LLM 全流程教学与复现代码基线。
- **走红原因（推断）／适合人群：** 随着模型黑盒化和微调脚本复杂化，低成本可单卡复现、代码极简的从零训练项目持续吸引学习者与实验验证；适合入门研究者、高校教学及需要快速验证训练/分词改动的工程师。小模型指标仅作原理验证，不代表百亿级模型的收敛规律。

### 4. [zhouxiaoka/autoclip](https://github.com/zhouxiaoka/autoclip)

- **确认信息：** [Repository API](https://api.github.com/repos/zhouxiaoka/autoclip) 当前 **12,798 stars**、2,070 forks，Python、MIT 协议，创建于 2025-07-08；2026-11-21 日榜第 16、**+689/日**。自述为开源 AI 视频剪辑桌面工具，支持从链接或长视频（播客、访谈、课程）自动切分为短视频并生成字幕、封面与发布文案，同时在 README 声明了 MCP 标识。
- **用途：** 面向创作者和中短视频运营的本地桌面端长转短剪辑与分发文案工作台。
- **走红原因（推断）／适合人群：** 将本地渲染控制与云端模型按量能力结合，且同时提供桌面界面与 MCP 接入潜力；适合自媒体、播客及教育内容团队。部署前应检查第三方视频下载来源版权、云端模型 API 费用上限以及本地临时大文件清理策略。

### 5. [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)

- **确认信息：** [Repository API](https://api.github.com/repos/mvanhorn/last30days-skill) 当前 **71,947 stars**、6,372 forks，Python、MIT 协议，创建于 2026-01-23；2026-11-21 日榜第 10、**+566/日**，周榜第 5、**+3,788/周**。自述为跨 Reddit、X、YouTube、HN、Polymarket 与网页的 30 天近期趋势研究 Agent Skill，并输出带依据的综述。
- **用途：** 为编码或研究型 Agent 注入多社区实时舆情与技术讨论检索能力。
- **走红原因（推断）／适合人群：** 通用大模型知识存在时间截止，把社区信号采集打包成标准化 Skill 可快速补足“近 30 天发生了什么”；适合产品调研、投研辅助及技术布道人员。使用前须评估多平台抓取速率限制、数据源可信度去噪及账号/API 合规要求。

### 6. [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills)

- **确认信息：** [Repository API](https://api.github.com/repos/google-labs-code/stitch-skills) 当前 **11,383 stars**、1,433 forks，TypeScript、Apache-2.0 协议，创建于 2026-01-16；2026-11-21 日榜第 11、**+324/日**，周榜第 2、**+2,152/周**。自述为配合 Stitch MCP server 的 Agent Skills 库，遵循 Agent Skills 开放标准，兼容 Codex、Claude Code、Cursor 等多款工具。
- **用途：** 将 UI/界面设计生成能力作为跨 IDE、跨 Agent 的标准化插件与技能包分发。
- **走红原因（推断）／适合人群：** 开放 Skill 标准降低了不同编码 Agent 生态间的重复适配成本；适合前端工程团队与设计—开发协同工作流搭建者。引入时需核验外部 MCP 服务的数据隐私条款与生成组件的可访问性/代码规范。

### 7. [bendlang/bend](https://github.com/bendlang/bend)

- **确认信息：** [Repository API](https://api.github.com/repos/bendlang/bend) 当前 **25,727 stars**、822 forks，TypeScript、Apache-2.0 协议，创建于 2023-08-29（11 月 18 日仍有运行时与编译器提交）；TypeScript 分区日榜第 5、**+58/日**。自述将 Bend 2 定位为“通过证明拦截 AI 编程错误”的高性能语言，强调 laws、proofs 与面向 CPU/GPU 的高并行编译。
- **用途：** 探索面向 AI 生成代码时代的强类型、线性与形式证明辅助编程语言及并行编译运行时。
- **走红原因（推断）／适合人群：** 当越来越多代码由 Agent 生成，“人类如何用机械可验证的约束与证明检验 AI 输出”成为前沿议题；适合编程语言研究者、编译器工程师与关注形式化验证的架构师。该项目仍处快速演进阶段，导入生产核心链路前需独立验证编译器稳定性与真实算子基准。

### 8. [nginx/nginx](https://github.com/nginx/nginx)

- **确认信息：** [Repository API](https://api.github.com/repos/nginx/nginx) 当前 **32,714 stars**、8,373 forks，C、BSD-2-Clause 协议，创建于 2015-06-23（11 月仍有 `nginx-1.31.9-RELEASE` 等主线维护提交）；2026-11-21 日榜第 7、**+195/日**。官方 NGINX 开源主仓库。
- **用途：** 高性能 HTTP/HTTPS、反向代理、负载均衡、缓存及流媒体/邮件代理基础设施。
- **走红原因（推断）／适合人群：** 大量本地及云端 Agent 服务、MCP 网关和边缘推理节点仍依赖稳定可控的反向代理、TLS 卸载与限流层，经典基础软件在架构回归中被反复纳入技术选型；适合后端、SRE 与 AI 基础设施团队。部署时应优先跟踪官方安全公告与版本分支策略，避免默认配置暴露管理接口或触发限流失效。

## 技术趋势与社区偏好

- **Agent 能力继续向“垂直领域契约 + 开放标准”收敛：** 无论是本地媒体处理的 `ffmpeg-skill`、移动发版守卫 `app-store-compliance`、社区情报 `last30days-skill`，还是跨端 UI 技能 `stitch-skills`，共同特征是把原本松散的自然语言提示词收拢为带工具契约、检查清单或开放 Skill 规范的可复用组件，减少 Agent 执行时的幻觉与参数漂移。
- **验证面与经典底座同步升温：** 从语言级试图用证明约束 AI 错误的 `bend`，到作为基础教学对照的 `minimind` 与支撑流量网关的 `nginx`，社区在追逐应用层效率的同时，也开始重视“AI 产出如何被形式化/确定性规则验证”以及底层运行底座的可控性；高 star 增幅同样不能替代安全沙箱、权限隔离与非标准许可证审查。

## 证据链接

- [GitHub Trending 2026-11-21 日榜归档 JSON](https://githubtrending.today/api/archive/2026-11-21.json)：日榜排名、快照总 star 与 `gained`。
- [GitHub 官方 Trending（日榜）](https://github.com/trending?since=daily)／[（周榜）](https://github.com/trending?since=weekly)／[（TypeScript 日榜）](https://github.com/trending/typescript?since=daily)。
- [GitHub Trending 数据方法](https://githubtrending.today/methodology/)：第三方镜像采集与统计口径说明。
- 各项目当前总 star、主语言与许可证以上述 GitHub Repository API 复核为准；走红原因与趋势研判均为编辑推断。
