---
name: prd-author
description: "Use when: writing a PRD, product requirements document, feature specification, technical proposal, project plan, acceptance criteria, rollout plan, or AI-system requirements for publication in Markdown or Feishu."
license: MIT
metadata:
  source: Adapted from github/awesome-copilot prd
---

# PRD Author

Turn a product idea into measurable, implementation-ready requirements.

## Discovery

Before drafting, establish:

- Problem, affected users, and urgency.
- Desired outcome and measurable success metrics.
- Scope and explicit non-goals.
- Constraints: timeline, budget, platform, compliance, compatibility.
- Dependencies, owners, and unresolved decisions.

Ask concise clarifying questions when critical information is missing. Mark unknowns as `TBD`; do not invent them.

## Required structure

## Executive summary

- Problem statement
- Proposed solution
- Success criteria

## Users and experience

- Personas or actors
- User journeys
- User stories
- Functional requirements
- Acceptance criteria
- Non-goals

## Technical design

- Architecture and data flow
- Interfaces and dependencies
- Data model and lifecycle
- Security, privacy, observability, and operations
- Migration and compatibility

## Validation

- Test strategy
- Quality metrics and thresholds
- Failure cases and recovery
- For AI systems: datasets, evaluation protocol, accuracy/safety criteria, latency and cost budgets

## Delivery

- Milestones and phased rollout
- Risks and mitigations
- Open questions
- Ownership and decision log

## Requirement quality

Every requirement should be testable. Replace vague words such as “fast”, “easy”, “robust”, and “modern” with observable criteria. Use stable IDs such as `FR-001`, `NFR-001`, and `AC-001` for substantial specifications.

For Feishu output, apply `markdown-polisher` with the Feishu profile, then use `feishu-doc-publisher`.
