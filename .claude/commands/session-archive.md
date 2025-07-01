Archive completed sessions to keep the workspace organized by:

1. **FIRST**: Use Bash tool to get correct GMT+7 timestamp:
   ```bash
   TZ='Asia/Bangkok' date '+%Y-%m-%d %H:%M'
   ```

2. If $ARGUMENTS provided, archive specific session(s) from specified module
3. If no arguments, show archival candidates across all modules (completed sessions older than 7 days)

**Archive Process:**
1. For each module, create `.claude/sessions/{module}/archive/` directory if it doesn't exist
2. Move completed session files to the module's archive directory
3. Maintain original filenames but add archive date to content
4. Update any references in `.claude/sessions/{module}/.current-session` if archiving active session
5. Create archive index with session summaries per module

**Auto-archive criteria:**
- Sessions marked as completed
- Sessions with no updates for 7+ days
- Sessions with "archive" or "done" in final update

**Archive format:**
- Original filename preserved
- Archive timestamp added to file header
- Session summary preserved for searchability
- Links to related git commits/branches

**Usage Examples:**
- `/project:session-archive` - Show archival candidates
- `/project:session-archive 2025-01-15-1030-frontend` - Archive specific session
- `/project:session-archive --auto` - Auto-archive old completed sessions

Archived sessions remain searchable but don't clutter active session lists.