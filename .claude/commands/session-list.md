List all development sessions organized by module:

1. Check if `.claude/sessions/` directory exists
2. For each module subdirectory in `.claude/sessions/`:
   - Show module name as header
   - List all `.md` files in that module (excluding `.current-session`)
   - For each session file:
     * Show the filename
     * Extract and show the session title
     * Show the date/time
     * Show first few lines of the overview if available
   - If `.claude/sessions/{module}/.current-session` exists, highlight which session is currently active for that module
3. Sort sessions within each module by most recent first
4. Show modules in alphabetical order

Present in a clean, readable format.