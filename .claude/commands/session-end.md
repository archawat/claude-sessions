End the current development session by:

1. Detect current module from working directory (e.g., if in `modules/frontend/`, module is "frontend")
2. If not in a module directory, ask user to specify module
3. Check `.claude/sessions/{module}/.current-session` for the active session
4. If no active session for this module, inform user there's nothing to end
5. **FIRST**: Use Bash tool to get correct GMT+7 timestamp:
   ```bash
   TZ='Asia/Bangkok' date '+%Y-%m-%d %H:%M'
   ```
6. If session exists, append a comprehensive summary including:
   - Session duration (calculate from start time to current GMT+7 time - use bash command result)
   - Git summary:
     * Total files changed (added/modified/deleted)
     * List all changed files with change type
     * Number of commits made (if any)
     * Final git status
   - Todo summary:
     * Total tasks completed/remaining
     * List all completed tasks
     * List any incomplete tasks with status
   - Key accomplishments
   - All features implemented
   - Problems encountered and solutions
   - Breaking changes or important findings
   - Dependencies added/removed
   - Configuration changes
   - Deployment steps taken
   - Lessons learned
   - What wasn't completed
   - Tips for future developers

7. Empty the `.claude/sessions/{module}/.current-session` file (don't remove it, just clear its contents)
8. Inform user the session has been documented

The summary should be thorough enough that another developer (or AI) can understand everything that happened without reading the entire session.