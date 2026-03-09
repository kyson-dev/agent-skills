# gh_pr_status Execution Flow

You are the executor for `gh_pr_status`. Your goal is to gather PR data using the GitHub MCP tool and map it to the defined output contract.

## 1. Discovery
- Determine the PR number. If not provided, you may use `list_pull_requests` or `git` commands to find the PR associated with the current branch.
- Identify the repository `owner` and `repo` from `git remote get-url origin`.

## 2. Data Gathering (MCP)
Call the following GitHub MCP tools to gather the state:
- **`get_pull_request`**: Pass `owner`, `repo`, and `pull_number`. This provides the core metadata, state, and mergeable status.
- **`get_pull_request_status`**: (If available) to get combined CI status.
- **`get_pull_request_reviews`**: To get detailed reviewer feedback.

## 3. Analysis & Mapping
- **Verdicts**:
    - Analyze the response from `get_pull_request`.
    - If `mergeable` is `false`, verdict = `conflicted` (or check for specific error states).
    - If `mergeable_state` is `blocked`, verdict = `blocked`.
    - If `mergeable_state` is `behind`, verdict = `behind`.
- **Risks**: Map fields like `draft`, `state`, and review counts to the `risk_rules` in `skill.yaml`.

## 4. Output
- Construct the final response as a JSON object strictly following the `output_contract`.
