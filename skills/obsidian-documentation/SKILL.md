---
name: obsidian-documentation
description: Create and manage documentation in Matt Wood's Obsidian vault following his established schema, folder structure, and frontmatter standards. Use when creating session logs, decision logs, project READMEs, or any Obsidian notes. Automatically applies proper frontmatter, wiki-links, tags, and naming conventions.
allowed-tools: mcp__obsidian__create_note_tool, mcp__obsidian__update_note_tool, mcp__obsidian__read_note_tool, mcp__obsidian__search_notes_tool, mcp__obsidian__list_notes_tool
---

# Obsidian Documentation Skill

## Purpose

This skill ensures all Obsidian vault documentation follows Matt Wood's established patterns, schema, and organizational structure. It prevents generic documentation and enforces consistency across all notes.

## When to Use

- Creating session logs for project work
- Creating decision logs for architectural choices
- Creating project README files
- Creating update notes for features/changes
- Creating issue tracking notes
- Any time you need to document work in Obsidian

## Vault Structure

### Primary Folders

```
Projects/                    # All project documentation
  ├── [Project-Name]/
  │   ├── README.md         # Project overview
  │   ├── sessions/         # Session logs
  │   ├── decisions/        # Decision logs
  │   └── technical-docs/   # Technical documentation

Professional/               # Professional work
  ├── LinkedIn-Voice-Lab/  # LinkedIn content system
  └── Marketing/           # Marketing materials

Development/               # Development workflows
  ├── GIT-REPOSITORY-WORKFLOW.md
  └── PROJECT-CREATION-QUICKSTART.md

Daily/                     # Daily notes and quick captures

_meta/                     # Vault configuration
_templates/                # Note templates
```

## Frontmatter Schema

### Core Fields (All Notes)

```yaml
---
created: "2025-11-13"           # YYYY-MM-DD
updated: "2025-11-13"           # YYYY-MM-DD
type: "session|decision|update|issue|project|index"
project: "Project Name"         # Human-readable
status: "active|completed|blocked|archived"
tags: ["tag1", "tag2"]
---
```

### Type-Specific Fields

#### Session Logs
```yaml
type: "session"
session_date: "2025-11-13"
hours_worked: 2.5
accomplishments: ["item1", "item2"]
blockers: ["blocker1"]
next_steps: ["step1", "step2"]
```

#### Decisions
```yaml
type: "decision"
decision_type: "architectural|technical|process"
impact: "high|medium|low"
alternatives_considered: ["alt1", "alt2"]
chosen_approach: "description"
```

#### Updates
```yaml
type: "update"
update_type: "feature|bugfix|refactor|config"
files_changed: ["path/to/file1.ts"]
breaking_changes: false
```

#### Project README
```yaml
type: "project"
project: "Project Name"
status: "active|completed|blocked|archived"
start_date: "2025-11-13"
client: "Client Name"         # If applicable
```

### External System Integration (Optional)

Only include if the system is accessible:

```yaml
# Airtable
airtable_base: "appXXXXXXXXXXXXX"
airtable_project_id: "recXXXXXXXXXX"

# Linear
linear_project_id: "PROJECT-123"
linear_issue_id: "ISSUE-456"

# GitHub
github_repo: "owner/repo"
github_issue: "123"
```

## Naming Conventions

### Files
- Session logs: `YYYY-MM-DD-session.md` or `YYYY-MM-DD-brief-description.md`
- Decisions: `decision-brief-name.md`
- Updates: `update-feature-name.md` or `YYYY-MM-DD-update.md`
- Issues: `issue-brief-description.md`
- Project README: `README.md` (at project root)

### Folders
- Project names: Use clear, descriptive names with hyphens
- Example: `Projects/US-Solar-Airtable-System/`

## Wiki Links

Use `[[wiki-links]]` to connect related notes:

```markdown
See also: [[decision-use-typescript]], [[2025-10-12-session]]
Related issue: [[issue-data-sync-error]]
Project: [[Projects/ProjectName/README]]
```

## Tags Taxonomy

### Project-Related
- `#project/active`
- `#project/archived`
- `#project/blocked`

### Technology
- `#tech/python`
- `#tech/typescript`
- `#tech/airtable`
- `#tech/automation`
- `#tech/n8n`

### Task Type
- `#task/bookkeeping`
- `#task/tax-return`
- `#task/automation`
- `#task/analysis`

### Priority
- `#priority/high`
- `#priority/medium`
- `#priority/low`

### Status
- `#status/todo`
- `#status/in-progress`
- `#status/review`
- `#status/completed`

