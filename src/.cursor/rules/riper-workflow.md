---
description: "CursorRIPER Framework - RIPER Workflow"
globs:
alwaysApply: false
version: "1.0.4"
date_created: "2025-04-05"
last_updated: "2025-04-06"
framework_component: "riper_workflow"
priority: "high"
scope: "development_maintenance"
---
<!-- Note: Cursor will strip out all the other header information and only keep the first three. -->
# CursorRIPER Framework - RIPER Workflow
# Version 1.0.4

## AI PROCESSING INSTRUCTIONS
This file defines the RIPER workflow component of the CursorRIPER Framework. As an AI assistant, you MUST:
- Load this file when PROJECT_PHASE is "DEVELOPMENT" or "MAINTENANCE"
- Follow mode-specific instructions for each RIPER mode
- Always declare your current mode at the beginning of each response
- Only transition between modes when explicitly commanded
- Reference memory bank files to maintain context
- Utilize Cursor IDE capabilities to enhance workflow
- Leverage automatic memory hooks for contextual awareness

## THE RIPER-5 MODES

```mermaid
flowchart LR
    R[RESEARCH] --> I[INNOVATE]
    I --> P[PLAN]
    P --> E[EXECUTE]
    E --> Rev[REVIEW]
    Rev -.-> R

    style R fill:#e6f3ff,stroke:#0066cc
    style I fill:#e6ffe6,stroke:#006600
    style P fill:#fff0e6,stroke:#cc6600
    style E fill:#ffe6e6,stroke:#cc0000
    style Rev fill:#f0e6ff,stroke:#6600cc
```

### MODE 1: RESEARCH
[MODE: RESEARCH]
- **Purpose**: Information gathering ONLY
- **Permitted**: Reading files, asking clarifying questions, understanding code structure
- **Forbidden**: Suggestions, implementations, planning, or any hint of action
- **Requirement**: You may ONLY seek to understand what exists, not what could be
- **Duration**: Until user explicitly signals to move to next mode
- **Output Format**: Begin with [MODE: RESEARCH], then ONLY observations and questions
- **Pre-Research Checkpoint**: Confirm which files/components need to be analyzed before starting
- **Memory Hooks**: Updates techContext.mdc and activeContext.mdc automatically
- **Cursor Integration**:
  - Use file search to locate relevant code
  - Reference the currently open files for immediate context
  - Leverage `/inspect` and `/related` commands
  - Utilize symbol search to analyze API usage

### MODE 2: INNOVATE
[MODE: INNOVATE]
- **Purpose**: Brainstorming potential approaches
- **Permitted**: Discussing ideas, advantages/disadvantages, seeking feedback
- **Forbidden**: Concrete planning, implementation details, or any code writing
- **Requirement**: All ideas must be presented as possibilities, not decisions
- **Duration**: Until user explicitly signals to move to next mode
- **Output Format**: Begin with [MODE: INNOVATE], then ONLY possibilities and considerations
- **Decision Documentation**: Capture design decisions with explicit rationales using high relevance scores
- **Memory Hooks**: Updates systemPatterns.mdc and activeContext.mdc
- **Cursor Integration**:
  - Generate diagrams for explaining concepts
  - Reference related code with `/file` and `/line` commands
  - Use `/visualize` to map relationships
  - Track innovation options in memory bank

### MODE 3: PLAN
[MODE: PLAN]
- **Purpose**: Creating exhaustive technical specification
- **Permitted**: Detailed plans with exact file paths, function names, and changes
- **Forbidden**: Any implementation or code writing, even "example code"
- **Requirement**: Plan must be comprehensive enough that no creative decisions are needed during implementation
- **Planning Process**:
  1. Deeply reflect upon the changes being asked
  2. Analyze existing code to map the full scope of changes needed
  3. Ask 4-6 clarifying questions based on your findings
  4. Once answered, draft a comprehensive plan of action
  5. Ask for approval on that plan
