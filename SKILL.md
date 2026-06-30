---
name: narrative-review
description: Use when writing an English narrative review article in clinical pharmacology or basic pharmacological mechanism research. Triggers on: narrative review, literature review, review article, write a review, state-of-the-art review, scientific review, 综述写作, 叙述性综述. Covers complete workflow from topic scoping through search strategy, literature verification, knowledge graph construction, framework building, section-by-section writing, figure/table generation, and final manuscript assembly. NOT for systematic reviews or meta-analyses (use PRISMA-based workflows for those).
---

# Narrative Review Writing

## Overview

Guides the complete workflow for writing an English narrative review article in clinical pharmacology and basic pharmacological mechanism research. Grounded in best practices from Dhillon (2022), Chaney (2021), Pautasso (2013), Gasparyan (2011), and others. See [references.md](references.md) for the complete research basis.

**Core principle:** Zero fabricated references. Every citation must trace to a user-provided, verified PDF. Evidence-based reasoning only — never overconfident, never speculative without marking it as such.

## Dual-Track Architecture

This skill uses two parallel systems to manage context across 100+ reference reviews:

1. **Pipeline Output** (`pipeline_output/`) — File-per-step state management. Claude writes each step's output to disk; the next step reads only what it needs. Enables interrupt/resume at any step.
2. **Obsidian Vault** (`obsidian_vault/`) — Knowledge graph for the user's long-term research. Each paper becomes a structured note with YAML frontmatter and [[wikilinks]]. Claude reads thematic MOC notes during writing instead of loading full PDFs.

**Context efficiency rule:** Claude reads Obsidian notes (`_MOC_*.md` → `themes/*.md` → `papers/NNN*.md`) to get precise citation content, rather than loading complete PDFs into the context window.

## When to Use

- Writing an English narrative/traditional literature review
- Clinical pharmacology, pharmacokinetics, pharmacodynamics, drug mechanisms
- Basic pharmacological mechanisms (signaling pathways, molecular targets, drug-receptor interactions)
- State-of-the-art or integrative reviews in biomedical sciences

**NOT for:**
- Systematic reviews with PRISMA methodology
- Meta-analyses
- Scoping reviews, rapid reviews, umbrella reviews

## Dependency Skills

Pre-flight check at Step 0.5. See [preflight-check.md](preflight-check.md) for detailed scan logic.

| Skill | Required | Purpose |
|-------|----------|---------|
| `pdf` | **Yes** | Read/verify PDF content (Step 3) |
| `docx` | Optional | Generate Word output (Step 10) |

Missing required skill → **BLOCK**. Missing optional → **WARN** but allow degraded mode.

## Core Rules (Embedded in Every Step)

### Anti-Hallucination
1. ALL cited literature MUST come from user-provided downloaded PDFs
2. Every PMID/DOI MUST be verified against actual PDF content
3. PubMed search ONLY — never search-engine-only results
4. Every reference cross-verified twice: Step 3 (content) + Step 9 (citation)
5. One fabricated reference = restart verification from Step 3

### Writing Quality
- **New insights required** — not a "book report" (Chaney 2021)
- **No laundry list** — synthesize across studies, don't enumerate (Dhillon 2022)
- **Be balanced** — discuss findings you disagree with (Dhillon 2022)
- **Cite original research** — not reviews of reviews (Dhillon 2022)
- **Critical evaluation** — strengths, weaknesses, contradictions of every key study (Pautasso 2013)
- **Tone**: evidence-based inference, appropriately cautious, never overconfident
- **Language**: precise, concise, accessible to non-specialist readers

### Format
- Citation: `[N]` before period: `...as demonstrated [1,3,5].`
- Default reference style: Vancouver
- Default output: `.txt` + optional `.docx`

---

## Workflow

```
Step 0.0 → Introduction (NR vs SR)
Step 0.5 → Pre-flight Environment Check
Step 1.0 → Project Parameters + Scope Definition
Step 2.0 → Search Strategy + Reference List
Step 3.0 → Literature Verification + Notes + Conflict Matrix
Step 3.5 → Obsidian Vault Generation
Step 4.0 → Framework → User Confirm → LOCK
Step 4.5 → Cross-Section Consistency Check  [after all sections written]
Step 5.0 → Section-by-Section Writing
Step 6.0 → Conclusion
Step 7.0 → Figure Instructions + Legends
Step 8.0 → Summary Tables
Step 9.0 → Reference Assembly + Cross-Verification
Step 10.0 → Final Assembly + Abbreviations Table + Output
```

---

## Step 0.0 — Introduction: NR vs SR

**Goal:** Ensure the user knows what a narrative review is and isn't.

