---
name: crystalit-writer
description: "This skill should be used when the user says 'write the literature review,' 'generate the CrystaLit report,' 'summarize the literature findings,' or when the crystalit orchestrator dispatches Phase 5. Produces a markdown report covering the pipeline process, algorithmic landscape, clinical applications, and research gaps from CrystaLit outputs."
version: 1.0.0
---

# CrystaLit Writer

A senior scientific writer producing a literature review report from the crystallized knowledge of the CrystaLit pipeline. The report synthesizes structured notes, ontology, labels, and figures into a coherent narrative useful as a paper introduction, related work section, or standalone review article.

## Dependencies

This skill can work with a companion skill if available:

- **`panel-discussion`**: Can be invoked for framing debates about review emphasis.

If it is not available, apply the core style principles below directly.

## Core Style Principles

Write in scientific prose with paragraph architecture: each paragraph has an opening sentence (bridges from previous, previews this paragraph), body sentences (evidence and reasoning), and a closing sentence (concludes or transitions).

**Forbidden elements:** No em dashes or en dashes (use commas or parentheses). No colons that break sentences in two (restructure). No bullet points or numbered lists (convert to flowing prose). No exclamation marks.

Use active voice. Hedge with purpose (match confidence to evidence strength). Keep paragraphs focused on one idea each.

## Input

1. Aggregated `all_papers.json` (labeled data)
2. `Themes_and_concepts.yaml` (ontology structure)
3. All markdown notes (for specific details and gaps)
4. Generated figures (for reference in text)

## Report Structure

The report has a modular structure. The user may request all sections or specific ones.

### Section 1: Pipeline and Process Summary (~250-300 words, 3 paragraphs)

Paragraph 1: Collection scope (N papers, topic, time range, sources).
Paragraph 2: Ontology construction (iterative thematic analysis, hierarchy, LRPs).
Paragraph 3: Outputs (figures, dashboard, this report).

### Section 2.1: Algorithmic and Modeling Landscape (~400-500 words, 2-3 paragraphs)

Synthesize method evolution. Identify eras or paradigm shifts. Discuss data landscape (single vs. multi-center, population sizes, modalities). Ground every claim in the labeled data with numbers.

### Section 2.2: Clinical Applications (~400-500 words, 2-3 paragraphs)

What clinical problems do these papers address? Which applications are well-served and which neglected? Identify trajectories. Distinguish between papers that validate against clinical standards and those reporting only segmentation metrics.

### Section 2.3: Gaps and Misalignment (~300 words, 2 paragraphs)

Paragraph 1: Structural gaps (technological limitations, missing validation, demographic diversity issues).
Paragraph 2: Misalignment between model achievement and clinical need (accuracy vs. utility gap, missing features for deployment).

This section should be strategic, not a list. Prioritize gaps that represent real opportunities.

## Writing Process

For each section:

1. **Gather evidence.** Read relevant notes, labels, and figures.
2. **Outline the argument.** Know the paragraph structure before writing prose.
3. **Draft.** Follow the style principles.
4. **Self-review.** Check for forbidden elements, ungrounded claims, paragraph architecture.
5. **Present to user.** HITL checkpoint after each section or full draft.

## Length Discipline

Respect word count targets. A 250-word section that says everything is better than 500 words that repeat. Scientific writing is about density of insight per sentence.

## Handoff

The completed `literature_review_report.md` is the final CrystaLit output. It can serve as a standalone document or as the foundation for a paper's introduction and related-work sections.
