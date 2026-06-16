---
name: eles-llm-wiki
description: Maintain Ele's bilingual Chinese/English Obsidian-style LLM-Wiki knowledge vault for research materials and reusable knowledge workflows. Use when Codex is asked to organize PDFs, articles, course materials, notes, or source folders into LLM-Wiki; create or update source pages, wiki pages, paper pages, reading notes, MOCs, claims, relationships, audits, backlinks, indexes, or maintenance logs; clean placeholders; rename notes; translate or align Chinese/English note conventions; or keep the vault consistent.
---

# Ele's LLM Wiki

Use this skill to maintain an LLM-Wiki vault as a living knowledge system, not a pile of summaries. It supports Chinese, English, and mixed Chinese-English vaults. Use Obsidian wikilinks for internal pages.

For detailed bilingual conventions, page patterns, note titles, audit patterns, and verification snippets, read `references/llm-wiki-workflow.md` when the task involves more than a small one-file edit.

## Language Policy

- Follow the user's language for conversation and final summaries.
- Follow the vault's existing language for page titles, headings, and links.
- In a Chinese vault, write explanations in Chinese while preserving important English terms, method names, paper titles, model names, and acronyms.
- In an English vault, write headings and explanations in English, while preserving Chinese source titles when they are the canonical filenames or citations.
- In a mixed vault, do not translate established page names unless the task is explicitly a rename/translation pass; add aliases or bilingual glosses only when useful.
- For bilingual pages, prefer `Chinese term (English term)` on first mention, then use the locally dominant term.

## Agent Compatibility

This folder is intentionally plain Markdown so Codex, Claude Code, and other coding agents can use the same workflow.

- Codex: invoke `$eles-llm-wiki`; the skill body and references are the source of truth.
- Claude Code: read `CLAUDE.md` or `AGENTS.md` in this skill folder, then follow `SKILL.md` and `references/llm-wiki-workflow.md`.
- Other compatible agents: read `AGENTS.md`, then follow `SKILL.md` and the reference file as ordinary project instructions.

Do not rely on Codex-only tool names. Use equivalent local file search, file reading, file editing, shell, and validation capabilities provided by the active agent. Preserve the same safety rules: inspect first, avoid destructive edits, update backlinks and logs, and verify before claiming completion.

## Default Vault

Assume the user's active vault is `E:\LLM-Wiki` unless they provide another path.

Common directory roles:

- Inbox: new or unprocessed material.
- Sources: source PDFs, extracted text, source pages.
- Wiki paper pages: maintained paper notes.
- Maps: MOCs and topical maps.
- Outputs: reports, audits, categorized reading notes.
- Memory: claims, relationships, contradictions.
- Meta: schemas, templates, workflows.
- `log.md`: maintenance log.

Read `references/llm-wiki-workflow.md` for the exact Chinese directory names.

## Workflow

1. Inspect before editing.
   - Read `AGENTS.md`, relevant templates/workflows under `90_系统_Meta/`, the target MOC/index, and existing nearby pages.
   - Follow local patterns before inventing new structure.

2. Identify the task type.
   - Ingest: add new PDFs, articles, courses, books, datasets, or folders into source pages and wiki entries.
   - Refine: improve existing pages from source text, extracted text, or original files.
   - Integrate: update reading notes by topic.
   - Audit: find missing links, placeholders, low confidence, orphan pages, duplicate pages, stale indexes.
   - Rename/restructure: update filenames, headings, wikilinks, backlinks, indexes, and log.

3. Preserve source traceability.
   - Keep original PDFs and source paths.
   - Do not fabricate bibliographic metadata, data sources, regions, findings, limitations, or claims.
   - If evidence is incomplete, write a traceable uncertainty statement instead of a bare placeholder.

4. Maintain source and wiki pages.
   - Use frontmatter and sections matching local pages of the same type.
   - For papers, include the corresponding-reading-notes section with backlinks to all relevant reading notes.
   - Prefer integrated prose and tables over detached "supplement" sections.

5. Maintain reading notes.
   - Categorize papers by research type, not only by file batch.
   - Integrate revisions into the original structure; avoid appending date-stamped maintenance notes unless the user asks for audit history.
   - Summarize core ideas, research methods, data sources, comparison logic, limitations, and reusable writing patterns.

6. Update navigation and memory.
   - Update `index.md`, relevant MOCs, reading-note indexes, source pages, and backlinks as applicable.
   - Add stable claims and relationships only when they are reusable and evidence-backed.

7. Record every maintenance pass.
   - Append a concise dated entry to `log.md` with action type, scope, changed pages, verification, and remaining backlog.

8. Verify before finishing.
   - Check old names and placeholders have no residual hits when renaming or cleaning.
   - Check reading-note links resolve to files.
   - Check paper-page backlinks match reading-note citations.
   - For cleanup tasks, report counts before and after.

## Editing Rules

- Prefer direct integration over append-only edits.
- Match the vault's language style; preserve important original-language titles, model names, method names, and citations.
- Use Obsidian wikilinks for internal pages.
- Use tables for comparisons, methods, datasets, and paper positioning.
- Avoid creating auxiliary docs unless the vault already uses that page type for the task.
- When working outside the current writable workspace, use the required approval or escalation flow.

## Useful Checks

Use PowerShell or ripgrep-style scans to verify:

- Reading-note files contain no unresolved placeholders.
- New or renamed reading-note links appear in source/wiki pages under the corresponding-reading-notes section when applicable.
- Reading-note indexes link to actual files.
- Old filenames or titles have no residual references after a rename.
- `log.md` has a matching entry for the maintenance action.
