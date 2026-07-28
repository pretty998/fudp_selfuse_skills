---
name: markdown-polisher
description: "Use when: beautifying, formatting, polishing, restructuring, or converting rough notes/plain text into readable Markdown; preparing Markdown for GitHub, VS Code, or Feishu cloud documents while preserving meaning."
license: MIT
metadata:
  source: Adapted from github/awesome-copilot convert-plaintext-to-md
---

# Markdown Polisher

Improve document structure and visual readability without changing factual meaning.

## Workflow

1. Read the entire source and identify title, audience, purpose, hierarchy, repeated patterns, code, warnings, decisions, and action items.
2. Preserve all technical facts. Flag contradictions rather than silently resolving them.
3. Normalize headings, paragraphs, lists, tables, code fences, links, whitespace, and terminology.
4. Apply restrained visual components appropriate to the target platform.
5. Re-read for information loss and malformed Markdown.

## Structural rules

- Use one H1 only for local Markdown; omit a duplicate H1 when the Feishu document title is supplied separately.
- Do not skip heading levels without reason.
- Keep paragraphs focused; split dense walls of text.
- Use tables for compact comparisons, not long prose.
- Use task lists for actionable checks.
- Use Mermaid for flows, architecture, sequence, state, and dependency diagrams when it clarifies the content.
- Add language identifiers to fenced code blocks.
- Preserve links and code exactly unless correction is explicitly requested.

## Feishu style profile

When `target=feishu` or a Feishu publication is requested:

- Do not add a manual table of contents.
- Prefer standard Markdown for headings, lists, quotes, code, links, and simple tables.
- Use `<callout>` sparingly for tips, warnings, errors, and success states.
- Use `<grid>` only for genuine side-by-side comparison or parallel content.
- Use `lark-table` only when cells require nested lists, code, or other complex blocks.
- Use Mermaid/PlantUML fenced blocks for diagrams; never fabricate a whiteboard token.
- Use `<image url="..."/>` and `<file url="..."/>`; never use media tokens for creation.
- Use `<mention-user>` only after obtaining a real user ID.
- Keep different block types separated by blank lines.

## Visual hierarchy

Recommended order where applicable:

1. One-sentence summary or callout.
2. Context and goals.
3. Main procedure or explanation.
4. Examples or diagrams.
5. Risks and troubleshooting.
6. Checklist or next steps.

## Completion checks

- No factual content was dropped.
- No duplicate title or manual Feishu TOC exists.
- Lists, tables, and fences render correctly.
- Callouts and diagrams add information rather than decoration.
- Sensitive values are removed or replaced with explicit placeholders.
