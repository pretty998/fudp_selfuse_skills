# little_model

本仓库集中存放模型导出文件、模型描述 JSON、用于统计模型 L3 内存占用的解析脚本，以及一组可供 AI 编程 Agent 使用的 Skills。

## 仓库内容

| 路径                           | 说明                                                                                                     |
| ------------------------------ | -------------------------------------------------------------------------------------------------------- |
| `parse_model_json.py`          | 递归解析模型 JSON 中的 `ifm`、`ofm`、`temp` 和 `params` 内存信息，校验张量 `size`，并导出 Excel 汇总表。 |
| `guide.md`                     | 模型 JSON 的字段说明及解析需求记录。                                                                     |
| `*_xprt/`、`*_network/` 等目录 | 模型导出文件、模型元数据及相关数据目录。                                                                 |
| `.agents/skills/`              | 已安装 Skill 的本地内容；每个 Skill 以其目录下的 `SKILL.md` 定义用途和工作流程。                         |
| `skills-lock.json`             | Skill 锁定清单，记录安装的 Skill、上游来源、路径与内容哈希。                                             |

## 模型 JSON 解析

`parse_model_json.py` 默认扫描脚本所在目录下包含顶层 `operator` 列表的 JSON 文件，输出 IFM、OFM、Temp 和 Params 的明细及汇总。

```bash
python3 -m pip install openpyxl
python3 parse_model_json.py
```

也可以指定待扫描目录和输出文件：

```bash
python3 parse_model_json.py /path/to/models -o result.xlsx
```

## Skills 功能索引

以下索引覆盖 `skills-lock.json` 当前记录的 **90 个**已安装 Skill。名称保留英文标识，便于按目录、配置或上游项目检索；功能说明为中文摘要，具体约束以对应的 `SKILL.md` 为准。

### Agent、上下文与评测工程

| Skill                            | 功能                                                                                    |
| -------------------------------- | --------------------------------------------------------------------------------------- |
| `advanced-evaluation`            | 构建高级 LLM 评测体系，包括裁判模型、直接评分、成对比较、评分校准、偏差缓解与置信度。   |
| `bdi-mental-states`              | 使用 BDI（信念、欲望、意图）建模智能体心理状态，支持 RDF 转换、推理轨迹和神经符号集成。 |
| `book-sft-pipeline`              | 将电子书处理为 SFT 训练数据，涵盖文本提取、文学分段、风格数据集、LoRA 与评测。          |
| `comprehensive-research-agent`   | 执行具有验证、错误恢复和透明推理过程的多步骤研究任务。                                  |
| `context-compression`            | 为长周期 Agent 会话做上下文压缩、结构化摘要与持久化交接。                               |
| `context-degradation`            | 诊断并缓解上下文退化问题，如中段遗忘、上下文污染、冲突和注意力失焦。                    |
| `context-engineering-collection` | 提供上下文工程、Agent 编排与生产级 Agent 系统的综合技能集合入口。                       |
| `context-fundamentals`           | 讲解上下文窗口、注意力机制、上下文质量与容量等基础概念。                                |
| `context-optimization`           | 优化上下文效率，包括预算控制、检索范围、缓存策略、观察屏蔽和 Token 成本。               |
| `digital-brain`                  | 支持个人知识与工作流，如内容创作、关系查询、会议准备、目标跟踪和个人品牌管理。          |
| `evaluation`                     | 建立 Agent 评测与质量门禁，包括确定性检查、回归测试、质量量表和生产监控。               |
| `filesystem-context`             | 利用文件系统保存 Agent 的持久草稿、工具输出、临时上下文与交接信息。                     |
| `harness-engineering`            | 设计自主 Agent 运行框架，包括研究循环、日志、回滚、创新门禁与人工审批边界。             |
| `hosted-agents`                  | 设计托管或后台 Agent 基础设施，如沙箱、远程环境、热池、会话持久化和协作。               |
| `latent-briefing`                | 为多 Agent 场景做 KV Cache/潜在表征式上下文压缩与跨 Agent 信息传递。                    |
| `long-horizon-prompting`         | 编写和评估长时间运行 Agent 的启动提示词、成功条件、执行边界和对抗审计机制。             |
| `memory-systems`                 | 设计跨会话语义记忆，包括实体追踪、时效性、图/向量检索和记忆巩固。                       |
| `multi-agent-patterns`           | 设计多 Agent 架构，涵盖上下文隔离、监督者/群体协同、显式交接与并行执行。                |
| `project-development`            | 对 LLM 项目进行顶层决策，如任务适配性、流水线形态、成本估算和结构化输出。               |
| `reasoning-trace-optimizer`      | 通过分析推理轨迹定位 Agent 的工具混淆、指令漂移、上下文问题和性能回退。                 |
| `self-improvement-loops`         | 构建受控的自我改进 Agent 循环，包括失败挖掘、版本化优化、搜索和验收门禁。               |
| `tool-design`                    | 设计 Agent 工具接口、描述、Schema、响应格式、错误恢复信息和工具集合。                   |

