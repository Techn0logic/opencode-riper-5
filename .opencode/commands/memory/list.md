---
description: List all memories across branches
---

# Memory Bank Overview

## ⚠️ Memory Bank Location Requirements

**CRITICAL PATH POLICY**:
- Memory-bank MUST be at repository root: Use `git rev-parse --show-toplevel` to find root, then `[ROOT]/.opencode/memory-bank/`
- NEVER create package-level memory-banks: `packages/*/.opencode/memory-bank/` ❌
- In monorepos: ONE memory-bank at root serves entire project

### Correct vs Incorrect Paths for Memory Listing
✅ **Correct**: `[ROOT]/.opencode/memory-bank/main/` (where ROOT = `git rev-parse --show-toplevel`)
❌ **Wrong**: `[ROOT]/packages/react/.opencode/memory-bank/main/`
❌ **Wrong**: `packages/react/.opencode/memory-bank/main/`

## Current Branch Memories
**Branch**: !`git branch --show-current`

!`ls -la $(git rev-parse --show-toplevel)/.opencode/memory-bank/$(git branch --show-current)/ 2>/dev/null || echo "No memories for current branch"`

## All Branch Memories
!`find $(git rev-parse --show-toplevel)/.opencode/memory-bank -type f -name "*.md" 2>/dev/null | head -20 || echo "No memories found"`

## Memory Organization
```
[ROOT]/.opencode/memory-bank/  (where ROOT = `git rev-parse --show-toplevel`)
├── main/
│   ├── 20250108-session.md
│   └── plans/
│       └── main-20250108-feature.md
├── feature-branch/
│   ├── 20250107-session.md
│   └── reviews/
│       └── feature-branch-20250107-review.md
└── experiment-riper5/
    └── 20250108-session.md
```

## Usage Tips
- Memories are organized by branch to prevent conflicts
- Use `/memory-save` to store important context
- Use `/memory-recall` to retrieve specific memories
- Plans and reviews are automatically stored by RIPER modes
