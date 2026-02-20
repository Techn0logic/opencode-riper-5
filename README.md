# RIPER Workflow for OpenCode

**R**esearch • **I**nnovate • **P**lan • **E**xecute • **R**eview

A structured, context-efficient development workflow for [OpenCode](https://github.com/anomalyco/opencode/) using [custom commands/](https://opencode.ai/docs/commands/) and [agents](https://opencode.ai/docs/agents).

## 🎯 Overview

RIPER creates a controlled, guided flow that enforces separation between research, planning, and execution phases. This helps:

- Reduce context usage through specialized agents
- Prevent premature implementation before understanding
- Maintain clear documentation of decisions
- Enable reproducible development processes

## 🚀 Quick Start

### Installation

1. Copy the `.opencode` directory to your project root:

   ```bash
   cp -r .opencode /path/to/your/project/
   ```

2. Update `.opencode/project-info.md` with your project details

3. Optional: Add `.opencode/memory-bank/` to `.gitignore` to keep plans and reviews private:

   ```bash
   echo ".opencode/memory-bank/" >> .gitignore
   ```

   Or selectively ignore just plans and reviews while keeping memory bank structure:

   ```bash
   echo ".opencode/memory-bank/*/plans/" >> .gitignore
   ```

   ```bash
   echo ".opencode/memory-bank/*/reviews/" >> .gitignore
   ```

   Note: If you accidentally commit these, remove them before merging:

   ```bash
   git rebase -i HEAD~n  # where n is number of commits to review
   ```

### Basic Usage

Start a guided RIPER session:

```
/riper-strict
```

Then use the workflow commands/:

1. **Research** - Investigate the codebase

   ```
   /riper-research analyze authentication system
   ```

2. **Plan** - Create technical specifications

   ```
   /riper-plan add OAuth2 support
   ```

3. **Execute** - Implement the approved plan

   ```
   /riper-execute
   ```

   Or execute a specific substep:

   ```
   /riper-execute 2.3
   ```

4. **Review** - Validate implementation

   ```
   /riper-review
   ```

## 📚 commands/ Reference

### RIPER Workflow commands/

| Command                 | Description                        | Mode Restrictions           |
| ----------------------- | ---------------------------------- | --------------------------- |
| `/riper-strict`         | Enable strict protocol enforcement | None                        |
| `/riper-research`       | Enter research mode (read-only)    | Read only                   |
| `/riper-innovate`       | Brainstorm approaches (optional)   | Read only                   |
| `/riper-plan`           | Create technical specifications    | Read + Write to memory bank |
| `/riper-execute`        | Implement approved plan            | Full access                 |
| `/riper-execute <step>` | Execute specific plan step         | Full access                 |
| `/riper-review`         | Validate against plan              | Read + Test execution       |
| `/riper-workflow`       | Full guided workflow               | Varies by phase             |

### Memory Bank commands/

| Command                  | Description            |
| ------------------------ | ---------------------- |
| `/memory-save <context>` | Save important context |
| `/memory-recall <topic>` | Retrieve saved context |
| `/memory-list`           | List all memories      |

## 🏗️ Architecture

### Agents

RIPER uses 3 consolidated agents with optimized model assignments:

| Agent | Model | Temperature | Purpose |
|-------|-------|-------------|---------|
| **research-innovate** | `opencode/gpt-5-nano` | 0.7 | Fast analysis and creative brainstorming |
| **plan-execute** | `opencode/glm-5-free` | 0.2 | Balanced planning and implementation |
| **review** | `opencode/minimax-m2.5-free` | 0.1 | Quality validation and review |

### Agent Permissions

- **research-innovate**: Read-only, git commands/ allowed (git log, diff, status, branch)
- **plan-execute**: Full access with bash operations requiring approval
- **review**: Read-only, test commands/ allowed (pnpm test, lint, type-check), git diff/log

### Memory Bank Structure

```
.opencode/memory-bank/
├── main/                  # Main branch memories
│   ├── plans/            # Technical specifications
│   ├── reviews/          # Code review reports
│   └── sessions/         # Session contexts
└── [feature-branch]/     # Feature branch memories
    └── ...
```

### Mode Capabilities

| Mode     | Read | Write | Execute | Plan | Validate |
| -------- | ---- | ----- | ------- | ---- | -------- |
| RESEARCH | ✅   | ❌    | ❌      | ❌   | ❌       |
| INNOVATE | ✅   | ❌    | ❌      | ❌   | ❌       |
| PLAN     | ✅   | 📄\*  | ❌      | ✅   | ❌       |
| EXECUTE  | ✅   | ✅    | ✅      | ❌   | ❌       |
| REVIEW   | ✅   | 📄\*  | ✅\*\*  | ❌   | ✅       |

\* Only to memory bank
\*\* Only test execution

## 🔧 Configuration

### project-info.md

Update with your project details:

- Project name and description
- Common commands/
- Directory structure
- Tech stack
- Development guidelines

### opencode.jsonc

OpenCode project configuration:

- Provider settings
- MCP tools
- Custom tools configuration

## 💡 Tips & Best Practices

### When to Use RIPER

✅ **Good for:**

- Complex multi-step features
- Refactoring critical code
- Implementing architectural changes
- Tasks requiring careful planning

❌ **Skip for:**

- Simple bug fixes
- Minor text changes
- Straightforward updates
- Exploratory coding

### Workflow Tips

1. **Always start with research** - Understanding before coding prevents wasted effort
2. **Use memory bank** - Save important context for future sessions
3. **Be specific in plans** - Detailed specs lead to accurate implementation
4. **Review ruthlessly** - Catch deviations early
5. **Iterate on substeps** - Use `/riper-execute 2.3` to fix specific parts

### Context Efficiency

- Research phase uses cheaper, focused tools
- Plans are saved to memory, reducing repetition
- Execute phase has full context from approved plan
- Review validates without reimplementing

## 🤝 Contributing

Improvements welcome! Key areas:

- Additional workflow commands/
- Better memory management
- Enhanced agent capabilities
- Integration examples

## 📜 Credits

This implementation is based on the RIPER-5 workflow created by an anonymous contributor ([robotlovehuman](https://forum.cursor.com/u/robotlovehuman/)) on the [Cursor Forums](https://forum.cursor.com/t/i-created-an-amazing-mode-called-riper-5-mode-fixes-claude-3-7-drastically/65516).

Adapted for OpenCode from [tony/claude-code-riper-5](https://github.com/tony/claude-code-riper-5).

## 📄 License

MIT - Use freely in your projects

---

## Example Session

Start strict mode (always):

```bash
/riper-strict
```

Research existing code:

```bash
/riper-research analyze current API structure
```

Create a plan:

```bash
/riper-plan add rate limiting to API endpoints
```

Review the generated plan in .opencode/memory-bank/main/plans/:

```bash
/riper-execute
```

Or execute specific steps

```bash
/riper-execute 1.2
```

```bash
/riper-execute 2
```

Validate implementation:

```bash
/riper-review
```

## Troubleshooting

**Q: commands/ not working?**
A: Ensure `.opencode` directory is in project root

**Q: Memory bank not saving?**
A: Check write permissions on `.opencode/memory-bank/`

**Q: Agent errors?**
A: Verify `opencode.jsonc` is valid JSON

**Q: How to customize for my project?**
A: Start with `project-info.md`

## Recognition

Adapted from the excellent [claude-code-riper-5](https://github.com/tony/claude-code-riper-5) project for [Claude Code](https://github.com/anthropics/claude-code/).
