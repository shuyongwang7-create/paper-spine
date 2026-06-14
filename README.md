# PaperSpine — 学术论文全流程辅助插件

PaperSpine 是一个 Claude Code 插件，覆盖学术论文从选题到投稿的完整工作流。

## 安装

```bash
claude plugins install github:19385/paper-spine
```

## 包含的 11 个 Skill

| Skill | 功能 |
|---|---|
| `paper-spine-intake` | 选题配置 — 收集工作流选项，生成 `paper_spine_config.json` |
| `paper-spine-research` | 文献研究 — 调研目标期刊、下载参考文献、学习优秀范例 |
| `paper-spine-build` | 框架构建 — 从素材构建论文/报告的完整框架 |
| `paper-spine-rewrite` | 改写润色 — 基于已有稿件进行段落级改写 |
| `paper-spine-humanize` | AI 降重 — 通过分级风格约束降低 AIGC 检测率 |
| `paper-spine-translate` | 中英翻译 — 生成完整翻译包，逐行对照 |
| `paper-spine-citation` | 引用管理 — 构建引言/讨论/背景的引用支撑库 |
| `paper-spine-latex` | LaTeX 排版 — 项目组装、图表定位、引用处理、编译清理 |
| `paper-spine-audit` | 审核审计 — 检查产出完整性、逻辑迁移、声明支撑 |
| `paper-spine-update` | 版本更新 — 从 GitHub 检查并更新 PaperSpine |
| `paper-spine-ui` | 交互界面 — 启动终端配置 UI |

## 工作流

典型论文写作流程：

```
intake → research → build → rewrite → humanize → translate → citation → latex → audit
  ↑                                                                                    │
  └──────────────────────────── update ────────────────────────────────────────────────┘
```

## 要求

- Claude Code v2.1.144+
- Python 3.10+（脚本工具需要）

## 许可

MIT License
