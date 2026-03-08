---
name: gh_pr_create
skill_type: executable
description: Atomic GitHub PR creator with automatic body synthesis from commits and safety pre-flights.
---

# gh_pr_create

## Purpose

- Formalize the proposal of changes from a feature branch to a base branch.
- Ensure PRs are only created when local changes are synchronized with the remote.
- Automatically generate high-quality PR descriptions from commit history.

## When to Use

Use this skill once your feature is complete, committed, and pushed. It is the
official entry point into the code review and collaboration phase.

Typical triggers:
- After a successful `git_push`.
- When you say "create a PR for these changes" or "我要提个PR".

## Source of Truth

- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- Usage documentation: `SKILL.md`

## Executor Directives

1. Read `skill.yaml` for mandatory pre-flights and default base branches.
2. Read `prompt.md` for the 5-phase creation flow, including metadata synthesis.
3. Execute strictly by `skill.yaml` policy and `prompt.md` flow.

## Usage Examples

### Standard PR
```
Create a PR to main.
→ Agent runs gh_pr_create with base=main
```

### Draft PR with custom title
```
Create a draft PR titled "WIP: New security checks".
→ Agent runs gh_pr_create with title="WIP: New security checks", draft=true
```
