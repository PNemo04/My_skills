# Workspace Layout

Use this reference before creating files for a note set.

## Output Root Selection

Do not hard-code an absolute output path. Choose the output root with this priority:

1. Use the directory explicitly requested by the user.
2. If the current workspace already contains a compatible `notes/README.md` and `notes/papers/`, extend that existing note library in place.
3. If the user says to work in the current folder, use the current working directory as the output root.
4. Otherwise create a new topic-scoped directory under the current working directory, such as `<topic-slug>-paper-notes/`.

Before writing files, state the selected output root and the planned layout. The layout below is relative to that selected root; it is not an absolute path and should not be copied as a literal machine-specific path.

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