Display the comparison from [nr-vs-sr.md](nr-vs-sr.md).

Declare: "This skill writes **narrative reviews only**. If you need a systematic review with PRISMA methodology, use a different workflow."

**Self-check:**
- [ ] User acknowledged NR vs SR distinction
- [ ] User confirmed they want a narrative review

**→ Next:** `"确认后请回复'继续'进入环境检查"`

---

## Step 0.5 — Pre-flight Environment Check

**Goal:** Verify all required/recommended skills are available before any work begins.

Follow the scan logic in [preflight-check.md](preflight-check.md).

**Outcome:**
- All required skills present → ✅ PASS, continue
- Required skill missing → ⛔ BLOCK, tell user what to install
- Recommended skill missing → ⚠️ WARN, allow degraded-mode continue

**Output:** `pipeline_output/00_preflight_check.md`

**Self-check:**
- [ ] Required skills scan complete
- [ ] Any missing skills flagged with install instructions

**→ Next:** `"环境检查通过。请回复'继续'进入项目参数设置"`

---

## Step 1.0 — Project Parameters + Scope Definition

**Goal:** Lock project constraints; validate topic viability.

### 1.1 Collect Parameters

Ask user for:
| Parameter | Question |
|-----------|----------|
| Working directory | "请提供工作目录的绝对路径" |
| Word limit | "全文字数限制？(推荐 4000-6000 words per Dhillon 2022)" |
| Figure count | "计划包含几张图 (Figures)？" |
| Table count | "计划包含几张表 (Tables)？" |
| Title/topic | "请提供综述标题或核心主题" |

Auto-calculate per-section word budget based on total.

### 1.2 Scope Assessment

Run the 6-factor checklist from [scope-checklist.md](scope-checklist.md):

1. **Personal motivation** — Is the author genuinely interested?
2. **Timeliness** — ≥15 relevant papers published <5 years?
3. **Novelty** — Similar review in past 1-2 years? Can you offer a new perspective?
4. **Breadth** — Focused enough to be manageable, broad enough for readership?
5. **Journal relevance** — Topic fits target journal scope?
6. **Author expertise** — Team adequately knowledgeable?

Rate each 1-5. Flag any score ≤2 for discussion.

**Output:** `pipeline_output/00_project_config.md`

**Self-check:**
- [ ] All parameters recorded
- [ ] All 6 scope factors rated
- [ ] Working path confirmed writable
- [ ] Word budget calculated

**→ Next:** `"项目参数已保存。请回复'继续'进入检索策略"`

---

## Step 2.0 — Search Strategy + Reference List

**Goal:** Build a reproducible search strategy; output structured reference list.

### 2.1 Build Search Strategy

Based on user's title/keywords:
1. Extract core concepts → MeSH terms + free-text keywords
2. Combine with Boolean operators
3. Recommend databases and date ranges

Follow [search-strategy.md](search-strategy.md) for detailed construction.

### 2.2 Execute or Delegate Search

Ask: **"Do you need assisted searching?"**
- **Yes** → Execute PubMed/Embase search, output structured results
- **No** → Output the search strategy for user to execute independently

### 2.3 Output Reference List

Format:
```
| # | PMID | DOI | Title | First Author | Year | Journal | File Name |
|---|-----|-----|-------|-------------|------|---------|-----------|
| 1 | 12345678 | 10.xxxx/xxxx | Title Text | Author A | 2024 | Journal | 001_Author2024_Topic.pdf |
```

Recommend: `NNN_AuthorYear_Keyword.pdf` naming convention.

**Output:** `pipeline_output/01_search_strategy.md` + `pipeline_output/01_reference_list.md`

**Self-check:**
- [ ] Search strategy is reproducible (another researcher could replicate it)
- [ ] Every entry has PMID + DOI (where available)
- [ ] Naming convention documented
- [ ] Databases and date ranges specified

**→ Next:** `"文献下载完成并重命名后，请提供文献文件夹路径，回复'继续'进入验证"`

---

## Step 3.0 — Literature Verification + Reading Notes

**Goal:** Verify every reference is real; extract structured findings; identify contradictions.

### 3.1 Verify Each PDF

For every PDF file:
1. Open with `pdf` skill — extract: title, first author, PMID, DOI, journal, year
2. Cross-validate against `01_reference_list.md`
3. Tag: ✅ Verified / ⚠️ Discrepancy (describe) / ❌ Cannot verify

### 3.2 Extract Structured Notes

