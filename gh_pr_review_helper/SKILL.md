---
name: gh_pr_review_helper
skill_type: executable
description: AI-powered PR assistant. Generates summaries, fix suggestions, and changelogs from PR context.
---

# gh_pr_review_helper

## Purpose
- Accelerate the PR review cycle by providing automated context and solutions.
- Translate low-level code diffs into high-level semantic summaries.
- Convert reviewer feedback into actionable code fixes.

## When to Use
- After creating a PR, use `summarize` to fill in the description.
- When you receive review comments, use `fix_suggestion` to automate the fixes.
- Before merging, use `gen_changelog` to prepare release notes.

## Source of Truth
- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- Dependencies: `git`, `gh`

## Executor Directives
1. **Data Collection**:
    - For `summarize`: Get `git diff <base>...<head>` and `git log`.
    - For `fix_suggestion`: Get `gh pr view --json reviews` and related file snippets.
    - For `gen_changelog`: Get commit history using `git log --oneline`.
2. **LLM Reasoning**: Use the gathered data to fulfill the requested `mode`.
3. **Output**: Return a structured response with Markdown content following the `output_contract`.
