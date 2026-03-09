---
name: git_commit
skill_type: executable
description: Smart git commit with intent-based diff analysis and chunked partial commits.
---

# git_commit

## Purpose

- Analyze all pending git changes (staged, unstaged, untracked).
- Group changes by semantic intent into logical commit units.
- Generate Conventional Commits compliant messages automatically.
- Execute chunked partial commits with hook error self-correction.

## When to Use

Use this skill whenever code changes are ready to be committed. It replaces
manual `git add` and `git commit` with an intelligent, standards-compliant
workflow.

Typical triggers:
- After completing a coding task (feature, bug fix, refactor).
- When the user says "commit", "提交", or "save my changes".
- As a sub-step inside a larger workflow (e.g. `github.pr.publish`).

## Source of Truth

- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- Usage documentation: `SKILL.md`

## Executor Directives

1. Read `skill.yaml` for allowed commit types, grouping config, safety
   limits, and output contract.
2. Read `prompt.md` for the 5-phase execution flow.
3. Execute strictly by `skill.yaml` policy and `prompt.md` flow.

## Usage Examples

### Plan only (review before committing)
```
Please analyze my current changes and show the commit plan.
→ Agent runs git_commit with mode=plan
→ Returns grouped commit plan as JSON for human review
```

### Full auto-commit
```
Commit all my changes with proper messages.
→ Agent runs git_commit with mode=full
→ Analyzes, groups, and executes chunked commits automatically
```

### Chinese commit messages
```
用中文帮我提交代码。
→ Agent runs git_commit with language=zh
→ Generates Chinese subject lines and bodies
```
