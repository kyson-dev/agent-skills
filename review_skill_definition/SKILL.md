---
name: review_skill_definition
skill_type: executable
description: Structured gatekeeper for reviewing new skills in the personal AI system.
---

# review_skill_definition

## Purpose

- Enforce naming and namespace discipline.
- Validate I/O clarity, verifiability, and side-effect safety.
- Enforce 3-file responsibility boundaries.

## When to Use

Use this as the foundational gatekeeper before deeper design testing.

## Source of Truth

- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- Usage documentation: `SKILL.md`

## Executor Directives

1. Read `skill.yaml` for rubric, verdict rules, reject conditions, and output contract.
2. Read `prompt.md` for evaluation and scoring flow.
3. Execute strictly by `skill.yaml` policy and `prompt.md` flow.
