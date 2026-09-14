# 财务与会计论文阅读器

[English](README.md) | 简体中文

这是一个 Codex 技能，用于从 Zotero 中读取单篇财务、会计或相关领域的学术论文，并为 Obsidian 创建可追溯证据的 Markdown 文献笔记。

该技能会匹配目标 Zotero 条目、验证 Better BibTeX 引用键（citekey）、读取可用的论文全文，并将笔记写入：

```text
<vault>/10_Papers/<citekey>.md
```

它面向需要长期保存的研究笔记，而不是一般性的论文摘要。笔记中的主张会关联到经过核验的原文位置，重要的零结果或相反结果会被保留，全文覆盖不完整时也会明确说明。

## 功能特性

- 支持通过 Better BibTeX citekey、Zotero 条目键、DOI、标题或作者与年份匹配论文。
- 将书目父条目键与附件键分开处理。
- 支持 `quick`、`standard` 和 `deep` 三种阅读模式。
- 所有模式共用一套带类型约束的 YAML schema，以兼容 Obsidian Bases。
- 区分论文类型、研究设计、研究方法和因果识别策略。
- 记录可合理辩护的主要分析样本量，而非罗列每个回归样本。
- 保留结果方向、统计显著性、经济量级，以及重要的零结果或相反结果。
- 根据阅读模式，将来源追溯粒度从简洁的行内定位扩展到完整的证据日志（Evidence Log）。
- 对不完整或不可获得的全文如实标记，不使用无依据的内容填补空缺。
- 更新已有笔记时保护用户撰写的内容。
- 在条件允许时，使用本地 YAML 解析器验证 YAML frontmatter。

## 阅读模式

| 模式 | 适用场景 | 典型正文长度 | 证据详细程度 |
| --- | --- | ---: | --- |
| `quick` | 快速判断论文是否值得进一步阅读 | 800–1,500 词 | 为核心主张提供简洁的原文位置 |
| `standard` | 创建常规、可长期保存的文献笔记 | 2,000–3,500 词 | 选择性证据日志，通常为 5–12 条 |
| `deep` | 深入研究奠基性论文、研究方法或复现目标 | 不设固定上限 | 详细覆盖研究设计、图表、附录和复现问题 |

未指定模式时自动使用 `standard`。阅读模式控制综合分析的深度，但不会降低证据和来源核验要求。

## 使用要求

- 支持本地技能的 Codex。
- Zotero Desktop，以及能够只读访问文献库的兼容 Zotero MCP 连接。
- 如果需要以 citekey 命名文件，则需要 Better BibTeX。
- 一个可以访问的 Obsidian 仓库（vault）。
- 要生成完整阅读笔记，需要可用的论文全文；同时支持并会明确标记仅元数据笔记和部分阅读笔记。

该技能会发现当前环境中可用的 Zotero 工具。它不会修改 Zotero 条目、批注、笔记、标签、设置或索引。

## 安装

将本仓库克隆或下载到 Codex 技能目录：

```text
$CODEX_HOME/skills/finance-accounting-paper-reader
```

如果未设置 `CODEX_HOME`，请使用默认位置：

```text
~/.codex/skills/finance-accounting-paper-reader
```

安装后的目录结构应如下：

```text
finance-accounting-paper-reader/
├── .env.example
├── SKILL.md
├── references/
│   ├── field-guidelines.md
│   └── paper-note-template.md
└── templates/
    └── Paper Note.md
```

如果技能未立即出现，请重启 Codex 或开始一个新会话。

## Obsidian 仓库配置

最方便的持久化配置方式，是在已安装的技能目录中创建本地 `.env` 文件。将 `.env.example` 复制为 `.env`，再把占位值替换为 Obsidian 仓库的绝对路径：

```dotenv
OBSIDIAN_VAULT_PATH=/absolute/path/to/your/Obsidian/vault
```

该技能会自动读取此文件，因此无需在每次请求中重复指定仓库路径。本地 `.env` 文件已被 Git 忽略，应保持未提交状态。

你也可以在启动 Codex 的环境中定义 `OBSIDIAN_VAULT_PATH`。

PowerShell：

```powershell
$env:OBSIDIAN_VAULT_PATH = "C:\path\to\your\vault"
```

macOS 或 Linux：

```bash
export OBSIDIAN_VAULT_PATH="/path/to/your/vault"
```

仓库路径按以下优先级解析：

1. 当前请求中明确指定的目标位置
2. 当前会话中已经确定的路径
3. 进程级环境变量 `OBSIDIAN_VAULT_PATH`
4. 技能目录 `.env` 文件中的 `OBSIDIAN_VAULT_PATH`

