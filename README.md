# Ele's LLM Wiki

Ele's LLM Wiki is a portable agent skill for maintaining a Chinese, Obsidian-style LLM-Wiki knowledge vault.

It turns repeated knowledge-base maintenance work into a reusable workflow: ingesting source material, compiling wiki pages, maintaining reading notes and MOCs, checking backlinks, cleaning placeholders, and recording maintenance logs.

The skill is designed to be readable by multiple coding agents:

- Codex: invoke `$eles-llm-wiki`.
- Claude Code: read `CLAUDE.md` or `AGENTS.md`.
- Other compatible agents: read `AGENTS.md`, then follow `SKILL.md`.

## What It Does

- Organizes PDFs, articles, course materials, notes, and source folders into an LLM-Wiki vault.
- Maintains source pages, wiki pages, paper pages, reading notes, MOCs, indexes, claims, relationships, and logs.
- Keeps Obsidian-style wikilinks and backlinks consistent.
- Provides audit patterns for broken links, missing backlinks, placeholders, orphan pages, stale indexes, and low-confidence pages.
- Encourages integrated revisions instead of appending loose maintenance notes to the end of pages.

## Repository Structure

```text
.
├── SKILL.md
├── AGENTS.md
├── CLAUDE.md
├── agents/
│   └── openai.yaml
└── references/
    └── llm-wiki-workflow.md
```

## References And Inspiration

This project is based on a personal LLM-Wiki workflow and borrows ideas from:

- Andrej Karpathy's LLM Wiki idea: compile useful knowledge into persistent, interlinked pages that an AI agent can keep improving over time.
- Obsidian-style Markdown vaults and wikilinks: <https://obsidian.md>
- Agent skill packaging with a `SKILL.md` entry point.
- Portable agent instructions through `AGENTS.md` and `CLAUDE.md`, so the same workflow can be used by Codex, Claude Code, and other compatible coding agents.

## Status

This is a small, personal workflow skill. It does not include the private vault itself, only the portable instructions for maintaining one.
