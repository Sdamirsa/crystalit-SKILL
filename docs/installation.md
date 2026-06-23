# Installation Guide

## Prerequisites

- **Claude Code** (Anthropic's CLI for Claude) installed and configured
- **Python 3.9+** (for figure generation in Phase 4)
- **Zotero** (recommended for bibliography management, not required)

## Install as a Claude Code Plugin (Recommended)

### 1. Clone the repository

```bash
git clone https://github.com/sdamirsa/crystalit-SKILL.git
cd crystalit-SKILL
```

### 2. Point Claude Code at the plugin

```bash
claude --plugin-dir /path/to/crystalit-SKILL
```

Claude Code will auto-discover all skills in the `skills/` directory. The skills appear in Claude Code's skill list and trigger automatically based on your prompts.

### 3. Verify installation

Open Claude Code and say: "What CrystaLit skills are available?"

Claude should list all 8 skills with their descriptions.

## Install by Copying Skills

If you prefer to embed skills directly in your project:

```bash
# Copy all skills into your project's .claude/ directory
cp -r crystalit-SKILL/skills/* /path/to/your-project/.claude/
```

This makes the skills available only in that specific project.

## Python Dependencies (for Phase 4)

Phase 4 (VizMaker) generates figures using Python. Install the required packages:

```bash
pip install matplotlib seaborn squarify networkx pyyaml numpy
```

Or with uv:

```bash
uv add matplotlib seaborn squarify networkx pyyaml numpy
```

## Zotero Setup (Recommended)

CrystaLit works best when papers are organized in Zotero:

1. Install Zotero and the browser connector
2. Create a collection for your project
3. Import papers with full-text PDFs attached
4. Use the subcollection structure recommended by `foundation-scout`:
   - Original, Reviews, Role Models, Logic, Interesting, Maybe

## Verify the Full Pipeline

1. Create a test folder with 3-5 PDFs
2. Open Claude Code in your project directory
3. Say: "Crystallize the papers in [path/to/pdfs]"
4. The orchestrator should start Phase 1 and pause at the HITL checkpoint

## Troubleshooting

**Skills not loading:** Verify each skill directory contains a `SKILL.md` file with valid YAML frontmatter (name and description fields).

**Plugin not recognized:** Ensure `.claude-plugin/plugin.json` exists and has a valid `name` field.

**Figure generation fails:** Check Python dependencies are installed. The generation script requires matplotlib, seaborn, squarify, networkx, pyyaml, and numpy.
