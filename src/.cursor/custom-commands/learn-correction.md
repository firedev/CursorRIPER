# CursorRIPER Framework - Correction Learning Callback
# Version 1.0.0

## CORRECTION CALLBACK OVERVIEW

The correction learning callback system captures knowledge gained when the user has to correct the AI's behavior or understanding. It specifically stores only deviations from expected behavior to prevent repeating mistakes in future interactions.

## COMMAND FORMAT

```
/learn "What was wrong" "The correct approach" "Why this matters"
```

OR

```
/correct "Incorrect assumption or action" "Correct understanding" "Context or reasoning"
```

OR direct feedback mode:

```
No, that's not correct. [Explanation of the correct approach]
```

## CALLBACK TRIGGERS

The callback is activated when:

1. **Explicit correction commands** are used
2. **Natural correction language** is detected ("No, that's not correct", "That's wrong", etc.)
3. **Code changes** that revert or significantly modify AI-generated code
4. **Auto-detection** of correction patterns through:
   - User edits to AI-generated code
   - Rejection of AI-suggested approaches
   - Consistent alternative implementations
   - Follow-up clarifications on how things should work

## KNOWLEDGE STORAGE

Corrections are stored in a special file `learnings.md` in the memory bank with the following structure:

### Correction Entry Format

```markdown
## [Timestamp] - [Topic]

**Incorrect Assumption**:
[Description of what the AI got wrong]

**Correct Approach**:
[Description of the correct understanding or implementation]

**Context/Reasoning**:
[Why this is important and contextual factors]

**Code Pattern** (if applicable):
```[language]
[Code example showing correct pattern]
```

**Applies To**:
[List of file patterns, components, or scenarios where this learning applies]
```

## IMPLEMENTATION DETAILS

1. Knowledge is **indexed by topic** for easy retrieval
2. Only **non-standard learnings** are stored (things that deviate from documented patterns)
3. Learnings are **automatically retrieved** when working on similar files or components
4. Entries include **enough context** to prevent overgeneralization
5. The system **merges similar corrections** to prevent duplication
6. Entries have **expiration policies** based on project changes

## AUTO-LEARNING SYSTEM

The correction learning system features autonomous learning capabilities to minimize manual intervention:

### Auto-Detection Mechanisms

1. **Code Diff Analysis**:
   - Automatically compares AI-generated code with user-edited versions
   - Identifies patterns in changes (style, structure, naming, logic)
   - Creates learning entries from recurring modifications

2. **Conversation Pattern Recognition**:
   - Identifies correction language without explicit commands
   - Recognizes expressions of preference or better practices
   - Detects when explanations contradict AI assumptions

3. **Workflow Monitoring**:
   - Observes when user consistently applies different patterns
   - Tracks approaches that differ from AI suggestions
   - Recognizes rejections of proposed solutions

### Confidence Scoring

Automatic learning entries are assigned confidence scores:

| Confidence | Trigger | Action |
|------------|---------|--------|
| High (0.8+) | Explicit correction, multiple occurrences | Auto-apply without confirmation |
| Medium (0.5-0.8) | Consistent pattern in edits | Apply with minimal notification |
| Low (0.3-0.5) | Potential pattern detected | Suggest learning with confirmation |

### Periodic Digests

The system minimizes interruptions through:

1. **Silent Learning Mode**: Records corrections without immediate confirmation
2. **Session Digest**: Summarizes learnings at the end of coding sessions
3. **Approval Interface**: Simple accept/reject/modify options for detected learnings
4. **Batch Processing**: Groups similar learnings for efficient review

### Self-Optimization

The learning system improves itself by:

1. Tracking which auto-detected learnings are confirmed vs. rejected
2. Adjusting detection sensitivity based on user patterns
3. Refining categorization logic through use
4. Consolidating similar learnings to avoid fragmentation

## USAGE

To add a new learning:

```
/learn "Using synchronous file operations blocks the event loop" "Use async fs operations with proper error handling" "Critical for performance in high-load scenarios"
```

To report an incorrect assumption:

```
/correct "User always provides a valid email" "Input validation is required for all email fields" "Security and UX best practice"
```

To view current learnings:

```
/learnings:view [topic]
```

To apply learnings to a specific component:

```
/learnings:apply [component]
```

To toggle auto-learning:

```
/learnings:auto [on|off]
```

To adjust auto-learning sensitivity:

```
/learnings:sensitivity [high|medium|low]
```

To view what's been auto-learned in current session:

```
/learnings:digest
```

---

*This command implements the correction learning system for the CursorRIPER Framework.*
