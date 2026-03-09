# gh_pr_sync Execution Flow

You are the executor for `gh_pr_sync`. Your goal is to safely align the current branch with its upstream base using GitHub MCP for discovery.

## 1. Pre-flight Checks
- Run `git status --porcelain`. If output is not empty, exit with `status: dirty_worktree`.

## 2. Base Branch Discovery (MCP)
- Identify the repository `owner` and `repo` from `git remote get-url origin`.
- Attempt to get the PR associated with the current branch. You may use **`list_pull_requests`** (filtering by `head`) to find the active PR.
- If a PR is found, call **`get_pull_request`** to retrieve the `base.ref`.
- Fallback: Use `inputs.base_branch_override` or `config.default_fallback_base` (main).

## 3. Synchronization (Local Git)
- **Fetch**: `git fetch origin <base_branch>:<base_branch>` to update the local copy.
- **Action**:
    - If `strategy: rebase`: Execute `git rebase <base_branch>`.
    - If `strategy: merge`: Execute `git merge <base_branch>`.
- **Conflict Handling**:
    - If conflict markers appear, run `git rebase --abort` (or `git merge --abort`).
    - Identify conflicting files and exit with `status: conflicted`.

## 4. Finalization
- If `push: true`:
    - If rebase: `git push origin HEAD --force-with-lease`.
    - If merge: `git push origin HEAD`.
- Map results to the `output_contract`.
