---
name: crystalit-ontologist
description: "This skill should be used when the user says 'build a taxonomy,' 'create an ontology,' 'organize themes from my papers,' 'find patterns across papers,' 'create a YAML of themes and concepts,' or when the crystalit orchestrator dispatches Phase 2. Reads all markdown notes and iteratively constructs a hierarchical ontology: Themes > Subthemes > Groups > Concepts with Lateral Reasoning Pairs."
version: 1.0.0
---

# CrystaLit Ontologist

A knowledge architect that reads a collection of structured research notes and distills them into a hierarchical thematic ontology. The ontology becomes the shared vocabulary for labeling, visualization, and report writing. It must be comprehensive enough to capture every meaningful concept across the papers, yet clean enough that each concept earns its place.

## The Ontology Structure

Four levels of hierarchy, plus a cross-cutting structure:

```yaml
themes:
  T1_Theme_Name:
    description: "What this theme covers"
    subthemes:
      T1-S1_Subtheme_Name:
        description: "What this subtheme covers"
        groups:
          Group_Name:
            description: "What this group covers"
            concepts:
              - Concept_One
              - Concept_Two

lateral_reasoning_pairs:
  - pair: ["Concept_A", "Concept_B"]
    rationale: "Why comparing these two concepts reveals something interesting"
```

**Themes** (5-8 typically): Major dimensions of the research landscape.

**Subthemes** (3-6 per theme): Distinct facets within a theme.

**Groups** (2-5 per subtheme): Clusters of related concepts.

**Concepts** (3-15 per group): Specific, labelable items. Each concept should be concrete enough that a labeler can decide yes/no whether a paper uses it.

**Lateral Reasoning Pairs (LRPs)** (15-30): Cross-theme concept pairs whose juxtaposition reveals an insight.

## The Process

### Pass 1: Seed Structure

Read all notes (or a representative sample of 15-20 for very large collections). Identify the major dimensions of variation. Draft the theme layer first, then expand downward.

Ask: If the entire research landscape had to be explained to a newcomer using only 6 categories, what would they be?

### Pass 2: Populate

Re-read all notes, extracting every concrete concept that appears in 2+ papers (or is significant enough in one). Place each concept in the appropriate group, creating new groups or subthemes as needed.

Watch for concepts that could live in multiple places. Choose the most natural home and note the tension for a potential LRP.

### Pass 3: Refine

Review the entire ontology for: balance (no theme should have 3x more concepts than another unless the literature genuinely skews that way), non-redundancy (merge synonyms), naming consistency (field-standard terminology with underscores), and completeness (any papers under-represented?).

### Pass 4: Lateral Reasoning Pairs

Scan across themes for concept pairs whose comparison would yield insight. Good LRPs connect a methodology with a clinical concept, a data limitation with a model ambition, or an evaluation metric with a clinical outcome.

## Naming Conventions

Use `Title_Case_With_Underscores` for all concept names. Include common abbreviations in parentheses when the full name is long: `CT_Pulmonary_Angiography_CTPA`.

Be specific: prefer `Dice_Similarity_Coefficient` over `Overlap_Metric`, prefer `Left_Ventricle` over `Heart_Chamber`.

## Quality Criteria

1. **Coverage test:** Can every paper be meaningfully labeled using only concepts from this ontology?
2. **Discrimination test:** Do the concepts distinguish papers from each other?
3. **Utility test:** Would a visualization built from these labels tell a meaningful story?
4. **Parsimony test:** Can any concept be removed without losing labeling ability?

## Typical Scale

For 30-60 papers in a well-defined subfield: 5-8 themes, 20-35 subthemes, 30-50 groups, 200-400 concepts, 15-30 LRPs. Adjust for collection size and breadth.

## Handoff

The finalized YAML file goes to `crystalit-labeler` (Phase 3) and `crystalit-vizmaker` (Phase 4). Present the YAML to the user at the HITL checkpoint with a summary: counts of themes, subthemes, groups, concepts, LRPs, plus a narrative of what the ontology reveals about the field.
