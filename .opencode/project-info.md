# [YOUR_PROJECT_NAME] - Project Information

## Project Overview
[Add your project description here]

## Essential commands/

### Development
```bash
# Add your project's common commands/ here
# Examples:
# npm install
# npm run dev
# npm run build
# npm test
```

## Directory Structure
```
your-project/
├── src/          # Adjust to match your structure
├── tests/        # Your test directory
├── docs/         # Your documentation
└── .opencode/    # RIPER workflow configuration
```

## Technology Stack
- [Add your technologies here]
- [e.g., React, Node.js, Python, etc.]

## RIPER Workflow

This project uses the RIPER development process for structured, context-efficient development.

### Agent Models

RIPER uses 3 consolidated agents with specific model assignments optimized for OpenCode:

| Agent | Model | Temperature | Purpose |
|-------|-------|-------------|---------|
| `research-innovate` | `opencode/gpt-5-nano` | 0.7 | Fast analysis and creative brainstorming |
| `plan-execute` | `opencode/glm-5-free` | 0.2 | Balanced planning and implementation |
| `review` | `opencode/minimax-m2.5-free` | 0.1 | Quality validation and review |

### Agent Permissions

- **research-innovate**: Read-only, git commands/ allowed (git log, diff, status, branch)
- **plan-execute**: Full access with bash operations requiring approval
- **review**: Read-only, test commands/ allowed (pnpm test, lint, type-check), git diff/log

### Available commands/
- `/riper-strict` - Enable strict RIPER protocol enforcement
- `/riper-research` - Research mode for information gathering
- `/riper-innovate` - Innovation mode for brainstorming (optional)
- `/riper-plan` - Planning mode for specifications
- `/riper-execute` - Execution mode for implementation
- `/riper-execute <substep>` - Execute a specific substep from the plan
- `/riper-review` - Review mode for validation
- `/memory-save` - Save context to memory bank
- `/memory-recall` - Retrieve from memory bank
- `/memory-list` - List all memories

### Workflow Phases
1. **Research & Innovate** - Understand and explore the codebase and requirements
2. **Plan** - Create detailed technical specifications saved to memory bank
3. **Execute** - Implement exactly what was specified in the approved plan
4. **Review** - Validate implementation against the plan

### Using the Workflow
1. Start with `/riper-strict` to enable strict mode enforcement
2. Use `/riper-research` to investigate the codebase
3. Optionally use `/riper-innovate` to brainstorm approaches
4. Create a plan with `/riper-plan`
5. Execute with `/riper-execute` (or `/riper-execute 1.2` for specific steps)
6. Validate with `/riper-review`

## Memory Bank Policy

### ⚠️ CRITICAL: Repository-Level Memory Bank
- Memory-bank location: Use `git rev-parse --show-toplevel` to find root, then `[ROOT]/.opencode/memory-bank/`
- NEVER create memory-banks in subdirectories or packages
- All memories are branch-aware and date-organized
- Memories persist across sessions and can be shared with team

### Memory Bank Structure
```
.opencode/memory-bank/
├── [branch-name]/
│   ├── plans/      # Technical specifications
│   ├── reviews/    # Code review reports
│   └── sessions/   # Session context
```

## Development Guidelines
- [Add your project-specific guidelines here]
- Follow existing code patterns
- Write tests for new functionality
- Document complex logic
