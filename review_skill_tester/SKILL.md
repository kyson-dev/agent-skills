---
name: review.skill.tester
skill_type: executable
description: LLM-driven test generator and executor for skills.
---

# review.skill.tester

## Purpose

- Infer target skill capabilities from its definition files.
- Generate structured test cases with explicit assertions.
- Execute cases and report pass/fail/blocked with concrete evidence.

## When to Use

Use this after definition and design reviews pass, to validate that the
skill behaves correctly under normal and adversarial conditions.

## Source of Truth

- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- Usage documentation: `SKILL.md`

## Executor Directives

1. Read `skill.yaml` for test operators, phases, verdict rules, and output contract.
2. Read `prompt.md` for the 4-step execution flow.
3. Generate and execute test cases strictly by config constraints.
