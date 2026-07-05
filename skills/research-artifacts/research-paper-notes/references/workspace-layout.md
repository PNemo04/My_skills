# Workspace Layout

Use this reference before creating files for a note set.

## Default Layout

```text
<topic-workspace>/
  papers/
    01_category_name/
    02_category_name/
  notes/
    README.md
    papers/
      01_short_slug.md
      02_short_slug.md
  .paper_text/
```

Use global continuous numbering across categories.

## File Naming

- Use two-digit numeric prefixes: `01_`, `02_`, ...
- Use lowercase ASCII slugs for filenames when possible.
- Keep original PDF filenames only if they are already clean; otherwise copy/rename into the category folder.
- Keep note filenames aligned with paper IDs.

## Link Conventions

In overview tables:

```markdown
[Note](papers/01_slug.md)
```

In per-paper notes:

```markdown
[Back to overview](../README.md)
```

For local PDFs, use relative links when possible.

## Updating Existing Notes

When a note library already exists:

- inspect current numbering, categories, and style first;
- preserve user-authored content;
- add or refactor incrementally;
- update the overview after changing per-paper notes;
- check for broken links after edits.

## Text Extraction

When PDFs are available, extract text into `.paper_text/` for search and citation support. Keep extracted text out of final notes unless short source expressions are needed for writing analysis.
