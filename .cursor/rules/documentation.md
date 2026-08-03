---
description: Documentation and cursor-rules maintenance. Trigger phrases and workflow for keeping docs current.
globs:
alwaysApply: true
---

# Documentation Rules

## Always keep docs current

- After any feature, architecture change, or removal: update relevant docs and `.cursor/rules` to match reality. Do not leave stale or contradictory documentation.
- Prefer editing existing docs over creating duplicates. Search `docs/` (or your project’s doc folder) before writing a new file.
- What to document: architecture decisions, removed/deprecated patterns, new conventions, critical constraints (things agents must NOT do), and cross-references between docs and rules.

## Doc location and naming

- Agent-facing reference docs live in [doc folder, e.g. "docs/"].
- Naming: [convention, e.g. "FEATURE_NAME.md in ALL_CAPS_WITH_UNDERSCORES", "kebab-case.md"]. Keep one convention and stick to it.
- New feature docs should include: one-sentence purpose, files/routes/tables touched, how it works, critical constraints, and links to related docs.

## Cursor rules maintenance

- If a change affects patterns or conventions other agents need, update `.cursor/rules/` as well as prose docs.
- Cross-cutting concerns → [global rules file, e.g. "global-rules.md"]. Domain-specific guidance → the matching rule file (tech, design, security, etc.) or a new focused rule file.
- Add a one-line “see `docs/FOO.md`” pointer from rules when a longer reference exists.

## Trigger phrases — "update documentation"

When the user says any of:

- "update documentation"
- "update docs"
- "update docs/"
- "update the docs"
- "update the documentation"

…do ALL of the following before reporting back:

### 1. Find related docs

Search the doc folder for files related to the work just performed. Use patterns derived from feature names, table names, and routes touched. If multiple docs may be relevant, read their headers and update every one that mentions the affected area.

### 2. Update existing docs

Edit in place. Remove references to deleted patterns. Do not leave incomplete or contradictory information.

### 3. Create a new doc when none exists

Only if no existing file covers the area. Follow the naming convention above. Do not invent behavior — document only what was actually implemented.

### 4. Cross-reference from `.cursor/rules/`

If agents need the new convention, update rules and add a short pointer to the doc.

### 5. Confirm in the response

End with a one-line list of every doc/rule file you edited or created.

### What NOT to do on this trigger

- Don’t ask “which docs should I update?” — find them yourself.
- Don’t create a new doc when an existing one already covers the area.
- Don’t write marketing fluff — write concise reference material agents will read.
- Don’t invent feature behavior.
