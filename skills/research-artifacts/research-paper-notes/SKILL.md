---
name: research-paper-notes
description: "Build topic-centered Markdown research-paper reading notes with a survey overview and per-paper deep notes. Use when the user asks to create, expand, or restructure paper-reading notes from: (1) specific paper titles, PDFs, or links, (2) a research topic, or (3) the user's own paper from which the agent should infer a related topic. The workflow emphasizes paper selection, source-backed reading, method and experiment explanation, and especially writing/positioning analysis that contrasts the paper's plain underlying contribution with the authors' packaged story."
---

# Research Paper Notes

## Core Promise

Create a reusable research-reading note set, not a loose summary. The output should help the user:

- choose research topics;
- learn paper writing, framing, and packaging;
- understand methods and experiments deeply enough to discuss the paper;
- navigate from one overview note to detailed per-paper notes.

Write generated notes in the user's requested language. If the user does not specify a language, use the language of the user's task request.

PDF export is out of scope unless the user separately requests it.

## Input Modes

Handle three entry points:

1. **Specific papers**: use provided titles, PDFs, DOIs, arXiv links, conference links, or local files as the paper set.
2. **Topic/topic phrase**: search for representative papers, then ask the user to confirm the candidate list before writing full notes.
3. **User's own paper**: read the user's manuscript first, infer the closest research topic and comparison space, then search and propose candidate papers for confirmation.

If the user provides no retrieval constraints, choose a defensible scope: recent top-tier or high-impact work, plus a few foundational or highly relevant papers when needed for context.

## Mandatory Gate

For topic-based or user-paper-based tasks, do not generate the full note library immediately. First produce a candidate paper list with titles, venues/years, links, categories, and selection rationale. Wait for user confirmation unless the user explicitly says to proceed without review.

For a fixed paper set, proceed directly unless paper identity is ambiguous.

Read `references/search-selection.md` before searching or proposing a paper list.

## Workflow

1. **Clarify scope only when necessary**: infer reasonable defaults for venue tier, years, and paper count if the user did not specify them.
2. **Collect sources**: prefer primary sources and stable metadata, including conference proceedings, ACL Anthology, OpenReview, arXiv, DOI/publisher pages, official project pages, and author-released code/data pages.
3. **Create a candidate list**: categorize papers by research role rather than only chronology.
4. **Confirm the list**: ask the user to approve, remove, add, or reorder papers.
5. **Choose and announce the output root**: follow `references/workspace-layout.md` to choose the note library root. Do not treat any example path as hard-coded. State the output root before writing files.
6. **Organize files**: save PDFs and notes under that topic workspace. Preserve existing user files and do not overwrite unrelated notes.
7. **Read each paper**: extract text from the PDF when possible; use the original PDF for method, experiment, table, and writing claims.
8. **Use subagents when supported**: for full note libraries, delegate category-level reading/synthesis passes to subagents or parallel worker agents when the host system supports them. Assign each worker one research category or method family, with all papers in that category. Require each worker to produce a category synthesis plus source-grounded per-paper reading notes for method, experiments, limitations, and packaging moves. If subagents are unavailable, read categories sequentially and state that fallback.
9. **Write the overview note**: create a survey-style map that links to each per-paper note. For multi-paper libraries, include the required Mermaid research storyline and method taxonomy diagrams from `references/note-schema.md`.
10. **Write per-paper notes**: every note must be detailed; do not split content into "brief" and "deep reading" sections.
11. **Verify navigation and completeness**: check that overview links, per-paper links, PDFs, numbering, required overview diagrams, and note sections are consistent.

Read `references/note-schema.md` before writing the overview or per-paper notes.
Read `references/workspace-layout.md` before creating or reorganizing files.

## Quality Bar

Every per-paper note must explain:

- what problem the authors claim to solve;
- what the paper actually does after removing terminology and packaging;
- how the method works step by step;
- how experiments are organized, what each experiment is meant to prove, and what the results do or do not support;
- how the authors package the contribution into a stronger paper story;
- what short original expressions are worth learning for writing;
- what limitations, open questions, and future research ideas follow from the paper.

The packaging section is mandatory. Always include a contrast between **plain essence before packaging** and **author-packaged story after packaging**.

Use short original phrases or sentences only where they teach writing or framing. Do not turn notes into long copied excerpts.

## Output Shape

Prefer this structure unless the existing workspace has a stronger convention:

```text
papers/
  01_category_name/
  02_category_name/
notes/
  README.md
  papers/
    01_slug.md
    02_slug.md
.paper_text/
```

The overview note should include:

- topic-level thesis;
- classification/storage map;
- paper table with links;
- Mermaid research storyline and method taxonomy diagrams for multi-paper libraries;
- cross-paper comparison tables;
- writing and packaging pattern summary;
- research direction candidates.

Per-paper notes should link back to the overview and to the local/source PDF when available.

## Working Rules

- Prefer accuracy over speed. If paper metadata, publication status, or venue may have changed, verify online.
- Use primary sources for technical and publication claims whenever possible.
- Do not invent code links, datasets, numbers, or experimental results.
- If a PDF cannot be downloaded, list the exact title and ask the user to provide it.
- If the note set already exists, extend and refactor it in place instead of creating a disconnected duplicate.
- Keep note headings formal and research-oriented; avoid casual headings such as "one-sentence summary."
