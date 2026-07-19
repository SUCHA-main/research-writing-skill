# 科研写作助手 (Research Writing Assistant)

> 📄 English version: [README_EN.md](README_EN.md)

> 本仓库是 [Norman-bury/research-writing-skill](https://github.com/Norman-bury/research-writing-skill) 的公开 fork。原项目、Skill 体系与 3.1.0 版本由旬常（GitHub: Norman-bury）维护；本仓库保留原作者署名与 MIT 许可证，并仅对 fork 的文档和安装说明做维护。详见 [NOTICE.md](NOTICE.md)。

把"论文写作"从一次性聊天，升级成可追踪、可恢复、可复用的工程化协作流程。  
这个 Skill 面向本科生、研究生和早期科研人员，目标很直接：少走弯路，减少返工，把时间花在真正有价值的研究内容上。

## 项目定位

这不是一个"只会润色句子"的提示词包，而是一套模块化的科研写作协作流程。
它会在任务开始前先对齐目标与约束，通过头脑风暴确认论文类型、研究背景、方法和章节结构，再按学科和任务路由到对应技能模块执行。

如果你在做毕业论文、课程项目论文或投稿初稿，这个 Skill 可以提供流程、记录和回写支持，减少对单轮对话记忆的依赖，但不会自动保证论文质量或结论正确性。

## 核心能力

- **头脑风暴**：7轮问答确认论文类型、学科、题目、研究背景、方法、章节结构
- **AI辅助写作**：从选题推进、正文写作、图表生成到投稿前自审，按阶段门禁执行
- **自然表达与信息保真**：原项目称为“去AI化写作”，重点是不把润色等同于压缩，并保留研究对象、数据口径、方法条件、指标含义和结论边界
- **图表生成支持**：Python 负责可复现数据图，Gemini 等生图工具负责流程图、架构图和概念图提示词
- **学科化写作支持**：工科、社科、医学、法学模块分流
- **文献综述支持**：英文检索整合与中文文献整理协作
- **LaTeX模板支持**：根据用户提供的学校/期刊模板协助生成 LaTeX 项目，最终可编译性需在本地环境验证
- **环境安装与排错**：提供 Miniconda、虚拟环境和绘图依赖的安装与排错指引

## 适用平台

本 Skill 采用目录化设计，为以下平台提供配置入口或安装说明；实际发现方式和兼容性仍取决于对应平台版本：

| 平台 | 配置文件 |
|------|----------|
| Claude Code | `.claude-plugin/plugin.json` |
| Cursor | `.cursor-plugin/plugin.json` |
| Codex | `.codex/INSTALL.md` |
| OpenCode | `.opencode/INSTALL.md` |
| Gemini CLI | `GEMINI.md` |
| 其他 | `AGENTS.md` |

## 你会得到什么产物

默认情况下，Skill 产物是项目内文件，不是 Word 成品文件。

| 产物类型 | 默认格式 | 说明 |
|---|---|---|
| 写作正文 | `.md` / 纯文本 / `.tex` | 便于版本管理和后续再加工 |
| 章节文件 | `chapters/*.md` | 每章一个独立文件 |
| LaTeX项目 | `chapters/*.tex` + `main.tex` | 按模板生成的草稿，需本地编译验证 |
| 图表脚本 | `.py` | 可复现图表生成逻辑 |
| 提示词资产 | `.md` | 可复用的翻译、润色、去AI化模板 |

## 去AI化写作边界

这里的“去AI化”只指自然表达与信息保真，不是规避 AI 检测或学术诚信审查。除非用户明确要求缩写，Skill 不应主动删减事实、数据、限定条件和解释句。研究对象、数据范围、样本口径、方法条件、指标含义、实验边界、结论限制和专有名词都应保留，语言调整只服务于表达自然、逻辑清楚和口径稳定。

正文优先使用连续段落，不把论文内容改成项目符号堆砌，也不依赖加粗或斜体制造重点。写作时会避开"首先、其次、最后、此外、另外、接下来、总之"等机械连接词，也会避开"值得注意的是、需要指出的是、重要的是、必须强调的是"等空壳句式。遇到原文信息完整、语序自然但略显啰嗦的情况，只做轻微整理，不为了显得精炼而压掉必要信息。

## 重要边界（务必先看）

1. Skill 默认不会自动生成或直接写入 `.docx`。  
2. Skill 默认不会替你"打开 Word 并排版"，需要你手动复制或用工具转换。  
3. Skill 可以生成适合粘贴进 Word 的纯文本段落，但最终样式（标题级别、页眉页脚、目录、参考文献域）需要你在 Word 端处理。  
4. 规则明确禁止编造文献、数据和实验结果，但输出仍需逐项核验，引用必须可追溯。
5. Skill 不替代导师指导、同行评审、统计或方法学审查，也不保证论文录用。
6. 不得用本 Skill 编造数据或引用，也不得用于规避学术诚信检查。

## 安装

### 方式一：直接下载

下载仓库，解压后把 `research-writing-skill/` 复制到你的论文写作目录就可以用了。

### 方式二：Git Clone

```bash
git clone https://github.com/SUCHA-main/research-writing-skill.git
cd research-writing-skill
```

需要跟踪原始项目时，请访问[上游仓库](https://github.com/Norman-bury/research-writing-skill)。

### 各平台安装

- **Codex**：参考 `.codex/INSTALL.md`
- **OpenCode**：参考 `.opencode/INSTALL.md`
- **其他平台**：将整个目录放入论文项目根目录即可

可选工具脚本有独立依赖：`scripts/scholar_search.py` 需要 `requests`，
`scripts/pdf_parser.py` 需要 `PyMuPDF`。它们不影响 Skill 完整性检查，运行前请在
隔离的 Python 环境中按脚本提示安装。

## 图表示例（上游示例产物）

数据结果图优先由 Skill 生成 Python 脚本，再在本地运行绘制。下面两张上游示例图用于说明训练曲线和指标对比等输出形式，不代表本仓库提供了可复现的实验数据或评测结论。

<p align="center">
  <img src="img/python-miou-comparison.png" alt="本地 Python 绘图示例：验证集 mIoU 对比" width="48%">
  <img src="img/python-training-loss-comparison.png" alt="本地 Python 绘图示例：训练损失对比" width="48%">
</p>

流程图、模型结构图和机制图可以先由 `figures-diagram` 生成提示词，再交给 Gemini 等生图工具绘制。下面两张图是上游仓库保留的提示词生成示例。

<p align="center">
  <img src="img/gemini-federated-calibration-diagram.png" alt="Gemini 生成图示示例：联邦校准流程" width="48%">
  <img src="img/gemini-mask2former-decoder-diagram.png" alt="Gemini 生成图示示例：Mask2Former 解码机制" width="48%">
</p>

## 标准协作流程（推荐）

1. **头脑风暴**：说"我要写论文"，Skill会引导你确认论文类型、题目、研究背景等
2. **章节规划**：确认章节结构后，Skill在 `chapters/` 创建框架
3. **逐章写作**：按章节顺序写作，每章一个文件
4. **图表生成**：需要数据图时，Skill生成Python脚本
5. **自审检查**：使用peer-review技能进行投稿前自审
6. **交付**：手动迁移到Word/LaTeX完成最终排版

## 质量门控

中型或整篇论文任务先使用 `skills/paper-orchestration/` 生成任务包，并在 `plan/progress.md` 记录 capability-use audit。引言和相关工作必须先形成 `refs/evidence-map.md` 或 `plan/evidence-map.md`。实验与结果章节必须先形成 `plan/experiment-protocol.md`、`tables/table-schema.md` 和 `figures/data-manifest.md`。

常用检查命令：

```powershell
powershell -ExecutionPolicy Bypass -File scripts/check_skill_integrity.ps1
powershell -ExecutionPolicy Bypass -File scripts/research_quality_gate.ps1 -ProjectPath <paper-project>
```

## 技能地图

| 场景 | 技能 |
|---|---|
| 入口与路由 | `skills/using-research-writing/` |
| 中型/整篇任务编排 | `skills/paper-orchestration/` |
| 头脑风暴 | `skills/brainstorming-research/` |
| 文献驱动引言/相关工作 | `skills/evidence-driven-writing/` |
| 章节写作 | `skills/writing-chapters/` |
| 实验与结果规划 | `skills/experiment-results-planning/` |
| LaTeX输出 | `skills/latex-output/` |
| 通用写作规范 | `skills/writing-core/` |
| 文科/社科写作 | `skills/writing-humanities/` |
| 医学/生物写作 | `skills/writing-medical/` |
| 法学写作 | `skills/writing-law/` |
| 文献综述 | `skills/literature-review/` |
| 翻译/润色/去AI化 | `skills/prompts-collection/` |
| 投稿前自审 | `skills/peer-review/` |
| 统计分析 | `skills/statistical-analysis/` |
| Python 图表 | `skills/figures-python/` |
| 流程图/架构图 | `skills/figures-diagram/` |
| 环境安装与排错 | `skills/environment-setup/` |

## LaTeX模板使用

如果你有学校或期刊提供的LaTeX模板：

1. 将模板文件（`.cls`, `.sty`, `.tex`等）放入 `latex-templates/` 目录
2. 告诉AI"使用我的LaTeX模板"
3. AI会解析模板结构并生成对应的章节 `.tex` 文件

详细说明见 `latex-templates/README.md`

## 如何把 Markdown 交付到 Word

### 方案 A：手动复制（默认推荐）

1. 让 Skill 输出"纯文本段落版"正文（避免 Markdown 标记）
2. 在编辑器中复制正文并粘贴到 Word
3. 在 Word 中应用学校模板样式（标题、正文、图注、表注）
4. 手动检查公式、参考文献、图表编号与交叉引用

### 方案 B：Pandoc 转换（可选）

如果你本地已安装 Pandoc，可以先确认命令可用：

```bash
pandoc --version
```

最简单的转换方式是把 Markdown 转成 Word：

```bash
pandoc draft.md -o draft.docx
```

如果你已经有学校或期刊的 Word 样式模板，可以使用参考模板生成 `.docx`：

```bash
pandoc draft.md --reference-doc=template.docx -o draft.docx
```

Pandoc 主要解决格式转换和样式继承，不替代最终人工校对。转换后仍需检查标题层级、图表编号、公式、参考文献、页眉页脚和目录域。

## FAQ

### 为什么默认产物不是 Word？

因为科研协作更需要可追踪、可复用、可版本化的文本资产，Markdown 更适合过程迭代。Word 适合最终交付，所以放在最后一步处理更稳妥。

### 可以直接让我"生成最终可提交版本"吗？

可以做接近终稿的内容，但学校模板、目录域、页码、参考文献域、格式细节仍建议在 Word 端完成。

### 这个 Skill 会不会瞎编文献？

规则明确禁止编造引用和数据，但规则本身不能替代核验。使用者仍需检查 DOI、作者、题名、年份、数据来源和原文是否一致。

## 仓库结构

```text
research-writing-skill/
├── SKILL.md                    # 主入口（兼容旧平台）
├── AGENTS.md                   # 通用代理配置
├── GEMINI.md                   # Gemini CLI 配置
├── CHANGELOG.md                # 版本记录
├── .claude-plugin/             # Claude Code 配置
├── .cursor-plugin/             # Cursor 配置
├── .codex/                     # Codex 配置
├── .opencode/                  # OpenCode 配置
├── hooks/                      # 会话启动脚本
│   ├── session-start
│   ├── hooks.json
│   └── hooks-cursor.json
├── img/                        # README 示例图片
├── skills/                     # 技能模块目录
│   ├── using-research-writing/
│   ├── paper-orchestration/
│   ├── brainstorming-research/
│   ├── evidence-driven-writing/
│   ├── writing-chapters/
│   ├── experiment-results-planning/
│   ├── latex-output/
│   ├── literature-review/
│   ├── figures-python/
│   ├── figures-diagram/
│   ├── peer-review/
│   ├── statistical-analysis/
│   ├── verification/
│   ├── environment-setup/
│   ├── prompts-collection/
│   ├── writing-core/
│   ├── writing-humanities/
│   ├── writing-medical/
│   └── writing-law/
├── latex-templates/            # 用户LaTeX模板目录
├── modules/                    # 旧模块（保留兼容）
├── templates/                  # 代码模板
├── plan-template/              # 计划模板
└── scripts/                    # 工具脚本
```

## 版本

- 版本：3.1.0
- 更新日期： 2026-05-10
