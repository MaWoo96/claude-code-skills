---
name: obsidian-session
description: Creates structured session logs in Obsidian vault when user says "start session [project-name]" or "create session note". Automatically fills in metadata, queries recent context, and structures work documentation.
allowed-tools: mcp__obsidian__create_note_tool, mcp__obsidian__search_notes_tool, mcp__obsidian__list_folders_tool, mcp__obsidian__read_note_tool
---

# Obsidian Session Creator Skill

## Purpose

This skill creates structured session log notes in the Obsidian vault following the established template pattern. It's designed to help track work sessions with proper metadata, context queries, and standardized structure.

## Trigger Phrases

Activate this skill when the user says:
- "Start session [project-name]"
- "Create session note for [project-name]"
- "New session [project-name]"
- "Begin work session [project-name]"

## Session Template Structure

### Frontmatter (YAML)
```yaml
created: YYYY-MM-DD HH:mm
updated: YYYY-MM-DD HH:mm
type: "session"
project: "Project-Name"
status: "active"
session_date: YYYY-MM-DD
claude_instance: "Claude Code Session"
hours_worked: 0
tags: [session, project-name]
accomplishments: []
blockers: []
next_steps: []
```

### Content Sections

1. **Session Context**
   - Project link
   - Date (full format: "Monday, November 11, 2025")
   - Time started
   - Current status

2. **Recent Context (Dataview Queries)**
   - Recent sessions from same project (last 3)
   - Recent decisions (last 3)

3. **What Was Accomplished**
   - Task checkboxes
   - Code changes list
   - Airtable/external system updates

4. **Decisions Made**
   - Context for decision
   - Chosen approach
   - Rationale
   - Link to decision doc if created

5. **Issues Encountered**
   - Problem description
   - Resolution status
   - Link to issue if created

6. **Technical Notes**
   - Implementation details
   - Dependencies added
   - Configuration changes

7. **Testing & Validation**
   - What was tested
   - What needs testing

8. **Blockers & Challenges**
   - Current blockers with impact level
   - Challenges overcome

9. **Next Steps**
   - Immediate actions with priority
   - Future considerations

10. **Handoff Notes**
    - For next Claude instance
    - Important context
    - Gotchas and warnings

11. **Related Notes**
    - Links to previous sessions
    - Related documents

## CRITICAL: Date Handling

**ALWAYS check the current date from the <env> section at the start of the conversation:**
- `<env>` contains: `Today's date: YYYY-MM-DD`
- Use this EXACT date for all date fields
- Double-check month number (November = 11, NOT 01, December = 12, NOT 01)
- Calculate day of week if needed (use correct day name)

**Common Month Mistakes to AVOID:**
- January = 01 (not 1)
- November = 11 (not 01!)
- December = 12 (not 01!)

**Date Formats Required:**
- Filename: `YYYY-MM-DD` (e.g., 2025-11-12)
- Frontmatter `created`: `YYYY-MM-DD HH:mm` (e.g., 2025-11-12 14:30)
- Frontmatter `session_date`: `YYYY-MM-DD` (e.g., 2025-11-12)
- Human readable: "Tuesday, November 12, 2025" (correct day of week!)

## When User Provides Meeting Transcript

If user provides a meeting transcript along with session request:

### Extract Key Information:
1. **Attendees mentioned** - Who was in the meeting
2. **Topics discussed** - Main discussion points
3. **Decisions made** - Explicit decisions and their rationale
4. **Action items** - Who does what
5. **Time references** - Meeting duration if mentioned
6. **Problems/blockers** - Issues raised
7. **Technical details** - Implementations discussed

### Auto-Populate Sections:
- **What Was Accomplished**: Extract completed work from transcript
- **Decisions Made**: Extract context, decision, and rationale
- **Issues Encountered**: Extract problems mentioned
- **Technical Notes**: Extract implementation details
- **Next Steps**: Extract action items with owners
- **Blockers**: Extract any blockers mentioned

