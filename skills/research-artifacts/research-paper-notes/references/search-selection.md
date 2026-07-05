# Search And Selection Protocol

Use this reference before paper discovery, candidate-list construction, or scope negotiation.

## Scope Defaults

If the user gives no constraints, choose:

- 10-30 papers for a full note set; fewer for a quick map.
- Recent papers from the last 1-3 years, plus older seminal papers only when they explain the research line.
- Top venues and high-impact sources relevant to the field, such as ACL/EMNLP/NAACL, NeurIPS/ICML/ICLR, WWW, KDD, AAAI/IJCAI, SIGIR, CVPR/ICCV/ECCV, CHI/CSCW, or field-specific venues.
- arXiv papers only when influential, very recent, or necessary to cover an emerging direction.

Adapt these defaults to the topic. For example, NLP-heavy topics should bias toward ACL venues; multimodal topics may need CV/ML venues; misinformation, social computing, and web topics may need WWW, ICWSM, CSCW, ACL, EMNLP, AAAI, and arXiv.

## Search Sources

Prefer source-backed discovery:

- official conference proceedings and program pages;
- ACL Anthology, OpenReview, ACM/IEEE/Springer publisher pages, DOI pages;
- arXiv for preprints;
- Semantic Scholar or Google Scholar for citation and influence signals;
- official author/project GitHub pages for code/data clues.

Use web search when the topic, publication status, venue, or latest papers may have changed.

## Candidate List Format

Before full notes, produce a confirmation table:

| ID | Paper | Venue/Year | Category | Why Include | Source/PDF |
|---|---|---|---|---|---|

Also include:

- proposed retrieval scope;
- excluded-but-related papers if useful;
- unclear items needing user confirmation or PDF upload;
- suggested categorization for file storage.

Do not label papers as "must-read / recommended / optional" unless the user asks. Prefer neutral categories by research role.

## Selection Rationale

Balance:

- benchmark/data papers;
- method papers;
- diagnostic/analysis papers;
- robustness/generalization papers;
- application/domain papers;
- recent high-impact or trend-setting papers.

When selecting from a user's own paper:

1. Read the user's paper abstract, introduction, related work, method, and experiments.
2. Infer the nearest research problem, method family, target venue, and evaluation context.
3. Search for papers that could serve as related work, baselines, contrastive framing, and future extensions.
4. Separate "direct competitors" from "writing/framing references."

## Confirmation Gate

Ask for confirmation after the candidate list. Accept user edits such as:

- add/remove papers;
- expand/relax year range;
- include/exclude arXiv;
- focus on top venues only;
- add a specific subtopic;
- proceed directly.
