# Pipeline Overview

CrystaLit is a five-phase literature crystallization pipeline orchestrated by Claude Code skills. Each phase has a dedicated skill, a defined input/output contract, and a human-in-the-loop (HITL) checkpoint.

## The Full Lifecycle

```
Phase 0: Foundation Scout
   Build your Zotero library, find reviews, select role models.
   Output: Organized PDF collection + mental map of the field.

Phase 1: CrystaLit Noter
   Extract structured notes from each PDF.
   Output: One markdown note per paper.

Phase 2: CrystaLit Ontologist
   Build a hierarchical thematic ontology from all notes.
   Output: YAML file with Themes > Subthemes > Groups > Concepts + LRPs.

Phase 3: CrystaLit Labeler
   Label each paper against the ontology.
   Output: One JSON file per paper + aggregated all_papers.json.

Phase 4: CrystaLit VizMaker
   Generate publication-quality figures and interactive dashboard.
   Output: PDF + PNG figures, generate_figures.py, dashboard HTML.

Phase 5: CrystaLit Writer
   Write a structured literature review report.
   Output: literature_review_report.md.
```

## HITL Checkpoints

Every phase pauses for human review:

| Phase | What the user reviews | What can change |
|-------|----------------------|-----------------|
| 1 | First 2-3 notes | Note template, extraction depth |
| 2 | Full YAML ontology | Theme structure, concept placement, LRPs |
| 3 | First 2-3 JSON labels | Labeling rules, concept coverage |
| 4 | All figures | Layout, font size, figure selection |
| 5 | Each report section | Emphasis, accuracy, coverage |

## Resuming Mid-Pipeline

The orchestrator detects existing outputs and resumes from the appropriate phase. If notes exist but no ontology, it starts at Phase 2. If labels exist but no figures, it starts at Phase 4.

## Running Individual Phases

Each phase can run independently:

- "Take notes on these papers" (Phase 1 only)
- "Build an ontology from my notes" (Phase 2 only)
- "Generate figures from the labels" (Phase 4 only)

## The Panel Discussion Utility

The `panel-discussion` skill is available at any phase for strategic decisions: naming, framing, methodology choices, figure selection. It simulates a 5-7 expert panel with independent voting.
