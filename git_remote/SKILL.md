---
name: git_remote
skill_type: executable
description: Atomic git remote configuration manager with connectivity validation.
---

# git_remote

## Purpose

- Manage git remote repositories (add, remove, rename, set-url).
- Verify URL connectivity and authentication during setup.
- Standardize remote metadata for other git skills.

## When to Use

Use this skill whenever you need to configure or update the remote repository
link. This is typically the bridge between a local-only repository and a
synchronized one.

Typical triggers:
- After creating a new project locally and wanting to push to a remote server.
- When `git_status` reports `no_remotes`.
- When the remote URL has changed (e.g. migrating from HTTPS to SSH).

## Source of Truth

- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- Usage documentation: `SKILL.md`

## Executor Directives

1. Read `skill.yaml` for allowed actions and output contract.
2. Read `prompt.md` for the 5-phase execution flow, focusing on validation.
3. Execute strictly by `skill.yaml` policy and `prompt.md` flow.

## Usage Examples

### Add origin
```
Add remote origin at git@github.com:user/repo.git.
→ Agent runs git_remote with action=add, remote=origin, url=git@github.com:user/repo.git
```

### Set new URL
```
Change origin URL to https://github.com/user/repo.git.
→ Agent runs git_remote with action=set_url, remote=origin, url=https://github.com/user/repo.git
```