该技能将 `.env` 作为纯配置数据读取，不会执行它。版本库中仅包含 `.env.example`，不包含个人仓库路径。

可选的手动模板可以从 [`templates/Paper Note.md`](templates/Paper%20Note.md) 复制到：

```text
<vault>/90_Templates/Paper Note.md
```

覆盖现有仓库模板前，请先检查其内容。随附模板对应 `standard` 模式；其他模式的正文结构由技能自动选择。

## 使用方法

使用 Better BibTeX citekey 的标准模式：

```text
使用 $finance-accounting-paper-reader 从 Zotero 阅读 smith2025EarningsQuality。
不要覆盖已有笔记。
```

快速筛选：

```text
使用 $finance-accounting-paper-reader，以 quick 模式从 Zotero 阅读
smith2025EarningsQuality。
```

深度阅读：

```text
使用 $finance-accounting-paper-reader，以 deep 模式从 Zotero 阅读
smith2025EarningsQuality。
```

明确指定仓库目标位置：

```text
使用 $finance-accounting-paper-reader 阅读 smith2025EarningsQuality。
将笔记保存到 C:/path/to/vault/10_Papers/<citekey>.md。
不要覆盖任何已有笔记。
```

也可以使用 Zotero 条目键、DOI、准确标题或作者与年份识别论文。在创建以 citekey 命名的文件前，该技能仍然要求获得经过验证的 Better BibTeX citekey。

## 输出内容

所有阅读模式都使用相同的 YAML 属性及其类型。该 schema 包括书目身份、Zotero 身份、主题与理论、论文类型、研究设计、研究方法、识别策略、数据来源、样本元数据、阅读模式、阅读状态和全文状态。

Markdown 正文会随阅读模式变化。一篇采用标准模式的实证论文笔记包括：

1. 一句话结论（One-Sentence Takeaway）
2. 研究问题与缺口（Research Question and Gap）
3. 研究贡献（Contribution）
4. 理论（Theory）
5. 数据与样本（Data and Sample）
6. 变量构造（Variable Construction）
7. 研究设计与识别（Research Design and Identification）
8. 主要结果（Main Results）
9. 机制与异质性（Mechanism and Heterogeneity）
10. 稳健性检验（Robustness）
11. 文献定位（Position in Literature）
12. 证据日志（Evidence Log）
13. 复现资源（Replication Resources）
14. 可直接引用的摘要（Citation-Ready Summary）
15. 受保护的 `My Notes` 区域

对于预测、实验、分析建模、结构模型、定性研究、综述等其他论文类型，正文结构会在保留相关核心分析职能的前提下进行调整。

## 已有笔记安全机制

新笔记使用不同的标记分别界定机器生成内容和用户笔记。目标文件已存在时，技能会在提出更新前读取它，并保留可识别的用户内容、未知 YAML 字段、评分、项目字段和手动笔记。如果无法安全地区分机器生成内容与用户内容，技能将保持现有文件不变并报告冲突。

在常规论文阅读过程中，该技能不会批量迁移整个仓库、重命名旧笔记，也不会重写 Obsidian 手动模板。

## 仓库结构

| 路径 | 职责 |
| --- | --- |
| [`.env.example`](.env.example) | 用于持久化本地仓库配置的脱敏示例 |
| [`SKILL.md`](SKILL.md) | 操作流程、阅读模式选择、来源规范、安全更新和质量控制 |
| [`references/paper-note-template.md`](references/paper-note-template.md) | 共用 YAML schema 和不同模式的笔记结构 |
| [`references/field-guidelines.md`](references/field-guidelines.md) | 财务与会计研究的方法论阅读指南 |
| [`templates/Paper Note.md`](templates/Paper%20Note.md) | 与标准模式一致的 Obsidian 手动备用模板 |

更改输出 schema 时，应同时更新参考模板和 Obsidian 手动模板。已有笔记属于向后兼容的历史记录，不是自动迁移目标。

## 隐私与仓库卫生

不要提交个人 Obsidian 仓库路径、Zotero 数据库文件、导出的文献库、凭据、受版权保护的 PDF 或生成的研究笔记。随附的 `.gitignore` 会排除 `.env` 和常见的本地研究数据；设置后可使用 `git check-ignore .env` 确认规则，并仍应在每次提交前检查变更。

## 验证

修改技能后，运行 Codex `skill-creator` 技能随附的验证器：

```text
python <skill-creator>/scripts/quick_validate.py <path-to-this-repository>
```

还应验证 `references/paper-note-template.md` 中的 YAML schema 与 `templates/Paper Note.md` 的 frontmatter 一致，并确认手动模板与标准模式正文一致。

## 许可证

本仓库尚未选择许可证。以开源方式发布前，请添加适当的许可证。
