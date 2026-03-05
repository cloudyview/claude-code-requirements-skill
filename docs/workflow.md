# Workflow Diagram

## Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    /gather-requirements                      │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  Phase 1: Initialize                                         │
│  ┌──────────────────────────────────┐                       │
│  │ Ask feature name                  │                       │
│  │ Create docs/requirements/<name>.md│                       │
│  │ Initialize template               │                       │
│  └──────────────┬───────────────────┘                       │
│                 ▼                                            │
│  Phase 2: Collect (Loop)                                     │
│  ┌──────────────────────────────────┐                       │
│  │ User describes a segment ──────► │                       │
│  │ Organize into sections    ──────► │                       │
│  │ Update document (Edit)    ──────► │                       │
│  │ Summarize + "还有补充吗？"        │                       │
│  └──────────┬───────────┬───────────┘                       │
│         Yes ▼           │ No ("没有了")                      │
│      (loop back)        ▼                                    │
│  Phase 3: Clarify                                            │
│  ┌──────────────────────────────────┐                       │
│  │ Read full document                │                       │
│  │ Identify gaps & ambiguities       │                       │
│  │ Ask 2-3 clarifying questions      │                       │
│  │ Update document with answers      │                       │
│  └──────────┬───────────┬───────────┘                       │
│      More Q ▼           │ All clear                         │
│      (loop back)        ▼                                    │
│  Phase 4: Finalize                                           │
│  ┌──────────────────────────────────┐                       │
│  │ Status → "已完成"                 │                       │
│  │ Add implementation notes          │                       │
│  │ Present document path             │                       │
│  │ Suggest: /planning-with-files     │                       │
│  └──────────────────────────────────┘                       │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

## Phase Details

### Phase 1: Initialize (~30 seconds)

- Input: Feature name from user
- Output: Empty requirements template at `docs/requirements/<name>.md`
- Creates `docs/requirements/` directory if needed

### Phase 2: Collect (~5-15 minutes)

- Input: User's natural language descriptions, one segment at a time
- Processing: Categorize into 6 sections (Overview, User Stories, Core Requirements, Interaction Design, Data Model, Technical Constraints)
- Output: Incrementally updated requirements document
- Loop condition: User says "还有补充吗？" → yes/no

### Phase 3: Clarify (~3-5 minutes)

- Input: Complete requirements document
- Processing: Gap analysis for missing flows, edge cases, data relationships, UI decisions
- Output: Clarifying questions → user answers → document updates
- Loop condition: Until major gaps are filled

### Phase 4: Finalize (~1 minute)

- Input: Fully clarified requirements
- Output: Final document with status "已完成" and implementation notes
- Next step: `/planning-with-files` or Claude Code plan mode

## Integration with Other Tools

```
/gather-requirements  →  Requirements Doc  →  /planning-with-files  →  Implementation
     (this skill)         (structured .md)      (planning skill)        (code)
```
