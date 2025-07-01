Update the current development session by:

1. Detect current module from working directory (e.g., if in `modules/frontend/`, module is "frontend")
2. If not in a module directory, ask user to specify module
3. Check if `.claude/sessions/{module}/.current-session` exists to find the active session
4. If no active session for this module, inform user to start one with `/project:session-start`
5. **FIRST**: Use Bash tool to get correct GMT+7 timestamp:
   ```bash
   TZ='Asia/Bangkok' date '+%Y-%m-%d %H:%M'
   ```
6. If session exists, append to the session file with:
   - Current timestamp (GMT+7) - use the bash command result
   - The update: $ARGUMENTS (or if no arguments, summarize recent activities)
   - Git status summary:
     * Files added/modified/deleted (from `git status --porcelain`)
     * Current branch and last commit
   - Todo list status:
     * Number of completed/in-progress/pending tasks
     * List any newly completed tasks
   - Any issues encountered
   - Solutions implemented
   - Code changes made

Keep updates concise but comprehensive for future reference.

Example format:
```
### Update - 2025-06-16 12:15 PM GMT+7

**Summary**: Implemented user authentication

**Git Changes**:
- Modified: app/middleware.ts, lib/auth.ts
- Added: app/login/page.tsx
- Current branch: main (commit: abc123)

**Todo Progress**: 3 completed, 1 in progress, 2 pending
- ✓ Completed: Set up auth middleware
- ✓ Completed: Create login page
- ✓ Completed: Add logout functionality

**Details**: [user's update or automatic summary]
```