### Estimate Session Duration:
- Review transcript length and depth
- Typical meetings: 1-2.5 hours
- Use best judgment based on content

## Generating Filename Description

The brief-description should be:
- **2-4 words**, hyphen-separated
- Describes **main focus** of session
- Use lowercase with hyphens

**Examples:**
- `quickbase-migration-planning`
- `client-tickets-setup`
- `aurora-sync-fixes`
- `financial-system-design`
- `r-and-r-workflow-design`

**If transcript provided:** Extract 2-3 main topics discussed
**If just "start session":** Ask user for brief description or use generic "work-session"

## Pre-Creation Validation Checklist

**Before calling `create_note_tool`, verify:**
- [ ] Date is from `<env>` section (CHECK THE MONTH NUMBER!)
- [ ] Month is correct (11 = November, NOT 01!)
- [ ] Day of week matches date
- [ ] Project name matches folder structure exactly
- [ ] Recent sessions search completed
- [ ] All frontmatter fields populated (no placeholders)
- [ ] If transcript provided, key content extracted and organized
- [ ] Filename description is concise and descriptive

## Implementation Instructions

### Step 1: Validate Project Exists

When user requests a session, first verify the project folder structure:

```
Projects/
  └── [Project-Name]/
      ├── README.md
      ├── sessions/
      ├── decisions/
      └── technical-docs/
```

Use `mcp__obsidian__list_folders_tool` to check if `Projects/[Project-Name]/sessions` exists.

### Step 2: Generate Session Note Path

Format: `Projects/[Project-Name]/sessions/YYYY-MM-DD-brief-description.md`

Example: `Projects/US-Solar-Airtable-System/sessions/2025-11-11-migration-work.md`

### Step 3: Get Current Context

Before creating the note, search for:
1. Recent sessions in the same project (to link as "Previous Session")
2. Project README (to understand current state)

Use `mcp__obsidian__search_notes_tool` with:
- `query`: "path:Projects/[Project-Name]/sessions/"
- `max_results`: 5

### Step 4: Create the Session Note

Use `mcp__obsidian__create_note_tool` with complete frontmatter and structured content.

#### Date/Time Format Reference:
- `created`: ISO format with time: "2025-11-11 14:30"
- `session_date`: ISO date only: "2025-11-11"
- Human-readable: "Monday, November 11, 2025"
- Time: "2:30 PM" format

#### Dataview Query Templates:

**Recent Sessions Query:**
```dataview
LIST
FROM "Projects/[PROJECT-NAME]/sessions"
WHERE file.name != this.file.name
SORT file.cday DESC
LIMIT 3
```

**Recent Decisions Query:**
```dataview
LIST
FROM "Projects/[PROJECT-NAME]/decisions"
SORT file.cday DESC
LIMIT 3
```

### Step 5: Confirm to User

After creating the note, confirm:
- ✅ Session note created
- 📍 Location: `Projects/[Project-Name]/sessions/YYYY-MM-DD-description.md`
- 🔗 Provide link or suggest opening it

## Example Interactions

### Example 1: Simple Session Start

**User**: "Start session US-Solar-Airtable-System"

**Assistant Actions**:
1. **Check `<env>`** for current date → November 12, 2025 (month = 11!)
2. Verify `Projects/US-Solar-Airtable-System/sessions/` exists
3. Search for recent sessions to link
4. Ask user for brief description or use generic "work-session"
5. Create note: `Projects/US-Solar-Airtable-System/sessions/2025-11-12-work-session.md`
6. Populate with template content
7. Confirm creation to user

**Assistant Response**:
"✅ Session started for **US-Solar-Airtable-System**

Created: `Projects/US-Solar-Airtable-System/sessions/2025-11-12-work-session.md`

The session note is ready with:
- Frontmatter metadata (November 12, 2025)
- Recent context queries
- Structured sections for tracking work

Start documenting your work!"

### Example 2: Session with Meeting Transcript

