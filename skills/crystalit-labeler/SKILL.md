---
name: crystalit-labeler
description: "This skill should be used when the user says 'label my papers,' 'code papers against the ontology,' 'create JSON labels,' 'apply the taxonomy to papers,' or when the crystalit orchestrator dispatches Phase 3. Reads each paper's note and PDF, maps concepts from the YAML ontology, and outputs one JSON per paper."
version: 1.0.0
---

# CrystaLit Labeler

A meticulous research coder that reads papers and assigns labels from a predefined ontology. Labels become the data layer for all downstream analysis. Precision matters more than speed: a wrongly applied label propagates through figures and reports; a missing label makes a paper's contribution invisible.

## The Cardinal Rule (inherited from Noter)

Label based on **methods and results only**. If a paper mentions a technique in its introduction as related work but actually uses a different approach, label the actual approach. If a paper discusses potential applications in the discussion but only validated on phantoms, label the validation as phantom.

## Input

1. The finalized YAML ontology (from `crystalit-ontologist`)
2. The markdown note for each paper (from `crystalit-noter`)
3. Access to the original PDF when the note is ambiguous

## Output Format

One JSON file per paper:

```json
{
    "paper_id": "AuthorLastName_Year",
    "title": "Full title of the paper",
    "T1_Theme_Name": {
        "T1-S1_Subtheme_Name": ["Concept_One", "Concept_Two"],
        "T1-S2_Another_Subtheme": ["Concept_Three"]
    },
    "T2_Another_Theme": {
        "T2-S1_Subtheme": []
    }
}
```

Every subtheme must appear in the JSON, even if empty (`[]`). This ensures consistent structure and simplifies aggregation.

## Labeling Decision Rules

Consult `references/labeling-rules.md` for detailed decision rules. Core principles:

**Inclusion threshold:** Apply a concept label if the paper uses, evaluates, or directly contributes to that concept in methods or results. Do not label mere mentions, citations of others' work, or future-work discussions.

**Multi-label is expected.** Papers typically map to multiple concepts per subtheme.

**Ambiguity resolution:** When ambiguous, check the original PDF. If still ambiguous, apply the most conservative label and add a `_comments` field.

**Hierarchy respect:** Label at the concept level, not the group or subtheme level.

## Process for Each Paper

1. Open the markdown note
2. Read the Data Extract section, mapping details to ontology concepts
3. Cross-reference the Theme Summary section
4. For each theme and subtheme, decide which concepts apply
5. If uncertain, consult the original PDF
6. Write the JSON file with all subthemes represented

## Aggregation

After all papers are labeled, aggregate all JSON files into `all_papers.json`. Also produce summary statistics: papers per concept, unused concepts, papers with unusually few labels.

## Quality Checks

1. **Completeness:** Every paper should have at least one concept in every theme (unless genuinely not applicable).
2. **Distribution:** If any concept has >80% of papers, it may be too broad. If zero papers, it may be too narrow.
3. **Consistency:** Similar papers should have similar label patterns. Spot-check 2-3 pairs.

## Additional Resources

### Reference Files
- **`references/labeling-rules.md`** -- Detailed decision rules for edge cases: algorithm labels, data labels, evaluation labels, clinical application labels, anatomy labels, foundation models, review papers, multi-task papers
