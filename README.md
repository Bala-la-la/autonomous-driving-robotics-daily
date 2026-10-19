# 自动驾驶、机器人与开源趋势日报

每日更新中文技术晨报，跟踪最新 arXiv 研究与 GitHub 开源趋势。

## 最新一期｜2026-10-20

- [arXiv 独立报告](reports/2026-10-20/arxiv.md)
- [GitHub Trending 独立报告](reports/2026-10-20/github-trending.md)
- [分类趋势总结](CATEGORY_SUMMARY.md)

# arXiv 自动驾驶、机器人与具身智能晨报｜2026-10-20

## 日期与证据口径

arXiv API 可核验的最新相关批次为 **2026-10-16 UTC 首次提交、10 月 19 日公告**。本期均来自该批次；实验数字来自摘要，价值与局限为编辑判断。

## 自动驾驶与导航

### 1. [SparseMax-dSTL](https://arxiv.org/abs/2610.23837)

- **作者与时间：** Sai Sandeep Damera、Ryan Matheu、John S. Baras、Calin Belta；v1 2026-10-16 17:54 UTC。
- **问题、创新与机制：** 现有 STL 平滑鲁棒性会在长时域梯度消失甚至误估违规；以 sparsemax 构造 min/max 下近似，非负即满足规格，并将梯度集中于违规样本。
- **实验与关键结果：** 单车/机械臂仿真中，80 秒时既有近似违规梯度 **0.22→0.04**，本法为 **1** 且返回满足 margin 的轨迹。**关注价值／局限：** 长时安全优化接口；感知误差、时延和真机动力学待验证。

### 2. [TransNav](https://arxiv.org/abs/2610.23635)

- **作者与时间：** Jianghan Zhu、Zhuo Li、Yanjun Zhang、Jian Sun 等；v1 2026-10-16 15:39 UTC。
- **问题、创新与机制：** 同时处理静态/动态障碍且不依赖专家轨迹；patch 点云编码、有限时域动作序列与点质量动力学自监督联合训练。
- **实验与关键结果：** 摘要报告密集静态场景强表现、动态避障竞争力与机载低成本，未给统一成功率。**关注价值／局限：** 无演示控制有价值；动力学近似、时域截断及高速障碍安全余量需核验。

## 机器人／具身智能

### 3. [Blind Precise Assembly](https://arxiv.org/abs/2610.23849)

- **作者与时间：** Antonia Bronars、Younghyo Park、Kushal Kedia、Pulkit Agrawal；v1 2026-10-16 17:58 UTC。
- **问题、创新与机制：** 仅凭关节位置、速度和动作历史进行接触搜索；在随机部件/抓取/接触的程序化 MuJoCo 装配中训练 RL。
- **实验与关键结果：** 多形状零样本真机插销 **73%** 成功，未见部件泛化优于视觉策略但更慢。**关注价值／局限：** 本体感觉可作接触通道；摩擦、柔顺性和磨损可能破坏迁移。

### 4. [PRIME: Learning Precise Progress Estimation from Imprecise Demonstrations](https://arxiv.org/abs/2610.23769)

- **作者与时间：** Huanqian Wang、Boshi Tang、Botong Xiao、Jie Zhang、Yang Yue、Danhua Tao、Shiji Song、Gao Huang；v1 2026-10-16 17:07 UTC。
- **问题、创新与机制：** 不再将含失误演示的每步都视作推进；以空间接近和视觉一致性建加权状态图，最短路径测地距离区分推进、停滞和回退。
- **实验与关键结果：** 真机/仿真精密操作对次优演示稳定，充电器插入成功率相对 SFT 最高 **5×**。**关注价值／局限：** 失败成为奖励证据；匹配误差、图搜索和稀缺成功终点需审计。

### 5. [Learning Robot Metareasoning](https://arxiv.org/abs/2610.23662)

- **作者与时间：** Lorenzo Magnino、Antonio Marino、Michael Amir、Daigo Shishika、Amanda Prorok；v1 2026-10-16 15:55 UTC。
- **问题、创新与机制：** 固定求解时间难兼顾反应和思考；SMDP 策略以状态、计划和 planner 统计量选择求解预算与开放环动作块。
- **实验与关键结果：** 地面导航、四旋翼和接触操作均胜过固定预算基线。**关注价值／局限：** “何时再算”进入控制状态；最坏算力和紧急回退尚待补齐。

## 交叉方向：空间表示与自治系统

### 6. [StopWatch: Goal Grounding for Object-goal Navigation](https://arxiv.org/abs/2610.23841)

- **作者与时间：** Xinhao Liu、Yunsheng Tian、Yuheng Qiu、Pieter Abbeel、Xi Chen、Guanya Shi、Chen Feng；v1 2026-10-16 17:57 UTC。
- **问题、创新与机制：** VLM 导航会探索却未确认已见目标；把目标可见性与距离显式纳入感知接口，并修正基准标注。
- **实验与关键结果：** 六个基准达 SOTA；真值 grounding 时几乎追平演示 expert。**关注价值／局限：** 失败归因明确；遮挡、光照与开放词表目标的真实可靠性待验证。

### 7. [F-LIVO](https://arxiv.org/abs/2610.23595)

- **作者与时间：** Xinye Dai 等；v1 2026-10-16 15:14 UTC。
- **问题、创新与机制：** 用视觉点—LiDAR 平面约束替代稠密外观地图；弱三角化时从局部平面恢复深度，并按可靠度调节协方差。
- **实验与关键结果：** 文中配置下 CPU、峰值 RSS、RSS 增长率最低，R2LIVE 的平均 RSS 更低。**关注价值／局限：** 紧凑可校准；代码待公开，动态/弱平面边界需核验。

