---
name: crystalit-vizmaker
description: "This skill should be used when the user says 'generate figures from the labels,' 'create literature review visualizations,' 'make charts from the ontology data,' 'build a dashboard,' or when the crystalit orchestrator dispatches Phase 4. Produces 10+ figure types in PDF and PNG format, plus an interactive HTML dashboard from labeled paper data."
version: 1.0.0
---

# CrystaLit VizMaker

An expert scientific illustrator that transforms structured literature data into publication-quality figures. Figures target high-impact journals (Nature, Lancet Digital Health, npj Digital Medicine). Combines the precision of a data visualization specialist with the aesthetic sensibility of a graphic designer.

## Input

1. Aggregated `all_papers.json` (all papers with ontology labels)
2. `Themes_and_concepts.yaml` (the ontology structure)
3. Markdown notes (for supplementary context)

## Output

1. Publication figures: PDF + PNG for each figure (dual format always)
2. A Python generation script (`generate_figures.py`) that reproducibly creates all figures
3. An interactive HTML dashboard (`dashboard/index.html`) with embedded data

## Publication Standards

Consult `references/figure-standards.md` for the full specification. Non-negotiable requirements:

- **Resolution:** 300 DPI minimum for PNG
- **Figure width:** 8-12 cm (single-column 8-9 cm, double-column 10-12 cm)
- **Font size:** Minimum 8pt for any text element
- **Font family:** Sans-serif (Arial, Helvetica, DejaVu Sans)
- **Color:** Colorblind-friendly palettes (viridis, cividis, or custom with sufficient contrast)
- **Layout:** `bbox_inches='tight'` in `savefig()` only, not in rcParams. `pad_inches=0.02`
- **Style:** Clean, minimal, Nature/Lancet aesthetic. No gridlines, no 3D, no decorative elements.

## The Figure Library

Generate at least 10 figure types, each with 2-3 variations. Typical set:

1. **Bar charts** (horizontal) -- Concept frequency within a subtheme
2. **Stacked bar charts** -- Multi-category breakdowns (e.g., by year period)
3. **Heatmaps** -- Co-occurrence matrices
4. **Treemaps** -- Hierarchical theme composition
5. **Network graphs** -- Concept co-occurrence networks
6. **Timeline/scatter** -- Publication year vs. method evolution
7. **Radar/spider charts** -- Multi-dimensional paper profiles
8. **Grouped bar charts** -- Comparisons across themes or time periods
9. **Bubble charts** -- Three-variable displays
10. **Sankey/alluvial** -- Flow between categories

## Handling Text in Figures

Text truncation and label overlap are the most common quality problems. Address proactively:

**Abbreviation strategy:** Build an `ABBREV_MAP` that maps long concept names to standard abbreviations. Apply before rendering.

**Label placement:** Horizontal bars for natural label reading. Circular layouts for networks with external labels. Treemap labels only above minimum size threshold.

**Fallback truncation:** After abbreviation, truncate at configurable `maxlen` (default 20 chars) with ellipsis.

## The Generation Script

Write a single `generate_figures.py` that:

1. Loads `all_papers.json` and the YAML ontology
2. Defines all constants at the top (DPI, widths, font sizes, palettes, abbreviation map)
3. Has one function per figure
4. Has a `save_fig(fig, name)` function saving both PDF and PNG
5. Has a `main()` function generating all figures with progress output
6. Is fully reproducible: running twice produces identical figures

## The Dashboard

Create an interactive HTML dashboard embedding data directly (no server required). Allow filtering by theme, subtheme, and individual papers. Use Chart.js, Plotly.js, or D3.js from CDN.

## Quality Assurance

After generating all figures, run a QA pass: view every figure at print size, check for truncated labels, overlapping text, illegible fonts, broken layouts, empty figures, and color issues. Fix and regenerate until all pass.

## Additional Resources

### Reference Files
- **`references/figure-standards.md`** -- Complete dimensional standards, typography specs, color palettes, layout guidelines, abbreviation map template, and anti-patterns to avoid
