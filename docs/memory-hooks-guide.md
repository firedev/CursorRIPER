# CursorRIPER Framework - Memory Hooks Guide
# Version 1.0.1

## Overview

This guide explains how the automatic memory hooks system works in the CursorRIPER Framework, providing efficient context tracking and memory updates.

## What Are Memory Hooks?

Memory hooks are special triggers that automatically update the memory bank files based on actions in Cursor IDE. They eliminate the need for manual updates and ensure consistent context across sessions.

## Key Benefits

- **Automatic Context Tracking**: No need to manually update memory files
- **Immediate Reflection**: Changes are reflected in memory immediately
- **Reduced Overhead**: Less manual documentation needed
- **Consistent Structure**: Memory files maintain a consistent format
- **Enhanced Continuity**: Better session-to-session continuity

## Hook Types

### Mode Transition Hooks

When switching between RIPER modes, hooks automatically:
- Update state.mdc with the new mode
- Update activeContext.mdc with mode-specific information
- Prepare relevant memory sections for the new mode

Example:
```
/research
```
Automatically updates:
- state.mdc with RIPER_CURRENT_MODE = "RESEARCH"
- activeContext.mdc focus section with research context
- Refreshes editor context in activeContext.mdc

### File Operation Hooks

When files are created, modified, or deleted:
- Changes are detected automatically
- Relevant sections in memory bank files are updated
- File relationships are tracked for dependency analysis

Example operations that trigger hooks:
- Creating a new component file
- Modifying an existing service
- Deleting an unused utility

### Command Hooks

Special commands trigger specific memory updates:

| Command | Effect |
|---------|--------|
| `/focus X` | Updates current focus in activeContext.mdc |
| `/checkpoint` | Creates save point in progress.mdc |
| `/decision X` | Records decision in systemPatterns.mdc |
| `/progress` | Updates status in progress.mdc |

### Session Hooks

When starting or ending a session:
- Current state is preserved
- Recent changes are summarized
- Focus areas are maintained

## Auto-Update Regions

Memory bank files contain special comment tags that mark regions for automatic updates:

```markdown
## Current Focus
<!-- @focus:auto-update -->
Currently working on authentication system implementation
<!-- @focus:end -->
```

The content between these tags is managed by memory hooks.

## Memory Files and Their Hooks

| File | Hook Regions | Update Triggers |
|------|--------------|----------------|
| activeContext.mdc | focus, changes, editor | Mode changes, file operations, /focus command |
| progress.mdc | status, in-progress, checkpoints | Step completion, /checkpoint, /progress |
| systemPatterns.mdc | decisions, patterns, debt | /decision, architecture changes |
| techContext.mdc | technologies, environment | New dependencies, environment changes |

## Implementation Details

### How Hooks Detect Changes

1. **Editor State**: Monitoring open files and cursor positions
2. **File System**: Tracking file creation and modification
3. **Command Input**: Processing special / commands
4. **Mode Transitions**: Detecting mode change commands

### How Updates Are Applied

1. Content between auto-update tags is replaced
2. Only relevant sections are modified
3. Updates are formatted according to file templates
4. Timestamps are added automatically

## Using Memory Hooks Effectively

### Best Practices

1. **Use Command Format**: Leverage /commands for explicit updates
2. **Trust Automatic Updates**: Let hooks handle routine documentation
3. **Review Memory Files**: Periodically check for accurate context
4. **Customize Tags**: Add custom auto-update regions as needed

### Common Commands

```
/focus Authentication
```
Sets the current focus area in activeContext.mdc

```
/checkpoint auth-complete
```
Creates a named checkpoint in progress.mdc

```
/decision "Use JWT for authentication" "Better for stateless API"
```
Records a design decision in systemPatterns.mdc

## Advanced Usage

### Creating Custom Hooks

You can define custom hooks in `.cursor/memory-hooks.mdc`:

```
## CUSTOM HOOKS

- name: "deployment"
  file: "progress.mdc"
  tag: "deployments"
  trigger: "/deploy"
```

### Disabling Hooks

To temporarily disable hooks:

```
/memory:pause
```

To re-enable:

```
/memory:resume
```

### Manual Control

For manual updates:

```
/memory:update activeContext
```

---

*This guide covers the memory hooks system in the CursorRIPER Framework. For general framework usage, see the main documentation.*
