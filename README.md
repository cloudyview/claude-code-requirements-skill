# Claude Code Requirements Skill

> **Stop coding before you know what to build.**
>
> **在动手写代码之前，先搞清楚要做什么。**

A Claude Code skill that adds an interactive requirements gathering phase to your workflow. Describe your feature in segments, get a structured requirements document, then proceed to planning with confidence.

一个 Claude Code 技能，为你的开发工作流添加交互式需求收集阶段。分段描述你的功能需求，获得结构化需求文档，然后自信地进入开发。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-green)](https://docs.anthropic.com/en/docs/claude-code)
[![Version](https://img.shields.io/badge/version-1.0.0-brightgreen)](https://github.com/cloudyview/claude-code-requirements-skill/releases)

---

## The Problem | 问题

Most AI coding workflows go straight from idea to implementation:

大多数 AI 编程工作流直接从想法跳到实现：

```
"I want feature X" → AI starts coding → Rework → More rework → Done (maybe)
"我想要功能X" → AI 开始写代码 → 返工 → 再返工 → 勉强完成
```

This leads to scope creep, misunderstood requirements, and wasted effort.

这导致需求蔓延、需求误解和大量返工。

## The Solution | 解决方案

Add a structured requirements phase:

添加一个结构化的需求收集阶段：

```
"I want feature X" → /gather-requirements → Structured doc → Clarifying Q&A → Plan → Code
"我想要功能X" → /gather-requirements → 结构化文档 → 反问澄清 → 方案设计 → 编码
```

The skill collects your requirements **segment by segment**, organizes them into a structured document, then asks smart questions to fill gaps — all before a single line of code is written.

技能**逐段收集**你的需求，整理成结构化文档，然后智能提问填补遗漏 — 一切在写代码之前完成。

---

## Quick Install | 快速安装

### Claude Code (Recommended | 推荐)

```bash
claude skill add --from github cloudyview/claude-code-requirements-skill
```

### Manual Install | 手动安装

```bash
# Clone the repo | 克隆仓库
git clone https://github.com/cloudyview/claude-code-requirements-skill.git

# Copy skill into your project | 复制到你的项目
cp -r gather-requirements/skills/gather-requirements YOUR_PROJECT/.claude/skills/
```

Or simply copy `skills/gather-requirements/SKILL.md` into your project's `.claude/skills/` directory.

或者直接将 `skills/gather-requirements/SKILL.md` 复制到你项目的 `.claude/skills/` 目录下。

See [docs/installation.md](docs/installation.md) for all installation methods.

---

## Usage | 使用方法

### 1. Start the skill | 启动技能

```
/gather-requirements
```

### 2. Name your feature | 命名功能

The skill asks for a short feature name (e.g., `ai-dubbing`, `timeline-editor`).

技能会要求输入一个简短的功能名（如 `ai-dubbing`、`timeline-editor`）。

### 3. Describe in segments | 分段描述

Just talk naturally. Describe one aspect at a time:

自然地说就行。每次描述一个方面：

```
User: "我想要一个时间轴编辑器，用户可以把视频片段拖到轨道上，
       裁剪片段，实时预览效果。"

Claude: 已记录：时间轴编辑器，支持拖拽视频片段、裁剪和实时预览。
        还有其他需要补充的吗？

User: "要支持多个音频轨道，每个片段可以调音量。"

Claude: 已记录：多音轨支持，可逐片段调节音量。
        还有其他需要补充的吗？

User: "没有了。"

Claude: 让我检查一下需求文档，提几个澄清问题...
```

### 4. Answer clarifying questions | 回答澄清问题

The skill analyzes your requirements for gaps:

技能会分析需求中的遗漏：

- Missing user flows | 缺失的用户流程
- Edge cases | 边界情况
- Data model questions | 数据模型问题
- UI/UX decisions | 交互设计决策

### 5. Get your document | 获取需求文档

Final output at `docs/requirements/<feature-name>.md`:

最终输出在 `docs/requirements/<功能名>.md`：

```markdown
# Timeline Editor — Requirements

> Created: 2026-03-06
> Status: Complete

## 1. Feature Overview
- Visual timeline editor for video clip arrangement
- Real-time preview capability

## 2. User Stories
- As an editor, I want to drag clips onto tracks...
```

### 6. Next step | 下一步

Use the requirements document as input for planning (e.g., `/planning-with-files` or Claude Code Plan Mode).

将需求文档作为方案设计的输入（如 `/planning-with-files` 或 Claude Code Plan Mode）。

---

## Document Structure | 文档结构

| Section | 章节 | Purpose | 说明 |
|---------|------|---------|------|
| Feature Overview | 功能概述 | What is this feature? | 这个功能是什么？ |
| User Stories | 用户故事 | Who uses it and how? | 谁用？怎么用？ |
| Core Requirements | 核心需求 | Must-have functionality | 必须实现的功能 |
| Interaction Design | 交互设计 | UI/UX behavior | 界面和交互行为 |
| Data Model | 数据模型 | Data and relationships | 涉及的数据和关系 |
| Technical Constraints | 技术约束 | Limits and dependencies | 限制和依赖 |
| Open Questions | 待澄清问题 | Resolved during clarification | 在反问阶段解决 |

After finalization, an **Implementation Notes** (实现建议) section is added.

---

## Works Great With | 最佳搭配

| Tool | Flow |
|------|------|
| **[planning-with-files](https://github.com/OthmanAdi/planning-with-files)** | Requirements → Planning → Code |
| **Claude Code Plan Mode** | Requirements → Architecture → Code |
| **Any AI coding workflow** | Requirements → Your process → Code |

```
/gather-requirements  →  需求文档  →  /planning-with-files  →  实现
     (收集需求)          (结构化 .md)      (方案设计)           (编码)
```

---

## Supported Languages | 支持语言

The skill adapts to the user's language:
- English
- 中文
- Any language the user communicates in

技能会自动适配用户的语言。

---

## Project Structure | 项目结构

```
gather-requirements/
├── README.md                          # This file | 本文件
├── LICENSE                            # MIT License
├── docs/
│   ├── installation.md                # Installation guide | 安装指南
│   └── workflow.md                    # Workflow diagram | 流程图
├── examples/
│   └── example-requirements.md        # Sample output | 示例输出
└── skills/
    └── gather-requirements/
        ├── SKILL.md                   # Skill definition | 技能定义（核心）
        └── templates/
            └── requirements.md        # Document template | 文档模板
```

## Contributing | 贡献

Contributions welcome! Open an issue or PR if you have ideas for improving the requirements gathering workflow.

欢迎贡献！如果你有改进需求收集流程的想法，请提 Issue 或 PR。

## License | 许可

MIT License — see [LICENSE](LICENSE) for details.
