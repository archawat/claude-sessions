# Project Memory (CLAUDE.md)

## Architecture Overview
Multi-module project workspace with modular organization and file-based session management.

```
{project-root}/
├── CLAUDE.md                   # This file (project memory)
├── README.md                   # Usage instructions and workflow
├── .claude/
│   ├── sessions/              # Auto-generated session files
│   └── commands/              # Session management commands
├── modules/                    # Module directories (can be symlinks or subdirs)
├── shared/                     # Shared resources (optional)
└── scripts/                    # Helper scripts (optional)
```

## Module Organization
Each module can be organized as:
- **Separate repositories** (symlinked or submoduled)
- **Subdirectories** within a monorepo
- **Packages** in a workspace (npm/yarn/pnpm workspaces, etc.)

**Module Memory Files:**
Each module should contain its own `CLAUDE.md` file serving as the main memory/documentation for that specific module, containing:
- Module-specific architecture and patterns
- Local development setup and commands
- Module's API contracts and interfaces
- Dependencies and external integrations
- Module-specific coding standards and conventions
- Testing strategies and test commands

## Project Types & Examples

### Web Application Stack
```
modules/
├── frontend/     # React/Vue/Angular/Svelte + TypeScript
├── backend/      # C#/Node.js/Python/Go/Rust API
├── database/     # Schema definitions and migrations
└── shared/       # Common types, utilities, configs
```

### Microservices Architecture
```
modules/
├── user-service/     # User management service
├── order-service/    # Order processing service
├── gateway/          # API gateway
├── shared-libs/      # Common libraries
└── deployment/       # Docker, K8s configs
```

### Mobile Development
```
modules/
├── mobile-app/       # React Native/Flutter/Native
├── backend/          # API server
├── shared/           # Common business logic
└── design-system/    # UI components
```

### Data/ML Pipeline
```
modules/
├── data-ingestion/   # ETL/ELT processes
├── ml-models/        # Training and inference
├── api/              # Model serving API
├── dashboard/        # Analytics dashboard
└── shared/           # Common utilities
```

### DevOps/Infrastructure
```
modules/
├── terraform/        # Infrastructure as Code
├── kubernetes/       # Container orchestration
├── monitoring/       # Observability stack
└── ci-cd/           # Pipeline definitions
```

## Integration Patterns
Common integration points to document in sessions:
- **API Contracts**: REST/GraphQL endpoints, message schemas
- **Data Schemas**: Database tables, document structures
- **Shared Libraries**: Common utilities, types, configurations
- **Build Dependencies**: Shared build tools, CI/CD pipelines
- **Environment Configuration**: Shared environment variables, secrets

## Key Principles
- **Two-level memory system**: Project-level `CLAUDE.md` + module-level `CLAUDE.md` files
- Session files contain temporary context, module `CLAUDE.md` files contain persistent context
- Module organization supports your chosen development model
- Each module's `CLAUDE.md` serves as its single source of truth for development context
- Context files are regenerated as project evolves
- Adaptable to any tech stack or project type