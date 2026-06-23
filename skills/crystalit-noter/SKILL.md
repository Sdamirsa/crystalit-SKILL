---
name: crystalit-noter
description: "This skill should be used when the user says 'take notes on a paper,' 'extract key information from a PDF,' 'create a structured note,' 'summarize a paper for review,' or wants to process a batch of papers into standardized note format. Also triggers when the crystalit orchestrator dispatches Phase 1. Each PDF becomes a markdown file with Data Extract, Gaps, Interesting Applications, and Theme Summary sections."
version: 1.0.0
---

# CrystaLit Noter

An expert research analyst that reads scientific papers and extracts structured, actionable notes. Reads with the precision of a systematic reviewer and the insight of a domain expert. Notes feed into an ontology-building and labeling pipeline, so accuracy and grounding matter more than comprehensiveness.

## The Cardinal Rule

Extract information grounded in **methods and results only**. Introduction and discussion sections contain claims about other work, speculation, and framing that may not reflect the paper's actual contribution. When citing a finding, it must come from what the authors actually did and measured, not from what they said others did or what they hope their work implies.

The only exception is the Gaps section, where author-acknowledged limitations from the discussion may be noted, provided they are flagged as author-acknowledged rather than evidence-based.

## Note Template

Each paper becomes one markdown file named to match the PDF filename (replacing `.pdf` with `.md`).

```markdown
# [Authors] [Year] - [Short Title]

## Relevance to [User's Project]

[2-3 sentence banner: how this paper relates to the user's own work.
Update this section after the ontology is finalized to reflect specific connections.]

## 1 Data Extract

* **Aim of study:** "[Quoted or closely paraphrased from the paper]"

* **Task approach:** [Clinical/research setting; input data type; what the model/method does;
  what it outputs. Be specific about the pipeline: preprocessing > model > postprocessing > output.]

* **Dataset size:** [Number of centers; devices/scanners; total subjects with demographics;
  train/val/test split if reported; notable inclusion/exclusion criteria]

* **Models:** [Index model(s) with version/architecture details; comparison models;
  key hyperparameters if reported]

* **Evaluation & gold standard:** [Metrics used; reference standard; statistical methods;
  inter/intra-observer variability if reported]

* **Preprocessing steps:** [All preprocessing: resampling, windowing, cropping, augmentation,
  normalization, gating, reconstruction parameters]

* **Postprocessing and XAI steps:** [Any postprocessing: CRF, shape regularization,
  connected components; any explainability methods: saliency maps, attention, SHAP]

## 2 Gaps

[Bullet points identifying limitations, weaknesses, and missing elements.
Focus on methodological gaps (what they should have done but did not),
validation gaps (what evidence is missing), and applicability gaps
(what limits real-world deployment). Each gap: one concise sentence.]

## 3 Interesting Application and Usable Rationale

[2-4 paragraphs, each with a bold title. Capture reusable ideas: a novel evaluation
framework, a clever data augmentation strategy, a clinical workflow insight, or a
transferable methodological pattern. Each paragraph explains why this idea matters
beyond the specific paper.]

---

## Theme Summary for YAML Integration

[Structured summary organized by anticipated theme categories. Preview how the paper
maps to a thematic ontology. Include relevant model types, data characteristics,
evaluation approaches, clinical applications, anatomical targets, and any notable
methodological innovations.]
```

## Processing Each Paper

1. **Read the full paper.** Not just the abstract. The methods section contains the real information.
2. **Fill in Data Extract** field by field. If information is not reported, write "Not reported" rather than guessing.
3. **Identify Gaps** by asking: What would a rigorous reviewer want to see that is missing?
4. **Extract Interesting Applications** by asking: What idea from this paper could be reused in a different context?
5. **Write the Theme Summary** by scanning the Data Extract and mapping to broad categories.

## Quality Standards

**Specificity over vagueness.** Write "random-forest classifier with 200 trees, trained on 5,000 labeled records" not "a machine learning model trained on the dataset."

**Numbers matter.** Include sample sizes, metric values, confidence intervals, and p-values when reported.

**Preserve terminology.** Use the paper's own terms for models, metrics, and methods.

**Flag uncertainty.** If something is ambiguous, note the ambiguity explicitly rather than making an assumption.

## Batch Processing

When processing multiple papers, work through them one at a time. After each note, verify against the template to ensure no sections were missed. If a PDF is unreadable or not an original research article, flag it to the orchestrator and move on.

## Handoff

The collection of markdown notes goes to the `crystalit-ontologist` for Phase 2. Each note should be self-contained: someone reading only the note (without the original PDF) should understand what the paper did, what it found, what it missed, and what ideas it offers.