## Session Log Structure

```markdown
---
created: "2025-11-13"
updated: "2025-11-13"
type: "session"
project: "Project Name"
session_date: "2025-11-13"
hours_worked: 3.5
status: "active"
tags: ["project/active", "tech/typescript"]
---

# Session: [Date] - [Brief Description]

## Context

Brief context about what this session is addressing.

## Accomplishments

- ✅ Specific thing completed
- ✅ Another specific thing
- ✅ Metrics when relevant (e.g., "Migrated 150 records")

## Technical Details

### Key Changes
- File/system changed and why
- Technical decisions made
- Code patterns used

### Challenges & Solutions
- **Challenge**: Specific problem encountered
- **Solution**: How it was solved
- **Outcome**: Result with metrics if applicable

## Blockers

- 🔴 Blocker with clear description
- 🟡 Waiting on: specific thing from specific person

## Next Steps

- [ ] Specific actionable next step
- [ ] Another specific step
- [ ] Follow up task

## Notes

Any additional context, learnings, or references.

## Related

- [[Projects/ProjectName/README]]
- [[Previous session note]]
- [[Related decision]]
```

## Decision Log Structure

```markdown
---
created: "2025-11-13"
updated: "2025-11-13"
type: "decision"
project: "Project Name"
decision_type: "architectural"
impact: "high"
status: "active"
tags: ["decision", "architecture"]
---

# Decision: [Brief Decision Title]

## Context

What necessitated this decision? What problem are we solving?

## Options Considered

### Option 1: [Name]
**Pros:**
- Specific advantage
- Another advantage

**Cons:**
- Specific disadvantage
- Another disadvantage

### Option 2: [Name]
**Pros:**
- Specific advantage

**Cons:**
- Specific disadvantage

## Chosen Approach

**Decision:** [Clear statement of what was chosen]

**Rationale:**
- Specific reason with data/metrics
- Another specific reason
- Trade-offs accepted

## Implementation Notes

- How this will be implemented
- What changes are required
- Timeline considerations

## Related

- [[Related session log]]
- [[Related project README]]
```

## Project README Structure

```markdown
---
created: "2025-11-13"
updated: "2025-11-13"
type: "project"
project: "Project Name"
status: "active"
start_date: "2025-11-13"
tags: ["project/active", "tech/python"]
---

# Project: [Project Name]

## Overview

**Status**: 🟢 Active
**Started**: YYYY-MM-DD
**Last Updated**: YYYY-MM-DD

### Quick Summary

2-3 sentence overview of what this project does.

## Goals & Objectives

1. **Primary Goal**: Clear statement
2. **Secondary Goal**: Another clear statement
3. **Success Criteria**: Measurable outcomes

## Current Status

### What's Working
✅ Specific completed items

### What's In Progress
🟡 Specific in-progress items

### What's Blocked
🔴 Specific blockers

## Session History

Recent sessions in reverse chronological order:

1. [[sessions/YYYY-MM-DD-session]] - Brief description
2. [[sessions/YYYY-MM-DD-session]] - Brief description

## Key Decisions

Important architectural/technical decisions:

1. [[decisions/decision-name]] - Brief description

## Quick Links

- 📊 [External System Link](url)
- 📧 [Contact Email](mailto:email)
```

## Best Practices

### DO
- ✅ Use specific dates in YYYY-MM-DD format
- ✅ Include metrics and numbers
- ✅ Link related notes with wiki-links
- ✅ Use proper frontmatter for all notes
- ✅ Keep session logs detailed but scannable
- ✅ Update the `updated` field when modifying notes
- ✅ Use emojis for status (✅ 🟡 🔴 🟢)

### DON'T
- ❌ Skip frontmatter
- ❌ Use vague descriptions
- ❌ Create notes without tags
- ❌ Forget to link to project README
- ❌ Use generic titles
- ❌ Mix different note types in one file

## Examples from Actual Notes

### Example Session Log Name
`2025-10-24-forms-completion-google-drive-integration.md`

### Example Decision Name
`decision-n8n-over-make.md`

### Example Project Name
`Projects/US-Solar-Airtable-System/README.md`

## Quality Checklist

Before creating any note, verify:

- [ ] Proper YAML frontmatter with all required fields?
- [ ] Correct folder location?
- [ ] Proper naming convention?
- [ ] Wiki-links to related notes?
- [ ] Relevant tags applied?
- [ ] Specific and actionable content?
- [ ] Numbers/metrics where applicable?

---

**Version**: 1.0
**Created**: 2025-11-13
**Last Updated**: 2025-11-13