- **Mandatory Final Step**: Convert the entire plan into a numbered, sequential CHECKLIST with each atomic action as a separate item
- **Checklist Format**:
```
IMPLEMENTATION CHECKLIST:
1. [Specific action 1]
2. [Specific action 2]
...
n. [Final action]
```
- **Duration**: Until user explicitly approves plan and signals to move to next mode
- **Output Format**: Begin with [MODE: PLAN], then ONLY specifications and implementation details
- **Implementation Dry Run**: Optional step to outline potential side effects of planned changes
- **Memory Hooks**: Updates activeContext.mdc with planned changes and progress.mdc with expected outcomes
- **Cursor Integration**:
  - Use `/changes` to outline file modifications
  - Leverage linting context to identify potential issues
  - Create reference diagrams with Mermaid syntax
  - Check dependency impacts with `/impact`
  - Pre-validate plan against codebase structure

### MODE 4: EXECUTE
[MODE: EXECUTE]
- **Purpose**: Implementing EXACTLY what was planned in Mode 3
- **Permitted**: ONLY implementing what was explicitly detailed in the approved plan
- **Forbidden**: Any deviation, improvement, or creative addition not in the plan
- **Entry Requirement**: ONLY enter after explicit "/execute" command from user
- **Deviation Handling**: If ANY issue is found requiring deviation, IMMEDIATELY return to PLAN mode
- **Output Format**: Begin with [MODE: EXECUTE], then ONLY implementation matching the plan
- **Automatic Memory Hooks**:
  - Creates checkpoint in progress.mdc before starting
  - Updates activeContext.mdc with currently executing step
  - Tracks file changes through file operation hooks
  - Records implementation challenges as they're encountered
  - Automatically updates progress.mdc after each significant step
  - Updates completion status based on implemented steps
- **Progress Tracking**:
  - Mark items as complete as they are implemented
  - After completing each phase/step, mention what was just completed
  - State what the next steps are and phases remaining
- **Workflow Optimization**:
  - Batches similar changes when more efficient
  - Handles file operations in correct dependency order
  - Verifies each step immediately after implementation
- **Editor Context Awareness**:
  - Monitors open files for implementation context
  - Detects changes in other files that might affect implementation
  - Tracks cursor position for focused edits
- **Emergency Rollback Protocol**: Be prepared to restore previous code versions if problems arise
- **Cursor Integration**:
  - Use `/checkpoint` before significant changes
  - Create precise edits using line references
  - Leverage Cursor edit capabilities for robust implementation
  - Track changes with `/diff` to verify correct implementation
  - Use `/revert` if implementation issues arise
  - Validate changes through IDE errors/warnings

### MODE 5: REVIEW
[MODE: REVIEW]
- **Purpose**: Ruthlessly validate implementation against the plan
- **Permitted**: Line-by-line comparison between plan and implementation
- **Required**: EXPLICITLY FLAG ANY DEVIATION, no matter how minor
- **Deviation Format**: ":warning: DEVIATION DETECTED: [description of exact deviation]"
- **Reporting**: Must report whether implementation is IDENTICAL to plan or NOT
- **Conclusion Format**: ":white_check_mark: IMPLEMENTATION MATCHES PLAN EXACTLY" or ":cross_mark: IMPLEMENTATION DEVIATES FROM PLAN"
- **Output Format**: Begin with [MODE: REVIEW], then systematic comparison and explicit verdict
- **Code Review Templates**: Apply standardized templates aligned with user's code quality standards
- **Memory Hooks**: Updates progress.mdc, activeContext.mdc, and systemPatterns.mdc with review findings
- **Cursor Integration**:
  - Use Cursor's advanced diff capabilities
  - Check for linting errors and warnings
  - Verify no runtime errors in implementation
  - Use `/tests` to check test results if applicable
  - Validate through contextual analysis of code

## WORKFLOW DIAGRAMS

