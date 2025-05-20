# Project Learnings
# Version: 1.0.0
# Last Updated: {{TIMESTAMP}}

This file tracks correction-based learnings specific to this project, focusing on deviations from standard practices or expectations that should be remembered to prevent repeated mistakes.

## Code Patterns

*Learnings about code implementations specific to this project*

<!-- Example:
## 2023-06-15 - Async File Handling

**Incorrect Assumption**:
Using synchronous file operations (fs.readFileSync) for all file access is acceptable.

**Correct Approach**:
All file operations must use async patterns with proper error handling, especially in server contexts.

**Context/Reasoning**:
This project handles high volumes of concurrent requests, and synchronous operations block the event loop.

**Code Pattern**:
```javascript
// Instead of:
const data = fs.readFileSync(filePath, 'utf8');

// Use:
try {
  const data = await fs.promises.readFile(filePath, 'utf8');
  // process data
} catch (error) {
  logger.error(`Failed to read file ${filePath}`, error);
  // handle error appropriately
}
```

**Applies To**:
- All server-side file operations
- Components: UserDataService, ReportGenerator
-->

## Workflow Rules

*Learnings about how work should be approached or managed*

<!-- Example:
## 2023-06-20 - Component Creation Process

**Incorrect Assumption**:
New components can be created directly in the components folder without following the project patterns.

**Correct Approach**:
All new components must:
1. Be created in their own directory
2. Include a test file
3. Follow the established naming convention (PascalCase for components)
4. Export from an index.ts file

**Context/Reasoning**:
This structure ensures consistency, testability, and proper code organization across the project.

**Applies To**:
- All new UI components
- Feature modules
-->

## Project Preferences

*Learnings about project-specific conventions or choices*

<!-- Example:
## 2023-06-25 - State Management

**Incorrect Assumption**:
Redux can be used for all state management needs.

**Correct Approach**:
- Use local React state for component-specific state
- Use Context API for shared state within a feature
- Use Redux only for global application state

**Context/Reasoning**:
This approach reduces boilerplate and improves performance by avoiding unnecessary re-renders.

**Applies To**:
- All new features
- State management decisions
-->

## Domain Knowledge

*Learnings about the problem domain or business logic*

<!-- Example:
## 2023-07-01 - User Roles

**Incorrect Assumption**:
User permissions are binary (can access or cannot access).

**Correct Approach**:
User permissions follow a hierarchical model with 5 distinct levels:
1. Viewer
2. Editor
3. Manager
4. Admin
5. System Admin

Each role inherits permissions from lower roles with additional capabilities.

**Context/Reasoning**:
The application's security model requires fine-grained control over resource access.

**Applies To**:
- Authentication flows
- Authorization checks
- User management features
-->

## Technical Constraints

*Learnings about limitations or requirements of the system*

<!-- Example:
## 2023-07-05 - API Response Size

**Incorrect Assumption**:
API responses can include complete data sets for client-side filtering.

**Correct Approach**:
All API endpoints must:
1. Implement pagination (max 100 items per page)
2. Allow filtering via query parameters
3. Include total count metadata

**Context/Reasoning**:
The application deals with large datasets that can cause performance issues if transmitted in full.

**Code Pattern**:
```typescript
// API Response Structure
interface PaginatedResponse<T> {
  data: T[];
  meta: {
    total: number;
    page: number;
    pageSize: number;
    totalPages: number;
  }
}
```

**Applies To**:
- All list/collection API endpoints
- Data fetching logic
-->

---

*This file is automatically updated by the CursorRIPER correction learning system. Manual edits are preserved.*
