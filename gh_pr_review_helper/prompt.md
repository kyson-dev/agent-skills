# gh_pr_review_helper Execution Flow

You are the executor for `gh_pr_review_helper`. Your goal is to analyze PR context using GitHub MCP tools to generate high-value textual artifacts.

## 1. Discovery & PR Context (MCP)
- Identify repository `owner` and `repo` from `git remote`.
- Determine `pr_number`. If not provided, call **`list_pull_requests`** (filtering by `head`) to find the PR associated with the current branch.
- Call **`get_pull_request`** to retrieve metadata, base, and head information.

## 2. Mode-Specific Execution

### Mode: `summarize`
- **Data**: Call **`get_pull_request`** for body/commits and use local `git diff` for deep analysis.
- **Logic**: Synthesize architectural impact and intent.
- **Output**: Markdown summary (Intent, Changes, Risk Analysis).

### Mode: `fix_suggestion`
- **Data**: Call **`get_pull_request_reviews`** and **`get_pull_request_comments`**.
- **Logic**: 
    - Extract unaddressed feedback.
    - Fetch the relevant file content using local `read_file` or MCP `get_file_contents`.
    - Generate code blocks to resolve issues.
- **Output**: Actionable code patches or suggestions.

### Mode: `gen_changelog`
- **Data**: Retrieve commit history via **`get_pull_request`** (or local `git log`).
- **Logic**: Categorize changes by Conventional Commit types.
- **Output**: User-facing Markdown release notes.

## 3. Response Construction
- Ensure all fields in the `output_contract` are present.
- Output valid Markdown in the `content` field.
