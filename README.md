# CrystaLit-SKILL

**AI-powered literature crystallization and scientific paper-writing toolkit for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).**

CrystaLit turns a folder of research papers (PDFs) into structured knowledge through a five-phase pipeline, with companion skills for building the library beforehand and making strategic decisions along the way. It is domain-agnostic and works for any research field.

## What it does

### Core Pipeline

| Phase | Skill | Input | Output |
|-------|-------|-------|--------|
| 1 | `crystalit-noter` | PDFs | Structured markdown notes |
| 2 | `crystalit-ontologist` | Notes | Hierarchical YAML ontology |
| 3 | `crystalit-labeler` | Notes + Ontology | JSON labels per paper |
| 4 | `crystalit-vizmaker` | Labels + Ontology | Publication figures + dashboard |
| 5 | `crystalit-writer` | All outputs | Literature review report |

The `crystalit` orchestrator skill manages the pipeline end-to-end with human-in-the-loop (HITL) checkpoints at every phase.

### Companion Skills

| Skill | Purpose |
|-------|---------|
| `foundation-scout` | Phase 0: literature search strategy, Zotero organization, role-model selection |
| `panel-discussion` | Utility: multi-expert deliberation for strategic decisions (naming, framing, methodology) |

## Installation

### Option A: As a Claude Code plugin (recommended)

```bash
# Clone or download this repo
git clone https://github.com/sdamirsa/crystalit-SKILL.git

# Point Claude Code at it
claude --plugin-dir /path/to/crystalit-SKILL
```

### Option B: Copy skills into your project

```bash
# Copy all skills into your project's .claude/ folder
cp -r crystalit-SKILL/skills/* your-project/.claude/
```

### Option C: Install as a plugin via marketplace (coming soon)

```bash
claude plugin install crystalit
```

## Quick start

1. Collect 20-60 research papers (PDFs) in a folder
2. Organize them in Zotero (recommended but optional)
3. Open Claude Code in your project
4. Say: **"crystallize my papers"** or **"/crystalit"**
5. Follow the HITL checkpoints at each phase

You can also run individual skills directly:
- "Take notes on this paper" (triggers `crystalit-noter`)
- "Build an ontology from my notes" (triggers `crystalit-ontologist`)
- "Generate figures from the labels" (triggers `crystalit-vizmaker`)
- "Help me build my paper library" (triggers `foundation-scout`)

## The full workflow

```
foundation-scout          # Phase 0: Build your library
        |
    crystalit             # Phases 1-5: Crystallize knowledge
   /    |    \    \   \
 noter  onto  labeler vizmaker writer
```

`panel-discussion` can be invoked at any phase for strategic decisions.

## Design principles

- **Human-in-the-loop at every phase.** The pipeline pauses for user review and approval. Claude proposes; you decide.
- **Methods and results only.** Notes and labels are grounded in what papers actually did and measured, not introduction claims or discussion speculation.
- **Domain-agnostic.** The ontology, labeling rules, and abbreviation maps are customizable for any research field.
- **Progressive disclosure.** SKILL.md files are lean (~1500 words); detailed references live in `references/` subdirectories and load only when needed.
- **Reproducible outputs.** Figure generation scripts produce identical results on re-run.

## File structure

```
crystalit-SKILL/
  .claude-plugin/
    plugin.json               # Plugin manifest
  skills/
    crystalit/                # Orchestrator
    crystalit-noter/          # Phase 1: Notes
    crystalit-ontologist/     # Phase 2: Ontology
    crystalit-labeler/        # Phase 3: Labels
      references/
        labeling-rules.md     # Detailed decision rules
    crystalit-vizmaker/       # Phase 4: Figures
      references/
        figure-standards.md   # Publication specs
    crystalit-writer/         # Phase 5: Report
    foundation-scout/         # Phase 0: Pre-pipeline library building
    panel-discussion/         # Utility (any phase)
  examples/                   # Example outputs
  docs/                       # User documentation
  CLAUDE.md                   # Claude Code project instructions
  README.md                   # This file
```

## Output structure

When you run the full pipeline, CrystaLit produces:

```
your-project/
  papers and notes/           # Phase 1: One .md per paper
  paper theme extract/        # Phase 2-3: YAML ontology + JSON labels
    Themes_and_concepts.yaml
    all_papers.json           # Aggregated labels
  figures/                    # Phase 4: PDF + PNG figures
    generate_figures.py       # Reproducible generation script
  dashboard/                  # Phase 4: Interactive HTML
    index.html
  literature_review_report.md # Phase 5: Final report
```

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (CLI)
- PDF papers in a folder
- Python 3.9+ with matplotlib, seaborn, squarify, networkx, pyyaml (for figure generation)
- Zotero (recommended for bibliography management)

## License

MIT

## Author

Seyed Amir Ahmad Safavi-Naini ([@sdamirsa](https://github.com/sdamirsa))
