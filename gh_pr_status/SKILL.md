---
name: gh_pr_status
skill_type: executable
description: GitHub Pull Request status inspector. Use to verify if a PR is healthy, compliant with policies, and ready for merge or sync.
---

# gh_pr_status

## Purpose
- Provide a deterministic, read-only snapshot of a GitHub Pull Request's health.
- Evaluate the PR against workspace policies (e.g., minimum approvals, CI success).
- Surface blockers (conflicts, failed checks) in a structured format for automated pipelines.

## When to Use
- Before calling `gh_pr_merge` or `gh_pr_sync`.
- To get a quick "Pulse Check" on your active PR without leaving the terminal.
- In CI/CD or automated workflows to gate further actions.

## Source of Truth
- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- CLI Dependency: `gh` (GitHub CLI)

## Executor Directives
1. Use `gh pr view` to get the core metadata and review status.
2. Use `gh pr checks` to get the detailed CI status.
3. Compare the retrieved data against the policies defined in `skill.yaml`.
4. Return a structured JSON object strictly following the `output_contract`.
