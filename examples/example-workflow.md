# Example End-to-End Workflow

This walkthrough shows what a typical CrystaLit session looks like, from start to finish.

## Setup

You have 35 PDF papers about cardiac CT segmentation in a folder called `papers/`.
You have Zotero set up with subcollections (Original, Reviews, Role Models).

## Starting the Pipeline

```
User: Crystallize my papers in the papers/ folder. The topic is
      AI-based cardiac CT segmentation methods.

Claude: I'll start the CrystaLit pipeline. I found 35 PDFs in papers/.
        Let me begin with Phase 1 (Notes). I'll process 3 sample
        papers first for your review.
```

## Phase 1: Notes (2-3 samples, then batch)

```
Claude: Here are the first 3 notes. [Shows structured markdown notes]

        HITL Checkpoint:
        - Is the depth of extraction appropriate?
        - Are the sections capturing what you need?
        - Any adjustments to the note template?

User: Looks good, but add a field for "Computational requirements"
      under Data Extract.

Claude: Updated. Processing remaining 32 papers...
        Done: 35 notes created. 2 papers flagged:
        - Paper_X.pdf: scanned without OCR, could not extract text
        - Paper_Y.pdf: editorial, not original research
```

## Phase 2: Ontology

```
Claude: Built initial ontology from all 35 notes. After 3 refinement
        passes, here is the result:

        6 themes, 24 subthemes, 38 groups, 287 concepts, 18 LRPs

        [Shows YAML ontology]

        HITL Checkpoint:
        - Are the themes well-separated?
        - Any missing concepts?
        - Should any themes be merged or split?

User: Merge "Preprocessing" and "Postprocessing" into a single
      "Processing Pipeline" theme. Add "Uncertainty_Quantification"
      as a concept under Evaluation.

Claude: Done. Updated ontology: 5 themes, 22 subthemes, 36 groups,
        289 concepts, 18 LRPs.
```

## Phase 3: Labeling

```
Claude: Here are the first 3 labeled papers. [Shows JSON labels]

        HITL Checkpoint:
        - Are the labels accurate?
        - Over-applied or under-applied?

User: Looks accurate. Proceed.

Claude: Labeled all 35 papers. Summary:
        - Most frequent concept: Dice_Similarity_Coefficient (31/35)
        - Least used theme: Clinical_Translation (8/35)
        - 3 unused concepts flagged for potential removal
```

## Phase 4: Figures

```
Claude: Generated 12 figures with 28 subpanels. [Shows thumbnails]

        HITL Checkpoint:
        - Any figures unclear or truncated?
        - Which are most useful for the paper?

User: F3 heatmap labels are overlapping. F7 radar chart has too
      many axes.

Claude: Fixed F3 (applied abbreviations, rotated labels).
        Simplified F7 to 8 axes. Regenerated.
```

## Phase 5: Report

```
Claude: Section 1 (Pipeline Summary): [Shows 280-word section]

        HITL: Is the coverage and tone right?

User: Good. Continue.

Claude: Section 2.1 (Algorithmic Landscape): [Shows 450-word section]

        ... [continues section by section with review]
```

## Final Output

After all phases complete:

```
papers and notes/                 # 35 markdown notes
paper theme extract/
  Themes_and_concepts.yaml        # 5 themes, 289 concepts
  Smith_2024.json                 # 35 JSON label files
  all_papers.json                 # Aggregated
figures/
  generate_figures.py             # Reproducible script
  F1a_algorithm_bar.pdf + .png    # 12 figures x 2 formats
  ...
dashboard/
  index.html                      # Interactive explorer
literature_review_report.md       # 1500-word review
```

## Time Investment

- Phase 1 (Notes): ~2 minutes per paper for Claude + review time for you
- Phase 2 (Ontology): ~15-30 minutes including HITL review
- Phase 3 (Labeling): ~1 minute per paper for Claude + review time
- Phase 4 (Figures): ~10 minutes generation + 1-2 iteration rounds
- Phase 5 (Report): ~30-60 minutes including section-by-section review

Total: a few hours of active involvement, spread across the phases.
