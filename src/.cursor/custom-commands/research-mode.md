# CursorRIPER - Enhanced Research Mode
# Version 1.0.0

## COMMAND DESCRIPTION
This command activates the RESEARCH mode with enhanced Cursor-specific features.

## COMMAND STRUCTURE
```
@research [optional_focus_area]
```

## COMMAND BEHAVIOR
1. Switches to RESEARCH mode
2. Updates project state to reflect current mode
3. If optional_focus_area is provided, sets the focus in activeContext.md
4. Enables all Cursor-specific research tools:
   - File inspection
   - Codebase search
   - Relationship analysis
   - Symbol reference exploration

## CURSOR INTEGRATION FEATURES

### Context Awareness
- References currently open files
- Considers cursor position in code
- Analyzes recent navigation history

### Visual Indicators
- Mode is explicitly shown at the beginning of responses
- References to files use consistent formatting
- Code snippets are properly highlighted

### Search Capabilities
- Symbol search across the codebase
- File text content search
- Import/export relationship mapping

## USAGE EXAMPLES

### Basic Research Mode Activation
```
@research
```

### Research with Focus Area
```
@research authentication
```

### Research with File Focus
```
@research @file:src/auth/service.js
```

## RELATED COMMANDS
- `@inspect [file]` - Deep analysis of a specific file
- `@search:[pattern]` - Search codebase for pattern
- `@related [component]` - Find related components
- `@dependencies [module]` - Analyze dependencies

---

*This command activates the enhanced Research mode in the CursorRIPER Framework.*
