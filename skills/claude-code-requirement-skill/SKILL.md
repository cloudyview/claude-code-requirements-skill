---
name: claude-code-requirement-skill
version: "1.0.0"
description: Interactive requirements gathering — collect user needs segment by segment, organize into structured documents, then ask clarifying questions to fill gaps. Use before planning or coding any new feature.
user-invocable: true
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - AskUserQuestion
---

# Gather Requirements

An interactive requirements gathering skill for Claude Code. The user describes their feature in segments, you organize each segment into a structured document, and when they're done you ask clarifying questions to fill gaps.

## Why This Skill?

Most AI coding workflows jump straight from a vague idea to implementation. This creates:
- **Scope creep** — features grow beyond what was intended
- **Rework** — misunderstood requirements lead to wasted effort
- **Missed edge cases** — gaps discovered too late in development

This skill adds a **requirements gathering phase** before planning and coding. It's the missing step between "I have an idea" and "Let's build it."

## Workflow

### Phase 1: Initialize

1. Ask the user for a **feature name** (short identifier, e.g., "ai-dubbing", "timeline-editor")
2. Create a requirements document at `docs/requirements/<feature-name>.md`
3. Initialize the document using the template at `${SKILL_DIR}/templates/requirements.md`
4. Tell the user: "Ready! Describe your feature, I'll organize as you go."

### Phase 2: Collect (Loop)

1. **Listen**: The user describes a segment of their requirements in natural language
2. **Organize**: Analyze what the user said and:
   - Summarize key points
   - Categorize content into the appropriate section(s) of the document:
     - **功能概述** (Feature Overview) — what is this feature?
     - **用户故事** (User Stories) — who uses it and how?
     - **核心需求** (Core Requirements) — specific functionality
     - **交互设计** (Interaction Design) — UI/UX behavior
     - **数据模型** (Data Model) — what data is involved?
     - **技术约束** (Technical Constraints) — limitations, dependencies
   - If the user's input spans multiple sections, split it accordingly
   - Preserve the user's original intent — do NOT add features they didn't mention
3. **Write**: Update the requirements document using the Edit tool. Append to existing sections — never overwrite previous content.
4. **Confirm**: Reply with:
   - A brief summary of what you recorded (2-3 sentences max)
   - Then ask: **"还有其他需要补充的吗？"** (or in the user's language: "Anything else to add?")
5. **Repeat** until the user says they're done (e.g., "没有了", "就这些", "done", "that's all")

### Phase 3: Clarify

When the user indicates they're done:

1. **Read** the full requirements document
2. **Analyze** for gaps, ambiguities, and missing details:
   - User flows that aren't fully described
   - Edge cases not addressed
   - Data relationships that need clarification
   - UI/UX decisions that need user input
   - Technical constraints or dependencies
   - Conflicts with existing features
3. **Ask** clarifying questions — focus on the 2-3 most important gaps first
4. **Update** the document with answers
5. **Repeat** until all major gaps are filled

### Phase 4: Finalize

1. Update the document status from "收集中" to "已完成"
2. Add a brief "实现建议" (Implementation Notes) section with:
   - Existing code/patterns that could be reused
   - Key files that will need changes
   - Suggested approach (high-level only)
3. Present the final document path to the user
4. Suggest next step: proceed to planning/implementation

## Rules

- **DO NOT** invent requirements the user didn't mention
- **DO NOT** propose detailed implementation during collection — just record what the user wants
- **DO** keep the document concise — bullet points over paragraphs
- **DO** match the user's language (Chinese/English) in the document
- **DO** ask about integration points with existing systems when relevant
- Each update should use the Edit tool to append — never overwrite the whole file