**User**: "Start session US-Solar-Airtable-System" + [provides meeting transcript]

**Assistant Actions**:
1. **Check `<env>`** for current date → November 12, 2025 (verify month is 11!)
2. Verify `Projects/US-Solar-Airtable-System/sessions/` exists
3. Search for recent sessions to link
4. **Extract from transcript:**
   - Attendees: Amelia, Matt
   - Main topics: QuickBase migration, client tickets setup, R&R workflow
   - Decisions: Communications tied to projects, all clients need projects
   - Action items: Create QB report, import tickets, build scripts
   - Duration estimate: ~2.5 hours based on content depth
5. Generate description from main topics: "quickbase-migration-client-tickets"
6. Create: `Projects/US-Solar-Airtable-System/sessions/2025-11-12-quickbase-migration-client-tickets.md`
7. **Populate with extracted content** from transcript in appropriate sections
8. Confirm creation with summary of what was auto-populated

**Assistant Response**:
"✅ Session note created for **US-Solar-Airtable-System**

Created: `Projects/US-Solar-Airtable-System/sessions/2025-11-12-quickbase-migration-client-tickets.md`

Auto-populated from meeting transcript:
- ✅ 7 accomplishments
- ✅ 3 major decisions documented
- ✅ Action items for Amelia and Matt
- ✅ 4 blockers identified
- ✅ Technical notes and gotchas

Duration: 2.5 hours | Status: Completed"

## Best Practices

1. **CHECK `<env>` FOR DATE FIRST** - Verify current date before creating any session note
2. **Verify month number** - November = 11 (not 01), December = 12 (not 01)
3. **Always use ISO date formats** in frontmatter for proper sorting
4. **Include dataview queries** to automatically link related notes
5. **Set status appropriately** - "active" for ongoing, "completed" if transcript from finished meeting
6. **Auto-link to project README** in Session Context section
7. **Keep project name consistent** with folder structure
8. **Use lowercase with hyphens** for tags (e.g., "us-solar-airtable-system")
9. **Extract content from transcripts** - Don't just copy, organize into structured sections
10. **Generate descriptive filenames** - Use 2-4 words that capture main topics

## Error Handling

### Project Doesn't Exist
If `Projects/[Project-Name]/` doesn't exist:
- Ask user: "I don't see a project folder for '[Project-Name]'. Would you like me to create the project structure first, or did you mean a different project?"
- List available projects

### Sessions Folder Missing
If project exists but no `sessions/` folder:
- Create the folder automatically
- Proceed with session creation
- Inform user: "Created sessions folder for this project"

### Invalid Project Name
If project name has spaces or special characters:
- Suggest the correct folder-friendly format
- Example: "US Solar System" → "US-Solar-System"

## Supporting Files Location

This skill references the following templates in the vault:
- `_templates/session-log-templater.md` - Original Templater version
- `_meta/PIECES-OBSIDIAN-INTEGRATION.md` - Integration guide
- `_meta/PLUGIN-CONFIG.md` - Plugin configuration reference

## Notes for LLM

### CRITICAL - Date Handling
- **ALWAYS check `<env>` section FIRST** for current date
- **Verify month number** (November = 11, NOT 01!)
- **Calculate correct day of week** for human-readable date
- Use **exact date/time from `<env>`**, not placeholder text

### Content Generation
- Replace `[PROJECT-NAME]` in dataview queries with actual project name
- The `<% tp.file.cursor() %>` Templater syntax should be replaced with actual values
- Don't use Templater syntax - generate the actual content
- Keep sections even if empty - user will fill them in

### Session Timing
- The session is created at START of work, not end
- If transcript provided, estimate hours_worked from content depth
- User will update `hours_worked`, `accomplishments`, etc. during/after session

### Transcript Handling
- If user provides transcript, extract and organize content into appropriate sections
- Don't just dump transcript - parse it into structured accomplishments, decisions, action items
- Generate descriptive filename from main topics discussed
