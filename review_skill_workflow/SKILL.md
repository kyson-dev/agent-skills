---
name: review.skill.workflow
skill_type: orchestrator
description: Orchestrator workflow for reviewing a new skill. Runs definition → knowledge (conditional) → design → tester in sequence.
---

# review.skill.workflow

## Purpose

- Orchestrate the end-to-end review pipeline.
- Enforce gate sequencing across definition, knowledge, design, and tester stages.
- Return one merged workflow decision object.

## When to Use

Use this as the default entrypoint for full skill review in CI or interactive
manual checks.

## Source of Truth

- Policy/config/contracts: `skill.yaml`
- Execution behavior: `prompt.md`
- Usage documentation: `SKILL.md`

## Executor Directives

1. Read `skill.yaml` for pipeline definition, gate rules, and output contract.
2. Read `prompt.md` for stage execution flow and decision logic.
3. Execute sub-skills in sequence and merge results per output contract.