### 开发流程、规划与质量保障

| Skill                            | 功能                                                                            |
| -------------------------------- | ------------------------------------------------------------------------------- |
| `brainstorming`                  | 在实现前澄清需求、比较方案、形成设计说明并取得用户确认。                        |
| `dispatching-parallel-agents`    | 将可独立执行的多个任务分派给并行 Agent。                                        |
| `executing-plans`                | 按既有实施计划执行开发任务，并在检查点进行审阅。                                |
| `finishing-a-development-branch` | 在实现和测试完成后，指导分支集成、合并或交付决策。                              |
| `pi-planning-with-files`         | 用文件化计划管理复杂任务，维护 `task_plan.md`、`findings.md` 和 `progress.md`。 |
| `planning-with-files`            | 通过持久化计划文件组织多步骤项目，并支持会话恢复。                              |
| `pr-review`                      | 审核 MiniMax Skills 仓库的 Pull Request，先运行硬性校验再进行质量检查。         |
| `receiving-code-review`          | 严谨地分析收到的代码审查意见，避免未经验证地照单全收。                          |
| `requesting-code-review`         | 在重要实现完成或合并前，请求并准备代码审查。                                    |
| `subagent-driven-development`    | 在当前会话按实施计划分任务调用子 Agent 完成开发。                               |
| `systematic-debugging`           | 面对缺陷、测试失败或异常行为时，按系统化流程定位根因。                          |
| `test-driven-development`        | 在实现功能或修复缺陷前执行测试驱动开发的红—绿—重构循环。                        |
| `using-git-worktrees`            | 在功能开发或执行计划前创建和管理隔离的 Git Worktree。                           |
| `using-superpowers`              | 在会话开始时识别并调用适用的技能与工作流程。                                    |
| `verification-before-completion` | 在宣称完成、修复或通过前，要求运行最新验证命令并基于证据报告结果。              |
| `writing-plans`                  | 将已确认的需求或设计拆解为可执行、可测试的详细实施计划。                        |
| `writing-skills`                 | 创建、修改和验证 Agent Skill 内容。                                             |

### Web、全栈与移动开发

| Skill                           | 功能                                                                            |
| ------------------------------- | ------------------------------------------------------------------------------- |
| `android-native-dev`            | 开发 Android 原生应用，涵盖 Kotlin/Compose、Material 3、可访问性和构建排障。    |
| `flutter-dev`                   | 开发 Flutter 跨平台应用，涵盖 Widget、状态管理、路由、性能与测试。              |
| `frontend-design`               | 为新建或重构的 Web UI 提供有辨识度的视觉设计、排版与审美方向。                  |
| `frontend-dev`                  | 构建完整前端体验，包括高质量 UI、动画、媒体资源、营销文案与交互效果。           |
| `fullstack-dev`                 | 设计全栈应用、后端服务和前后端集成，覆盖 API、认证、上传、实时通信与生产加固。  |
| `ios-application-dev`           | 开发 iOS 应用，覆盖 UIKit、SwiftUI、布局、导航、动态字体、深色模式与无障碍。    |
| `react-native-dev`              | 开发 React Native / Expo 应用，覆盖组件、动画、导航、状态、网络和发布。         |
| `shader-dev`                    | 使用 GLSL 开发视觉特效，如光线步进、SDF、流体、粒子、程序化生成和后处理。       |
| `vercel-composition-patterns`   | 使用可扩展的 React 组合模式设计组件 API，如复合组件、Render Props 和 Context。  |
| `vercel-react-best-practices`   | 依据 Vercel 工程实践优化 React/Next.js 的渲染、数据获取、包体积和性能。         |
| `vercel-react-native-skills`    | 应用 Vercel 的 React Native / Expo 性能实践，优化列表、动画与原生能力。         |
| `vercel-react-view-transitions` | 使用 React View Transition API 实现路由、共享元素和组件状态切换动画。           |
| `web-artifacts-builder`         | 使用 React、Tailwind CSS 和 shadcn/ui 构建多组件、带状态或路由的 Web Artifact。 |
| `web-design-guidelines`         | 审核 Web UI 的设计规范、可访问性和用户体验。                                    |
| `webapp-testing`                | 通过 Playwright 测试本地 Web 应用，验证交互、调试页面并采集浏览器日志。         |

### 文档、办公文件与沟通

