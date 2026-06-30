# Narrative Review Writing Skill

A Claude Code skill for writing English narrative review articles in clinical pharmacology and basic pharmacological mechanism research. Guides users through a complete 11-step workflow — from topic scoping to final manuscript assembly — with mandatory verification gates, zero-fabrication reference enforcement, and dual-track context management for large-scale reviews (100+ references).

## Features

- **11-step guided pipeline**: Each step outputs to disk; interrupt and resume at any step
- **Zero fabricated references**: Every citation must trace to a user-provided, verified PDF; PMID/DOI cross-validated
- **Obsidian knowledge graph**: Auto-generates a vault with structured paper notes, theme aggregations, and [[wikilinks]] for visual graph exploration
- **Dual-track context management**: File-per-step pipeline + Obsidian vault — handles reviews with 100+ references without context overflow
- **Conclusion-style headings**: Every section heading states a core finding, not a descriptive label
- **Figure drawing instructions**: Detailed per-figure guidance designed to hand off to external AI drawing tools
- **Vancouver reference format**: Default output style with [N] in-text citation before period
- **Pre-flight dependency check**: Scans environment for required skills before starting

## Domain Focus

**Primary**: Clinical pharmacology + basic pharmacological mechanism research
- Drug mechanisms of action
- Signaling pathways and molecular targets
- Pharmacokinetics / pharmacodynamics
- Drug-induced toxicity mechanisms
- Structure-activity relationships

The skill can be adapted to other biomedical fields with similar mechanism-focused review needs.

## Installation

### Prerequisites

- [Claude Code](https://claude.ai/code) installed
- Required skill: [`pdf`](https://github.com/anthropics/skills/tree/main/pdf) (for literature verification)
- Optional skill: [`docx`](https://github.com/anthropics/skills/tree/main/docx) (for Word output)

### Install

```bash
# Clone into Claude Code skills directory
git clone https://github.com/YOUR_USERNAME/narrative-review-skill.git ~/.claude/skills/narrative-review
```

Or manually:

```bash
mkdir -p ~/.claude/skills/narrative-review
cp SKILL.md nr-vs-sr.md scope-checklist.md search-strategy.md \
   figure-template.md table-template.md vancouver-guide.md \
   obsidian-templates.md preflight-check.md quality-checklist.md \
   references.md ~/.claude/skills/narrative-review/
```

### Verify

In Claude Code, type: `write a narrative review`. The skill should auto-trigger.

## Quick Start

```
You: write a narrative review about mitochondrial mechanisms in drug-induced cardiotoxicity

Claude: [Triggers narrative-review skill]
        Step 0.0 — Displays NR vs SR comparison
        Step 0.5 — Pre-flight check: pdf [FOUND], docx [FOUND]
        Step 1.0 — Please provide: working directory, word limit, figure/table count
        ...
```

The skill will guide you through all 11 steps, each with a confirmation prompt.

## Workflow Overview

```
Step 0.0  Introduction: NR vs SR distinction
Step 0.5  Pre-flight environment check
Step 1.0  Project parameters + 6-factor scope definition
Step 2.0  PubMed search strategy + reference list (PMID/DOI)
Step 3.0  Literature verification + structured notes + conflict matrix
Step 3.5  Obsidian vault generation (knowledge graph)
Step 4.0  Framework → user review → LOCK
Step 4.5  Cross-section consistency check
Step 5.0  Section-by-section writing
Step 6.0  Conclusion (limitations + outlook + resolved/unresolved)
Step 7.0  Figure drawing instructions + legends
Step 8.0  Summary tables with traceable citations
Step 9.0  Reference assembly (Vancouver) + cross-verification
Step 10.0 Final assembly + abbreviations table + output (txt + optional docx)
```

## Output Structure

```
{working_directory}/
├── 📁 obsidian_vault/              ← Knowledge graph (open in Obsidian)
│   ├── _MOC_Overview.md
│   ├── _MOC_Mechanisms.md
│   ├── papers/
│   │   └── NNN_AuthorYear.md       ← One structured note per paper
│   └── themes/
│       └── ThemeName.md            ← Aggregated topic synthesis
│
└── 📁 pipeline_output/             ← Writing pipeline state
    ├── 00_preflight_check.md
    ├── 00_project_config.md
    ├── 01_search_strategy.md
    ├── 01_reference_list.md
    ├── 02_literature_notes.md
    ├── 03_framework.md
    ├── 04_draft_section_*.md
    ├── 04.5_cross_section_check.md
    ├── 05_conclusion.md
    ├── 06_figure_instructions.md
    ├── 07_tables.md
    ├── 08_references_final.md
    ├── 09_final_manuscript.txt
    ├── 09_final_manuscript.docx     ← Optional
    └── 10_selfcheck_log.md
```

## Core Rules

- **Zero fabricated references** — every citation traced to user-provided, verified PDF
- **Evidence-based reasoning** — never overconfident, never dogmatic
- **Critical synthesis** — no "laundry list" style; evaluate strengths and weaknesses
- **Balanced coverage** — discuss conflicting findings, not just supporting evidence
- **Cite original research** — not reviews of reviews

## NOT For

- Systematic reviews (use PRISMA-based workflows)
- Meta-analyses
- Scoping reviews, rapid reviews, umbrella reviews

## Research Basis

This skill is grounded in 13 peer-reviewed publications on scientific review writing, including:

- **Dhillon P** (2022). How to write a good scientific review article. *FEBS J*. — Scope checklist, core components, figure design
- **Chaney MA** (2021). So you want to write a narrative review article? *JCVA*. — NR quality standards, NR vs SR, retrograde search
- **Pautasso M** (2013). Ten simple rules for writing a literature review. *PLoS Comput Biol*. — Notes-while-reading, critical evaluation, feedback
- **Gasparyan AY, et al.** (2011). Writing a narrative biomedical review. *Rheumatol Int*. — NR authorship, ethics, title/abstract

See [references.md](references.md) for the complete reference list.

## File Structure

```
narrative-review/
├── SKILL.md                    # Main orchestrator (11-step workflow)
├── nr-vs-sr.md                 # Narrative vs Systematic comparison
├── scope-checklist.md          # 6-factor topic assessment
├── search-strategy.md          # PubMed/MeSH search construction
├── figure-template.md          # Figure drawing instruction template
├── table-template.md           # Summary table template
├── vancouver-guide.md          # Vancouver reference format
├── obsidian-templates.md       # Obsidian note templates
├── preflight-check.md          # Dependency scan logic
├── quality-checklist.md        # Final acceptance checklist (30 items)
├── references.md               # Complete research basis (13 references)
├── README.md                   # This file
└── LICENSE                     # MIT License
```

## License

MIT — see [LICENSE](LICENSE) for details.
