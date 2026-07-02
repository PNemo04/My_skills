---
name: prompt-optimizer
description: Use when the user asks to optimize, strengthen, rewrite, audit, or improve LLM prompts, especially prompts for structured outputs, multimodal inputs, agent workflows, or review-only translations. Applies OpenAI, Anthropic, and Google Gemini prompt-engineering guidance.
---

# Prompt Optimizer

Use this workflow for prompt optimization tasks.

## Workflow

1. Identify the runtime prompt separately from documentation or review-only translations.
2. Put the instruction and success criteria near the top of the runtime prompt.
3. Structure context with explicit sections or delimiters such as `# Role`, `# Objective`, `# Input`, `# Instructions`, and `# Output Contract`.
4. Define what the model should do, what evidence it may use, and what shortcuts are forbidden.
5. Specify the output schema exactly. For JSON tasks, require one valid JSON object and no extra text.
6. Prefer positive instructions over only saying what not to do. Include concise edge-case handling.
7. Add examples only when they materially reduce ambiguity; avoid examples that leak labels or encourage shortcuts.
8. For multimodal prompts, explicitly tell the model how to use each modality and how to handle unclear, missing, irrelevant, or conflicting evidence.
9. If a Chinese version is requested for review, store it separately and mark it as non-runtime.
10. Validate by compiling/loading the prompt templates and running a dry run or small sample when code is involved.

## Quality Checks

- The prompt is task-specific, concrete, and avoids vague adjectives.
- It separates role, objective, inputs, rules, checklist, and output contract.
- It prevents hidden-label, source-reputation, path-name, and metadata shortcut reasoning when relevant.
- It tells the model how to handle uncertainty instead of forcing a false precision.
- It preserves schema compatibility with the calling code.

## Reference Guidance

When current source attribution is needed, consult the official pages:

- OpenAI prompt engineering best practices: https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-openai-api
- Anthropic prompt engineering overview: https://docs.anthropic.com/en/docs/prompt-engineering
- Google Gemini prompt design strategies: https://ai.google.dev/gemini-api/docs/prompting-intro
