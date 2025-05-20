# CursorRIPER Framework - Cursor IDE Commands
# Version 1.0.1

## CURSOR-SPECIFIC COMMAND REFERENCE

This file defines special commands and features specific to Cursor IDE that enhance the CursorRIPER Framework.

## SPECIAL SHORTCUTS

| Command | Syntax | Description |
|---------|--------|-------------|
| Quick Mode Switch | `@research`, `@innovate`, etc. | Shorthand for mode switching |
| File Reference | `@file:path/to/file.js` | Reference a specific file |
| Line Reference | `@line:file.js:25-30` | Reference specific lines in a file |
| Search Codebase | `@search:pattern` | Quick search throughout codebase |
| View Memory | `@memory:activeContext` | View specific memory bank file |

## ENHANCED CONTEXT AWARENESS

### Editor State
- Active file(s) are automatically incorporated into responses
- Cursor position is tracked for focused edits
- Recently viewed files are tracked for relevant suggestions

### IDE Integration
- Error messages and warnings are automatically considered
- Terminal output can be referenced with `@terminal`
- Test results can be referenced with `@tests`

## WORKFLOW INTEGRATIONS

### Research Mode Enhancements
- `@inspect file.js` - Detailed file analysis
- `@related Component` - Find files related to a component
- `@dependencies Module` - List dependencies of a module

### Plan Mode Enhancements
- `@visualize component` - Generate component structure diagram
- `@changes file.js` - Outline changes planned for file
- `@impact Module` - Assess impact of planned changes

### Execute Mode Enhancements
- `@checkpoint` - Create a save point before major changes
- `@diff file.js` - Show changes made to file
- `@revert file.js` - Revert specific file changes

## MEMORY BANK EXTENSIONS

### Auto-Documentation
- Code changes are automatically recorded in appropriate memory bank files
- References to documentation are preserved across sessions
- Implementation notes are captured during work

### Smart Context
- `@focus Feature` - Set the current focus area in activeContext.md
- `@snapshot` - Create a snapshot of current project state
- `@recap` - Summarize recent work from memory bank

### Correction Learning
- `@learn "wrong" "right" "why"` - Record a correction learning
- `@correct "assumption" "reality" "context"` - Record a correction
- `@learnings:view topic` - View learnings for a specific topic
- `@learnings:apply component` - Apply learnings to a component
- `@learnings:auto on|off` - Toggle automatic learning
- `@learnings:sensitivity level` - Set sensitivity (high|medium|low)
- `@learnings:digest` - View what's been learned in current session
- `@learnings:approve` - Batch approve pending learnings

## COMMAND USAGE

Commands can be used as standalone instructions or embedded within other requests:

```
@research
Can you examine the authentication system?
```

Or:

```
Please @inspect auth.js and check for security issues.
```

---

*This file defines Cursor-specific commands for the CursorRIPER Framework.*