### 8. [Self-Building Labs](https://arxiv.org/abs/2610.23826)

- **作者与时间：** Jiaru Bai、Yuchi Zhao、Han Hao、Miroslav Bogdanovic、Yang Cao、Varinia Bernales、Alán Aspuru-Guzik；v1 2026-10-16 17:48 UTC。
- **问题、创新与机制：** 自驱实验室从预设流程推进到按科学目标构建布局、孪生、机器人 Skills 和工作流。
- **实验与关键结果：** 展示单工作站至多机器人扩展，并以真实量子点合成验证；摘要未给成本/成功率细节。**关注价值／局限：** 环境构建成为 Agent 能力；安全、合规和审批不可省略。

## 趋势总结

安全梯度、任务进度、计算时机、目标确认与跨模态测量正成为显式运行时接口；下一步须同步报告感知误差、最坏时延、回退与真机失败。

# GitHub 开源趋势晨报｜2026-10-20

## 时间与证据口径

GitHub Daily Trending 请求在 20 秒内未返回，因此**不声明 `stars today` 或日榜入选**。以下使用 Search/Repository API 检索 2026-10-13 至 10-19 创建的项目；总 star 为查询时“创建至查询”增长，不是 24 小时增量。用途来自 API 描述/README，走红原因均为编辑推断。

## 精选项目

### 1. [feder-cr/git-ai](https://github.com/feder-cr/git-ai)
- **数据：** 2,443 stars；Go；2026-10-15 创建；Agent 开发工具。
- **确认用途：** 为 AI agents 设计的 Git。**走红原因（推断）：** 版本、恢复和提交成为长期 Agent 接口。**适合人群：** 编码 Agent 团队；核查 Git/CI、签名与合并策略兼容性。

### 2. [Tencent-Hunyuan/Hy-Memory](https://github.com/Tencent-Hunyuan/Hy-Memory)
- **数据：** 954 stars；Python；2026-10-15 创建；Agent 记忆基础设施。
- **确认用途：** 双系统认知记忆 SDK，覆盖聊天长期记忆、工作经验/事实、代码版本 diff 链和本地优先 MemHub。**走红原因（推断）：** 记忆、冲突处理和跨应用检索成为统一运行时。**适合人群：** 跨会话团队；审计数据目录、保留期和删除机制。

### 3. [Leonxlnx/earshot](https://github.com/Leonxlnx/earshot)
- **数据：** 1,492 stars；Python；2026-10-15 创建；多模态 Agent 工具。
- **确认用途：** CPU-only 声音输入、检查与生成工具。**走红原因（推断）：** 低资源音频 I/O 补足媒体测试循环。**适合人群：** 音频自动化团队；检查录音授权和质量。

### 4. [LiCinCan/blender-ai-mcp-addon](https://github.com/LiCinCan/blender-ai-mcp-addon)
- **数据：** 964 stars；Python；2026-10-15 创建；3D/MCP 工具。
- **确认用途：** Blender AI 插件/MCP server，提供场景工具、视觉对话、bpy 脚本和多 Agent 工作流。**走红原因（推断）：** Agent 进入可编辑三维工件。**适合人群：** Blender 自动化团队；最小化文件修改权限并留备份。

### 5. [OpenMOSS/MOSS-Image](https://github.com/OpenMOSS/MOSS-Image)
- **数据：** 941 stars；Python；2026-10-16 创建；图像生成模型。
- **确认用途：** 5B DiT 图像基础模型，聚焦文字渲染、版式和高效微调。**走红原因（推断）：** 版式/文字是生成设计物缺口。**适合人群：** 自托管设计生成；核查权重许可、算力、训练数据和版权。

### 6. [Zfinix/eleven](https://github.com/Zfinix/eleven)
- **数据：** 791 stars；TypeScript；2026-10-13 创建；Agent 原生逆向工具。
- **确认用途：** 让 ACP Agent 读取、重命名和补丁多平台二进制、Android 应用与 GPU kernel。**走红原因（推断）：** 授权软件理解被工具化。**适合人群：** 授权审计/兼容性团队；限制目标、保留溯源并遵守法律。

### 7. [datalab-to/indra](https://github.com/datalab-to/indra)
- **数据：** 676 stars；Python；2026-10-13 创建；文档/OCR 基础设施。
- **确认用途：** CPU OCR，覆盖行检测、CTC、阅读顺序和 Markdown 输出。**走红原因（推断）：** 结构化本地文档入口适合 Agent/RAG。**适合人群：** 文档摄取团队；以多语言、扫描件、表格/公式错误率验收。

### 8. [mistralai/timestral](https://github.com/mistralai/timestral)
- **数据：** 548 stars；Python；2026-10-15 创建；时间序列基础模型。
- **确认用途：** 支持协变量、32,768 步上下文与 CPU 的多变量概率预测。**走红原因（推断）：** 本地预测扩展了 Agent 的传感器与运营决策能力。**适合人群：** 数据/边缘团队；核对权重许可、漂移监控和校准。

## 技术趋势与社区偏好

新仓库热度集中在**持久记忆、版本化动作、可编辑三维工件与低资源数据入口**。这不是官方当日排名；权限、数据来源和许可证仍须逐项验证。

## 历史归档

报告按 [reports/](reports/) 下的 `YYYY-MM-DD/` 保存，保留每日两份独立报告。

## 内容标准

- arXiv 报告明确提交日期、问题、机制、实验、关注价值与局限。
- GitHub 报告区分 Trending 证据、仓库元数据和编辑推断。
- README 最新一期直接展示两份报告正文；跨期判断维护于 [CATEGORY_SUMMARY.md](CATEGORY_SUMMARY.md)。
