Record a blocker or issue that's preventing progress by:

1. Detect current module from working directory (e.g., if in `modules/frontend/`, module is "frontend")
2. If not in a module directory, ask user to specify module
3. Check if `.claude/sessions/{module}/.current-session` exists to find the active session
4. If no active session for this module, inform user to start one with `/project:session-start`
5. **FIRST**: Use Bash tool to get correct GMT+7 timestamp:
   ```bash
   TZ='Asia/Bangkok' date '+%Y-%m-%d %H:%M'
   ```

6. Add blocker entry with:
   - Current timestamp (GMT+7)
   - Issue ID and/or description from $ARGUMENTS (e.g., "ABC-456 API timeout", "deployment pipeline failing")
   - Impact on current work
   - Potential solutions investigated
   - Resources needed to resolve
   - Workarounds implemented
   - Priority level

**Blocker Entry Format:**
```
### 🚫 BLOCKER - 2025-01-15 16:20 GMT+7

**Issue ID**: ABC-456
**Issue**: API endpoint returning 500 error for user creation
**Impact**: Cannot complete user registration feature
**Priority**: High - blocking main task ABC-123

**Details**:
- POST /api/users consistently fails
- Error: "Database connection timeout"
- Affects both dev and staging environments

**Investigation**:
- Checked database connectivity ✓
- Reviewed API logs - found connection pool exhaustion
- Tested with smaller payloads - same error

**Potential Solutions**:
1. Increase database connection pool size
2. Add request timeout handling  
3. Implement retry logic
4. Contact DevOps for database scaling

**Workaround**: Using mock data for frontend development
**Status**: Escalated to backend team
**Resolution ETA**: Unknown
```

**Usage Examples:**
- `/project:session-blocker ABC-456 API timeout preventing user creation`
- `/project:session-blocker DEF-789 missing test data for integration tests`
- `/project:session-blocker deployment pipeline failing`
- `/project:session-blocker GHI-101 database migration script errors`

This helps track and communicate blockers that need resolution.