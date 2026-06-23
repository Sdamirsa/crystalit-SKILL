# CLAUDE.md -- CrystaLit Plugin

CrystaLit is a Claude Code plugin that turns a folder of research papers into crystallized knowledge:
structured notes, a thematic ontology, coded labels, publication figures, and a literature review report.

## What this repo is

A **Claude Code plugin** containing 8 skills:

### Core Pipeline
| Skill | Phase | What it does |
|-------|-------|-------------|
| `crystalit` | Orchestrator | Sequences phases, manages HITL checkpoints, dispatches to sub-skills |
| `crystalit-noter` | Phase 1 | Extracts structured markdown notes from PDFs |
| `crystalit-ontologist` | Phase 2 | Builds hierarchical thematic ontology (YAML) from notes |
| `crystalit-labeler` | Phase 3 | Labels each paper against the ontology (JSON per paper) |
| `crystalit-vizmaker` | Phase 4 | Generates publication-quality figures and dashboard |
| `crystalit-writer` | Phase 5 | Writes a literature review report from all outputs |

### Companion Skills
| Skill | What it does |
|-------|-------------|
| `foundation-scout` | Phase 0: guides literature search, Zotero organization, role-model selection |
| `panel-discussion` | Utility: multi-expert deliberation for naming, framing, and strategic decisions |

## How to install

Copy or clone this folder into your project, then point Claude Code at it:

```bash
# Option A: as a plugin (recommended)
claude --plugin-dir /path/to/crystalit-SKILL

# Option B: copy skills into your project's .claude/ folder
cp -r crystalit-SKILL/skills/* your-project/.claude/
```

## How to use

1. Collect research papers (PDFs) in a folder
2. Organize them in Zotero (optional but recommended)
3. Say `/crystalit` or "crystallize my papers" or "run CrystaLit"
4. Follow the HITL (human-in-the-loop) checkpoints at each phase

Individual skills can be triggered independently. See `docs/pipeline-overview.md`.

## Conventions

- All skills are domain-agnostic. Customize the ontology and labeling rules for your field.
- Skills follow progressive disclosure: SKILL.md is lean; detailed content lives in `references/`.
- The pipeline produces a standard output structure (see `examples/`).
- Every claim in notes and labels must be grounded in methods and results, not introduction speculation.

## File structure

```
crystalit-SKILL/
  .claude-plugin/plugin.json    # Plugin manifest
  CLAUDE.md                     # This file
  README.md                     # GitHub-facing documentation
  skills/                       # All 8 skills (auto-discovered by Claude Code)
  examples/                     # Example outputs from each phase
  docs/                         # User-facing documentation
```
