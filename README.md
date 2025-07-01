# Claude Session Management Template

A comprehensive template for managing Claude development sessions across multi-module projects with structured documentation and session tracking.

## Project Structure

```
{project-root}/
├── CLAUDE.md                   # Project memory and architecture
├── README.md                   # This file - usage instructions
├── .gitignore                  # Excludes modules/ and sessions/
├── .claude/
│   ├── sessions/              # Session files organized by module
│   │   ├── .gitkeep          # Preserves directory structure
│   │   ├── frontend/          # Frontend module sessions
│   │   │   ├── .gitkeep      # Preserves directory structure
│   │   │   ├── .current-session (created when session starts)
│   │   │   ├── 2025-01-15-1030-task.md (example session)
│   │   │   └── archive/       # Archived sessions
│   │   ├── backend/           # Backend module sessions
│   │   │   ├── .gitkeep      # Preserves directory structure
│   │   │   ├── .current-session (created when session starts)
│   │   │   └── 2025-01-15-1100-api.md (example session)
│   │   └── shared/            # Shared/general sessions
│   │       └── .gitkeep      # Preserves directory structure
│   └── commands/              # Session management commands
├── modules/                   # Module directories (git-ignored)
│   ├── frontend/              # Each has own git repo
│   ├── backend/
│   ├── database/
│   └── shared/
└── scripts/                   # Helper scripts (optional)
```

## Getting Started

### 1. Initial Setup

Copy this template to your project root:
```bash
cp -r claude-session-template/* your-project/
cd your-project
```

### 2. Configure Project Memory

Edit `CLAUDE.md` to describe your project architecture and modules.

### 3. Create Module Memory Files

**IMPORTANT: Every module MUST have its own `CLAUDE.md` file** with module-specific context.

This file serves as the single source of truth for module development and is required before starting development work.

```bash
# Example: modules/frontend/CLAUDE.md
echo "# Frontend Module

## Tech Stack
- React 18 with TypeScript
- Tailwind CSS
- React Router
- Axios for API calls

## Architecture
- Component-based architecture
- State management with Context API
- Custom hooks for business logic

## Development Commands
- \`npm run dev\` - Start development server
- \`npm run build\` - Build for production
- \`npm run test\` - Run test suite
- \`npm run lint\` - Run ESLint

## Dependencies
- External APIs: Backend REST API
- Shared libraries: ../shared/types/, ../shared/utils/

## API Contracts
- Consumes: /api/users, /api/auth, /api/products
- Authentication: JWT tokens via Authorization header

## Testing
- \`npm run test\` - Jest unit tests
- \`npm run test:e2e\` - Cypress integration tests
- Test coverage target: >80%

## Deployment
- Build target: static files for CDN
- Environment variables: REACT_APP_API_URL

## Notes
- Use TypeScript strict mode
- Follow component naming convention: PascalCase
- API calls through axios interceptors for auth
" > modules/frontend/CLAUDE.md
```

**Module CLAUDE.md Template:**

Every module should include these sections:
- **Tech Stack** - Technologies, frameworks, libraries used
- **Architecture** - Module structure and design patterns  
- **Development Commands** - How to run, build, test the module
- **Dependencies** - External dependencies and other modules
- **API Contracts** - Interfaces provided/consumed by this module
- **Testing** - Testing strategy and commands
- **Deployment** - Build and deployment information
- **Notes** - Important considerations and common issues

## Development Workflow

### Starting Development

**Option 1: Using Module Start Command (Recommended)**
```
# Start Claude in project root
cd your-project

# Use the module-start command to begin development
/project:module-start frontend
# This will:
# - Check if modules/frontend/CLAUDE.md exists
# - Create .claude/sessions/frontend/ directory if needed
# - Display the module context
# - Guide you to: cd modules/frontend
# - Then start session with: /project:session-start [task-name]
```

**Option 2: Manual Setup**
1. **Load Project Context**
   ```bash
   cd your-project
   # Start Claude and run:
   cat CLAUDE.md
   ```

