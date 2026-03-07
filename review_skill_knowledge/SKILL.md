---
name: review.skill.knowledge
skill_type: executable
description: Content quality reviewer for knowledge-type skills.
---

# review.skill.knowledge

## Purpose

- Evaluate source authority, freshness strategy, and correctness.
- Detect hardcoded volatile facts and scope drift.
- Focus on content quality only; structural checks are handled by
  review.skill.definition.

## When to Use

Use this as a supplementary reviewer after definition review passes,
for skills whose main value is knowledge/documentation.

## Source of Truth

- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- Usage documentation: `SKILL.md`

## Executor Directives

1. Read `skill.yaml` for rubric, verdict rules, and output contract.
2. Read `prompt.md` for evaluation criteria and scoring flow.
3. Execute strictly by `skill.yaml` policy and `prompt.md` flow.
