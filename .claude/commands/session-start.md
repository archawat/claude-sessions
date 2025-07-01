Start a new development session by creating a session file in the appropriate module directory. Detect current module from working directory and create session in `.claude/sessions/{module}/` with the format `YYYY-MM-DD-HHMM-$ARGUMENTS.md` (or just `YYYY-MM-DD-HHMM.md` if no name provided). Use GMT+7 timezone for all timestamps.

**IMPORTANT**: Always use the Bash tool to get the correct GMT+7 timestamp to prevent date/time errors:

```bash
# Get current GMT+7 time for filename
TZ='Asia/Bangkok' date '+%Y-%m-%d-%H%M'

# Get current GMT+7 time for display
TZ='Asia/Bangkok' date '+%Y-%m-%d %H:%M'
```

**Implementation Steps:**
1. **FIRST**: Use Bash tool to get correct GMT+7 timestamp
2. Detect current module from working directory (e.g., if in `modules/frontend/`, module is "frontend")
3. If not in a module directory, ask user to specify module or use "general"
4. Create `.claude/sessions/{module}/` directory if it doesn't exist
5. Use the timestamp to create the session filename in the module directory
6. Use the same timestamp in the file content
7. Create the session file with proper GMT+7 timestamps

The session file should begin with:
1. Session name and timestamp as the title (GMT+7)
2. Session overview section with start time (GMT+7)
3. Goals section (ask user for goals if not clear)
4. Empty progress section ready for updates

After creating the file, create or update `.claude/sessions/{module}/.current-session` to track the active session filename for this module using the Write tool (not bash echo).

Confirm the session has started and remind the user they can:
- Update it with `/project:session-update`
- End it with `/project:session-end`