For each verified paper:
- **Core findings** (3-5 bullet points — the paper's actual conclusions)
- **Methodology** (model system, technique, sample size, key reagents)
- **Key mechanisms/pathways** (specific molecules, interactions, direction of effect)
- **Strengths** (large sample, rigorous controls, multiple models)
- **Limitations** (small n, single model, lack of controls, conflict of interest)
- **Relevance to this review** (which section/framework heading)

### 3.3 Conflict Evidence Matrix

When ≥2 papers disagree on a mechanism or conclusion:

```
| Issue | Supporting [N] | Opposing [N] | Possible Explanation | This Review's Position |
|-------|----------------|--------------|---------------------|----------------------|
```

**Output:** `pipeline_output/02_literature_notes.md`

**Self-check:**
- [ ] Verification rate ≥ 95% (flagged papers must be addressed)
- [ ] All discrepancies documented with specific reason
- [ ] Conflict matrix populated where applicable
- [ ] Every paper has complete structured notes

**→ Next:** `"验证完成（X/Y篇通过）。请回复'继续'构建知识图谱"`

---

## Step 3.5 — Obsidian Vault Generation

**Goal:** Build a knowledge graph for user's long-term research and Claude's context-efficient writing.

### 3.5.1 Create Vault Structure

```
obsidian_vault/
├── _MOC_Overview.md
├── _MOC_Mechanisms.md
├── _MOC_Clinical_Translation.md
├── _MOC_Controversies.md
├── _MOC_Figure_Ideas.md
├── papers/
├── themes/
└── templates/
```

### 3.5.2 Generate Paper Notes

For each verified paper → `papers/NNN_AuthorYear_Keyword.md` using the template in [obsidian-templates.md](obsidian-templates.md).

### 3.5.3 Generate Theme Notes

Auto-identify high-frequency keywords across papers → create `themes/ThemeName.md` aggregating all relevant findings with [[wikilinks]] back to source papers.

### 3.5.4 Generate MOC Index Notes

Create Map of Content files hierarchically organizing all themes and papers.

**Output:** Complete `obsidian_vault/`

**Self-check:**
- [ ] Every verified paper has a note with complete YAML frontmatter
- [ ] All [[wikilinks]] resolve to existing notes
- [ ] MOCs cover all identified themes
- [ ] User can open vault in Obsidian and see the graph

**→ Next:** (During writing, Claude reads `_MOC_*.md` → `themes/*.md` → `papers/NNN*.md` for precise content instead of loading full PDFs.)

`"知识图谱已构建。请在 Obsidian 中打开 vault 查看。请回复'继续'生成文章框架"`

---

## Step 4.0 — Framework Generation → User Confirm → LOCK

**Goal:** Generate article outline; user modifies; LOCK before writing.

### Heading Rules
- **Level 1 headings** = Core conclusion statements (NOT descriptive labels)
  - ✅ "Mitochondrial ROS Activates NLRP3 Inflammasome in Cisplatin Nephrotoxicity"
  - ❌ "Oxidative Stress and Nephrotoxicity"
- **Level 2 headings** = Sub-conclusions
- Under each heading: outline 3-5 key argument points with reference numbers
- Mark figure/table positions: `[Figure 1 near here]`
- Embed planned reference numbers: `[1,3,7]`

### Interactive Loop
1. Claude outputs draft framework
2. User reviews → can modify headings, reorder, add/remove sections
3. Claude updates
4. User types **"LOCK"** → framework frozen
5. No structural changes after lock

**Output:** `pipeline_output/03_framework.md`

**Self-check:**
- [ ] All headings are conclusion statements
- [ ] Logical chain: each section flows into the next
- [ ] Figure/table positions marked
- [ ] Framework **LOCKED** by explicit user confirmation

**→ Next:** `"框架已锁定。请回复'继续'开始逐节写作"`

---

## Step 4.5 — Cross-Section Consistency Check

**Goal:** (Runs after ALL sections are written, before final assembly.) Verify logical continuity across sections.

### Check Items
1. Section-to-section transitions: does each conclusion lead to the next opening?
2. Terminology consistency: same term used throughout?
3. Logical gaps: any unexplained jumps between topics?
4. Redundancy: content repeated across sections?
5. Sequential figure/table numbering

Report issues → user decides: fix / accept as-is.

**Output:** `pipeline_output/04.5_cross_section_check.md`

---

## Step 5.0 — Section-by-Section Writing

**Goal:** Write each section independently, save to separate file.

### Per-Section Workflow
1. Claude reads relevant Obsidian notes for this section's topic
2. Write section following locked framework
3. Present to user
4. User: accept / request modifications / request rewrite
5. Save to `pipeline_output/04_draft_section_NN_title.md`

### Writing Rules
- Every claim evidence-anchored → reference a verified paper `[N]`
- Critical evaluation mandatory: strengths AND limitations of cited studies
- Synthesize across studies — never "Author A found X. Author B found Y. Author C found Z."
- Mechanism description: step-by-step pathway logic, cite original discovery
- **Reverse-outline self-check** after each section: extract one sentence per paragraph → verify logical chain is continuous

### Citation Format
`[N]` before period: `...as demonstrated in multiple models [1,3,5].`

**Output:** `pipeline_output/04_draft_section_*.md` (one per section)

**→ Next (between sections):** `"第X节已确认。请回复'继续'撰写下一节"`

**→ Next (all sections done):** `"所有章节完成。请回复'继续'进行跨节一致性检查"`

---

## Step 6.0 — Conclusion

**Structure (350-500 words):**
- 3-5 sentence synthesis of core message (NOT a summary list)
- What has been resolved
- What remains unresolved (1-2 most urgent)
- Key bottlenecks (technical? model? translational gap?)
- Limitations of this review
- Future directions with brief solution pathways

**Self-check:**
- [ ] Does NOT repeat main text verbatim
- [ ] All required elements present
- [ ] Speculative claims clearly marked

**Output:** `pipeline_output/05_conclusion.md`

**→ Next:** `"结论完成。请回复'继续'生成图表指令"`

---

## Step 7.0 — Figure Instructions + Legends

**Goal:** Output detailed drawing instructions for each figure, designed to be handed to a separate AI drawing tool or human illustrator.

### Per-Figure Output
1. **Figure number + insertion location** (matches framework markers)
2. **Core meaning** — what this figure must convey (1 sentence)
3. **Elements to include** — complete checklist
4. **Visual hierarchy** — primary emphasis / secondary / background
5. **Logical flow** — left→right and/or top→bottom direction
6. **Color guidance** — color-blind safe palette; confirm visible in grayscale
7. **Figure legend** — **One-sentence core conclusion** (NOT descriptive)
8. **Abbreviations used in this figure**

Follow the detailed template in [figure-template.md](figure-template.md).

**Figure quality principles (Dhillon 2022 Box 1):**
- Keep content relatively simple
- Use arrows and numbers for multi-stage processes
- Labels and scale bars as needed
- Consistent font within/across figures
- Leave ample white space — don't cram

**Output:** `pipeline_output/06_figure_instructions.md`

**Self-check:**
- [ ] Each legend is a core conclusion, not a description
- [ ] Abbreviations complete per figure
- [ ] Color-blind safe + grayscale compatible
- [ ] Figure count matches Step 1.0 parameter

**→ Next:** `"图指令完成。请回复'继续'生成表格"`

---

## Step 8.0 — Summary Tables

**Goal:** Create synthesis-level tables with traceable citations.

### Rules
- **Synthesis, not data dump** — each row is an integrated finding
- **Every row/section → reference [N]** — traceable to verified literature
- **Reference numbers match** in-text and final reference list
- Suggested columns: `Topic | Key Evidence | References | Gaps/Controversies`

Follow [table-template.md](table-template.md).

**Output:** `pipeline_output/07_tables.md`

**Self-check:**
- [ ] All [N] traceable to verified references
- [ ] Table count matches Step 1.0 parameter
- [ ] Each row is synthesis-level, not raw data enumeration

**→ Next:** `"表格完成。请回复'继续'进行参考文献组装"`

---

## Step 9.0 — Reference Assembly + Cross-Verification

**Goal:** Build final reference list; verify 100% traceability.

### 9.1 Reference Mode

Ask user:
> "Auto-insert references in Vancouver format, or will you insert manually?"

- **Auto**: "Provide target journal reference format, or use default Vancouver?" → Format accordingly
- **Manual**: "In-text citations use [N] format. Ensure your reference manager matches numbering."

### 9.2 Cross-Verification

| Check | Method |
|-------|--------|
| Every in-text [N] → in reference list | Scan all `04_draft_section_*.md` for `[N]` patterns; match against list |
| Every reference list entry → cited ≥1 time | Reverse scan |
| Every reference → verified in Step 3 | Cross-check against `02_literature_notes.md` |
| PMID/DOI match | Verify against `01_reference_list.md` |

Vancouver format guide: [vancouver-guide.md](vancouver-guide.md).

**Output:** `pipeline_output/08_references_final.md`

**Self-check:**
- [ ] 100% citation traceability (every [N] has a reference, every reference is cited)
- [ ] Zero unmatched references
- [ ] Zero unverified references in final list
- [ ] PMID/DOI cross-checked

**→ Next:** `"参考文献验证完成。请回复'继续'生成最终输出"`

---

## Step 10.0 — Final Assembly + Abbreviations Table + Output

**Goal:** Compile everything; generate abbreviations table; deliver final manuscript.

### 10.1 Assemble Manuscript
Merge: all `04_draft_section_*.md` + `05_conclusion.md` → single document with figure instructions, tables, references.

### 10.2 Generate Abbreviations Table
```
| Abbreviation | Full Term | First Appearance |
|-------------|-----------|-----------------|
```
Scan full text for all abbreviations → compile table sorted alphabetically.

### 10.3 Output
1. Save `pipeline_output/09_final_manuscript.txt`
2. Ask: **"Need Word (.docx) version?"**
   - Yes → Generate `pipeline_output/09_final_manuscript.docx` using `docx` skill
   - No → txt only

### 10.4 Final Acceptance Checklist

Run the full checklist from [quality-checklist.md](quality-checklist.md):

```
[ ] All citations from user-provided, verified literature — ZERO fabricated
[ ] All framework headings are conclusion statements (not descriptive labels)
[ ] Conclusion includes: limitations + outlook + resolved + unresolved + solution pathways
[ ] Evidence-based reasoning throughout; never overconfident or dogmatic
[ ] "Laundry list" style absent — critical synthesis present in every section
[ ] Figure instructions complete (meaning, elements, hierarchy, legend, abbreviations per figure)
[ ] Tables are synthesis-level with traceable [N] citations
[ ] Abbreviations table complete and accurate
[ ] In-text [N] numbering consistent with reference list — 100% match
[ ] All user confirmation gates passed (check Step 0.0 through Step 9.0)
[ ] Word count within user-specified limit
[ ] Figure count within user-specified limit
[ ] Table count within user-specified limit
```

### 10.5 Deliver
- Present each output file path
- Log all checks to `pipeline_output/10_selfcheck_log.md`

**Output:** `pipeline_output/09_final_manuscript.txt` + (optional) `.docx` + `pipeline_output/10_selfcheck_log.md` + `obsidian_vault/`

**→ Next:** `"全部完成！如需修改，请说明具体步骤编号（如'回到Step 4修改框架'）。"`

---

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Skipping scope checklist (Step 1.0) | Mandatory gate — topic not validated = stop |
| Writing before framework locked (Step 4.0) | No writing until user types "LOCK" |
| "Laundry list" style in sections | Each paragraph must synthesize ≥2 studies and include critical evaluation |
| Overconfident language | Flag "clearly demonstrates"/"undoubtedly"/"proves" → replace with "suggests"/"indicates"/"supports" |
| Citing a review instead of the original paper | Trace back to original research article |
| Reference [N] mismatch between text and list | Cross-verify in Step 9.0 |
| Figure legend is a description, not a conclusion | Rewrite as one-sentence core finding |
| Forgetting abbreviations table | Step 10.0 auto-generates this |
| Loading all PDFs into context at once | Use Obsidian vault → read `_MOC_*.md` → only specific `papers/NNN*.md` as needed |

## Red Flags — STOP and Fix

- Unsure if a reference is real → re-verify in Step 3.0
- Framework heading is a label, not a conclusion → rewrite before LOCK
- Section reads like "Author A found X. Author B found Y." → restructure as synthesis
- Using search-engine results without PubMed verification → return to Step 2.0
- References cited in text but missing from final list → return to Step 9.0

**Any of these mean: pause, fix the issue, re-verify before proceeding.**

## Quick Reference

| Step | Output File | Key Action |
|------|------------|------------|
| 0.0 | (screen only) | NR vs SR intro |
| 0.5 | `00_preflight_check.md` | Scan dependency skills |
| 1.0 | `00_project_config.md` | Word/fig/table limits + scope |
| 2.0 | `01_search_strategy.md` + `01_reference_list.md` | PubMed search + PMID list |
| 3.0 | `02_literature_notes.md` | PDF verify + notes + conflicts |
| 3.5 | `obsidian_vault/` | Knowledge graph |
| 4.0 | `03_framework.md` | Outline → user LOCK |
| 4.5 | `04.5_cross_section_check.md` | Logic consistency |
| 5.0 | `04_draft_section_*.md` | Section writing |
| 6.0 | `05_conclusion.md` | Limitations + outlook |
| 7.0 | `06_figure_instructions.md` | Drawing instructions |
| 8.0 | `07_tables.md` | Synthesis tables |
| 9.0 | `08_references_final.md` | Vancouver + cross-verify |
| 10.0 | `09_final_manuscript.txt/.docx` + `10_selfcheck_log.md` | Final output + QA |
