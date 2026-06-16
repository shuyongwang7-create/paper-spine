# PaperSpine — 学术论文全流程辅助插件

PaperSpine 是一个面向 **Claude Code** 的学术论文写作插件套件，覆盖从选题构思、文献调研、框架搭建、初稿撰写、改写润色、AI 降重、中英互译、引用管理、LaTeX 排版，到最终审核审计的完整学术写作工作流。

> **核心理念**：不只是一次性生成，而是提供可审计、可迭代、有章可循的学术写作过程。

---

## 目录

- [如何找到和使用它（写给完全没接触过的人）](#如何找到和使用它写给完全没接触过的人)
- [快速开始](#快速开始)
- [11 个 Skill 详解](#11-个-skill-详解)
  - [paper-spine-intake — 选题配置](#paper-spine-intake--选题配置)
  - [paper-spine-research — 文献研究](#paper-spine-research--文献研究)
  - [paper-spine-build — 框架构建](#paper-spine-build--框架构建)
  - [paper-spine-rewrite — 改写润色](#paper-spine-rewrite--改写润色)
  - [paper-spine-humanize — AI 降重](#paper-spine-humanize--ai-降重)
  - [paper-spine-translate — 中英翻译](#paper-spine-translate--中英翻译)
  - [paper-spine-citation — 引用管理](#paper-spine-citation--引用管理)
  - [paper-spine-latex — LaTeX 排版](#paper-spine-latex--latex-排版)
  - [paper-spine-audit — 审核审计](#paper-spine-audit--审核审计)
  - [paper-spine-update — 版本更新](#paper-spine-update--版本更新)
  - [paper-spine-ui — 交互界面](#paper-spine-ui--交互界面)
- [完整工作流](#完整工作流)
- [工作场景示例](#工作场景示例)
- [配置说明](#配置说明)
- [输出目录结构](#输出目录结构)
- [常见问题](#常见问题)
- [环境要求](#环境要求)
- [贡献与反馈](#贡献与反馈)
- [许可](#许可)

---

## 如何找到和使用它（写给完全没接触过的人）

### 先搞明白一件事：这个插件是什么？

简单说，**PaperSpine 是一套给 Claude Code 用的"论文助手工具包"**。

Claude Code 是一款 AI 编程/写作工具（类似 ChatGPT 但更强，由 Anthropic 公司开发）。PaperSpine 就是这个工具里的"学术论文专用扩展包"，安装后能在 Claude Code 里用 `/paper-spine-intake`、`/paper-spine-rewrite` 这样的命令来辅助写论文。

> **类比**：Claude Code 像一台手机，PaperSpine 就是你装的一个 App。装了之后才有那些论文相关的功能。

---

### 情况一：你收到了别人发来的链接，说"装这个就能用"

别人发给你的是这句话：

```
https://github.com/shuyongwang7-create/paper-spine
```

**你需要做的：**

1. **确保你已经安装了 Claude Code**。如果还没有，去 [claude.ai/code](https://claude.ai/code) 下载安装。

2. 打开终端（Windows 上叫"命令提示符"或 PowerShell，Mac 上叫"终端"），输入这一行命令，回车：

   ```bash
   claude plugins install github:shuyongwang7-create/paper-spine
   ```

3. 等待几秒钟，看到 "Installed" 或 "Success" 字样就完成了。

4. 打开 Claude Code，输入 `/paper-spine-intake`，回车，就可以开始用了。

> **就像装一个手机 App 一样，复制这一行命令，粘贴回车，等几秒，完事。**

---

### 情况二：你想自己搜到这个插件

在 Claude Code 里直接搜是搜不到的（因为 PaperSpine 还没加入官方插件商店）。但有几种方法可以找到它：

#### 方法 1：GitHub 上搜索（最简单）

1. 打开 [github.com](https://github.com)
2. 在搜索框输入：**paper-spine** 或 **论文 Claude Code**
3. 搜索结果里第一个就是：`shuyongwang7-create/paper-spine`
4. 点进去，把仓库地址复制下来，然后按"情况一"的步骤安装

#### 方法 2：在 Claude Code 里搜索（需要先"告诉" Claude Code 去哪找）

这一步稍微复杂一点。你需要先在你的电脑上编辑一个配置文件：

1. 找到文件 `~/.claude/settings.json`

   - **Windows**: 在文件管理器地址栏输入 `%USERPROFILE%\.claude\settings.json`
   - **Mac**: 在访达按 `Cmd+Shift+G`，输入 `~/.claude/settings.json`

2. 用记事本或任意文本编辑器打开这个文件。

3. 找到 `"extraKnownMarketplaces"` 这一行（如果没有，就在最后一个 `}` 前面加一个逗号，然后把下面的内容粘贴进去；如果有就在它的大括号 `{}` 里面添加）：

   ```json
   "paper-spine": {
     "source": {
       "repo": "shuyongwang7-create/paper-spine",
       "source": "github"
     }
   }
   ```

   **完整示例（如果你的 settings.json 是空的或很简单）：**

   ```json
   {
     "extraKnownMarketplaces": {
       "paper-spine": {
         "source": {
           "repo": "shuyongwang7-create/paper-spine",
           "source": "github"
         }
       }
     }
   }
   ```

4. 保存文件。

5. 打开终端，输入：

   ```bash
   claude plugins search paper-spine
   ```

   现在你就能搜到它了！找到之后输入：

   ```bash
   claude plugins install paper-spine@paper-spine
   ```

> **一句话总结**：加了上面的配置之后，以后搜 `paper-spine` 就能直接找到了，不需要每次手动输入 GitHub 地址。

#### 方法 3：让更多人能搜到（提交到官方插件市场）

以上只是你个人的配置。如果你想**让全世界所有 Claude Code 用户都能直接搜到**，可以把 PaperSpine 提交到官方插件市场：

| 插件市场 | 描述 | 怎么提交 |
|---|---|---|
| **claude-plugins-official** | Anthropic 官方维护的插件目录 | 去 github.com/anthropics/claude-plugins 提一个 Pull Request，在他们的 `marketplace.json` 文件里加上 PaperSpine 的条目 |
| **claude-code-skills** | 社区最大的技能库（300+ 插件） | 去 github.com/alirezarezvani/claude-skills 提 Pull Request |

提 PR 的大致步骤（会一点 git 的话就能搞）：
1. Fork 目标仓库
2. 在 marketplace.json 里加一条你的插件信息
3. 提交 PR，描述清楚 PaperSpine 是什么、有什么用

提交成功后，**任何 Claude Code 用户**输入 `claude plugins search paper` 都能搜到你。

---

### 常见疑问

**Q: 为什么不能像 ChatGPT 的 GPTs 商店那样直接搜？**
A: Claude Code 的插件系统目前还比较新，没有一个集中的"应用商店"。目前主要靠 GitHub 仓库分发。未来官方可能会推出类似的功能。

**Q: 别人搜到之后怎么用？**
A: 安装后，在 Claude Code 里直接输入以 `/paper-spine-` 开头的命令即可：

```
/paper-spine-intake       → 开始配置论文
/paper-spine-research     → 文献调研
/paper-spine-rewrite      → 改写润色
/paper-spine-humanize     → AI 降重
/paper-spine-translate    → 翻译
/paper-spine-citation     → 引用管理
/paper-spine-latex        → LaTeX 排版
/paper-spine-audit        → 最终审核
```

**Q: 我把 GitHub 链接发给别人，他们怎么装？**
A: 复制下面这行发给对方，对方在终端里粘贴回车即可：

```bash
claude plugins install github:shuyongwang7-create/paper-spine
```

---

## 快速开始

如果你有一篇想投稿的论文草稿，推荐走**标准快速流**：

```
1. /paper-spine-intake    → 配置工作流选项（生成 paper_spine_config.json）
2. /paper-spine-research  → 调研目标期刊要求、学习优秀范文
3. /paper-spine-rewrite   → 基于研究结果改写你的稿件
4. /paper-spine-humanize  → AI 检测降重（如需）
5. /paper-spine-translate → 翻译（如需中→英/英→中）
6. /paper-spine-citation  → 补充和验证引用
7. /paper-spine-latex     → LaTeX 排版
8. /paper-spine-audit     → 最终审核，确保质量过关
```

如果你是**从零开始**写一篇新论文，走**从零构建流**：

```
1. /paper-spine-intake    → 配置（workflow 选 "build_new"）
2. /paper-spine-research  → 文献调研
3. /paper-spine-build     → 从素材构建论文框架
4. /paper-spine-rewrite   → 逐段完善
5. （后续同上）
```

---

## 11 个 Skill 详解

### paper-spine-intake — 选题配置

**功能**：收集并配置 PaperSpine 工作流的所有选项，是整个流程的入口。

**产出**：
- `paper_rewriting_output/paper_spine_config.json`
- `paper_rewriting_output/paper_spine_config.md`

**配置项包括**：
| 选项 | 说明 | 可选值 |
|---|---|---|
| `workflow` | 工作模式 | `rewrite_existing`（改写已有稿件）/ `build_new`（从零构建） |
| `scene` | 投稿场景 | `journal` / `conference` / `competition` / `report_review` |
| `tier` | 处理深度 | `flash`（快速）/ `pro`（深度） |
| `output_language` | 输出语言 | `en` / `zh` |
| `target_name` | 目标期刊/会议名称 | 任意字符串 |
| `materials_dir` | 素材目录路径 | 本地路径 |
| `draft_path` | 已有稿件路径 | 本地路径 |
| `user_motivation` | 研究方向 / 核心论点 | 自由文本 |

**调用方式**：
```
/paper-spine-intake
```

**何时使用**：任何 PaperSpine 工作流开始之前。

---

### paper-spine-research — 文献研究

**功能**：调研目标期刊/会议的要求，下载参考文献，学习优秀范例，准备研究动机选项。

**核心能力**：
- **目标期刊研究**：分析期刊的 scope、风格偏好、格式要求、近期热门话题
- **参考文献采集**：从知网、Google Scholar、arXiv 等来源获取相关文献
- **范例学习**：自动识别优秀论文的结构、论证方式、数据呈现模式
- **动机选项**：基于调研结果，提供多个可行的研究动机方向

**调用方式**：
```
/paper-spine-research
```

**前置条件**：需先完成 `paper-spine-intake` 生成配置文件。

**何时使用**：写作/改写之前，或发现文献综述不够充分时。

---

### paper-spine-build — 框架构建

**功能**：从素材（笔记、数据、提纲）构建论文或报告的完整框架。

**适用场景**：
- 从零开始写论文，手头有实验数据/笔记/提纲
- 有一个大致方向但缺少结构化框架
- 需要快速产出论文初稿骨架

**调用方式**：
```
/paper-spine-build
```

**前置条件**：`paper-spine-intake` 配置（workflow 需设为 `build_new`），以及 `paper-spine-research` 的调研结果。

---

### paper-spine-rewrite — 改写润色

**功能**：基于已有的稿件，结合调研结果、研究动机和段落级写作理由进行深度改写。

**核心流程**（两轮修订）：

**第一轮 — 文献修订（Round 1）**：
- 重写引言和文献综述部分
- 确保文献覆盖全面、逻辑链条完整
- 对齐目标期刊的引用风格

**第二轮 — 期刊修订（Round 2）**：
- 全文段落级改写
- 适应目标期刊的语言风格和结构偏好
- 强化研究动机的表述
- 优化论证逻辑和数据呈现

**调用方式**：
```
/paper-spine-rewrite
```

**前置条件**：`paper-spine-intake` + `paper-spine-research` 都已完成。

---

### paper-spine-humanize — AI 降重

**功能**：通过分级风格约束降低 AI 生成文本的检测率，产出可教学的降重矩阵。

**分级处理**：

| 级别 | 说明 | 适用场景 |
|---|---|---|
| Tier 1 | 基础去模板化 | 快速处理，轻度调整 |
| Tier 2 | 句式多样化 | 标准投稿，平衡质量与效率 |
| Tier 3 | 深度风格注入 | 高要求期刊，最大程度降低检测率 |

**产出**：
- 降重后的文本
- `humanize_matrix.md`：记录了每次降重的策略矩阵，可复现、可教学

**调用方式**：
```
/paper-spine-humanize
```

**何时使用**：论文初稿完成后，尤其在 AIGC 检测比较严格的目标期刊/平台提交前。

---

### paper-spine-translate — 中英翻译

**功能**：生成完整的翻译包（`translation_zh/`），包含所有必需工件的逐行对照翻译。

**产出结构**：
- 全文翻译
- 逐段/逐行对照表
- 术语对照表
- 翻译说明（关键决策和理由）

**调用方式**：
```
/paper-spine-translate
```

**何时使用**：中→英 或 英→中 翻译需求。

---

### paper-spine-citation — 引用管理

**功能**：为引言（Introduction）、讨论（Discussion）和背景声明构建引用支撑库。

**核心能力**：
- 自动检查每一条声明是否有足够的引用支撑
- 识别"孤声明"（无引用支持的断言）
- 按期刊要求格式化引用格式
- 中文引用验证（知网/万方来源核实）

**调用方式**：
```
/paper-spine-citation
```

**何时使用**：稿件基本成型后，提交前的引用检查环节。

---

### paper-spine-latex — LaTeX 排版

**功能**：处理 LaTeX 项目组装、图表定位、引用处理、编译安全清理。

**核心能力**：
- LaTeX 项目文件结构组装
- 图片/表格浮动体位置优化
- `\cite{}` 引用自动补全和验证
- `\label{}` / `\ref{}` 交叉引用检查
- 编译安全清理（删除中间文件、日志文件）

**调用方式**：
```
/paper-spine-latex
```

**何时使用**：文本内容定稿后，需要排版输出 PDF 时。

---

### paper-spine-audit — 审核审计

**功能**：对 PaperSpine 所有产出进行系统性审核，检查遗漏工件、浅层修订、逻辑迁移、声明支撑和翻译覆盖率。

**检查项目**：
- **工件完整性**：所有预期输出文件是否齐全
- **修订深度**：是否存在仅改表面、未动实质的段落
- **逻辑迁移**：论证逻辑在多次修改后是否保持一致
- **声明支撑**：关键声明是否有引用/数据支持
- **翻译覆盖率**：翻译包是否覆盖所有必需内容
- **LaTeX 合规**：LaTeX 源码是否可编译、无语法错误

**调用方式**：
```
/paper-spine-audit
```

**何时使用**：每次重大修改后、投稿/提交前。

---

### paper-spine-update — 版本更新

**功能**：从 GitHub 检查并更新 PaperSpine 插件，同时保留用户的全局配置。

**调用方式**：
```
/paper-spine-update
```

**何时使用**：需要升级到最新版本，或怀疑本地版本有 bug 时。

---

### paper-spine-ui — 交互界面

**功能**：启动 PaperSpine 的外部终端配置 UI，提供可视化的配置体验。

**调用方式**：
```
/paper-spine-ui
```

**平台支持**：Windows（PowerShell）、macOS/Linux（Shell）。

---

## 完整工作流

### 标准流程（改写已有稿件）

```
                    ┌──────────────┐
                    │   intake     │  选题配置：设定目标期刊、语言、深度
                    └──────┬───────┘
                           │
                    ┌──────▼───────┐
                    │  research    │  文献调研：期刊分析、范文学习、参考文献采集
                    └──────┬───────┘
                           │
                    ┌──────▼───────┐
                    │   rewrite    │  改写润色：两轮（文献修订 → 期刊修订）
                    └──────┬───────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
     ┌────────▼───┐  ┌─────▼──────┐  ┌─▼───────────┐
     │  humanize  │  │ translate  │  │  citation    │
     │  AI 降重   │  │  翻译      │  │  引用管理    │
     └────────┬───┘  └─────┬──────┘  └─┬───────────┘
              │            │            │
              └────────────┼────────────┘
                           │
                    ┌──────▼───────┐
                    │    latex     │  LaTeX 排版
                    └──────┬───────┘
                           │
                    ┌──────▼───────┐
                    │    audit     │  最终审核
                    └──────────────┘
```

**update** 可在任意环节调用，用于检查插件更新。

### 从零构建流程

```
intake → research → build → rewrite → [humanize] → [translate] → citation → latex → audit
```

---

## 工作场景示例

### 场景一：中文论文改投英文期刊

```
1. intake:    workflow=rewrite_existing, scene=journal, output_language=en
2. research:  调研目标英文期刊的要求和风格
3. rewrite:   按期刊风格深度改写
4. humanize:  确保英文表达自然，降低 AI 痕迹
5. citation:  调整为英文期刊的引用格式
6. latex:     使用目标期刊模板排版
7. audit:     全面审核后投稿
```

### 场景二：从实验数据到论文初稿

```
1. intake:    workflow=build_new, materials_dir=./实验数据/
2. research:  调研相关文献和范文
3. build:     从数据+笔记构建论文框架
4. rewrite:   Round 1 文献修订 + Round 2 期刊修订
5. humanize:  降重处理
6. citation:  补充引用支撑
7. latex:     排版输出
8. audit:     终审
```

### 场景三：中文投稿（知网/万方）

```
1. intake:    output_language=zh, scene=journal
2. research:  调研中文目标期刊，知网采集参考文献
3. rewrite:   按中文期刊风格改写
4. humanize:  使用中文降重策略（Tier 2+）
5. citation:  启用中文引用验证
6. latex:     中文 LaTeX 模板排版
7. audit:     审核（含中文学术规范检查）
```

---

## 配置说明

所有配置集中在 `paper_rewriting_output/paper_spine_config.json`：

```json
{
  "workflow": "rewrite_existing",
  "scene": "journal",
  "tier": "pro",
  "output_language": "en",
  "target_name": "Nature Communications",
  "materials_dir": "./my_materials",
  "draft_path": "./my_draft.docx",
  "user_motivation": "探究深度学习在医学影像诊断中的可解释性问题",
  "official_urls": ["https://www.nature.com/ncomms/"]
}
```

| 字段 | 类型 | 说明 |
|---|---|---|
| `workflow` | string | `rewrite_existing` 或 `build_new` |
| `scene` | string | `journal` / `conference` / `competition` / `report_review` |
| `tier` | string | `flash`（快速模式）/ `pro`（深度模式） |
| `output_language` | string | `en` / `zh` |
| `target_name` | string | 目标期刊或会议名称 |
| `materials_dir` | string | 素材目录路径（build_new 模式必需） |
| `draft_path` | string | 已有稿件路径（rewrite_existing 模式必需） |
| `user_motivation` | string | 研究方向/核心论点描述 |
| `official_urls` | array | 目标期刊官网链接 |

---

## 输出目录结构

完成完整流程后，`paper_rewriting_output/` 下的典型目录结构：

```
paper_rewriting_output/
├── paper_spine_config.json          # 工作流配置
├── paper_spine_config.md            # 配置可读版
├── research/                        # 研究调研产出
│   ├── target_journal_analysis.md
│   ├── exemplar_dossier.md
│   └── references/
├── rewritten/                       # 改写产出
│   ├── round1_literature_revision/
│   └── round2_journal_revision/
├── humanize_matrix.md               # AI 降重矩阵
├── translation_zh/                  # 翻译包（如启用翻译）
│   ├── full_translation.md
│   ├── row_by_row.md
│   └── glossary.md
├── latex/                           # LaTeX 项目
│   ├── main.tex
│   ├── figures/
│   └── references.bib
└── audit/                           # 审核报告
    └── audit_report.md
```

---

## 常见问题

### Q: 一定要走完所有 11 个 skill 吗？

不需要。最小可用路径只需 3 个：`intake → rewrite → audit`。其他的按需选用。

### Q: flash 和 pro 模式有什么区别？

- **flash**：快速处理，适合初稿迭代、内部讨论稿
- **pro**：深度处理，每一步都有更详细的产出和更多的审计点，适合正式投稿

### Q: 可以在流程中间修改配置吗？

可以。直接编辑 `paper_spine_config.json`，或重新运行 `paper-spine-intake` 覆盖配置。

### Q: 各 skill 之间如何传递数据？

通过 `paper_rewriting_output/` 目录下的文件传递。每个 skill 读取前序 skill 的产出，追加自己的产出。

### Q: 支持非 LaTeX 的排版方式吗？

目前排版环节仅支持 LaTeX。但前面的所有环节（intake → citation）不依赖 LaTeX，你可以用 Word 或其他工具完成排版。

### Q: 插件更新会影响我的论文数据吗？

不会。`paper_rewriting_output/` 目录在你的项目文件夹中，与插件安装位置无关。更新插件不影响已有产出。

---

## 环境要求

| 依赖 | 版本要求 | 说明 |
|---|---|---|
| Claude Code | ≥ v2.1.144 | 插件系统支持 |
| Python | ≥ 3.10 | 脚本工具运行时 |
| Git | 任意 | 插件安装 |

Python 脚本仅使用标准库，无需额外安装 pip 包。

---

## 贡献与反馈

- **Issues**: https://github.com/shuyongwang7-create/paper-spine/issues
- **Pull Requests**: 欢迎提交改进

---

## 许可

MIT License © PaperSpine
