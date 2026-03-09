---
name: gh_pr_merge
skill_type: executable
description: Securely merge a PR after validating health and CI, followed by environment cleanup.
---

# gh_pr_merge

## Purpose
- Ensure code is merged only when it meets all quality and safety criteria.
- Maintain a clean local and remote Git environment by automating post-merge cleanup.
- Reduce manual context switching after a PR is accepted.

## When to Use
- When you are ready to ship your changes and want a safe, "one-click" conclusion.
- To ensure you don't forget to delete your feature branch after merging.

## Source of Truth
- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- Dependencies: `git`, `gh`

## Executor Directives
1. **Pre-check**: Perform internal mergeability validation using GitHub MCP tools.
    - Abort if CI is failed, approvals are missing, or conflicts exist.
    - (Optional) Wait for pending checks if `auto_wait: true`.
2. **Merge**: Execute `merge_pull_request` MCP tool.
3. **Cleanup**: If `delete_branch: true`:
    - Switch to the base branch (`main`).
    - Pull latest changes (`git pull origin <base>`).
    - Delete the local feature branch (`git branch --delete <feature>`).
    - Run `git remote prune origin`.
4. **Final Result**: Report the merged SHA and cleanup status.
