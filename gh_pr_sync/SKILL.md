---
name: gh_pr_sync
skill_type: executable
description: Sync current branch with base (main/PR target). Automates fetch + rebase/merge + push safely.
---

# gh_pr_sync

## Purpose
- Keep feature branches updated with their base branch (e.g., `main`).
- Resolve "Out of date" status on GitHub Pull Requests.
- Automate the multi-step `fetch` -> `rebase/merge` -> `push` flow.

## When to Use
- When your PR shows it is behind the base branch.
- Before final testing or merging to ensure logic compatibility.
- Periodically during long-running feature development.

## Source of Truth
- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- Dependencies: `git`, `gh`

## Executor Directives
1. **Safety Check**: Ensure the working directory is clean.
2. **Base Discovery**:
    - Try `gh pr view --json baseRefName`.
    - If fail/no PR, use `base_branch_override`.
    - If still none, use `config.default_fallback_base` (main).
3. **Execution**:
    - `git fetch origin <base>:<base>`
    - `git rebase/merge <base>`
    - Handle conflicts by immediately aborting and reporting.
4. **Push**: If `push: true`, perform `git push --force-with-lease` (for rebase) or `git push` (for merge).
