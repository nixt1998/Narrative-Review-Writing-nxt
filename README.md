<!--
╔══════════════════════════════════════════════════════════╗
║  Author / 作者                                            ║
║  Name / 姓名:  [倪啸庭] [Xiaoting Ni]                                ║
║  Affiliation / 所属单位:  [School of Pharmacy, Qiqihar Medical University, China. Department of Pharmacy, The First affiliated Hospital of Harbin Medical University, China.]               ║
║  Email:  [nixt1998@163.com]                     ║
║  ORCID:  [0009-0009-6400-4071]                           ║
╚══════════════════════════════════════════════════════════╝
-->

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-orange)](https://claude.ai/code)

**Language:** &nbsp; 🇬🇧 **English** &nbsp; | &nbsp; [🇨🇳 中文](README_zh.md)

---

# Narrative Review Writing Skill

**A Claude Code skill for writing English narrative review articles in clinical pharmacology and basic pharmacological mechanism research.**

Guides users through a complete 11-step workflow — from topic scoping to final manuscript assembly — with mandatory verification gates, zero-fabrication reference enforcement, and dual-track context management for large-scale reviews (100+ references).

---

## Table of Contents

- [Features](#features)
- [Domain Focus](#domain-focus)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Workflow Overview](#workflow-overview)
- [Output Structure](#output-structure)
- [Core Rules](#core-rules)
- [What This Skill Is NOT For](#what-this-skill-is-not-for)
- [Research Basis](#research-basis)
- [File Structure](#file-structure)
- [License](#license)

---

## Features

| Feature | Description |
|---------|-------------|
| **11-step guided pipeline** | Each step outputs to disk; interrupt and resume at any step |
| **Zero fabricated references** | Every citation must trace to a user-provided, verified PDF; PMID/DOI cross-validated |
| **Obsidian knowledge graph** | Auto-generates a vault with structured paper notes, theme aggregations, and `[[wikilinks]]` for visual graph exploration |
| **Dual-track context management** | File-per-step pipeline + Obsidian vault — handles reviews with 100+ references without context overflow |
| **Conclusion-style headings** | Every section heading states a core finding, not a descriptive label |
| **Figure drawing instructions** | Detailed per-figure guidance designed to hand off to external AI drawing tools |
| **Vancouver reference format** | Default output style with `[N]` in-text citation before period |
| **Pre-flight dependency check** | Scans environment for required skills before starting |
| **Bilingual abstract support** | English academic writing with structured abstract format |
| **Conflict evidence matrix** | Identifies and documents contradictory findings across studies |

---

## Domain Focus

**Primary**: Clinical pharmacology + basic pharmacological mechanism research

- Drug mechanisms of action (receptor binding, enzyme inhibition, transporter interactions)
- Signaling pathways and molecular targets (NF-κB, PI3K/Akt, MAPK, JAK/STAT, etc.)
- Pharmacokinetics / pharmacodynamics (ADME, drug-drug interactions)
- Drug-induced toxicity mechanisms (nephrotoxicity, cardiotoxicity, hepatotoxicity)
- Structure-activity relationships (SAR)
- Pharmacogenomics and precision medicine

The skill can be adapted to other biomedical fields with similar mechanism-focused review needs.

---

## Installation

### Prerequisites

| Dependency | Required | Purpose |
|-----------|----------|---------|
| [Claude Code](https://claude.ai/code) | Yes | Runtime environment |
| [`pdf` skill](https://github.com/anthropics/skills/tree/main/pdf) | **Yes** | Literature PDF verification (Step 3) |
| [`docx` skill](https://github.com/anthropics/skills/tree/main/docx) | Optional | Word document output (Step 10) |

### Via Git Clone

```bash
git clone https://github.com/YOUR_USERNAME/narrative-review-skill.git ~/.claude/skills/narrative-review
```

### Manual Install

```bash
mkdir -p ~/.claude/skills/narrative-review

# Copy all files into the skill directory
cp *.md LICENSE ~/.claude/skills/narrative-review/
```

### Verify Installation

In Claude Code, type:

```
write a narrative review about [your topic]
```

The skill should auto-trigger, starting with the NR vs SR introduction at Step 0.0.

---

## Quick Start

```
You: write a narrative review about mitochondrial mechanisms
    in cisplatin-induced nephrotoxicity

Claude: [narrative-review skill triggered]
  Step 0.0 — NR vs SR: "This skill writes narrative reviews only."
  Step 0.5 — Pre-flight: pdf [✓], docx [✓] → PASS
  Step 1.0 — "Please provide: working directory, word limit,
             figure/table count, and topic title."
  Step 1.0 — 6-factor scope assessment...
  ...
  Step 10.0 — Final manuscript + abbreviations table delivered.
```

The skill will guide you through all 11 steps, each with a confirmation prompt and a next-step hint.

---

## Workflow Overview

```
Step 0.0  Introduction: NR vs SR distinction
Step 0.5  ⭐ Pre-flight environment check (dependency scan)
Step 1.0  ⭐ Project parameters (word/fig/table limits) + 6-factor scope
Step 2.0  PubMed search strategy + reference list (PMID/DOI)
Step 3.0  Literature verification + structured notes + conflict matrix
Step 3.5  ⭐ Obsidian vault generation (knowledge graph)
Step 4.0  Framework → user review → LOCK
Step 4.5  ⭐ Cross-section consistency check
Step 5.0  Section-by-section writing (per-section file output)
Step 6.0  Conclusion (limitations + outlook + resolved/unresolved)
Step 7.0  Figure drawing instructions + legends
Step 8.0  Summary tables with traceable citations
Step 9.0  Reference assembly (Vancouver) + cross-verification
Step 10.0 ⭐ Final assembly + abbreviations table + output (txt + optional docx)
```

⭐ = New in this version

---

## Output Structure

```
{working_directory}/
│
├── 📁 obsidian_vault/              ← Knowledge graph (open in Obsidian)
│   ├── _MOC_Overview.md            ← Hierarchical index of all content
│   ├── _MOC_Mechanisms.md          ← Grouped by pathway/mechanism
│   ├── _MOC_Clinical_Translation.md ← Translational relevance
│   ├── _MOC_Controversies.md       ← Disputed findings
│   ├── _MOC_Figure_Ideas.md        ← Visualizable concepts
│   ├── papers/
│   │   ├── 001_Author2024_Topic.md
│   │   ├── 002_Author2023_Topic.md
│   │   └── ...
│   ├── themes/
│   │   ├── NF-kB_Pathway.md
│   │   ├── Mitochondrial_Dysfunction.md
│   │   └── ...
│   └── templates/
│       ├── paper_template.md
│       └── theme_template.md
│
└── 📁 pipeline_output/             ← Writing pipeline state
    ├── 00_preflight_check.md
    ├── 00_project_config.md
    ├── 01_search_strategy.md
    ├── 01_reference_list.md
    ├── 02_literature_notes.md       ← Includes conflict evidence matrix
    ├── 03_framework.md             ← User-LOCKED framework
    ├── 04_draft_section_01_intro.md
    ├── 04_draft_section_02_*.md
    ├── ...
    ├── 04.5_cross_section_check.md
    ├── 05_conclusion.md
    ├── 06_figure_instructions.md
    ├── 07_tables.md
    ├── 08_references_final.md
    ├── 09_final_manuscript.txt
    ├── 09_final_manuscript.docx     ← Optional
    └── 10_selfcheck_log.md
```

---

## Core Rules

Enforced throughout every step of the workflow:

| # | Rule | Enforcement |
|---|------|-------------|
| 1 | **Zero fabricated references** | Every citation traced to user-provided, verified PDF |
| 2 | **Evidence-based reasoning** | Never overconfident; speculative claims must be marked |
| 3 | **Critical synthesis** | No "laundry list" — evaluate strengths and weaknesses of each study |
| 4 | **Balanced coverage** | Conflicting findings discussed, not ignored |
| 5 | **Cite original research** | Primary articles cited, not reviews of reviews |
| 6 | **PMID/DOI verified** | Cross-checked against PubMed and PDF content |
| 7 | **User gates confirmed** | Every step requires explicit user acceptance |

---

## What This Skill Is NOT For

- ❌ **Systematic reviews** — Use PRISMA-based workflows
- ❌ **Meta-analyses** — Requires statistical synthesis frameworks
- ❌ **Scoping reviews, rapid reviews, umbrella reviews** — Different methodologies

If you need a systematic review, this skill will tell you so at Step 0.0 and recommend alternatives.

---

## Research Basis

This skill is grounded in **13 peer-reviewed publications** on scientific review writing methodology. Key sources:

| Author (Year) | Journal | Core Contribution |
|---------------|---------|-------------------|
| **Dhillon P** (2022) | *FEBS J* | Scope checklist, core components, figure design principles |
| **Chaney MA** (2021) | *JCVA* | NR three quality standards, NR vs SR, retrograde search |
| **Pautasso M** (2013) | *PLoS Comput Biol* | Ten rules: notes-while-reading, critical evaluation, feedback loops |
| **Gasparyan AY** (2011) | *Rheumatol Int* | Narrative biomedical review: authorship, ethics, title/abstract |

See **[references.md](references.md)** for the complete list of 13 references with DOIs, and **[references_summary.txt](references_summary.txt)** for a ranked summary by journal quartile and impact factor.

---

## File Structure

```
narrative-review/
├── SKILL.md                    # Main orchestrator (11-step workflow)
├── README.md                   # This file (English)
├── README_zh.md                # Chinese version
├── LICENSE                     # MIT License
├── .gitignore
│
├── nr-vs-sr.md                 # Narrative vs Systematic comparison table
├── scope-checklist.md          # 6-factor topic assessment rubric
├── search-strategy.md          # PubMed/MeSH search construction guide
├── figure-template.md          # Figure drawing instruction template
├── table-template.md           # Summary table template
├── vancouver-guide.md          # Vancouver reference format specification
├── obsidian-templates.md       # Obsidian note templates (paper/theme/MOC)
├── preflight-check.md          # Dependency skill scan logic
├── quality-checklist.md        # Final acceptance checklist (30 items)
├── references.md               # Complete research basis (13 references)
└── references_summary.txt      # Ranked reference list (by journal quartile/IF)
```

---

## A Note on Gray Literature

While our research basis includes Paez (2017) on gray literature search methodologies, **this skill's protocol operates exclusively on data from verified, peer-reviewed published literature provided by the user.** No references from non-commercial publications, preprints, conference abstracts, or other gray literature sources are incorporated into the manuscript unless the user explicitly provides and verifies them through the standard PDF verification pipeline (Step 3.0). This ensures every citation in the final manuscript is traceable to a credible, peer-reviewed source.

---

## Disclaimer

**For academic research purposes only.** This skill is designed as a research assistance tool to support the academic writing process. It is NOT a complete, publication-ready manuscript generation system. Users are solely responsible for:

- The scientific accuracy and integrity of all content
- Final verification of all citations and references
- Compliance with target journal guidelines and ethical standards
- Peer review and revision processes required for publication
- Any legal or regulatory requirements applicable to their field

The authors assume no liability for manuscripts produced using this skill.

---

## Feedback & Contact

Questions, suggestions, or collaboration ideas are welcome. Please open a GitHub Issue or reach out via the contact information at the top of this page.

---

## License

MIT — see [LICENSE](LICENSE) for details.

---

<p align="center">
  <sub>Built with ❤️ for rigorous, reproducible scientific writing.</sub>
</p>
