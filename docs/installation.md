# Installation Guide

## Method 1: Claude Code Skill Install (Recommended)

```bash
claude skill add --from github cloudyview/gather-requirements
```

This automatically installs the skill into your Claude Code environment.

## Method 2: Manual Copy

1. Clone the repo:

```bash
git clone https://github.com/cloudyview/gather-requirements.git
```

2. Copy the skill folder into your project:

```bash
cp -r gather-requirements/skills/gather-requirements YOUR_PROJECT/.claude/skills/
```

3. Verify the skill is recognized:

```
/gather-requirements
```

## Method 3: Direct File

If you just want the skill without cloning:

1. Create `.claude/skills/` in your project root (if it doesn't exist)
2. Download `skills/gather-requirements/SKILL.md` into `.claude/skills/gather-requirements/SKILL.md`
3. Optionally download the template into `.claude/skills/gather-requirements/templates/requirements.md`

## Requirements

- **Claude Code** (any recent version with skill support)
- No additional dependencies — this is a pure prompt-based skill

## Verify Installation

After installing, type `/gather-requirements` in Claude Code. You should see the skill activate and ask for a feature name.

## Output Location

Requirements documents are saved to `docs/requirements/` in your project directory. This directory is created automatically if it doesn't exist.

## Uninstall

Simply delete the `.claude/skills/gather-requirements/` directory from your project.
