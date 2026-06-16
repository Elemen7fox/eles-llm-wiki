# LLM-Wiki Workflow Reference

## Core Model

Treat the vault as a four-layer LLM Wiki:

| Layer | Directory | Purpose |
|---|---|---|
| Source | `00_入口_Inbox/`, `01_原始资料_Sources/` | Raw PDFs, batches, extracted text, source pages |
| Wiki | `02_知识库_Wiki/`, `03_实体_Entities/`, `04_地图_Maps/` | Paper pages, concepts, entities, MOCs |
| Output | `05_输出_Outputs/` | Reading notes, audits, reports, presentation-ready summaries |
| Memory/System | `06_记忆_Memory/`, `90_系统_Meta/` | Claims, relationships, contradictions, templates, workflows |

Do not treat an import as finished until the relevant source, wiki, output, navigation, memory, and log pieces are coherent.

## Language Conventions

This workflow supports Chinese, English, and mixed-language vaults.

| Context | Recommended style |
|---|---|
| Chinese vault | Chinese headings and explanations; preserve English paper titles, model names, methods, acronyms, and citations |
| English vault | English headings and explanations; preserve Chinese source titles when they are canonical filenames or bibliographic titles |
| Mixed vault | Follow nearby pages and existing indexes; avoid translating established page names unless explicitly asked |
| Bilingual explanation | Use `中文术语 (English term)` or `English term (中文术语)` on first mention, then follow the dominant local style |

Do not mass-translate filenames, wikilinks, or headings just to normalize language. Rename only when the user asks for a rename/translation pass, and then update all backlinks, indexes, and logs.

## Page Standards

Long-lived pages should use frontmatter like:

```yaml
---
type: paper | source | moc | output | memory | entity
status: seed | growing | stable | stale | archived
created: YYYY-MM-DD
updated: YYYY-MM-DD
source_count: 0
confidence: 0.60
tags: []
---
```

Paper pages often contain the local-language equivalent of:

- `# Title`
- `## 基本信息`
- `## 摘要`
- `## 核心概念`
- `## 研究方法`
- `## 数据集来源`
- `## 研究区域`
- `## 关键发现`
- `## 局限性`
- `## 对应读书笔记`
- `## 精读笔记`

If a field is uncertain, prefer "原文/抽取文本未给出明确..." plus what is known. Do not leave bare `未提及` in final maintained pages.

For English pages, use the equivalent traceable uncertainty statement, such as "The source/extracted text does not clearly specify...". Avoid bare placeholders like "not mentioned" in final maintained pages.

## Reading Note System

Reading notes usually live in `05_输出_Outputs/` and use concise names. Chinese vaults may use names like `读书笔记 - 主题名`; English vaults may use names like `Reading Note - Topic`. If a domain has a classification index, keep the index synchronized with note filenames, headings, and backlinks.

When adding papers to reading notes:

1. Classify by research object and method, not just filename or batch.
2. Add paper links in the relevant note where they strengthen the existing argument.
3. If a source starts a distinct cluster, create a new reading note and add it to the relevant index.
4. Add or update `## 对应读书笔记` in every affected paper page.
5. Verify bidirectional consistency.

When revising a reading note:

- Merge new material into existing sections.
- Avoid tail sections named like "本轮补充", "修订补充", or date-stamped maintenance notes.
- Use "核心理念", method framework, paper-positioning tables, comparisons, common limitations, and reusable conclusions.
- Keep the note usable for oral presentation or literature review planning.
- Preserve the note's established language. If adding bilingual glosses, integrate them into the main text rather than appending a translation block.

## Review/Progress Source Handling

For review or progress sources, create or update a review-writing note when the task is about how to write reviews, research-progress articles, or synthesis reports.

Useful review-writing categories:

| Type | Use |
|---|---|
| 技术谱系型综述 | Traditional methods to modern methods to challenges |
| 系统综述/文献计量型 | Search strategy, screening, bibliometrics, theme synthesis |
| 机制综合型综述 | Basic process, evidence, model expression, scale transfer |
| 方法比较型综述 | Model families, inputs, metrics, applicability |
| 平台/传感器应用综述 | Platform, data processing, applications, limitations |
| 研究进展与展望型 | Development stages, key progress, problems, future directions |
| 对象-机理-治理型综述 | Object, mechanism, cases, intervention or application |
| 政策/风险思考型综述 | Risk background, evidence synthesis, impact, strategy |

## Audit Patterns

Common audits:

- Low confidence pages: scan frontmatter `confidence`.
- Placeholder cleanup: scan placeholders such as `未提及`, `not mentioned`, `TBD`, `TODO`, or local equivalents.
- Missing backlinks: compare reading-note links with source/wiki-page `## 对应读书笔记` sections when applicable.
- Missing note membership: scan relevant `type: paper`, `type: source`, or other content pages and classify into existing or new reading notes.
- Broken links: extract `[[...]]` and check target `.md` exists.
- Rename cleanup: replace old title across all Markdown files and verify zero residual hits.
- Orphan pages: identify content pages with no inbound links from MOCs, indexes, or notes.

Always report both actions taken and residual backlog.

## Maintenance Log Pattern

Append to `log.md`:

```markdown
## [YYYY-MM-DD] action | short title

- Scope: what was scanned or edited.
- Changes: pages created/updated/renamed.
- Integration: indexes, MOCs, backlinks, claims/relationships.
- Verification: counts or checks proving consistency.
- Backlog: remaining issues, if any.
```

Action labels commonly used: `ingest`, `maintain`, `audit`, `output`, `lint`, `memory`, `split`, `refine`.

## Verification Snippets

PowerShell examples to adapt:

```powershell
# Count placeholder hits in reading notes
Get-ChildItem -LiteralPath 'E:\LLM-Wiki\05_输出_Outputs' -Filter '读书笔记 - *.md' |
  Select-String -Pattern '未提及' |
  Measure-Object
```

```powershell
# Check old title residuals after rename
Get-ChildItem -LiteralPath 'E:\LLM-Wiki' -Recurse -Filter '*.md' -File |
  Select-String -Pattern '旧标题'
```

```powershell
# Check reading-note index links resolve
$idx='E:\LLM-Wiki\05_输出_Outputs\读书笔记索引.md'
$txt=Get-Content -LiteralPath $idx -Raw -Encoding UTF8
$links=[regex]::Matches($txt,'\[\[(读书笔记 - [^\]|#]+)') | ForEach-Object { $_.Groups[1].Value } | Sort-Object -Unique
$missing=@()
foreach($l in $links){
  if(-not (Test-Path -LiteralPath ('E:\LLM-Wiki\05_输出_Outputs\'+$l+'.md'))){ $missing+=$l }
}
$missing
```

Use these as patterns, not rigid scripts.
