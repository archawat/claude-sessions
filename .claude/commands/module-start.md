Start development in a specific module with proper context loading by:

1. Parse module name from $ARGUMENTS (required)
2. If no module name provided, list available modules from `modules/` directory
3. **FIRST**: Use Bash tool to get correct GMT+7 timestamp:
   ```bash
   TZ='Asia/Bangkok' date '+%Y-%m-%d %H:%M'
   ```

4. Check if the specified module exists in `modules/` directory
5. **IMPORTANT**: Check if `modules/{module}/CLAUDE.md` exists
6. Create `.claude/sessions/{module}/` directory if it doesn't exist
7. If module CLAUDE.md doesn't exist, inform user it's required and provide template
8. If module CLAUDE.md exists, display its contents for context loading
9. Remind user of the workflow:
   - Navigate to module directory: `cd modules/{module}`
   - Load module context: `cat CLAUDE.md`
   - Start session: `/project:session-start [task-name]`
   - Sessions will be stored in `.claude/sessions/{module}/`

10. **Multi-Terminal Coordination:**
   
   When working across multiple terminals/sessions on different modules, use session commands for coordination:

   **Recommended Actions:**
   - Use `/project:session-update` when making changes that affect other modules
   - Use `/project:session-blocker` to flag issues impacting other development streams  
   - Use `/project:session-current` to check status of other modules before cross-module changes
   - Check other module sessions in `.claude/sessions/` before making breaking changes

   **Session Files as Communication:**
   - Session files serve as shared state between different development sessions
   - Updates can be read by other developers/sessions to understand current work
   - Broadcast important changes via session updates
   - Share blockers that affect multiple development streams

   **Example Usage:**
   ```bash
   # When changing an API:
   /project:session-update changed user API - added 'role' field - other modules should check session
   
   # When encountering blockers:
   /project:session-blocker DB-123 database migration failing - affects modules using user table
   
   # Before breaking changes:
   /project:session-current  # Check what other modules are working on
   ```

   This enables coordinated parallel development across modules.

**Module CLAUDE.md Template (if missing):**
```markdown
# {Module Name} Module

## Tech Stack
- [List technologies, frameworks, libraries]

## Architecture
- [Module structure and patterns]

## Development Commands
- `[command]` - [description]
- `[command]` - [description]

## Dependencies
- [External dependencies]
- [Integration with other modules]

## API Contracts
- [Endpoints or interfaces this module provides]
- [External APIs this module consumes]

## Testing
- `[test-command]` - [description]
- [Testing strategies and approaches]

## Deployment
- [Build and deployment steps]
- [Environment configurations]

## Notes
- [Important considerations]
- [Common issues and solutions]
```

**Usage Examples:**
- `/project:module-start frontend`
- `/project:module-start backend`
- `/project:module-start user-service`

This ensures proper module context is loaded before development begins.