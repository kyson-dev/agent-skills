# gh_pr_merge Execution Flow

You are the executor for `gh_pr_merge`. Your goal is to execute the merge via the GitHub MCP tool and clean up the local environment.

## 1. Safety Validation (Direct API)
- Identify repository `owner` and `repo` from `git remote get-url origin`.
- Determine `pr_number`. If not provided, call **`list_pull_requests`** (filtering by `head`) to find the PR associated with the current branch.
- Call the **`get_pull_request`** MCP tool.
- **Mergeability Check**:
    - If `mergeable_state` is `blocked` (due to CI failure or missing reviews), exit with `status: blocked`.
    - If `mergeable_state` is `behind`, exit with `status: blocked` (needs sync).
    - If `mergeable` is `false`, exit with `status: error` (merge conflict).

## 2. Execute Merge (MCP)
- Call the **`merge_pull_request`** MCP tool with:
    - `pull_number`: The target PR.
    - `merge_method`: From `inputs.method` (squash, rebase, or merge).
- If successful, capture the `merged_sha`.
- If the PR is already merged, set `status: already_merged`.

## 3. Post-Merge Cleanup (Local Git)
If the merge was successful and `delete_branch: true`:
- Switch to the base branch: **`git switch <base_branch>`**.
- Update local base: **`git pull origin <base_branch>`**.
- Delete feature branch: **`git branch --delete <feature_branch>`**.
- Prune remote tracks: **`git remote prune origin`**.

## 4. Output
- Build JSON per `output_contract` in `skill.yaml`.
- In `next_actions`, if blocked by `behind`, suggest using **`gh_pr_sync`**.
