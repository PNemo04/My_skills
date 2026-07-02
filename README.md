# My Skills

This is a modest collection of skills I use for research writing, paper
polishing, small AI experiments, MATLAB work, and coding-agent workflows.

I am still a research beginner, so this repository is not meant to be an
authoritative skill library. It is closer to a personal toolbox that I found
useful while learning how to write papers, organize experiments, and work with
AI coding agents. I am sharing it in case the structure or a few of the skills
are useful to other students and early-stage researchers.

## What's Inside

Skills are organized by topic:

| Folder | Purpose |
|---|---|
| `skills/research-writing` | Paper writing, rewriting, citation-aware manuscript work, and publication figures. |
| `skills/research-ideation` | Brainstorming research ideas and finding new angles. |
| `skills/research-artifacts` | Recording research provenance, compiling notes/logs, and reviewing rigor. |
| `skills/experiment-ml` | Running small ML experiments, fine-tuning, evaluation, tracking, and GPU feasibility checks. |
| `skills/matlab` | MATLAB coding, testing, debugging, apps, databases, signal processing, and visualization. |
| `skills/engineering` | Coding-agent workflows for implementation, review, debugging, GitHub, TDD, PRDs, and issues. |
| `skills/productivity` | Handoffs, teaching, grilling plans, and writing better skills. |
| `skills/design` | Frontend design guidance. |
| `skills/writing-polish` | Prompt improvement and human-style writing polish. |

The repository follows a simple layout inspired by
[`mattpocock/skills`](https://github.com/mattpocock/skills):

```text
skills/
  category/
    skill-name/
      SKILL.md
.claude-plugin/
  plugin.json
```

## Privacy Changes

Some skills came from my local `cc switch` setup. Before publishing, I removed
the one private `experiment-preview-numbers` skill and sanitized personal
machine details from:

- `skills/experiment-ml/gpubox`
- `skills/engineering/github-codex-key`

The public `gpubox` skill is now a generic template for using a spare personal
GPU computer over SSH. It does not assume my own hardware, hostname, user name,
IP address, key path, or network setup.

## How To Use

Use the skills with any agent or tool that understands `SKILL.md` directories.
The `.claude-plugin/plugin.json` file lists all included skills for tools that
support Claude Code-style skill plugins.

For manual use, copy the skill directory you want into your agent's skill
folder, or install/import this repository with your skill manager if it supports
GitHub repositories.

## Notes

This repository contains both my own small templates and skills originally
created by other people or projects. I am grateful to those creators. See
[`NOTICE.md`](NOTICE.md) for attribution and licensing notes.

If you reuse this repository, please review each skill before running it. Some
skills are templates that expect you to fill in your own paths, hostnames,
environment names, or project-specific details.
