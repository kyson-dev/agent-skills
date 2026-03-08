---
name: git_push
skill_type: executable
description: Atomic git push with pre-flight safety gates, connectivity checks, and protected branch rules.
---

# git_push

## Purpose

- Securely synchronize local commits with a remote repository.
- Intelligent handling of upstream relationships and auto-association.
- Guardrails against accidental history overwrites on protected branches.
- Clear error classification for rejected pushes and connectivity issues.

## When to Use

Use this skill whenever you have local commits (ahead > 0) that need to be
pushed to a remote. It is the final step in the typical `status` -> `commit`
-> `push` workflow.

Typical triggers:
- After a successful `git_commit`.
- When the user says "push my changes" or "推送到远端".

## Source of Truth

- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- Usage documentation: `SKILL.md`

## Executor Directives

1. Read `skill.yaml` for safety limits, protected branches, and output contract.
2. Read `prompt.md` for the 5-phase execution flow, prioritizing Phase 0.
3. Execute strictly by `skill.yaml` policy and `prompt.md` flow.

## Usage Examples

### Standard push
```
Push my changes to origin.
→ Agent runs git_push
```

### Force push with safety lease (e.g. after a rebase)
```
Force push this branch.
→ Agent runs git_push with allow_force=true
→ Skill uses --force-with-lease internally
```