2. **Navigate to Module**
   ```bash
   cd modules/frontend  # or your target module
   cat CLAUDE.md         # Load module-specific context
   ```

3. **Start Development Session**
   ```
   /project:session-start implement-user-auth
   # Creates: .claude/sessions/frontend/2025-01-15-1030-implement-user-auth.md
   # Updates: .claude/sessions/frontend/.current-session
   # (Session file location detected from working directory: modules/frontend/)
   ```

### During Development

- **Record progress:**
  ```
  /project:session-update completed form validation
  ```

- **Document blockers:**
  ```
  /project:session-blocker ABC-456 API endpoint returning 500 error
  ```

- **Check current status:**
  ```
  /project:session-current
  ```

### Ending Sessions

```
/project:session-end
```

This creates a comprehensive summary with git changes, completed tasks, and lessons learned.

## How Session Commands Work

### Directory Detection
Session commands automatically detect which module you're working in:

- **From module directory**: `cd modules/frontend` → sessions go to `.claude/sessions/frontend/`
- **From project root**: Commands ask you to specify module or use "shared"
- **From other directories**: Commands guide you to proper module location

### Session File Organization
```
.claude/sessions/
├── frontend/           # Frontend sessions
│   ├── .current-session
│   └── 2025-01-15-1030-task.md
├── backend/            # Backend sessions  
│   ├── .current-session
│   └── 2025-01-15-1100-api.md
└── shared/             # Cross-module sessions
    └── 2025-01-15-1200-integration.md
```

## Session Management Commands

### Module Development Commands

| Command | Description | Example |
|---------|-------------|---------|
| `/project:module-start [module-name]` | Start module development with context | `/project:module-start frontend` |

### Core Session Commands

| Command | Description | Example |
|---------|-------------|---------|
| `/project:session-start [name]` | Start new session | `/project:session-start user-auth` |
| `/project:session-update [notes]` | Add progress notes | `/project:session-update fixed login bug` |
| `/project:session-end` | End with full summary | `/project:session-end` |
| `/project:session-current` | Show current status | `/project:session-current` |

### Organization Commands

| Command | Description | Example |
|---------|-------------|---------|
| `/project:session-list` | List all sessions | `/project:session-list` |
| `/project:session-archive` | Archive old sessions | `/project:session-archive` |
| `/project:session-help` | Show command help | `/project:session-help` |

### Issue Tracking Commands

| Command | Description | Example |
|---------|-------------|---------|
| `/project:session-blocker [id] [desc]` | Record blocking issue | `/project:session-blocker ABC-456 API timeout` |

## Multi-Module Development

### Parallel Development Strategy

1. **Separate Sessions per Module**
   - Each module gets its own development sessions
   - Load module-specific context before starting
   - Session files named by timestamp and module

2. **Module Context Loading**
   ```bash
   # Using module-start command (recommended)
   /project:module-start frontend
   # Navigate to module as instructed
   cd modules/frontend
   /project:session-start implement-dashboard
   # Work on frontend...
   
   # Later, switch to backend
   cd ../../  # Back to project root
   /project:module-start backend
   # Navigate to module as instructed
   cd modules/backend
   /project:session-start api-endpoints
   # Work on backend...
   ```

3. **Integration Points**
   - Document API contracts in shared module
   - Track cross-module dependencies in sessions
   - Use session updates to note integration impacts

### Example Multi-Module Workflow

```bash
# Morning: Frontend work
/project:module-start frontend
cd modules/frontend  # as instructed by module-start
/project:session-start dashboard-components
# Creates: .claude/sessions/frontend/2025-01-15-0900-dashboard-components.md
# Updates: .claude/sessions/frontend/.current-session

# ... development work ...
/project:session-update completed user list component
/project:session-end

# Afternoon: Backend work  
cd ../../  # back to project root
/project:module-start backend  
cd modules/backend  # as instructed by module-start
/project:session-start user-api-endpoints
# Creates: .claude/sessions/backend/2025-01-15-1300-user-api-endpoints.md
# Updates: .claude/sessions/backend/.current-session

# ... development work ...
/project:session-update implemented CRUD endpoints
/project:session-blocker DEF-789 need database migration for new fields
/project:session-end
```

