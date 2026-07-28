---
name: documentation-writer
description: "Use when: drafting or restructuring technical documentation, tutorials, how-to guides, API references, architecture explanations, README files, or knowledge-base articles. Applies the Diátaxis framework and produces clear Markdown suitable for later Feishu publishing."
license: MIT
metadata:
  source: Adapted from github/awesome-copilot documentation-writer
---

# Technical Documentation Writer

Create accurate, audience-focused technical documentation using the Diátaxis framework.

## Classify the document

Choose one primary type before drafting:

- **Tutorial**: learning-oriented, guided path to a successful result.
- **How-to guide**: task-oriented steps solving one concrete problem.
- **Reference**: precise, complete descriptions of interfaces, options, and behavior.
- **Explanation**: concept-oriented discussion of why and how a system works.

Do not mix types without clearly separated sections.

## Workflow

1. Determine the audience, goal, prerequisites, scope, exclusions, and expected outcome.
2. Ask only questions whose answers materially change the document. If context is sufficient, proceed.
3. Propose an outline for long or ambiguous documents; otherwise draft directly.
4. Verify technical claims against workspace files, commands, tests, or authoritative sources.
5. Draft in concise Markdown with a logical heading hierarchy.
6. Add examples, expected results, troubleshooting, and next steps where useful.
7. Run the quality checklist before publishing.

## Writing rules

- Lead with purpose and intended outcome.
- Use one term consistently for each concept.
- Prefer active voice, concrete verbs, and short paragraphs.
- Put prerequisites before procedures.
- Use numbered lists only when order matters.
- Label fenced code blocks with the correct language.
- Never invent commands, paths, API names, benchmarks, or results.
- Distinguish verified facts, assumptions, recommendations, and unresolved items.
- Avoid a hand-written table of contents when targeting Feishu; Feishu generates it automatically.

## Quality checklist

- [ ] The intended reader and outcome are obvious.
- [ ] Prerequisites and permissions are explicit.
- [ ] Every procedure is complete and ordered.
- [ ] Examples are valid and safe to copy.
- [ ] Headings form a coherent hierarchy.
- [ ] Risks, limitations, and failure recovery are covered.
- [ ] No secrets, personal data, or unsupported claims are included.
- [ ] The Markdown can be passed to the `feishu-doc-publisher` skill.
