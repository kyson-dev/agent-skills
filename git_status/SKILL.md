---
name: git_status
skill_type: executable
description: Read-only Git repository state inspector. Use when you need a normalized status snapshot before commit/push/rebase workflows, including branch/upstream health, staged-unstaged-untracked-conflict breakdown, and actionable next steps.
---

# git_status

## Purpose

- Provide a deterministic, read-only snapshot of repository state.
- Normalize git status details into a machine-friendly output contract.
- Surface immediate risks and recommended next actions.

## When to Use

Use this skill before any mutating git action (`git_commit`, `push`, `sync`,
rebase/merge continuation) or when diagnosing "what state is my repo in?".

## Source of Truth

- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- Usage documentation: `SKILL.md`

## Executor Directives

1. Read `skill.yaml` for status categories, limits, and output contract.
2. Read `prompt.md` for the read-only execution flow.
3. Execute strictly by `skill.yaml` policy and `prompt.md` flow.