## Project Types & Examples

### Web Application Stack
```
modules/
├── frontend/     # React/Vue/Angular + TypeScript
├── backend/      # Node.js/Python/C# API
├── database/     # Schema and migrations
├── shared/       # Common types and utilities
└── docs/         # API documentation
```

### Microservices Architecture
```
modules/
├── user-service/     # User management
├── order-service/    # Order processing
├── gateway/          # API gateway
├── shared-libs/      # Common libraries
└── deployment/       # Docker, K8s configs
```

### Mobile Development
```
modules/
├── mobile-app/       # React Native/Flutter
├── backend/          # API server
├── shared/           # Business logic
└── design-system/    # UI components
```

## Best Practices

### Session Management
- **Start sessions for significant work** (> 30 minutes)
- **Update regularly** with progress and findings
- **End with comprehensive summaries** for future reference
- **Archive completed sessions** to keep workspace clean

### Documentation
- **Keep CLAUDE.md files current** with architecture changes
- **Document integration points** clearly
- **Track dependencies** between modules
- **Record deployment steps** and configurations

### Multi-Module Coordination
- **Check related modules** before making breaking changes
- **Document API changes** in shared module
- **Use consistent naming** across modules
- **Coordinate testing** of integration points

### Multi-Terminal/Multi-Developer Coordination

The session management system supports coordination across multiple development streams:

**Use Cases:**
- **Multiple terminals** working on different modules simultaneously
- **Multiple developers** collaborating on interconnected modules  
- **Claude instances** running parallel development across modules
- **Mixed human/AI development** with shared session state

**How It Works:**
- Session files in `.claude/sessions/` serve as **shared communication layer**
- Updates broadcast changes that affect other modules
- Blockers alert about issues impacting multiple development streams
- Status checks prevent conflicts before making breaking changes

**Coordination Commands:**
- `/project:session-update` - Broadcast changes affecting other modules
- `/project:session-blocker` - Flag issues impacting parallel work
- `/project:session-current` - Check status before cross-module changes
- `/project:session-list` - Review all active development streams

**Example Scenarios:**

**Frontend/Backend Coordination:**
```bash
# Frontend developer/Claude:
/project:session-update need new API endpoint: GET /api/users/{id}/preferences

# Backend developer/Claude:
/project:session-current  # See frontend requirements
/project:session-update implemented user preferences API as requested
```

**Shared Dependency Changes:**
```bash
# Module A:
/project:session-update upgrading shared library to v2.0 - breaking changes to auth utils

# Module B:
/project:session-blocker AUTH-456 shared auth library breaking changes - need migration guide
```

**Database Schema Changes:**  
```bash
# Database team:
/project:session-update user table migration scheduled - adding 'role' column affects all modules

# All modules check sessions before user-related changes
```

This enables **coordinated parallel development** with full visibility across all work streams.

## Troubleshooting

### Common Issues

**Session not starting:**
- Check if `.claude/sessions/` directory exists
- Verify GMT+7 timezone commands work in your environment

**Commands not working:**
- Ensure you're in the project root directory
- Check that command files exist in `.claude/commands/`

**Context not loading:**
- Verify `CLAUDE.md` files exist in project root and modules
- Check file permissions and readability

### Getting Help

- Run `/project:session-help` for command reference
- Check session examples in `.claude/sessions/`
- Review this README for workflow guidance

## Advanced Usage

### Custom Commands

Add new commands by creating files in `.claude/commands/`:

```bash
# Example: .claude/commands/session-deploy.md
echo "Deploy current work and update session with deployment info..." > .claude/commands/session-deploy.md
```

### Integration with CI/CD

Session files can be used to:
- Generate deployment notes
- Track feature completion
- Document breaking changes
- Provide context for code reviews

### Team Usage

- Share session templates across team
- Use consistent module naming
- Archive sessions to shared storage
- Review sessions during retrospectives

---

**Note:** This template is designed to work with Claude Code and provides structured session management for complex, multi-module development projects.