---
name: crystalit
description: "This skill should be used when the user says 'run CrystaLit,' 'crystallize my papers,' 'process my literature,' 'turn papers into notes,' 'build an ontology from my papers,' 'generate literature review figures,' or mentions 'CrystaLit' by name. Also triggers when the user has a folder of PDFs and wants structured analysis. Orchestrates the five-phase CrystaLit literature crystallization pipeline: notes, ontology, labels, figures, and report."
version: 1.0.0
---

# CrystaLit -- Literature Crystallization Pipeline

The orchestrator of CrystaLit, a five-phase pipeline that transforms a collection of research papers into crystallized knowledge: structured notes, a thematic ontology, coded labels, publication-quality figures, and a literature review report.

## Role

The orchestrator does not do the work itself. It sequences the phases, manages transitions, enforces HITL checkpoints, and dispatches to sub-agent skills. Think of it as a project manager who understands every phase deeply enough to coordinate handoffs and catch problems, but delegates execution to specialists.

## Prerequisites

Before starting, verify the user has a foundation:

1. A folder of PDF papers exists (ask the user for the path)
2. Papers are organized (ideally in Zotero with subcollection structure)
3. The user knows roughly how many papers they have and what the topic is

If the user has not yet built a library, suggest running the `foundation-scout` skill first.

## The Five Phases

### Phase 1: Notes -- `crystalit-noter`

**Input:** Folder of PDFs
**Output:** One markdown note per paper

Process each PDF into a structured markdown note with three core sections (Data Extract, Gaps, Interesting Applications) plus a Theme Summary.

**HITL Checkpoint:** After the first 2-3 notes, pause and show them to the user. Ask whether the depth, sections, and template are appropriate. After confirmation, process all remaining papers.

### Phase 2: Ontology -- `crystalit-ontologist`

**Input:** All markdown notes from Phase 1
**Output:** A YAML file with Themes > Subthemes > Groups > Concepts + LRPs

The ontologist reads all notes and builds a hierarchical thematic ontology through iterative passes.

**HITL Checkpoint:** Present the YAML ontology. Ask whether themes are well-separated, concepts are complete, and LRPs capture interesting cross-theme connections. The user may edit the YAML directly.

### Phase 3: Labeling -- `crystalit-labeler`

**Input:** All PDFs/notes + finalized YAML ontology
**Output:** One JSON label file per paper

Each paper is re-read against the ontology and labeled: which concepts apply. Labels are grounded exclusively in methods and results.

**HITL Checkpoint:** After the first 2-3 JSON files, pause for user review of label accuracy, concept coverage, and labeling rule calibration.

### Phase 4: Visualization -- `crystalit-vizmaker`

**Input:** All JSON labels (aggregated), YAML ontology, markdown notes
**Output:** Publication figures (PDF + PNG) + interactive HTML dashboard

The vizmaker aggregates all JSON labels into a single dataset, then generates 10+ figure types following publication standards.

**HITL Checkpoint:** Present all figures. Iterate on quality issues (font size, label overlap, layout) until the user approves.

### Phase 5: Report -- `crystalit-writer`

**Input:** Aggregated data, figures, notes, ontology
**Output:** A literature review report (markdown)

The writer produces a structured literature review covering the algorithmic landscape, clinical applications, and gaps.

**HITL Checkpoint:** Present each section as it is written. Multiple revision rounds are expected.

## Orchestration Flow

```
START
  |
  +-- Verify prerequisites (PDFs exist, user confirms scope)
  |
  +-- Phase 1: crystalit-noter
  |    +-- Process 2-3 sample papers
  |    +-- HITL: User reviews samples, adjusts template if needed
  |    +-- Process remaining papers
  |    +-- Summary: N notes created, any issues flagged
  |
  +-- Phase 2: crystalit-ontologist
  |    +-- Build initial ontology from all notes
  |    +-- Refine through 2-3 passes
  |    +-- HITL: User reviews and edits YAML
  |    +-- Finalize ontology
  |
  +-- Phase 3: crystalit-labeler
  |    +-- Label 2-3 sample papers
  |    +-- HITL: User reviews sample labels
  |    +-- Label remaining papers
  |    +-- Summary: N papers labeled, distribution stats
  |
  +-- Phase 4: crystalit-vizmaker
  |    +-- Aggregate all labels
  |    +-- Generate all figures
  |    +-- HITL: User reviews figures, iterate on quality
  |    +-- Generate dashboard
  |
  +-- Phase 5: crystalit-writer
  |    +-- Write section by section
  |    +-- HITL: User reviews each section
  |    +-- Finalize report
  |
  +-- DONE: Present summary of all outputs with file paths
```

## Output File Structure

```
project-folder/
  papers and notes/              # Phase 1 output
    Author1_2024.md
    Author2_2023.md
  paper theme extract/           # Phases 2-3 output
    Themes_and_concepts.yaml
    Author1_2024.json
    Author2_2023.json
    all_papers.json              # Aggregated labels
  figures/                       # Phase 4 output
    generate_figures.py
    F1a_algorithm_bar.pdf
    F1a_algorithm_bar.png
  dashboard/
    index.html                   # Phase 4 interactive output
  literature_review_report.md    # Phase 5 output
```

## Resuming Mid-Pipeline

If the user has already completed some phases (notes exist but no ontology), detect what exists and resume from the appropriate phase. Check for the existence of notes, YAML, JSON labels, figures, and the report to determine the current state.

## Error Handling

If a PDF cannot be read (scanned without OCR, corrupted, password-protected), flag it to the user and continue with the remaining papers. Never silently skip a paper.

If the ontology has fewer than 3 themes or fewer than 50 concepts for a 30+ paper collection, flag it as potentially under-extracted and suggest reviewing the notes.
