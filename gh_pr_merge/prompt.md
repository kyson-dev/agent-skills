# gh_pr_merge Execution Flow

You are the executor for `gh_pr_merge`. Your goal is to finalize the PR lifecycle with high-quality, human-readable commit history.

## 1. Context & Metadata Discovery
- Identify repository `owner` and `repo` from `git remote get-url origin`.
- Call **`get_pull_request`** MCP tool.
- **Capture**:
    - `Target_Base`: From `base.ref`.
    - `PR_Head_SHA`: From `head.sha`.
    - `PR_Title`: The current PR title.
    - `PR_Body`: The PR description.
    - `PR_Number`: The pull request number.

## 2. Metadata Synthesis (High Quality)
Before merging, synthesize the final commit metadata to ensure a clean `main` history:
- **`final_title`**: 
    - Ensure it follows **Conventional Commits** (e.g., `feat(git): add merge logic`).
    - It should describe the *total result* of the PR, not just the last commit.
    - Append the PR number at the end: `(#PR_NUMBER)`.
- **`final_message`**: 
    - Do NOT use the raw list of commit messages.
    - Create a concise summary based on the PR Body. 
    - Structure:
        - **Description**: 1 sentence summary.
        - **Key Changes**: 2-3 bullet points of the most important technical shifts.

## 3. Pre-Merge Safety Gates
- **Local Consistency**: Execute `git rev-parse HEAD`. If `Local_SHA != PR_Head_SHA`, exit with `status: blocked`.
- **Worktree Hygiene**: Execute `git status --porcelain`. If non-empty, exit with `status: blocked`.
- **Mergeability**: If `mergeable_state` is `blocked`, `behind`, or `conflicted`, exit with `status: blocked`.

## 4. Execute Merge (MCP)
- Call **`merge_pull_request`** with:
    - `pull_number`: `PR_Number`.
    - `merge_method`: From `inputs.method`.
    - **`commit_title`**: Use the synthesized `final_title`.
    - **`commit_message`**: Use the synthesized `final_message`.

## 5. Post-Merge Cleanup
If merge was successful:
- **Step A: Switch & Sync Base**:
    - Execute **`git switch <Target_Base>`**.
    - Execute **`git pull origin <Target_Base>`**.
- **Step B: Local Branch Deletion**:
    - **Policy**: Use **`git branch --delete <Feature_Branch>`** (standard -d).
- **Step C: Remote Branch Deletion**:
    - Execute **`git push origin --delete <Feature_Branch>`**.
- **Step D: Hygiene**: Execute **`git remote prune origin`**.

## 6. Output
- Build JSON per `output_contract`.
- Report success of merge and both local/remote deletions.
