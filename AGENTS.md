# Ele's LLM Wiki Agent Guide

This directory defines a portable skill for maintaining Ele's LLM-Wiki vault.

Use this guide for Codex, Claude Code, or any agent that reads project-level instructions.

## Entry Points

1. Read `SKILL.md` for the core workflow.
2. Read `references/llm-wiki-workflow.md` for Chinese vault conventions, page patterns, audits, logs, and verification snippets.
3. Treat `E:\LLM-Wiki` as the default vault unless the user gives another path.

## Agent-Agnostic Rules

- Inspect existing vault structure before editing.
- Preserve source traceability.
- Update source/wiki/output/memory/navigation/log layers when relevant.
- Keep page edits integrated into the original structure.
- Use Obsidian wikilinks for internal pages.
- Avoid bare placeholders in final maintained pages.
- Verify links, backlinks, renamed titles, and cleanup counts before finishing.

## Tool Translation

- File search: use any fast search available (`rg`, `grep`, IDE search, or native file APIs).
- File edits: use the active agent's normal safe-edit mechanism.
- Shell: use PowerShell on Windows when working with `E:\LLM-Wiki`.
- Validation: use count-based scans and link-resolution checks from the reference file.

Do not depend on Codex-specific tool names; preserve the workflow semantics instead.
