# Customization Guide

CrystaLit is domain-agnostic. This guide explains how to customize it for your research field.

## Customizing the Note Template (Phase 1)

The default note template in `crystalit-noter` includes fields designed for empirical research papers (dataset size, models, evaluation). For other paper types:

**Theoretical/mathematical papers:** Replace "Dataset size" and "Models" with "Key theorems," "Proof techniques," and "Mathematical framework."

**Social science/qualitative research:** Replace "Models" with "Methodology" (interview, ethnography, survey). Replace "Evaluation & gold standard" with "Validity and rigor measures."

**Review/survey papers:** Replace the Data Extract with "Scope" (what the review covers), "Taxonomy" (how they organize the field), and "Key findings."

To customize: edit the note template in `skills/crystalit-noter/SKILL.md` under the "Note Template" section. The HITL checkpoint after the first 2-3 notes is specifically designed for template adjustment.

## Customizing the Ontology (Phase 2)

The ontology structure (Themes > Subthemes > Groups > Concepts) is universal, but the content is domain-specific. The ontologist builds it from your notes, so the ontology naturally reflects your field.

**Guiding the ontologist:** When the ontologist presents the initial YAML, you can:
- Rename themes to match your field's standard terminology
- Merge or split subthemes based on your domain knowledge
- Add concepts the ontologist missed (especially niche or emerging topics)
- Remove concepts that are too granular or irrelevant

**Seeding with an existing taxonomy:** If your field has an established taxonomy (e.g., MeSH terms, ACM CCS), mention it when starting Phase 2. The ontologist will incorporate it as a structural starting point.

## Customizing Labeling Rules (Phase 3)

The default labeling rules in `skills/crystalit-labeler/references/labeling-rules.md` cover common edge cases for empirical research. To customize:

**Add domain-specific rules:** Create rules for your field's common ambiguities. For example, in clinical research: "Label the study design (RCT, cohort, case-control) based on the methods section, not the title or abstract claim."

**Adjust thresholds:** The default population size categories (Small < 200, Medium 200-1000, Large > 1000) may not fit your field. Adjust in the ontology definition.

**Change the grounding rule:** The "methods and results only" rule is strong for empirical research but may need relaxation for theoretical papers where the contribution is in the argument rather than the experiment.

## Customizing Figures (Phase 4)

### Abbreviation map

Edit the `ABBREV_MAP` in `skills/crystalit-vizmaker/references/figure-standards.md` to include your domain's standard abbreviations.

### Color palette

Replace the default palette with your field's conventions or your institution's brand colors. Maintain colorblind-friendliness.

### Figure types

The default 10 figure types cover most literature reviews. For specialized needs:
- **Geographical maps:** If your corpus spans multiple countries, add a choropleth
- **Timeline with events:** If your field has landmark papers or regulatory milestones, add an annotated timeline
- **Methodology flowcharts:** If methods are complex, add Sankey diagrams showing method evolution

### Journal-specific standards

Update the dimensional standards in `references/figure-standards.md` to match your target journal's requirements. Check the journal's author guidelines for exact specifications.

## Customizing the Writer (Phase 5)

The report structure (pipeline summary, algorithmic landscape, clinical applications, gaps) assumes a technical/medical field. To customize:

**Rename sections:** "Clinical Applications" becomes "Practical Applications" or "Industry Applications" depending on your field.

**Adjust word counts:** The default targets (250-500 words per section) work for a paper supplement or introduction. For a standalone review article, increase to 1000-2000 words per section.

**Change the prose style:** The default forbids bullet points, dashes, and sentence-breaking colons. If your field's conventions differ (e.g., computer science papers often use bullets), relax these rules.

## Customizing the Panel Discussion

The default panel composition is tailored for medical/scientific decisions. Customize the panelist roles for your domain. The key principle: include at least one contrarian and one end-user voice.

## Creating New Skills

To extend CrystaLit with a new skill:

1. Create a directory under `skills/` with a `SKILL.md` file
2. Follow the YAML frontmatter format (name + description with trigger phrases)
3. Keep the SKILL.md body under 2000 words
4. Move detailed content to `references/`
5. Test that the skill triggers on expected user prompts
