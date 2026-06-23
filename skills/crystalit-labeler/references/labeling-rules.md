# CrystaLit Labeling Decision Rules

Detailed decision rules for labeling papers against the thematic ontology. Addresses ambiguous cases with consistent resolution strategies.

## General Principles

### Source Sections

Label from methods and results sections only. Introduction and discussion sections contain claims about other work and speculation that should not be attributed to the current paper.

**Exception:** The Gaps section in noter output may capture author-acknowledged limitations from the discussion. These can inform labeling of validation scope or study design concepts, but treat them as self-reported rather than independently verified.

### Granularity

Always label at the most specific applicable concept level. If a paper uses nnU-Net, label it as `nnU-Net`, not just as `Deep_Learning` or `3D_CNN`. The hierarchy exists for organization, not for labeling.

### Absence vs. Non-Applicability

An empty array `[]` for a subtheme means "this paper does not use or contribute to any concept in this subtheme." This is different from "we could not determine the label." For genuine ambiguity, use the `_comments` field.

## Domain-Specific Rules

### Algorithm Labels

Label the **index model** (main contribution) and any **comparison models** evaluated in the paper. If a paper proposes a new architecture and compares against baselines, label all models evaluated.

If a paper uses an existing architecture without modification, label the specific architecture. If it modifies an architecture (e.g., "attention U-Net with squeeze-and-excitation blocks"), label both the base and the modification.

### Data Labels

**Population size categories:** Use thresholds defined in the ontology (e.g., Small < 200, Medium 200-1000, Large > 1000). Use total unique subjects across all splits.

**Multi-center vs. single-center:** Label based on the data used, not author affiliations.

**Imaging modality:** Label the modality actually used in the study. Do not label modalities mentioned only as context.

### Evaluation Labels

**Reference standard:** Label what the paper actually compared against, not what could theoretically serve as reference.

**Validation type:** Internal = held-out split from same institution. External = data from a different institution not seen during training. Cross-validation = its own category.

### Clinical Application Labels

Label the **demonstrated** clinical application, not the intended one. If a paper proposes a clinical tool but only validates segmentation accuracy, label the task as segmentation. Note the intended application in `_comments`.

### Anatomy Labels

Label all anatomical structures the paper's method **explicitly segments, quantifies, or analyzes**.

## Edge Cases

### Papers Using Foundation Models

If a paper applies a foundation model without modification, label the foundation model name. If it fine-tunes, label both the model and the fine-tuning strategy.

### Review Papers in the Collection

If the collection includes review papers, label only their methodological contribution (e.g., a novel taxonomy), not the papers they review.

### Multi-Task Papers

Some papers address multiple tasks (segmentation + classification + quantification). Label all tasks with methods and results. Do not label tasks mentioned only as extensions.

## Version Control

If the ontology is updated after labeling has begun, re-label affected papers. The orchestrator should flag which concepts changed and which papers need re-labeling.
