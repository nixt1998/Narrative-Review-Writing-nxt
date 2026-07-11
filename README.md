<!--
╔══════════════════════════════════════════════════════════╗
║  Author / 作者                                            ║
║  Name / 姓名:  Xiaoting Ni (倪啸庭)                      ║
║  Affiliation: School of Pharmacy, Qiqihar Medical Univ.  ║
║               Dept. of Pharmacy, The First Affiliated    ║
║               Hospital of Harbin Medical University       ║
║  Email:       nixt1998@163.com                           ║
║  ORCID:       0009-0009-6400-4071                        ║
╚══════════════════════════════════════════════════════════╝
-->

<div align="center">

# Narrative Review Writing Skill · Clinical Pharmacology & Drug Mechanisms

### A structured AI-assisted workflow for rigorous, reproducible pharmaceutical narrative review writing — grounded in NLM standards, 13 peer-reviewed methodology papers, and evidence-based scientific integrity

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-orange)](https://claude.ai/code)
[![Version](https://img.shields.io/badge/Version-v2.1-brightgreen.svg)]()
[![NLM Vancouver](https://img.shields.io/badge/Citation-Vancouver%2FNLM-purple.svg)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen.svg)]()
[![Stars](https://img.shields.io/badge/GitHub-Stars%20Welcome-yellow.svg)]()

**19 workflow steps · 40 curated requirements · 30 NLM citation types · 13 methodology papers · Zero fabricated references**

> ⭐⭐ If this skill supports your research, please star⭐ this repository to show your support!⭐⭐

</div>

**Language:** &nbsp; 🇬🇧 **English** &nbsp; | &nbsp; [🇨🇳 中文](README_zh.md)

---

## Purpose

To establish a rigorous, reproducible, and evidence-grounded framework for pharmacological narrative review writing, enabling researchers to produce publication-quality manuscripts that uphold the highest standards of scientific integrity. This skill bridges the gap between AI assistance and scholarly rigor — combining structured workflow enforcement with indispensable human judgment — to support evidence-based exploration of drug mechanisms, pharmacokinetics, and clinical pharmacology.

---

## Table of Contents

- [Why Human-AI Collaboration?](#why-human-ai-collaboration)
- [Comparative Advantages](#comparative-advantages)
- [Feature Highlights](#feature-highlights)
- [What This Skill Can and Cannot Do](#what-this-skill-can-and-cannot-do)
- [Target Audience](#target-audience)
- [Workflow Overview](#workflow-overview-v21--19-steps)
- [User Input Templates by Stage](#user-input-templates-by-stage)
- [Output Files Overview](#output-files-overview)
- [Output Article Structure](#output-article-structure)
- [Supported Citation Formats](#supported-citation-formats)
- [Supported Languages](#supported-languages)
- [Version Update Notes](#version-update-notes)
- [Domain Focus](#domain-focus)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Core Rules](#core-rules)
- [Research Basis](#research-basis)
- [File Structure](#file-structure)
- [Disclaimer](#disclaimer)
- [Feedback and Contact](#feedback-and-contact)
- [Contribution](#contribution)
- [Changelog](#changelog)
- [License](#license)

---

## Why Human-AI Collaboration?

The pharmacological literature is mechanistically complex and rapidly evolving. Full automation risks fabricated citations, oversimplified mechanistic interpretations, and the erasure of critical synthesis. Pure manual writing, on the other hand, is time-consuming, prone to organizational inconsistencies, and susceptible to missed literature across multiple databases.

This skill operates on a **human-AI collaboration model**:

- **The AI handles:** Structural enforcement, format compliance, anti-hallucination protocol, systematic three-pass verification, context management across 100+ references, dynamic batch processing, reproducible search documentation.
- **The researcher handles:** Scientific judgment, literature selection, mechanistic interpretation, framework decisions, and final confirmation at every major step.

At every critical juncture — framework locking, section acceptance, reference verification — the researcher provides explicit approval. This is not a "press-go" manuscript generator. It is a precision instrument that amplifies researcher capacity while keeping every scientific decision where it belongs: with the domain expert.

---

## Comparative Advantages

| Dimension | Manual Writing | Full Automation | Other Skills | NRW v2.1 |
|-----------|:---:|:---:|:---:|:---:|
| Zero fabricated references | ✅ | ❌ | ⚠️ | ✅✅ |
| Citation triple-verification (3 passes) | ⚠️ | ❌ | ❌ | ✅ |
| Human approval gates at every step | ✅ | ❌ | ⚠️ | ✅ |
| 100+ reference context management | ❌ | ⚠️ | ❌ | ✅ |
| Dynamic N-based batch verification | ❌ | ❌ | ❌ | ✅ |
| Obsidian knowledge graph | ❌ | ❌ | ❌ | ✅ |
| Section Brief (writing logic per section) | ❌ | ❌ | ❌ | ✅ |
| Vancouver/NLM 30-type full ruleset | ⚠️ | ⚠️ | ⚠️ | ✅ |
| Gene/protein nomenclature enforcement | ⚠️ | ❌ | ❌ | ✅ |
| Multi-platform (DeepSeek / Claude) | — | ⚠️ | ❌ | ✅ |
| Reproducible search record (9-item) | ⚠️ | ⚠️ | ❌ | ✅ |
| Standalone Word outputs per component | ❌ | ❌ | ❌ | ✅ |
| Session run log with full audit trail | ❌ | ❌ | ❌ | ✅ |
| Scientific judgment preserved | ✅ | ❌ | ⚠️ | ✅ |
| Time to draft | Very High | Very Low | Low | Medium |

Legend: ✅ Full support · ⚠️ Partial or variable · ❌ Not supported or high risk

---
## Feature Highlights

Each feature is a deliberate design choice grounded in identified failure modes of existing approaches.

**1. Dynamic Anti-Hallucination Protocol**
Every citation must trace to a user-provided, verified PDF. Unverifiable references are excluded outright -- not retained with a warning.
*Why it matters:* AI citation hallucination is well-documented in academic contexts. A single fabricated reference undermines the entire manuscript.
*Rationale:* PMID/DOI cross-validation + three-pass verification (Steps 3.0, 5.0, 9.0). See [SKILL.md Step 3.1](SKILL.md).

**2. Dynamic N-Based Batch Verification**
Verification intensity scales with your target reference count N. If N < 35, every paper is verified individually (100% coverage). If N >= 35, batches activate at the N/2 mark with >= 50% audit per batch, rounded up.
*Why it matters:* Fixed thresholds either over-sample small reviews or under-sample large ones.
*Rationale:* Proportional audit design ensures consistent coverage regardless of review size. See [SKILL.md Step 3.1](SKILL.md).

**3. Obsidian Knowledge Graph**
After verification, each paper becomes a structured Obsidian note with wikilinks; theme notes and MOC maps are auto-generated for visual graph exploration.
*Why it matters:* Loading 100+ PDFs directly into an AI context window overflows any model's capacity.
*Rationale:* Claude reads vault notes in strict order (MOC -> themes -> papers) during writing, never loading all papers simultaneously. See [SKILL.md Step 3.5](SKILL.md).

**4. Section Brief Before Every Section Draft**
Before writing each section, Claude outputs a Section Brief: writing logic, core argument, evidence basis, and word budget.
*Why it matters:* Articulating the section's logical role before prose is generated catches structural errors before they are written into 500 words of text.
*Rationale:* Forces explicit argument design; enables user to redirect before investment is made. See [SKILL.md Step 5.0](SKILL.md).

**5. Batched Output Protocol**
Large outputs (literature notes, section drafts, reference lists) are split into platform-appropriate batches with continuation markers [OUTPUT PART X/N].
*Why it matters:* Claude app, Claude terminal, and DeepSeek have different output token limits. Unconstrained output risks mid-response truncation that permanently loses work.
*Rationale:* Platform-calibrated batch sizes recorded at Step 0.0b; all large-output steps apply the protocol. See [SKILL.md Batched Output Protocol](SKILL.md).

**6. Multi-Database Reproducible Search Record**
Searches across PubMed, Web of Science, ScienceDirect, Wiley Online Library, and Embase (user-selectable). Full reproducibility record includes search date, database versions, exact Boolean queries, and pre/post-deduplication counts (9 items total).
*Why it matters:* Reproducibility is a core scientific value; peer reviewers increasingly request full search documentation.
*Rationale:* Step 2.8 nine-item record allows independent search replication. See [SKILL.md Step 2.8](SKILL.md).

**7. Gene and Protein Nomenclature Enforcement**
Human genes ALL CAPS italics (HGNC), mouse/rat genes first-cap lowercase italics (MGI), proteins non-italic (UniProt) -- verified before writing.
*Why it matters:* Nomenclature errors are a frequent cause of editorial desk rejection in pharmacological journals.
*Rationale:* Verification against HGNC, GeneCards, MGI, UniProt enforced in writing rules. See [SKILL.md Core Rules](SKILL.md).

**8. Standalone Word Outputs per Manuscript Component**
Figure legends, tables, and abbreviations table are each output as separate .docx files with correct journal formatting, in addition to the main manuscript.
*Why it matters:* Most pharmacology journals require tables and figures submitted as separate files; inline inclusion causes submission errors.
*Rationale:* Three standalone .docx files (06_figure_legends.docx, 07_tables_standalone.docx, 10_abbreviations.docx). See [SKILL.md Steps 7.0, 8.0, 10.3](SKILL.md).

**9. Full Vancouver/NLM Citation Ruleset**
Internal vancouver-guide.md contains all 30 NLM document-type formats, punctuation rules, date conventions, and appendixes from Citing Medicine (NLM, 2007, updated 2020).
*Why it matters:* Partial Vancouver implementations miss unusual types (preprints, dissertations, patents) that appear in pharmacological reviews.
*Rationale:* No external file dependency; full NLM guide merged into skill file. See [Citing Medicine PDF](Citing%20Medicine-The%20NLM%20Style%20Guide%20for%20Authors%2C%20Editors%2C%20and%20Publishers.pdf).

**10. Session Run Log with Full Audit Trail**
A run log (pipeline_output/run_log.md) created at Step 0.0 records every user input, action, output file, and timestamp throughout the session.
*Why it matters:* Long review sessions can be interrupted; the log enables exact reconstruction of what was decided and when.
*Rationale:* Global rule applies to all 19 steps. See [SKILL.md Step 0.0](SKILL.md).

---

## What This Skill Can and Cannot Do

### This skill CAN help you:

- Provide a structured 19-step workflow from topic selection to final manuscript
- Enforce anti-hallucination protocols so every citation is traceable to a verified source
- Manage references across large literature sets (100+ papers) without context overflow
- Generate a Section Brief before each draft -- articulating writing logic, core argument, and evidence basis
- Verify gene/protein symbols against HGNC, MGI, and UniProt standards before writing
- Format references in Vancouver/NLM (default), AMA, APA, or journal-specific styles
- Output manuscripts in .txt and .docx with proper formatting (TNR 10pt, 1.5x spacing, justified)
- Generate standalone Word files for figure legends, tables, and abbreviations
- Document your full search strategy with a 9-item reproducibility record
- Maintain a session run log as an audit trail for the entire writing process

### This skill CANNOT do -- and these limitations are by design:

- **Replace scientific judgment.** Which papers to emphasize, how to handle contradictory evidence, and what position the review takes are irreducibly human decisions.
- **Evaluate methodology quality** of a cited paper -- it can confirm the paper exists and the cited claim matches what the paper reports; it cannot assess whether the paper's methods are sound.
- **Generate novel hypotheses** beyond what the cited literature explicitly supports.
- **Replace peer review, editorial assessment, or institutional oversight.**
- **Guarantee publication acceptance** -- it improves structure and format, not the scientific contribution.

> **On critical and independent thinking:** This skill is a precision instrument, not a substitute for intellectual engagement. The most valuable contribution of a narrative review -- the synthesis of mechanistic evidence, the identification of knowledge gaps, the critical evaluation of contradictory findings -- cannot be automated and must not be delegated. The skill enforces the scaffolding. You provide the science. Treat every AI-generated draft as a starting point for rigorous revision, not a finished product.

---

## Target Audience

**Recommended for:**
- Pharmacologists and pharmaceutical scientists writing narrative review articles
- PhD students and postdoctoral researchers in clinical pharmacy, pharmacology, or related biomedical fields
- Non-native English researchers who need structural and format support for English-language academic writing
- Researchers managing large literature sets (50-150 papers) who need systematic organization
- Laboratory heads and PIs who supervise narrative review manuscripts

**Not recommended for:**
- Systematic review or meta-analysis writing (use PRISMA-based workflows)
- Fields entirely outside pharmacology or biomedical mechanism research without adaptation

---
## Workflow Overview (v2.1 -- 19 Steps)

```
Step 0.0    Language Selection                                 [NEW in v2.1]
Step 0.0b   Model and Platform Selection                       [NEW in v2.1]
Step 0.1    NR vs SR Introduction
Step 0.5    Pre-flight Environment Check
Step 0.9    Title Confirmation                                 [NEW in v2.1]
Step 1.0    Project Parameters + Scope Definition
Step 2.0    Multi-Database Search Strategy + Reference List
Step 3.0    Literature Verification + Notes + Conflict Matrix
Step 3.5    Obsidian Vault Generation
Step 4.0    Framework Generation -> User Confirm -> LOCK
Step 5.0    Section-by-Section Writing (with Section Brief)
Step 5.5    Cross-Section Consistency Check                    [renamed from Step 4.5]
Step 6.0    Conclusion
Step 6.5    Abstract (structured or unstructured)              [NEW in v2.1]
Step 6.6    Keywords (MeSH preferred terms)                    [NEW in v2.1]
Step 7.0    Figure Instructions + Legends (+ standalone .docx)
Step 8.0    Summary Tables (+ standalone .docx)
Step 9.0    Reference Assembly + Triple Verification
Step 10.0   Final Assembly + Output
```

---

## User Input Templates by Stage

**Step 0.0 -- Language Selection**
```
Please type A or B:
  A) Chinese  (all interaction in Chinese; manuscript in English)
  B) English  (interaction and manuscript in English)
Default: B
```

**Step 1.0 -- Project Parameters**
```
Working directory : C:/Users/YourName/Documents/MyReview
Word limit        : 5000 words           (recommended: 4000-6000)
Figures           : 3
Tables            : 2
Target references : 100                  (default: 100)
Citation format   : Vancouver            (or: AMA / APA / journal-specific)
Target journal    : [Journal name, e.g., Cell, Nature, Science, Lancet]
```

**Step 2.0 -- Search Strategy**
```
Databases    : PubMed (default); also WOS, ScienceDirect, Wiley, Embase
Year range   : 2015 to 2026
Article types: Original research, review articles, clinical trials
Language     : English
Exclude      : Preprints, conference abstracts, editorials
```

**Step 4.0 -- Framework LOCK**
```
Review the proposed framework above.
  Type LOCK to accept and freeze the framework.
  Or specify modifications, for example:
    "Move section 2 before section 1"
    "Rename section 3 to: [new heading as a conclusion statement]"
    "Add a sub-section under 1.2 on [topic]"
```

**Step 5.0 -- Section Confirmation**
```
After reading the Section Brief and draft:
  CONFIRM  -- accept and proceed to the next section
  REVISE   -- followed by specific revision instructions
  REWRITE  -- regenerate the section with a different emphasis
```

**Step 9.0 -- Reference Assembly**
```
Auto-assemble : Claude compiles the reference list from verified notes
Manual insert : I will format references in my reference manager
Format        : Vancouver  (or specify alternative confirmed in Step 1.0)
```

---

## Output Files Overview

| File | Path | Contents |
|------|------|----------|
| Run log | pipeline_output/run_log.md | Full session log: inputs, actions, timestamps |
| Language | pipeline_output/00_language.md | Interaction language choice |
| Pre-flight | pipeline_output/00_preflight_check.md | Skills and network status |
| Project config | pipeline_output/00_project_config.md | All parameters, title, journal, format |
| Search strategy | pipeline_output/01_search_strategy.md | Full reproducibility record (9 items) |
| Reference list | pipeline_output/01_reference_list.md | All references with PMID/DOI |
| Literature notes | pipeline_output/02_literature_notes.md | Verified notes + conflict matrix |
| Obsidian vault | obsidian_vault/ | Complete knowledge graph |
| Framework | pipeline_output/03_framework.md | Locked outline with ref estimates |
| Section drafts | pipeline_output/04_draft_section_*.md | One file per section + Section Brief |
| Consistency check | pipeline_output/05.5_cross_section_check.md | Cross-section report |
| Conclusion | pipeline_output/05_conclusion.md | Conclusion draft |
| Abstract | pipeline_output/05b_abstract.md | Abstract draft |
| Keywords | pipeline_output/05c_keywords.md | MeSH keyword list |
| Figure instructions | pipeline_output/06_figure_instructions.md | Drawing instructions per figure |
| Figure legends .txt | pipeline_output/06_figure_legends.txt | Plain-text legends |
| Figure legends .docx | pipeline_output/06_figure_legends.docx | Standalone Word -- legends only |
| Tables .md | pipeline_output/07_tables.md | Summary tables in markdown |
| Tables .docx | pipeline_output/07_tables_standalone.docx | Standalone Word -- tables only |
| References | pipeline_output/08_references_final.md | Final formatted reference list |
| Manuscript .txt | pipeline_output/09_final_manuscript.txt | Complete plain-text manuscript |
| Manuscript .docx | pipeline_output/09_final_manuscript.docx | Word-formatted manuscript (main body) |
| Abbreviations .md | pipeline_output/10_abbreviations.md | Abbreviations table in markdown |
| Abbreviations .docx | pipeline_output/10_abbreviations.docx | Standalone Word -- abbreviations only |
| Self-check log | pipeline_output/10_selfcheck_log.md | QA passes and gate confirmations |

---
## Output Article Structure

```
Title
Abstract (structured: Background/Methods/Results/Conclusion -- or unstructured prose)
Keywords (5-8 MeSH preferred terms)
1. Introduction (300-500 words; gap identification + scope + signposting)
   Body sections (numbered 1., 1.1., 1.2., 2., 2.1., etc.)
   Each section heading is a CONCLUSION STATEMENT, not a descriptive label.
   Example: "1.1. NLRP3 Inflammasome Activation Mediates Cisplatin Nephrotoxicity"
   Not:      "1.1. Cisplatin and NLRP3"
Conclusion (350-500 words)
Acknowledgments (placeholder)
References (Vancouver/NLM format with [N] in-text citation)
Tables (also as 07_tables_standalone.docx)
Figure legends (also as 06_figure_legends.docx)
Abbreviations table (also as 10_abbreviations.docx)
```

---

## Supported Citation Formats

| Format | Status | Notes |
|--------|--------|-------|
| Vancouver / NLM | Default | Full 30-type ruleset in vancouver-guide.md; see also [Citing Medicine PDF](Citing%20Medicine-The%20NLM%20Style%20Guide%20for%20Authors%2C%20Editors%2C%20and%20Publishers.pdf) |
| AMA | Supported | Provide journal author guidelines URL in Step 1.0 |
| APA | Supported | Provide journal author guidelines URL in Step 1.0 |
| Journal-specific | Supported | Provide a sample reference or author instructions URL in Step 1.0 |

**About the NLM Citing Medicine Guide:** The Vancouver/NLM format rules used in this skill are derived from *Citing Medicine: The NLM Style Guide for Authors, Editors, and Publishers*, 2nd ed. (Patrias K; NLM, 2007, updated 2020). The full guide covers 30 document types including journal articles, books, book chapters, theses, patents, preprints, and internet sources. The internal vancouver-guide.md file contains the complete ruleset. For edge cases not covered internally, consult the [Citing Medicine PDF](Citing%20Medicine-The%20NLM%20Style%20Guide%20for%20Authors%2C%20Editors%2C%20and%20Publishers.pdf) or the [NLM online version](https://www.ncbi.nlm.nih.gov/books/NBK7256/).

---

## Supported Languages

| Component | Language |
|-----------|----------|
| Manuscript output | English only |
| User interaction | Chinese or English (selected in Step 0.0) |
| Compatible AI platforms | Claude terminal (Kiro CLI), Claude app (claude.ai), DeepSeek (with batched output protocol) |

---

## Version Update Notes

### v2.1 (current) vs v1.0

| Component | v1.0 | v2.1 |
|-----------|------|------|
| Workflow steps | 11 | 19 |
| New steps | -- | Language selection, platform selection, title confirmation, abstract, MeSH keywords |
| Reference verification | Single-pass | Triple-pass (Steps 3.0 + 5.0 + 9.0) |
| Batch verification | Fixed threshold | Dynamic N-based protocol (N/2 trigger, 50% audit/batch) |
| Output token management | None | Batched Output Protocol (DeepSeek/Claude compatible) |
| Search databases | PubMed only | PubMed, WOS, ScienceDirect, Wiley, Embase |
| Word outputs | Single manuscript | Manuscript + 3 standalone .docx (legends, tables, abbreviations) |
| Vancouver rules | Basic | Full 30-type NLM ruleset (internally merged) |
| Gene/protein nomenclature | Not enforced | Enforced (HGNC, MGI, UniProt verification) |
| Session audit | None | Full run log from Step 0.0 |
| Requirements covered | ~11 | 40 (+ 8 design fixes + 20 consistency improvements) |

---

## Domain Focus

**Primary:** Clinical pharmacology and basic pharmacological mechanism research

- Drug mechanisms of action (receptor binding, enzyme inhibition, transporter interactions)
- Signaling pathways and molecular targets (NF-kB, PI3K/Akt, MAPK, JAK/STAT, mTOR, etc.)
- Pharmacokinetics and pharmacodynamics (ADME, drug-drug interactions, bioavailability)
- Drug-induced toxicity mechanisms (nephrotoxicity, cardiotoxicity, hepatotoxicity)
- Structure-activity relationships (SAR) and molecular pharmacology
- Pharmacogenomics and precision medicine

The skill can be adapted to other mechanism-focused biomedical fields.

---

## Installation

### Prerequisites

| Dependency | Required | Purpose |
|-----------|----------|---------|
| [Claude Code](https://claude.ai/code) or Kiro CLI | Yes | Runtime environment |
| pdf skill | Yes | Literature PDF verification (Step 3.0) |
| docx skill | Optional | Word document output (Step 10.0) |
| Obsidian (desktop app) | Recommended | Knowledge graph visualization (Step 3.5) |

### Install via Git

```bash
git clone https://github.com/YOUR_USERNAME/narrative-review-skill.git ~/.claude/skills/narrative-review
```

### Manual Install

```bash
mkdir -p ~/.claude/skills/narrative-review
cp *.md LICENSE ~/.claude/skills/narrative-review/
```

### Verify Installation

In Claude Code or Kiro CLI, type:
```
write a narrative review about [your topic]
```
The skill should auto-trigger at Step 0.0 (Language Selection).

---

## Quick Start

```
You:    write a narrative review about the role of mitochondrial dysfunction
        in cisplatin-induced nephrotoxicity

Claude: [narrative-review skill triggered]
Step 0.0  -- Language: A) Chinese  B) English  -> select
Step 0.0b -- Platform: Claude terminal / Claude app / DeepSeek  -> select
Step 0.1  -- NR vs SR: This skill writes narrative reviews only.
Step 0.5  -- Pre-flight: pdf [OK] docx [OK] network [OK] -> PASS
Step 0.9  -- Proposed title: "..." -> confirm or revise
Step 1.0  -- Parameters: directory / word limit / figures / tables / references / journal
Step 2.0  -- Search across PubMed (+ selected databases); output reference list
Step 3.0  -- Verify all PDFs; build structured notes; identify conflicts
Step 3.5  -- Generate Obsidian vault (papers + themes + MOC maps)
Step 4.0  -- Framework -> user review -> LOCK
Step 5.0  -- Section Brief + draft for each section -> user confirms each
Step 5.5  -- Cross-section consistency check
Step 6.0  -- Conclusion
Step 6.5  -- Abstract (structured or unstructured)
Step 6.6  -- Keywords (MeSH terms)
Step 7.0  -- Figure drawing instructions + legend file
Step 8.0  -- Summary tables
Step 9.0  -- Reference assembly + triple verification
Step 10.0 -- Final assembly -> deliver all output files
```

---
## Core Rules

Enforced at every step of the workflow:

| # | Rule | Enforcement |
|---|------|-------------|
| 1 | Zero fabricated references | Every citation traced to user-provided, verified PDF |
| 2 | Evidence-based reasoning | Never overconfident; speculative claims must be marked (author synthesis) |
| 3 | Critical synthesis | No laundry-list enumeration -- evaluate strengths and limitations of every key study |
| 4 | Balanced coverage | Conflicting findings discussed, not selectively ignored |
| 5 | Cite original research | Primary articles cited; not reviews of reviews |
| 6 | Triple PMID/DOI verification | Passes 1-3 across Steps 3.0, 5.0, 9.0 |
| 7 | Human gates confirmed | Every step requires explicit user acceptance before proceeding |
| 8 | Dynamic batch verification | N-based protocol: N<35 individual; N>=35 batch with >=50% audit per batch |
| 9 | Gene/protein nomenclature | HGNC/GeneCards (genes) and UniProt (proteins) verified before writing |
| 10 | No AI-characteristic language | Banned expressions scanned and removed before each section delivery |

---

## Research Basis

This skill is grounded in **13 peer-reviewed publications** on scientific review writing methodology,
plus the authoritative NLM citation style guide.

| Author (Year) | Journal | JCR | Core Contribution |
|---------------|---------|-----|-------------------|
| Dhillon P (2022) | FEBS J | Q1 | Scope checklist, core components, figure design |
| Chaney MA (2021) | JCVA | Q2 | NR quality standards, NR vs SR, retrograde search |
| Pautasso M (2013) | PLoS Comput Biol | Q1 | Ten rules: notes-while-reading, critical tone, feedback |
| Gasparyan AY (2011) | Rheumatol Int | Q3 | Narrative biomedical review: authorship, ethics, title |
| Balon R (2022) | Psychother Psychosom | Q1 | Review article definition, typology, purpose |
| Goodfellow LT (2023) | Respir Care | Q2 | 7 stages of literature review, database selection |
| Page MJ (2021) | BMJ | Q1 | PRISMA 2020: reporting standards (adapted) |
| Wright RW (2007) | Clin Orthop Relat Res | Q1 | PICO framework, research protocol |
| Harris JD (2014) | Am J Sports Med | Q1 | PRISMA guidelines, evidence grading |
| Paez A (2017) | J Evid Based Med | Q2 | Gray literature search strategies |
| Pati D (2018) | HERD | Q3 | SLR methodology in healthcare design |
| Randles R (2023) | Nurse Educ Today | Q1 | SR guidelines, Cochrane/JBI frameworks |
| Livschitz J (2023) | Am J Surg | Q2 | 6 steps to SR, common pitfalls |

**Reference Format Authority:** Patrias K. Citing Medicine: The NLM Style Guide for Authors, Editors, and Publishers. 2nd ed. Bethesda (MD): NLM; 2007. Updated 2020. [PDF](Citing%20Medicine-The%20NLM%20Style%20Guide%20for%20Authors%2C%20Editors%2C%20and%20Publishers.pdf) | [Online](https://www.ncbi.nlm.nih.gov/books/NBK7256/)

See **[references.md](references.md)** for full citations and **[references_summary.txt](references_summary.txt)** for journal quartile/IF ranking.

---

## File Structure

```
narrative-review/
+-- SKILL.md                    # Main orchestrator (19-step v2.1 workflow)
+-- README.md                   # This file (English)
+-- README_zh.md                # Chinese version
+-- LICENSE                     # MIT License
|
+-- nr-vs-sr.md                 # Narrative vs Systematic comparison
+-- scope-checklist.md          # 6-factor topic assessment
+-- search-strategy.md          # Multi-database search construction guide
+-- figure-template.md          # Figure instruction + legend format template
+-- table-template.md           # Summary table template
+-- vancouver-guide.md          # Full NLM 30-type citation ruleset (55KB)
+-- obsidian-templates.md       # Obsidian note templates (paper/theme/MOC)
+-- preflight-check.md          # Dependency scan logic
+-- quality-checklist.md        # Final acceptance checklist (v2.1 extended)
+-- references.md               # Research basis (13 papers + NLM guide)
+-- references_summary.txt      # Ranked by journal quartile/IF
+-- Citing Medicine-The NLM Style Guide...pdf  # NLM citation authority
```

---

## A Note on Gray Literature

While our research basis includes Paez (2017) on gray literature search methodologies, **this skill operates exclusively on verified, peer-reviewed published literature provided by the user.** No content from preprints, conference abstracts, or other gray literature is incorporated unless the user explicitly provides and verifies it through the PDF verification pipeline (Step 3.0).

---

## Disclaimer

**For academic research assistance only.** This skill supports the writing process but is NOT a publication-ready manuscript generator. Users are solely responsible for:

- The scientific accuracy and integrity of all content
- Final verification of all citations and references
- Compliance with target journal guidelines and ethical standards
- Peer review and revision processes required for publication

The skill is a writing aid. It cannot replace domain expertise, independent critical thinking, or scholarly judgment. Always review AI-generated content with the same rigor you would apply to any other research tool.

---

## Feedback and Contact

Questions, suggestions, or collaboration ideas are welcome.

- **Email:** nixt1998@163.com
- **ORCID:** 0009-0009-6400-4071
- Please open a GitHub Issue for bug reports or feature requests.

---
## Contribution

| Name | Institution | Role |
|------|-------------|------|
| Xiaoting Ni | School of Pharmacy, Qiqihar Medical University; Department of Pharmacy, The First Affiliated Hospital of Harbin Medical University | Creator and Lead Developer |
| Wenyu Fu | School of Pharmacy, Qiqihar Medical University | v2.1Optimization |
| [Research Group / Team Name] | [Institution] | [Team Contribution Description] |

We welcome contributions from pharmacologists, pharmaceutical scientists, clinical pharmacists, and AI researchers. Whether it is improving the workflow, adding domain-specific knowledge, fixing issues, or extending support to new citation formats -- your expertise matters.

> **Join us in building the Narrative Review Writing Skill for Clinical Pharmacology and Basic Pharmacological Mechanism Research -- together, for more rigorous and reproducible pharmaceutical science writing!**

---

## Changelog

### v2.1 -- 2026-07-09

This major update transforms the skill from an 11-step framework into a comprehensive 19-step production-grade workflow. The update integrates 34 original user requirements, 6 additional requirements, 8 architectural design fixes, and 20 post-analysis consistency improvements identified through systematic review of the full skill specification.

- **New:** Step 0.0 (language selection), Step 0.0b (platform selection for max-token management), Step 0.9 (title confirmation with post-writing revision option), Step 6.5 (abstract -- structured or unstructured), Step 6.6 (MeSH keywords), Batched Output Protocol (DeepSeek/Claude compatible), Multi-Agent Context Strategy, Section Brief (writing logic + core argument + evidence basis before each section), Dynamic N-based batch verification (replaces all fixed thresholds), full session run log from Step 0.0, multi-database search support (PubMed + WOS + ScienceDirect + Wiley + Embase), standalone Word outputs for figure legends/tables/abbreviations, gene/protein nomenclature enforcement (HGNC, MGI, UniProt), three-pass citation verification.
- **Changed:** Step 4.5 renamed to Step 5.5 (cross-section consistency check, correctly positioned after all sections are written), Vancouver/NLM citation rules moved to internal vancouver-guide.md (NLM Citing Medicine fully merged, no external path dependency), Obsidian listed as recommended dependency, run log initialization moved to Step 0.0.
- **Fixed:** Verification rate thresholds unified (90% return threshold / 95% target), cross-section check filename corrected (04.5 to 05.5), all 40 requirements fully traceable in requirements traceability table, Common Mistakes table cleaned of developer notes, justified paragraph alignment consistently specified across all Word output sections.

---

### v1.0 -- 2026-06-30

Initial release of the Narrative Review Writing Skill for clinical pharmacology and basic pharmacological mechanism research. This version established the core 11-step guided pipeline covering topic scoping through final manuscript assembly.

- **New:** Complete 11-step workflow; zero-fabrication reference protocol with PMID/DOI verification; Obsidian vault auto-generation with structured paper notes and MOC maps; conflict evidence matrix; pre-flight dependency scan; conclusion-statement heading requirement; figure drawing instruction template with per-figure visual hierarchy guidance; Vancouver citation format with [N] in-text citation before period; dual-track context management (pipeline output files + Obsidian vault); 6-factor scope assessment; research basis grounded in 13 peer-reviewed methodology papers.

---

## License

MIT -- see [LICENSE](LICENSE) for details.

---

<p align="center">
  <sub>Built with ❤️ for rigorous, reproducible scientific writing.</sub>
</p>
