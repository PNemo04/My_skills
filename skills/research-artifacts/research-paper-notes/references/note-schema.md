# Note Schema

Use this reference before generating the overview note or per-paper notes.

## Overview Note

Use a formal title such as:

```markdown
# <Topic> Research Map
```

Recommended sections:

1. **Research Goal And Overall Thesis**: explain the topic-level thesis and why this set matters.
2. **Storage And Category Structure**: show the paper categories and file layout.
3. **Per-Paper Note Structure**: briefly define how each per-paper note is organized.
4. **Paper Map**: table with ID, paper, venue/year, role, essence, note link.
5. **Research Storyline**: optional Mermaid diagram if it improves readability.
6. **Method Taxonomy**: optional Mermaid mindmap or table.
7. **Cross-Paper Comparison**: compare research problems, methods, assumptions, evidence, and limitations.
8. **Writing And Packaging Patterns**: extract reusable writing strategies across papers.
9. **Research Direction Candidates**: list research ideas inspired by the corpus.

## Per-Paper Note

Use this exact section family unless a paper requires small adaptations:

```markdown
# <Paper Title>

[Back to overview](../README.md)

## Basic Information
## Core Positioning
## Plain Essence Before Packaging
## Author-Packaged Paper Story
## Packaging Contrast And Writing Lessons
## Method Reading Notes
## Experiment Reading Notes
## Key Figures, Tables, And Concepts
## Limitations And Open Questions
## Future Directions And Research Ideas
## Reading Takeaways
```

Do not add a separate "deep reading" block after a shallow block. The whole note must be detailed.

## Packaging Section

The packaging section is central. Use a comparison table:

| Plain Essence Before Packaging | Author-Packaged Story | Short Source Phrase | Why It Is More Persuasive | Reusable Writing Move |
|---|---|---|---|---|

Rules:

- "Plain Essence Before Packaging" should be blunt and technical.
- "Author-Packaged Story" should explain the narrative arc the authors use.
- "Short Source Phrase" should be a short phrase or sentence that teaches framing, naming, motivation, or claim construction.
- "Why It Is More Persuasive" should explain the rhetorical move, not praise vaguely.
- "Reusable Writing Move" should be reusable for the user's future papers.

Examples of useful packaging moves:

- rename a failure as a benchmark gap;
- turn a classification task into evidence, reasoning, attribution, tool-use, or process modeling;
- frame a limitation of current models as a new evaluation protocol;
- introduce controlled variables to make claims more defensible;
- package model components as necessary responses to data heterogeneity;
- use "from X to Y" structure to show a paradigm shift.

## Method Detail Standard

Explain:

- task definition and input/output;
- data construction or annotation process;
- model components and their roles;
- training, prompting, retrieval, adaptation, or inference flow;
- why each module exists;
- what would break if the module were removed.

Use Mermaid flowcharts only when they clarify a pipeline.

## Experiment Detail Standard

For each experiment group, explain:

- what question it asks;
- which datasets, baselines, metrics, and settings are used;
- what the result says;
- what alternative explanation remains possible;
- how it supports or weakens the paper's story.

Cover main results, ablations, robustness/generalization tests, case studies, human evaluation, annotation quality, and error analysis when present.

## Future-Idea Standard

The future-work section should produce usable research leads:

- direct extension;
- missing benchmark;
- stronger evaluation;
- cross-domain transfer;
- cheaper or more reliable method variant;
- combination with another paper in the note set.
