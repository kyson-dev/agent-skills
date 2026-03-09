---
name: review_skill_design
skill_type: executable
description: Design-level reviewer for skills. Evaluate whether a proposed skill is a good product/design for long-term use.
---

# review_skill_design

## Purpose

- Evaluate design feasibility and scope quality.
- Assess ROI, workflow fit, safety, and evolution path.
- Produce human decision support instead of strict gatekeeping.

## When to Use

Use this after foundational contract review passes, especially for complex or
high-impact skills.

## Source of Truth

- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- Usage documentation: `SKILL.md`

## Executor Directives

1. Read `skill.yaml` for rubric, config, and output contract.
2. Read `prompt.md` for feasibility-first evaluation flow.
3. Execute strictly by `skill.yaml` policy and `prompt.md` flow.
