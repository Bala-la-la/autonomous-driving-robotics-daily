# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪最新 arXiv 研究与 GitHub Star 增长项目。

## 最新一期｜2026-08-19

- [arXiv 独立报告](reports/2026-08-19/arxiv.md)
- [GitHub Trending 独立报告](reports/2026-08-19/github-trending.md)
- [分类趋势总结](CATEGORY_SUMMARY.md)

## arXiv 自动驾驶与机器人晨报｜2026-08-19

说明：截至北京时间 2026-08-19 06:00，最新可用相关批次为 2026-08-17 UTC。

### 自动驾驶

#### Q-based Variational Inverse Reinforcement Learning
链接：https://arxiv.org/abs/2608.16888。以 Q 函数为潜变量联合推断奖励与多峰驾驶偏好，目标是让规划器从示范轨迹恢复可解释的行为分布；摘要报告优于传统 IRL 与行为克隆，真实道路安全结果仍待核验。

#### CaliBench: Are the Stochastic Dynamics of Video World Models Physically Calibrated?
链接：https://arxiv.org/abs/2608.16829。用骰子、二项分布和轮盘等闭式离散结果测试视频世界模型的概率校准，分离可评分率与不确定性误差；提示驾驶世界模型必须校准风险采样，而不只是生成逼真画面。

### 机器人／具身智能

#### Don’t Drop the BATON
链接：https://arxiv.org/abs/2608.16889。冻结 VLA，由语言 Agent 规划、解析原语处理自由空间、VLA 处理接触段，并用 transition-aware memory 记录子任务进出条件，以降低长时操作的指数级探索代价。

#### τ₀-VLA
链接：https://arxiv.org/abs/2608.16885。层级 VLA 在困难子任务上调用世界模型搜索候选再提交，低层策略跨本体执行；训练数据约 40,115 小时，代表测试时计算按风险伸缩的路线。

#### HAF
链接：https://arxiv.org/abs/2608.16837。用层级动作流与谱潜空间强化学习适配通用 VLA 到人形全身 loco-manipulation，降低直接在线调大骨干的成本和风险。

#### FlexWorm
链接：https://arxiv.org/abs/2608.16853。对多节吸附软体机器人进行离散吸附转移与连续形变的混合规划，IKHS 仅在自由块求逆运动学并叠加动作原语，推进复杂曲面导航的几何可行性搜索。

### 交叉方向：安全与长期自治

#### Security of Foundation-Model-Powered Embodied Agents
链接：https://arxiv.org/abs/2608.16843。以首个失守的信任边界组织具身 Agent 安全，覆盖供应链、指令、记忆、物理环境、感知、规划与动作等五层十二类攻击面，为权限和动作前验证提供统一威胁模型。

趋势：VLA 正从固定一次推理转向按风险追加计算；长时操作的核心接口变成过渡条件、失败归因和可恢复记忆；世界模型评价与具身安全都转向可校准、可审计的闭环证据。

## GitHub 开源趋势晨报｜2026-08-19

说明：项目入榜与 `stars today` 来自 GitHub Trending daily 页面；当前 Star、语言和描述由 Repository API 核验，走红原因是编辑推断。

### 精选项目

1. [volcengine/OpenViking](https://github.com/volcengine/OpenViking)：298 stars today，Python；统一 Agent Memory、Knowledge RAG 与 Skills 的上下文数据库。
2. [akitaonrails/ai-memory](https://github.com/akitaonrails/ai-memory)：730 stars today，Rust；编码 CLI 长期记忆与跨 Agent handoff。
3. [mukul975/Anthropic-Cybersecurity-Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills)：726 stars today，Python；映射多套安全框架的 817 个结构化 Skills。
4. [chaitanyagiri/munder-difflin](https://github.com/chaitanyagiri/munder-difflin)：256 stars today，TypeScript；本地多 Agent harness。
5. [bojieli/ai-agent-book](https://github.com/bojieli/ai-agent-book)：556 stars today，Python；Agent 原理、PDF 与章节代码。
6. [jundot/omlx](https://github.com/jundot/omlx)：366 stars today，Python；Apple Silicon continuous batching 与 SSD cache 推理服务。
7. [agalwood/Motrix](https://github.com/agalwood/Motrix)：607 stars today，TypeScript；跨平台下载管理器，适合模型与数据集获取。
8. [basecamp/omarchy](https://github.com/basecamp/omarchy)：411 stars today，Shell；现代化、可控的 Linux 桌面环境。

趋势：Agent 社区继续向上下文数据库、长期记忆、可安装 Skills、多 Agent harness 和端侧推理分层；教程资产与可运行本地产品同时升温，语言分工呈现 Rust 资源效率、Python 研究迭代、TypeScript 终端产品和 Shell 宿主环境的组合。

## 历史归档

报告按 `reports/YYYY-MM-DD/` 保存，保留每日 arXiv 与 GitHub Trending 独立文件。

## 内容标准

- arXiv 报告明确提交日期、问题、机制、实验、关注价值、局限与回溯日期。
- GitHub 报告区分 Trending 页面确认的增量、Repository API 元数据与编辑推断，排除营销、攻击、账号自动化和疑似灌星项目。
- README 最新一期直接展示本次两份报告正文；跨期判断维护于 [CATEGORY_SUMMARY.md](CATEGORY_SUMMARY.md)。
