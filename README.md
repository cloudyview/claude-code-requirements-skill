# Gather Requirements

> **Stop coding before you know what to build.**

A Claude Code skill that adds an interactive requirements gathering phase to your workflow. Describe your feature in segments, get a structured requirements document, then proceed to planning with confidence.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-green)](https://docs.anthropic.com/en/docs/claude-code)
[![Version](https://img.shields.io/badge/version-1.0.0-brightgreen)](https://github.com/YOUR_USERNAME/gather-requirements/releases)

## The Problem

Most AI coding workflows go straight from idea to implementation:

```
"I want feature X" → AI starts coding → Rework → More rework → Done (maybe)
```

This leads to scope creep, misunderstood requirements, and wasted effort.

## The Solution

Add a structured requirements phase:

```
"I want feature X" → /gather-requirements → Structured doc → Clarifying questions → Plan → Code
```

The skill collects your requirements **segment by segment**, organizes them into a structured document, then asks smart questions to fill gaps — all before a single line of code is written.

## Quick Install

### Claude Code (Recommended)

```bash
claude skill add --from github YOUR_USERNAME/gather-requirements
```

### Manual Install

```bash
# Clone into your project
git clone https://github.com/YOUR_USERNAME/gather-requirements.git

# Copy the skill into your project's .claude/skills/
cp -r gather-requirements/skills/gather-requirements .claude/skills/
```

Or simply copy `skills/gather-requirements/SKILL.md` into your project's `.claude/skills/` directory.

## Usage

### 1. Start the skill

```
/gather-requirements
```

### 2. Name your feature

The skill asks for a short feature name (e.g., `ai-dubbing`, `user-auth`).

### 3. Describe your feature in segments

Just talk naturally. Describe one aspect at a time:

```
User: "I want a timeline editor where users can drag video clips onto tracks,
       trim them, and preview the result in real-time."

Claude: Recorded: Timeline editor with drag-and-drop clips, trimming, and real-time preview.
        还有其他需要补充的吗？

User: "It should support multiple audio tracks and allow adjusting volume per clip."

Claude: Recorded: Multi-track audio support with per-clip volume control.
        还有其他需要补充的吗？

User: "That's all."

Claude: Let me review the requirements and ask some clarifying questions...
```

### 4. Answer clarifying questions

The skill analyzes your requirements for gaps and asks targeted questions:

- Missing user flows
- Edge cases
- Data model questions
- UI/UX decisions

### 5. Get your structured document

The final output is a clean requirements document at `docs/requirements/<feature-name>.md`:

```markdown
# Timeline Editor — Requirements

> Created: 2026-03-06
> Status: Complete

## 1. Feature Overview
- Visual timeline editor for video clip arrangement
- Real-time preview capability
...

## 2. User Stories
- As an editor, I want to drag clips onto tracks...
...
```

### 6. Proceed to implementation

Use the requirements document as input for your planning phase (e.g., `/planning-with-files`).

## Document Structure

The generated requirements document has 7 sections:

| Section | Purpose |
|---------|---------|
| **Feature Overview** | What is this feature? High-level description |
| **User Stories** | Who uses it and how? |
| **Core Requirements** | Specific functionality — the "must haves" |
| **Interaction Design** | UI/UX behavior, user flows |
| **Data Model** | What data is involved, relationships |
| **Technical Constraints** | Limitations, dependencies, performance needs |
| **Open Questions** | Resolved during the clarification phase |

After finalization, an **Implementation Notes** section is added with technical suggestions.

## Works Great With

- **[planning-with-files](https://github.com/OthmanAdi/planning-with-files)** — Use gather-requirements first, then planning-with-files for implementation planning
- **Claude Code Plan Mode** — Feed the requirements doc into plan mode for architecture design
- Any AI coding workflow that benefits from clear requirements

## Supported Languages

The skill adapts to the user's language. Requirements can be collected and documented in:
- English
- Chinese (中文)
- Any language the user communicates in

## Project Structure

```
gather-requirements/
├── README.md                                    # This file
├── LICENSE                                      # MIT License
├── docs/
│   ├── installation.md                          # Detailed installation guide
│   └── workflow.md                              # Workflow diagram
├── examples/
│   └── example-requirements.md                  # Sample output
└── skills/
    └── gather-requirements/
        ├── SKILL.md                             # Skill definition (core)
        └── templates/
            └── requirements.md                  # Document template
```

## Contributing

Contributions welcome! If you have ideas for improving the requirements gathering workflow, please open an issue or PR.

## License

MIT License — see [LICENSE](LICENSE) for details.
