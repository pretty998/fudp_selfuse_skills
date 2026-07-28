---
name: feishu-doc-publisher
description: "Use when: creating, publishing, updating, beautifying, or synchronizing Feishu/Lark cloud documents through Feishu MCP; converting Markdown into Feishu-enhanced syntax; safely editing an existing Feishu document or knowledge-base node."
license: MIT
---

# Feishu Document Publisher

Prepare polished content and publish it safely through Feishu MCP.

## Inputs to establish

- Operation: create, append, replace a section, insert, or full rebuild.
- Destination: My Library, folder token, knowledge-space ID, or parent Wiki node.
- Title and target audience.
- Source content or source document link.
- Whether existing media, comments, and collaboration history must be preserved.

## Authoring pipeline

1. Draft or restructure content with `documentation-writer` or `prd-author`.
2. Apply `markdown-polisher` using `target=feishu`.
3. Validate Feishu syntax and remove secrets or private identifiers.
4. For an existing document, fetch it first unless the requested operation is an unambiguous append.
5. Choose the smallest safe MCP update operation.
6. Publish and inspect warnings/errors.
7. Fetch the result when practical to verify title, hierarchy, and critical content.

## Safe update policy

Prefer operations in this order:

1. `replace_range` for one uniquely identifiable fragment or section.
2. `insert_before` / `insert_after` for localized additions.
3. `append` for new terminal sections or long-document continuation.
4. `replace_all` only for deliberate repeated replacements.
5. `overwrite` only when the user explicitly wants a complete rebuild and accepts possible loss of media, comments, and collaboration context.

When replacing a section, use title-based selection if the title is unique. Otherwise use a short, unique ellipsis range. Never guess a document token or Wiki node.

## Feishu syntax rules

- The body must not begin with an H1 identical to the document title.
- Do not create a manual table of contents.
- Keep special block types separated by blank lines.
- Callouts may contain text, headings, lists, and quotes—not code blocks, tables, or images.
- Grid columns should usually be 2–3, with explicit widths totaling 100 when widths are given.
- In `lark-table`, every row must have the same number of `lark-td` cells; do not mix it with Markdown table syntax.
- Media creation accepts URLs, not tokens.
- Create an empty board with `<whiteboard type="blank"></whiteboard>`; never write a fetched `<whiteboard token="..."/>` back as creation syntax.
- Use Mermaid or PlantUML code fences for diagrams.
- Mentions require a real open ID obtained from a user search.
- Reminders require an ISO 8601 timestamp with timezone and a real user ID.

## Long documents

Create a concise initial document, then append coherent sections in batches. Do not split in the middle of a table, code fence, grid, callout, or diagram.

## Permission behavior

With TAT, only operate on documents or knowledge-base nodes explicitly authorized to the application. A successful directory listing does not guarantee that every child document is readable or writable. Report permission failures precisely.

## Publication checklist

- [ ] Correct destination and title.
- [ ] No duplicate H1 or manual TOC.
- [ ] No credential, token, App Secret, or private data.
- [ ] Existing document fetched before destructive changes.
- [ ] Smallest safe update mode selected.
- [ ] Feishu extended syntax is structurally valid.
- [ ] Tool warnings reviewed and result verified.