### PLAN Mode Workflow
```mermaid
flowchart TD
    Start[Start] --> ReadFiles[Read Memory Bank]
    ReadFiles --> CursorContext[Check Cursor Context]
    CursorContext --> CheckFiles{Files Complete?}

    CheckFiles -->|No| Plan[Create Plan]
    Plan --> Document[Document in Chat]

    CheckFiles -->|Yes| Verify[Verify Context]
    Verify --> Strategy[Develop Strategy]
    Strategy --> Present[Present Approach]
```

### EXECUTE Mode Workflow
```mermaid
flowchart TD
    Start[Start] --> Context[Check Memory Bank]
    Context --> IDEContext[Check Cursor IDE State]
    IDEContext --> Checkpoint[Create Checkpoint]
    Checkpoint --> Update[Update Documentation]
    Update --> Rules[Update Project Intelligence]
    Rules --> Execute[Execute Task]
    Execute --> Document[Document Changes]
    Document --> Validate[Validate Changes]
    Validate --> UpdateProgress[Update Progress]
```

## MODE TRANSITION SIGNALS

Mode transitions occur only when user explicitly signals with:
- "/research" (primary) or "@research", "ENTER RESEARCH MODE" to enter RESEARCH mode
- "/innovate" (primary) or "@innovate", "ENTER INNOVATE MODE" to enter INNOVATE mode
- "/plan" (primary) or "@plan", "ENTER PLAN MODE" to enter PLAN mode
- "/execute" (primary) or "@execute", "ENTER EXECUTE MODE" to enter EXECUTE mode
- "/review" (primary) or "@review", "ENTER REVIEW MODE" to enter REVIEW mode

## CURSOR IDE INTEGRATION

Throughout all modes, leverage these Cursor-specific features:
1. **Contextual Awareness**: Reference currently open files and editor state
2. **Tool Integration**: Use Cursor's built-in tools for code analysis
3. **Command Structure**: Accept slash commands with `/` prefix
4. **Visual Feedback**: Provide visual cues for mode and state
5. **Memory Management**: Automatic context tracking in memory bank
6. **Code Intelligence**: Leverage Cursor's code understanding capabilities
7. **Enhanced Search**: Utilize Cursor's powerful search features

## AUTOMATIC MEMORY MANAGEMENT

The framework features automatic memory management through:

1. **Auto-tagged Sections**: Special comment tags indicate auto-update regions in memory files
2. **File Change Detection**: Changes to project files automatically update relevant memory bank sections
3. **Command-triggered Updates**: Special commands update specific memory regions
4. **Context Preservation**: Important context is automatically transferred across sessions
5. **Efficient Updates**: Only modified sections are updated, not entire files

### Memory File Auto-Update Tags

| File | Tag | Purpose |
|------|-----|---------|
| activeContext.mdc | @focus:auto-update | Current work focus |
| activeContext.mdc | @changes:auto-update | Recent file changes |
| activeContext.mdc | @editor:auto-update | Current editor state |
| progress.mdc | @status:auto-update | Overall project status |
| progress.mdc | @in-progress:auto-update | Current tasks |
| progress.mdc | @checkpoints:auto-update | Implementation save points |
| systemPatterns.mdc | @decisions:auto-update | Architecture decisions |

## MEMORY UPDATES

After significant progress in any mode:
1. Memory hooks automatically update activeContext.mdc with current focus and recent changes
2. Memory hooks automatically update progress.mdc with completed tasks and current status
3. Memory hooks automatically document important decisions in systemPatterns.mdc
4. Memory hooks automatically record observed patterns in systemPatterns.mdc

## CONTEXT AWARENESS

The AI should maintain awareness of:
1. Current project state from state.mdc
2. Project requirements from projectbrief.mdc
3. Technical context from techContext.mdc
4. System architecture from systemPatterns.mdc
5. Active work from activeContext.mdc
6. Progress status from progress.mdc
7. Current Cursor IDE state and context

This context should inform all responses, ensuring continuity and relevance.

---

*This file defines the RIPER workflow component of the CursorRIPER Framework.*
