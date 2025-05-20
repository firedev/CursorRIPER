# CursorRIPER Framework - Cursor IDE Integration Guide

## Overview

This guide explains how to effectively leverage Cursor IDE's features with the CursorRIPER Framework for a more streamlined and powerful development experience.

## Quick Mode Switching

Cursor allows for quick mode switching using the `@` prefix command:

```
@research
// Starts or switches to Research mode
```

This is equivalent to typing `/research` or "ENTER RESEARCH MODE" but is much faster and recognizes the command even when embedded within text.

## Enhanced File Operations

### File References

Reference files directly using:

```
@file:path/to/file.js
```

This tells CursorRIPER to focus on that specific file during operations.

### Line References

Reference specific lines of code:

```
@line:utils.js:25-30
```

This helps during discussions or when planning precise changes.

## Context-Aware Workflows

### Editor Context

CursorRIPER automatically:
- Analyzes currently open files
- Considers cursor position
- Tracks recently viewed files
- Monitors unsaved changes

### Navigation

Move between related files with special commands:
- `@related Component` - Find files related to a component
- `@dependencies Module` - See what depends on a module

## Mode-Specific Enhancements

### Research Enhancements

```
@inspect auth.js
```
Performs deep analysis of a file including:
- Function signatures
- API patterns
- Documentation
- Import/export relationships

### Plan Enhancements

```
@visualize AuthFlow
```
Generates:
- Component relationship diagrams
- Data flow visualizations
- Architecture maps

### Execute Enhancements

```
@checkpoint
```
Create save points before significant changes:
- Marks current state in memory bank
- Updates progress tracking
- Creates mental checkpoints for rollback

## Memory Bank Integration

### Smart Context Management

```
@focus Authentication
```
Sets current focus area in `activeContext.md` and enables:
- Automatic progress tracking
- Context-specific responses
- Intelligent file suggestions

### Project History

```
@recap
```
Generates a summary of recent work from the memory bank to help maintain continuity between sessions.

## Best Practices

1. **Always Begin With Research**: Start every new task with `@research` to avoid premature implementation
2. **Use Checkpoints**: Create checkpoints with `@checkpoint` before major code changes
3. **Leverage Context**: Let CursorRIPER know what you're focusing on with `@focus X`
4. **Document Decisions**: Use `@decision X` to record important decisions in the memory bank
5. **Track Progress**: Update progress explicitly with `@progress` to maintain accurate records

## Cursor-Specific Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `@search:x` | Search codebase | `@search:authenticateUser` |
| `@inspect x` | Analyze file/component | `@inspect LoginForm.tsx` |
| `@related x` | Find related components | `@related AuthController` |
| `@visualize x` | Generate diagrams | `@visualize DataFlow` |
| `@changes x` | Plan changes to file | `@changes api.js` |
| `@checkpoint` | Create a save point | `@checkpoint` |
| `@diff x` | Show changes to file | `@diff users.model.js` |
| `@revert x` | Revert changes | `@revert auth.service.js` |
| `@focus x` | Set focus area | `@focus PaymentProcessing` |
| `@recap` | Summarize recent work | `@recap` |

## Troubleshooting

### Command Not Recognized

If a command isn't working:
1. Ensure the command starts with `@` with no spaces
2. Check that the command is spelled correctly
3. Verify the command is supported in the current mode

### Context Issues

If CursorRIPER seems to miss context:
1. Use `@memory:activeContext` to view the current context
2. Update the context with `@focus X` if needed
3. Use `@recap` to summarize recent work

### File References

If file references aren't working:
1. Ensure paths are relative to project root
2. Check for typos in filenames
3. Verify the file exists in the project

## Examples

### Research Phase Example

```
@research
I need to understand how the authentication flow works in our application.
@inspect auth/authService.js
```

### Plan Phase Example

```
@plan
We need to add two-factor authentication to our login process.
@changes auth/login.js
@visualize AuthFlow
```

### Execution Phase Example

```
@execute
@checkpoint
Let's implement the OTP verification as planned in step 4.
```

---

*This guide covers the integration between CursorRIPER Framework and Cursor IDE. For general CursorRIPER usage, see the main documentation.*
