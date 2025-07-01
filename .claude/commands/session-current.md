Show the current session status by:

1. Detect current module from working directory (e.g., if in `modules/frontend/`, module is "frontend")
2. If not in a module directory, ask user to specify module or show all active sessions
3. Check if `.claude/sessions/{module}/.current-session` exists
4. If no active session for this module, inform user and suggest starting one
5. If active session exists:
   - Show session name and filename
   - Calculate and show duration since start
   - Show last few updates
   - Show current goals/tasks
   - Remind user of available commands

Keep the output concise and informative.