| Skill                | 功能                                                                       |
| -------------------- | -------------------------------------------------------------------------- |
| `doc-coauthoring`    | 以收集上下文、分段打磨和读者测试的流程协作编写文档、提案和技术规格。       |
| `docx`               | 创建、读取、编辑和格式化 Word 文档及模板。                                 |
| `internal-comms`     | 编写内部沟通内容，如进展报告、领导力更新、FAQ、事故报告和项目通报。        |
| `markdown-polisher`  | 将粗略文本整理、润色并格式化为适合 GitHub、VS Code 或飞书阅读的 Markdown。 |
| `minimax-docx`       | 使用 OpenXML SDK 创建、编辑、填充或格式化专业 Word 文档。                  |
| `minimax-pdf`        | 创建、填充或重排具备设计一致性和印刷质量的 PDF 文档。                      |
| `minimax-xlsx`       | 创建、读取、分析、编辑和校验 Excel、CSV 等表格文件及财务模型。             |
| `pdf`                | 处理 PDF，包括提取、合并、拆分、旋转、水印、表单填写、加密和 OCR。         |
| `pptx`               | 创建、读取、编辑或合并 PowerPoint 演示文稿和模板。                         |
| `pptx-generator`     | 用 PptxGenJS 或 XML 工作流生成、编辑和解析 PowerPoint 演示文稿。           |
| `prd-author`         | 编写 PRD、功能规格、技术提案、验收标准、发布计划等 Markdown 或飞书文档。   |
| `theme-factory`      | 为文档、幻灯片、报告或 HTML 页面应用预设或定制化视觉主题。                 |
| `writing-guidelines` | 审核文档和散文的写作风格、语气与写作规范符合度。                           |
| `xlsx`               | 处理以电子表格为主要输入或输出的创建、清洗、转换、公式和格式化任务。       |

### 设计、媒体与创意生成

| Skill                    | 功能                                                                            |
| ------------------------ | ------------------------------------------------------------------------------- |
| `algorithmic-art`        | 使用 p5.js 和可复现随机性创作交互式算法艺术。                                   |
| `brand-guidelines`       | 将 Anthropic 官方品牌色彩和排版应用于需要品牌化的产物。                         |
| `buddy-sings`            | 让 Claude Code 的 Buddy 宠物进行歌曲或音乐表演。                                |
| `canvas-design`          | 创建具有设计语言的静态视觉作品，如 PNG、PDF、海报或艺术设计。                   |
| `gif-sticker-maker`      | 将照片、人物、宠物或物体转换为带文字的动画 GIF 贴纸。                           |
| `minimax-music-gen`      | 生成歌曲、音乐、歌词配乐或背景音轨。                                            |
| `minimax-music-playlist` | 基于用户音乐偏好和反馈生成个性化播放列表。                                      |
| `mmx-cli`                | 使用 MiniMax 命令行生成文本、图像、视频、语音和音乐，或进行网页搜索与资源管理。 |
| `slack-gif-creator`      | 创建适合 Slack 使用的动画 GIF，并校验尺寸、质量和动画约束。                     |
| `vision-analysis`        | 使用视觉能力分析图像、截图、图表、线框图，或执行 OCR 与 UI 评审。               |

### 集成、部署与平台工具

| Skill                    | 功能                                                                               |
| ------------------------ | ---------------------------------------------------------------------------------- |
| `claude-api`             | 查询 Claude API / Anthropic SDK 的模型、价格、缓存、流式响应、工具调用和迁移实践。 |
| `composio`               | 通过 Composio CLI 或 SDK 连接和使用大量外部应用服务。                              |
| `deploy-to-vercel`       | 将应用或网站部署到 Vercel，并获取线上部署结果。                                    |
| `mcp-builder`            | 使用 Python FastMCP 或 Node/TypeScript MCP SDK 构建高质量 MCP Server。             |
| `skill-creator`          | 创建或更新扩展 Agent 能力的专业 Skill。                                            |
| `vercel-cli-with-tokens` | 使用 Token 鉴权的 Vercel CLI 完成部署、配置和环境变量管理。                        |
| `vercel-optimize`        | 基于 Vercel 指标分析并优化已部署应用的性能与成本。                                 |

### 模板与多语言变体

| Skill                     | 功能                                                              |
| ------------------------- | ----------------------------------------------------------------- |
| `planning-with-files-ar`  | 文件化计划 Skill 的阿拉伯语版本，用文件化计划组织与跟踪复杂任务。 |
| `planning-with-files-de`  | 文件化计划 Skill 的德语版本，用文件化计划组织与跟踪复杂任务。     |
| `planning-with-files-es`  | 文件化计划 Skill 的西班牙语版本，用文件化计划组织与跟踪复杂任务。 |
| `planning-with-files-zh`  | 文件化计划 Skill 的简体中文版本，用文件化计划组织与跟踪复杂任务。 |
| `planning-with-files-zht` | 文件化计划 Skill 的繁体中文版本，用文件化计划组织与跟踪复杂任务。 |
| `skill-template`          | 创建上下文工程 Agent Skill 时使用的模板。                         |
| `template-skill`          | 通用 Skill 占位模板，供定义名称、描述和触发条件时参考。           |

## 来源与使用说明

- 本地 Skill 内容位于 [`.agents/skills/`](.agents/skills/)；安装清单、上游仓库和内容哈希以 [`skills-lock.json`](skills-lock.json) 为准。
- 本仓库仅索引和使用这些 Skill；各 Skill 的完整说明、许可证、更新策略及适用条款请查阅其上游项目与本地 `SKILL.md`。
- 使用模型文件、解析结果或第三方 Skill 前，请自行确认其对应的许可、数据合规和使用限制。