---
name: narrative-review
description: Use when writing an English narrative review article in clinical pharmacology or basic pharmacological mechanism research. Covers full workflow from language selection through final manuscript assembly. NOT for systematic reviews or meta-analyses.
---

# Narrative Review Writing [REVISED v2.1]

## Overview [UPDATED]

Guides the complete workflow for writing an English narrative review article in clinical pharmacology and basic pharmacological mechanism research. Grounded in best practices from Dhillon (2022), Chaney (2021), Pautasso (2013), Gasparyan (2011), and others.

Core principle: Zero fabricated references. Every citation must trace to a user-provided, verified PDF. Every factual claim must reflect what the cited paper actually reports. No inference or extrapolation beyond the source is permitted.

This is revision v2.1, incorporating 40 user requirements, 8 architectural design fixes, and 20 post-analysis consistency fixes.

---

## Dual-Track Architecture [UPDATED]

1. Pipeline Output (pipeline_output/) - File-per-step state management. Claude writes each step output to disk; the next step reads only what it needs. Enables interrupt/resume at any step.
2. Obsidian Vault (obsidian_vault/) - Knowledge graph for long-term research. Each paper becomes a structured note with YAML frontmatter and wikilinks.

Context efficiency rule (Obsidian reading path): During writing, Claude reads notes in this strict order only: _MOC_*.md, then relevant themes/*.md, then only the specific papers/NNN*.md notes needed for the current section. Do NOT load all paper notes simultaneously.

Resume protocol: If the session is interrupted, check pipeline_output/ for the most recently written file to determine the last completed step, then resume from that point.

---

## Multi-Agent Context Strategy [NEW]

The 1M context window fills quickly with 100+ PDFs, notes, writing, and verification. Mandatory triggers:

| Trigger | When | Action |
|---------|------|--------|
| PDF batch verification | Step 3.0, when N >= 35 and processed count reaches N/2 | Spawn one verification sub-agent per batch of 20-25 |
| Long section writing | Step 5.0, section > 800 words | Spawn a dedicated writing agent per major section |
| Reference QA | Step 9.0, when the target reference count N (from Step 1.0) is large enough that a single-pass QA risks missed errors: spawn a dedicated citation QA agent for Pass 3. Scale identically to the Step 3.1 dynamic protocol -- N < 35 verify all in one pass; N >= 35 delegate Pass 3 to a QA sub-agent | Spawn a dedicated citation QA agent |
| Second-pass review | Any step with complex output | Spawn a dedicated QA agent |

Each sub-agent writes output to pipeline_output/ files. The orchestrator coordinates, reads file outputs, and synthesizes results. Sub-agents receive only the files needed for their specific task.

---

## Batched Output Protocol [NEW]

Large outputs (literature notes, section drafts, reference lists, final assembly) must be written in batches to avoid hitting the platform output token limit mid-response.

### When to Apply
Apply batched output to any step where a single response would exceed the platform batch size recorded in Step 0.0b:
- Step 3.0: literature notes (one batch per 10-15 papers)
- Step 5.0: each section draft (split at natural paragraph breaks if >batch size)
- Step 5.5: consistency check report
- Step 9.0: final reference list (batches of 30-40 entries)
- Step 10.0: final assembly (split by manuscript section)

### Batch Format
When splitting output across multiple responses, use this format:

  [OUTPUT PART 1/3]
  ...content...
  [END PART 1 - type "continue" to receive Part 2/3]

Claude resumes on the next "continue" or equivalent user input. Each part must be complete and coherent -- never cut mid-sentence or mid-paragraph. Before the first batch, state the total number of parts.

### Platform-Specific Guidance
- DeepSeek (~384 token limit): every paragraph-level output may require a separate batch; output one or two paragraphs then pause
- Claude app (~8000 tokens): most individual sections fit in one response; split only long sections (>1500 words) or large reference lists (>50 entries)
- Claude terminal (~16000 tokens): split only when approaching the limit (>2500 words or >80 references per response)

### Writing to Disk
For outputs destined for pipeline_output/ files, write each batch to the file as it is produced (using append mode). Never wait until the entire output is ready before writing -- this risks losing work if the session is interrupted.

---

## When to Use

- English narrative/traditional literature review
- Clinical pharmacology, pharmacokinetics, pharmacodynamics, drug mechanisms
- Basic pharmacological mechanisms (signaling pathways, molecular targets, drug-receptor interactions)
- State-of-the-art or integrative reviews in biomedical sciences

NOT for: Systematic reviews (PRISMA), meta-analyses, scoping reviews, rapid reviews, umbrella reviews.

---

## Dependency Skills [UPDATED]

| Skill | Required | Purpose |
|-------|----------|---------|
| pdf | Yes | Read/verify PDF content (Step 3.0) |
| docx | Optional | Generate Word output (Step 10.0) |
| web-search or equivalent | Yes for assisted search | Execute database search (Step 2.0); if absent, user must search independently |

Missing required skill -> BLOCK. Missing optional -> WARN, allow degraded mode.

Note: Obsidian (desktop app, obsidian.md) is recommended but not required. Without it, vault notes remain usable as plain markdown files. The knowledge graph view (Step 3.5 second-pass QA) requires Obsidian to be installed.

---

## Core Rules [UPDATED]

### Anti-Hallucination
1. ALL cited literature MUST come from user-provided downloaded PDFs
2. Every PMID/DOI MUST be verified against actual PDF content
3. Database search only - never use search-engine-only results (Google, Bing, etc.)
4. Three-pass verification: Step 3.0 (content) + Step 5.0 (per-citation check during writing) + Step 9.0 (final list cross-verification)
5. One fabricated reference = restart verification from Step 3.0
6. Citation QA agent: scale with the target reference count N (Step 1.0), matching the Step 3.1 dynamic protocol -- if N < 35, run Pass 3 in a single pass; if N >= 35, delegate final citation QA (Step 9 Pass 3) to a dedicated sub-agent. Do not hard-code a fixed threshold.
7. Unverifiable references are EXCLUDED, not retained with a warning
8. Dynamic batch verification: the trigger and audit intensity scale with the target reference count N (set in Step 1.0). Full protocol is defined in Step 3.1. Summary: if N < 35, verify every paper individually; if N >= 35, batch in groups of 20-25 and audit >= 50% per batch starting when processed count reaches N/2.

### Writing Quality
- New insights required - not a book report (Chaney 2021)
- No laundry list - synthesize across studies, do not enumerate (Dhillon 2022)
- Be balanced - discuss conflicting findings; do not ignore opposing evidence (Dhillon 2022)
- Cite original research - not reviews of reviews; for concept-level citations, prefer the original discovery paper and high-impact journals (Nature, Science, Cell, NEJM, Lancet, JAMA, Nature Medicine) over secondary reviews
- Critical evaluation - strengths, weaknesses, and contradictions of every key cited study (Pautasso 2013)
- Tone: evidence-based, appropriately cautious, never overconfident; use suggests, indicates, supports rather than proves, clearly demonstrates, undoubtedly
- ALL factual claims must be traceable to a user-provided verified PDF. Claude may not infer, extrapolate, or synthesize claims beyond what the paper explicitly reports. If a logical connection is the author synthesis and not stated in any paper, mark it explicitly: (author synthesis)

### Gene and Protein Nomenclature [NEW]
- Human gene symbols: ALL CAPS, italics - e.g., TP53, BRCA1, NFE2L2 (verify: HGNC / GeneCards)
- Mouse/rat gene symbols: First letter capitalized, rest lowercase, italics - e.g., Tp53, Brca1 (verify: MGI / GeneCards)
- Human protein symbols: ALL CAPS, non-italic - e.g., TP53, NRF2 (verify: UniProt)
- Mouse/rat protein symbols: First letter capitalized, rest lowercase, non-italic - e.g., Tp53, Nrf2 (verify: UniProt)
- When uncertain, verify the official symbol before writing; do not guess

### Language and Style Rules [NEW]
- Minimize question marks and em-dashes; use declarative sentences throughout
- Adhere to pharmacology and pharmaceutical academic writing norms
- When citing an author in prose, use only the first author surname followed by the citation number: Smith [1] demonstrated that... Do NOT use and colleagues, et al., or and co-workers in running prose
- BANNED expressions: paradigm, paradigm shift, profound, it is worth noting, it is well-established that (without a specific citation), a growing body of evidence, shedding light on, recent advances, holds great promise, landscape of, comprehensive overview
- BANNED symbols in body text: directional arrows - describe direction in words instead. Arrows are permitted only in figure drawing instructions (Step 7.0).
- Before delivering any section draft, scan for and remove AI-characteristic language
- All vocabulary and phrasing must be grounded in the provided PDF literature; do not invent descriptions not present in the sources

### Abbreviation Rules [NEW]
- Abbreviate a term only if it appears MORE THAN 3 times in the full text
- Exception: established proper-noun abbreviations (ATP, DNA, mRNA, NF-kB, NLRP3, etc.) are always used regardless of frequency
- First use in body text: full term followed by abbreviation in parentheses - e.g., nuclear factor-kappa B (NF-kB)
- Do NOT introduce new abbreviations in the Abstract unless also defined in the body text

### Citation Rules [NEW]
- Each reference should be cited at ideally ONE location in body text - the most relevant sentence
- One sentence (or sentence pair) maps to one or a group of references; avoid citing the same reference across multiple unrelated sentences in different paragraphs
- Exception 1: Key foundational papers may appear once in the Introduction and once in a later section if both instances are essential
- Exception 2: Table citations are exempt - a reference may appear in a table AND in body text without counting as a repeat
- Reference numbering follows strictly the order of first appearance in body text (Introduction first). Tables do not affect the numbering order.
- For concept-level citations, prefer the original discovery paper or a high-impact journal source over a secondary review
- The claim made in body text must accurately represent what the cited paper actually reports; do not overstate, generalize, or misattribute findings

### Format
- In-text citation: [N] immediately before the sentence period - e.g., ...as demonstrated in multiple models [1,3,5].
- Default reference style: Vancouver (locked in Step 1.0; can be changed to AMA, APA, or journal-specific format)
- Section heading numbering: Level 1 = 1., 2., 3.; Level 2 = 1.1., 1.2.; Level 3 = 1.1.1. etc.
- Word (.docx) formatting: Times New Roman throughout; body text 10 pt; section headings 12 pt; line spacing 1.5x; paragraph spacing before and after 0 pt; align paragraphs in justify.

---

## Workflow [UPDATED]

Step 0.0  -> Language Selection                                    [NEW]
Step 0.0b -> Model and Platform Selection                          [NEW]
Step 0.1  -> Introduction: NR vs SR                               [was 0.0]
Step 0.5  -> Pre-flight Environment Check                         [UPDATED]
Step 0.9  -> Title Confirmation                                   [NEW]
Step 1.0  -> Project Parameters + Scope Definition               [UPDATED]
Step 2.0  -> Search Strategy + Reference List                    [UPDATED]
Step 3.0  -> Literature Verification + Notes + Conflict Matrix   [UPDATED]
Step 3.5  -> Obsidian Vault Generation                           [UPDATED]
Step 4.0  -> Framework -> User Confirm -> LOCK                   [UPDATED]
Step 5.0  -> Section-by-Section Writing                          [UPDATED]
Step 5.5  -> Cross-Section Consistency Check                     [was 4.5, RENAMED]
Step 6.0  -> Conclusion                                          [UPDATED]
Step 6.5  -> Abstract                                            [NEW]
Step 6.6  -> Keywords                                            [NEW]
Step 7.0  -> Figure Instructions + Legends                       [UPDATED]
Step 8.0  -> Summary Tables                                      [UPDATED]
Step 9.0  -> Reference Assembly + Cross-Verification             [UPDATED]
Step 10.0 -> Final Assembly + Output                             [UPDATED]

---

## Step 0.0 - Language Selection [NEW]

Goal: Establish the interaction language for the entire workflow.

Ask the user:

  This workflow supports two interaction languages. Please choose one:
  A) Chinese (all prompts, questions, and step instructions will be in Chinese)
  B) English (all prompts, questions, and step instructions will be in English)

Lock the choice. All subsequent step instructions, questions to the user, and continue prompts will be delivered in the chosen language. The manuscript itself is always written in English regardless of the interaction language chosen.

Output: Record language choice in pipeline_output/00_language.md

### Run Log Creation [MOVED HERE from Step 0.5]
Create the session run log at the very start of the workflow, before any other steps run:
- Path: pipeline_output/run_log.md
- Record on creation:
  - Skill name and version: narrative-review v2.1
  - Run start date and time
  - Interaction language (choice made in this step)
  - Working directory (if already known; otherwise update in Step 1.0)
- Format for all subsequent entries (append at the end of EVERY step without exception -- this rule is global and applies to all 19 steps; no per-step reminder will be repeated):
    [STEP X.X - StepName] YYYY-MM-DD HH:MM
    User input: [summary of what the user provided or decided]
    Actions taken: [what Claude did]
    Output file(s): [file paths written]
    Notes: [any interruptions, modifications, or issues]
- If the session is interrupted and resumed, add:
    [SESSION RESUME] YYYY-MM-DD HH:MM
    Resumed from: Step X.X

Output: pipeline_output/run_log.md (created here; appended at every subsequent step)

Self-check:
- [ ] Language choice confirmed
- [ ] run_log.md created and initial entry written

Second-pass QA: Re-read the choice and confirm it is recorded in 00_language.md before proceeding.

Next: Proceed to Step 0.0b

---

## Step 0.0b - Model and Platform Selection [NEW]

Goal: Record which AI model and platform is being used. This determines the batched output batch size for all large-output steps throughout the workflow.

Ask the user:
  Which model and platform are you running this workflow on?
  (A) Claude terminal (claude-cli / Kiro CLI)
  (B) Claude app (claude.ai web or desktop)
  (C) DeepSeek (API or web app)
  (D) Other (specify model name and approximate max output token limit)

Output token limits and batch sizes by platform:
| Platform | Approx. Max Output Tokens | Recommended Batch Size |
|----------|--------------------------|------------------------|
| Claude terminal | ~8000-16000 | ~2000-3000 words per output |
| Claude app | ~8000 | ~1500-2000 words per output |
| DeepSeek | ~384 tokens | ~200-250 words per output |
| Other | User-specified | Scale proportionally |

Record the chosen platform and batch size in pipeline_output/00_project_config.md.
All steps that produce large outputs (Steps 3.0, 5.0, 5.5, 9.0, 10.0) will use this batch size.
See the Batched Output Protocol section for implementation details.

Output: Recorded in pipeline_output/00_project_config.md

Self-check:
- [ ] Platform confirmed and recorded
- [ ] Batch size calculated and recorded

Second-pass QA: Re-read 00_project_config.md and confirm the platform name and batch size are correctly recorded before proceeding.

Next: Proceed to Step 0.1

---

## Step 0.1 - Introduction: NR vs SR [was Step 0.0]

Goal: Ensure the user understands what a narrative review is and is not.

Display the comparison from nr-vs-sr.md.

Declare: This skill writes narrative reviews only. If you need a systematic review with PRISMA methodology, use a different workflow.

Self-check:
- [ ] User acknowledged NR vs SR distinction
- [ ] User confirmed they want a narrative review

Output: (none -- screen display only)

Second-pass QA: Confirm explicit acknowledgment before advancing.

Next: Proceed to Step 0.5

---

## Step 0.5 - Pre-flight Environment Check [UPDATED]

Goal: Verify all required skills and network access are available before any work begins.

Follow the scan logic in preflight-check.md, extended with the additions below.

### Skills to Check

| Skill | Required | Check | Purpose |
|-------|----------|-------|---------|
| pdf | Yes | ~/.claude/skills/pdf/ exists | PDF verification (Step 3.0) |
| docx | Optional | ~/.claude/skills/docx/ exists | Word output (Step 10.0) |
| web-search or equivalent | Required for assisted search | Attempt a test search call | Database search (Step 2.0) |

### Network Connectivity Check
Before any database search in Step 2.0, confirm network access is available:
- Attempt a minimal ping or test query to the target database
- If connectivity fails: warn the user and switch to manual search mode
- Record the result in 00_preflight_check.md

### Outcomes
- All required present -> PASS, continue
- Required skill missing -> BLOCK, tell user what to install
- Recommended skill missing -> WARN, allow degraded-mode continue
- Network unavailable -> WARN, note that Step 2.0 will use manual search mode

Output: pipeline_output/00_preflight_check.md

Self-check:
- [ ] Required skills scan complete
- [ ] Network connectivity verified (or manual mode flagged)
- [ ] Any missing skills flagged with install instructions

### Run Log Update [was: Run Log Initialization -- log is now created in Step 0.0]
At this step, append retroactive entries for Steps 0.0, 0.0b, 0.1, and 0.5 since those steps ran before the first natural log checkpoint. Then continue appending normally from Step 0.9 onward.

Output: pipeline_output/00_preflight_check.md + update pipeline_output/run_log.md

Second-pass QA: Re-read 00_preflight_check.md and verify all items are present before continuing.

Next: Proceed to Step 0.9

---

## Step 0.9 - Title Confirmation [NEW]

Goal: Lock the manuscript title before any parameter collection.

### 0.9.1 Title Proposal
Based on the topic provided by the user (or from Step 0.1 discussion), propose a working title following best practices:
- Specific and informative: states the drug/class, the mechanism, and the population or context
- Not too broad (avoid: A Review of Drug X) and not too narrow
- Appropriate for a narrative review (avoid implying systematic methodology)

Present the proposed title to the user for confirmation or revision.

### 0.9.2 Lock
User confirms -> Title locked. Save to pipeline_output/00_project_config.md

### 0.9.3 Post-writing Revision Option
After Step 10.0 is complete, offer a second-pass title revision:
  Now that the full manuscript is complete, would you like to revise the title to better reflect the actual content and conclusions?

Output: Title recorded in pipeline_output/00_project_config.md

Self-check:
- [ ] Title proposed based on scope discussion
- [ ] User confirmed or revised the title
- [ ] Title locked and saved

Second-pass QA: Confirm the title is saved in 00_project_config.md before continuing.

Next: Proceed to Step 1.0

---

## Step 1.0 - Project Parameters + Scope Definition [UPDATED]

Goal: Lock all project constraints and validate topic viability before searching begins.

### 1.1 Path Explanation (for non-technical users)
Before asking for the working directory, explain:

  A file path is the full address of a folder on your computer.
  Windows example: C:/Users/YourName/Documents/MyReview
  How to find it: open the folder in File Explorer, click the address bar at the top, copy the full text.
  Tip: forward slashes (/) work fine on Windows.

### 1.2 Collect Parameters

For each parameter, ask the user and show the default answer template:

Parameter 1 - Working directory
  Question: Please provide the full folder path where all output files will be saved.
  Default: C:/Users/YourName/Documents/MyReview

Parameter 2 - Word limit
  Question: Total word count target for the manuscript?
  Recommendation: 4000-6000 words (Dhillon 2022)
  Default: 5000 words

Parameter 3 - Figure count
  Question: How many figures are planned?
  Default: 3

Parameter 4 - Table count
  Question: How many tables are planned?
  Default: 2

Parameter 5 - Reference count
  Question: How many references are targeted for this review?
  Default: 100

Parameter 6 - Reference format
  Question: Which reference format should be used?
  Options: Vancouver (default), AMA, APA, journal-specific (provide author guidelines URL)
  Default: Vancouver

Parameter 7 - Target journal
  Question: Which journal is the submission target? Please provide the journal name.

Auto-calculate per-section word budget based on total word limit and the number of planned sections.

### 1.3 Journal and Special Issue Check
Based on the target journal provided:
1. Search for whether the journal currently has a relevant open Special Issue
2. Report: journal name, any open Special Issue title and submission deadline, scope requirements
3. Add mandatory requirement: the final reference list must include at least 5 papers published in the target journal
4. Save all journal information to 00_project_config.md

### 1.4 Reference Format Lock
- Vancouver (default): formatting rules are defined in the internal skill file vancouver-guide.md (located in the same narrative-review skills directory). Reference that file directly -- do not rely on any external file path. The NLM Citing Medicine guide (Citing Medicine-The NLM Style Guide for Authors, Editors, and Publishers) is the authoritative source for entry-type conventions; consult it when the internal guide does not cover a specific entry type.
- AMA, APA, or journal-specific: ask for the journal author instructions URL or a sample reference in the target format
- Lock the format. It cannot be changed after Step 4.0 is locked.

Note: File paths containing spaces should be quoted when used in command-line contexts.

### 1.5 Scope Assessment

Run the 6-factor checklist from scope-checklist.md:
1. Personal motivation - Is the author genuinely interested in this topic?
2. Timeliness - Are there >= 15 relevant papers published in the past 5 years?
3. Novelty - Has a similar review appeared in the past 1-2 years? What new perspective does this review offer?
4. Breadth - Is the topic focused enough to be manageable yet broad enough to attract readership?
5. Journal relevance - Does the topic fit the target journal scope?
6. Author expertise - Is the team adequately knowledgeable for this topic?

Rate each factor 1-5. Flag any score <= 2 for discussion before proceeding.

Output: pipeline_output/00_project_config.md

Self-check:
- [ ] All 7 parameters recorded
- [ ] Journal special issue searched and result recorded
- [ ] Self-citation requirement (>= 5 papers from target journal) documented
- [ ] Working path confirmed writable
- [ ] Per-section word budget calculated
- [ ] All 6 scope factors rated; any score <= 2 flagged and discussed

Second-pass QA: Re-read 00_project_config.md and verify every parameter is present before advancing.

Next: Proceed to Step 2.0

---

## Step 2.0 - Search Strategy + Reference List [UPDATED]

Goal: Build a reproducible search strategy, confirm platforms and date range, and output a structured reference list.

### 2.1 Confirm Search Platforms
Ask the user:
  Which database(s) should be searched? Select all that apply.
  Default: PubMed
  Options: (A) PubMed  (B) Web of Science (WOS)  (C) ScienceDirect  (D) Wiley Online Library  (E) Embase  (F) Other (specify)

Record selected platforms. Each selected platform will be searched with the same strategy. Results are combined and deduplicated.

### 2.2 Confirm Publication Year Range
Ask the user:
  What is the publication year range?
  Recommendation: the past 10 years, or specify a custom range for topic-specific historical depth
  Default template: 2015 to 2026

### 2.3 Article Type Filter
Permitted article types for citation in a narrative review:
- Original research articles and original investigations
- Review articles (narrative, systematic, meta-analysis)
- Clinical trial reports (RCT, phase I/II/III)
- Letters containing substantive original data

EXCLUDED - these article types must NOT appear in the final reference list:
- Preprints (bioRxiv, medRxiv, SSRN, ResearchSquare, ChemRxiv, etc.)
- Conference abstracts and conference proceedings
- Editorials and opinion pieces without data
- Book chapters (unless no primary source is available for a key concept)

Apply these filters in the database search interface. Document which filters were applied.

### 2.4 Network and Tool Confirmation
Before executing the search:
1. Confirm network connectivity is available (from Step 0.5 result)
2. State explicitly which tool will execute the search (e.g., web-search skill, browser tool). Available tools depend on the platform selected in Step 0.0b.
3. If no tool is available or network is unavailable: output the search strategy only; user executes independently

### 2.5 Build Search Strategy
Based on the title and keywords from Step 1.0:
1. Extract core concepts -> MeSH terms + free-text synonyms
2. Combine with Boolean operators (AND, OR, NOT)
3. Apply the confirmed year range and article type filters
4. Build a separate query string for each selected database (syntax differs across platforms)
5. Confirm the strategy is fully reproducible

Follow search-strategy.md for detailed construction guidance.

### 2.6 Execute or Delegate
Ask: Do you need assisted searching?
- Yes -> Execute the search using the confirmed tool; output structured results
- No -> Output the search strategy for the user to execute independently

### 2.7 Output Reference List
Format:
| # | PMID | DOI | Title | First Author | Year | Journal | File Name |
|---|------|-----|-------|--------------|------|---------|-----------|
| 1 | 12345678 | 10.xxxx/xxxx | Title text | Smith A | 2024 | Journal Name | 001_Smith2024_Keyword.pdf |

Naming convention for downloaded PDFs: NNN_AuthorYear_Keyword.pdf (e.g., 001_Smith2023_NLRP3.pdf)

Verify the list includes at least 5 papers from the target journal.

### 2.8 Full Search Reproducibility Record [NEW]
The search strategy output file (01_search_strategy.md) must include ALL of the following for full reproducibility:

1. Search execution date: exact date (YYYY-MM-DD) when each database was searched
2. Literature time range: the publication year range applied (e.g., January 2015 to December 2026)
3. Database and version: name of each database searched and the access date
4. Complete query strings: the exact Boolean query submitted to each database, verbatim
5. Filter settings applied: article types included/excluded, language filters, species filters
6. MeSH term expansion details: which MeSH terms were used and any MeSH explosions applied
7. Search result counts: number of results before and after deduplication for each database
8. Inclusion/exclusion rationale: brief explanation of any manual exclusions after initial retrieval
9. Total records: final count of records included in 01_reference_list.md

This record allows any researcher to independently replicate the search.

Output: pipeline_output/01_search_strategy.md + pipeline_output/01_reference_list.md

Self-check:
- [ ] Search platforms confirmed and documented
- [ ] Year range confirmed
- [ ] Article type filters applied; preprints and conference papers explicitly excluded
- [ ] Search strategy is reproducible
- [ ] Every entry has PMID + DOI where available
- [ ] Naming convention documented
- [ ] At least 5 papers from the target journal included
- [ ] Reference count on track to meet target set in Step 1.0
- [ ] Full reproducibility record (Step 2.8) includes: search execution date, database versions, complete query strings, result counts, inclusion/exclusion rationale
- [ ] Search execution date recorded in 01_search_strategy.md
- [ ] Database access dates recorded
- [ ] Complete Boolean query strings saved verbatim for each database
- [ ] Result counts before and after deduplication recorded for each database

Second-pass QA: Re-read 01_reference_list.md. Verify PMID/DOI coverage and target journal self-citation count.

Next: After downloading and renaming all PDFs, provide the folder path and proceed to Step 3.0

---

## Step 3.0 - Literature Verification + Reading Notes [UPDATED]

Goal: Verify every reference is real; extract structured findings; identify contradictions; prepare for knowledge graph construction.

Note: For large outputs (when note count exceeds platform batch size from Step 0.0b), apply the Batched Output Protocol.

### 3.1 Dynamic Batch Verification Protocol [UPDATED]

At the start of Step 3.0, read the target reference count N from 00_project_config.md and compute the following parameters. State these values explicitly before beginning verification:

  Target N      = [value from 00_project_config.md]
  Mode          = [Individual / Batch -- see rule below]
  Batch trigger = N / 2 = [X papers -- the count at which batch protocol activates]
  Batch size    = 20-25 papers per batch
  Audit per batch = ceil(batch_size * 0.5) papers [at least 50% per batch, rounded up]
  Estimated batches = ceil(N / 22)

Rules:
- If N < 35: Individual mode. Verify every single paper one by one. No batching; 100% coverage.
- If N >= 35: Batch mode. Begin batch protocol once the processed count reaches N/2 (50% of target).
  Each batch contains 20-25 papers.
  Within each batch, re-open and re-verify at least ceil(batch_size * 0.5) randomly selected entries.
    Example: N = 100, trigger = 50, batch of 22 papers -> audit at least 11 papers per batch.
    Example: N = 60, trigger = 30, batch of 20 papers -> audit at least 10 papers per batch.
  After each batch completes, run a hallucination check: confirm re-verified entries match 01_reference_list.md.

Once the processed count reaches N/2, spawn a dedicated verification sub-agent for all subsequent batches (see Multi-Agent Context Strategy).

### 3.2 Verify Each PDF
For every PDF file:
1. Open with the pdf skill - extract: title, first author, PMID, DOI, journal, year
2. Cross-validate all extracted fields against 01_reference_list.md
3. Assign verification status:
   - Verified: all fields match
   - Discrepancy: at least one field differs from the reference list (describe the discrepancy)
   - Cannot verify: PDF is inaccessible, corrupted, password-protected, or content is unreadable

### 3.3 Protocol for Unverifiable or Discrepant PDFs [NEW]
- Cannot verify: EXCLUDE from reference list. This paper may NOT be cited anywhere in the manuscript.
- Discrepancy: flag for user review. Only include after explicit user confirmation.
- If verification rate falls below 90%: return to Step 2.0 to find replacement papers before proceeding.
- Document all excluded papers with reason in 02_literature_notes.md.

### 3.4 Extract Structured Notes
For each verified paper, record:
- Core findings (3-5 bullet points reflecting the paper actual conclusions)
- Methodology (model system, technique, sample size, key reagents or tools)
- Key mechanisms and pathways (specific molecules, interactions, direction of effect)
- Strengths (large sample size, rigorous controls, multiple experimental models)
- Limitations (small n, single model, lack of controls, potential conflict of interest)
- Relevance to this review (which section or framework heading this paper supports)

### 3.5 Conflict Evidence Matrix
When >= 2 papers disagree on a mechanism or conclusion, populate:

| Issue | Supporting [N] | Opposing [N] | Possible Explanation | This Review Position |
|-------|----------------|--------------|---------------------|---------------------|
| [describe conflict] | [ref numbers] | [ref numbers] | [methodological, model, or dosing differences] | [which interpretation is adopted and why] |

### 3.6 Top-Journal and Original Source Check
For each concept-level finding in the notes, flag whether:
- The source is the original discovery paper or a top-impact journal (Nature, Science, Cell, NEJM, Lancet, JAMA, Nature Medicine)
- The source is a secondary review or textbook

Prefer original sources for concept-level citations in Step 5.0. Note this preference in the structured notes.

Output: pipeline_output/02_literature_notes.md

Self-check:
- [ ] Verification rate >= 95% (if < 95% flag for discussion before proceeding; if < 90% return to Step 2.0 to source replacement papers)
- [ ] Cannot-verify papers excluded and documented
- [ ] All conflict matrix rows populated where applicable
- [ ] Every paper has complete structured notes
- [ ] Top-journal and original source flags added

Second-pass QA: Re-read 02_literature_notes.md. Randomly spot-check 5 entries against their PDFs. Confirm exclusion list is accurate.

Next: Proceed to Step 3.5

---

## Step 3.5 - Obsidian Vault Generation [UPDATED]

Goal: Build a knowledge graph that enables context-efficient writing in Step 5.0.

### 3.5.1 Create Vault Structure

obsidian_vault/
  _MOC_Overview.md
  _MOC_Mechanisms.md
  _MOC_Clinical_Translation.md
  _MOC_Controversies.md
  _MOC_Figure_Ideas.md
  papers/
  themes/
  templates/

### 3.5.2 Generate Paper Notes
For each verified paper: create papers/NNN_AuthorYear_Keyword.md using the template in obsidian-templates.md.

### 3.5.3 Generate Theme Notes
Auto-identify high-frequency keywords and mechanisms across all papers. Create themes/ThemeName.md for each theme, aggregating relevant findings with wikilinks back to source papers.

### 3.5.4 Generate MOC Index Notes
Create Map of Content files that hierarchically organize all themes and papers by topic.

### 3.5.5 Vault Reading Path for Step 5.0 (critical)
When writing any section in Step 5.0, Claude reads the vault in this strict order:
1. Open _MOC_Overview.md - identify which themes are relevant to the current section
2. Read the relevant themes/ThemeName.md file(s)
3. Load only the specific papers/NNN_AuthorYear_Keyword.md notes that are relevant to this section
4. Do NOT load all paper notes simultaneously
5. Do NOT re-read the original PDFs during writing - use the vault notes

This reading path is the primary mechanism for staying within the context limit during long writing sessions.

Output: Complete obsidian_vault/

Self-check:
- [ ] Every verified paper has a note with complete YAML frontmatter
- [ ] All wikilinks resolve to existing notes
- [ ] MOCs cover all identified themes
- [ ] Vault reading path documented and understood for Step 5.0 use

Second-pass QA: Open vault in Obsidian (if available) and verify graph view shows connected nodes. Spot-check 3 paper notes against source PDFs.

Next: Proceed to Step 4.0

---

## Step 4.0 - Framework Generation -> User Confirm -> LOCK [UPDATED]

Goal: Generate article outline with numbered headings and per-section reference estimates; user reviews and locks.

### Heading Rules [UPDATED]
- Level 1 headings: Core conclusion statements, NOT descriptive labels. Use numbered format: 1., 2., 3.
  - Correct: 1. Mitochondrial ROS Activates NLRP3 Inflammasome in Cisplatin Nephrotoxicity
  - Incorrect: 1. Oxidative Stress and Nephrotoxicity
- Level 2 headings: Sub-conclusions, numbered: 1.1., 1.2., 1.3.
- Level 3 headings: Further sub-points, numbered: 1.1.1., 1.1.2.
- Under each heading: outline 3-5 key argument points with planned reference numbers
- Mark figure positions: [Figure 1 near here]
- Mark table positions: [Table 1 near here]
- Include per-section reference estimate: each heading must show the estimated number of references for that section

Note: The Introduction section has distinct structural requirements (see Step 5.0 Introduction Special Handling) and does not follow the conclusion-statement heading format. Create the Introduction framework entry accordingly.

### Per-Section Reference Budget [NEW]
Format each framework heading as:
  1. Section Title (est. ~15 refs)
    1.1. Sub-section title (est. ~6 refs)
    1.2. Sub-section title (est. ~9 refs)

The total of all per-section estimates must sum to approximately the target reference count from Step 1.0. Distribute references proportionally to section scope.

### Framework Must Include These Elements
- Introduction (with signposting paragraph)
- All main body sections with conclusion-statement headings
- Conclusion section
- Abstract (Step 6.5) - placeholder only at this stage
- Keywords (Step 6.6) - placeholder only at this stage
- Figure and table position markers
- A note on the minimum 5 target-journal self-citations distributed across sections

### Interactive Lock Loop
1. Claude outputs draft framework
2. User reviews: can modify headings, reorder sections, adjust reference estimates
3. Claude updates
4. User types LOCK -> framework frozen
5. No structural changes after LOCK

Output: pipeline_output/03_framework.md

Self-check:
- [ ] All headings are conclusion statements (not descriptive labels)
- [ ] All headings use numbered hierarchy (1., 1.1., etc.)
- [ ] Every section has a reference estimate; estimates sum to the target count
- [ ] Logical chain: each section flows into the next
- [ ] Figure and table positions marked
- [ ] Framework explicitly LOCKED by user confirmation

Second-pass QA: Re-read 03_framework.md after LOCK. Verify no heading is a bare topic label without a conclusion statement.

Next: Proceed to Step 5.0

---

## Step 5.0 - Section-by-Section Writing [UPDATED]

Goal: Write each section using vault notes, output with a Section Brief, save to separate files.

### Introduction - Special Handling [NEW]
The Introduction requires these specific elements:
1. Why this review is needed: identify the gap or controversy that motivates it
2. Scope boundaries: what is and is not covered
3. Signposting paragraph: brief overview of what each section covers
4. Do NOT include detailed findings in the Introduction - reserve all mechanism discussion for body sections
5. Suggested length: 300-500 words

### Obsidian Reading Path Before Each Section [UPDATED]
1. Open _MOC_Overview.md - identify which themes are relevant to this section
2. Read the relevant themes/ThemeName.md file(s)
3. Load only the specific papers/NNN_AuthorYear_Keyword.md notes for this section
4. Do NOT load all paper notes at once - context efficiency is critical
5. Begin writing only after loading section-specific notes

### Section Brief [NEW - required before each draft]
Before presenting the section draft, output this brief:

  Section Brief: [Section Title]
  Writing Logic: [Why this section appears here; how it connects to preceding and following sections]
  Core Argument: [Central claim this section establishes - 1 to 2 sentences]
  Evidence Basis: [Key papers with reference numbers [N] supporting the core argument]
  Word Budget: [Target word count from 00_project_config.md]

Save the Section Brief in the same pipeline_output file as the section draft.

### Per-Section Workflow
1. Follow the Obsidian reading path above
2. Output the Section Brief
3. Write the section following the locked framework
4. Check word count against the section budget
5. Present Section Brief and draft to user
6. User: accept / request modifications / request rewrite
7. Save to pipeline_output/04_draft_section_NN_title.md

### Writing Rules [UPDATED]
- Every claim must be evidence-anchored with a verified reference [N]
- Critical evaluation is mandatory: state strengths AND limitations of key cited studies
- Synthesize across studies - do not write Author A found X. Author B found Y. Author C found Z.
- For mechanism descriptions, trace the step-by-step pathway logic; cite the original discovery paper for each step
- Reverse-outline self-check: extract one sentence per paragraph; verify logical continuity
- Word count check: if >110% or <80% of budget, flag to user before proceeding to next section
- Logical redundancy check: confirm content is not repeated from a prior section
- Gene and protein symbols: apply nomenclature rules from Core Rules
- No directional arrows in prose; use words to describe direction
- No AI-characteristic language (scan and remove before delivering)

### Citation Discipline During Writing
- Each reference cited at ideally ONE location (the most relevant sentence in the most relevant section)
- Verify the specific claim in text matches the cited paper content before assigning [N]
- Prefer original discovery papers and high-impact journals for concept-level claims
- Do not cite a review as the sole source for a primary mechanistic claim
- In-text format: [N] immediately before the sentence period

Output: pipeline_output/04_draft_section_NN_title.md (one per section, includes Section Brief)

Self-check after each section:
- [ ] Section Brief written and saved
- [ ] All claims evidence-anchored
- [ ] Critical evaluation present for key studies
- [ ] No laundry-list style - synthesis across sources
- [ ] Word count within 80-110% of budget
- [ ] No content redundancy with prior sections
- [ ] AI-characteristic language removed
- [ ] No directional arrow symbols in prose
- [ ] Gene and protein naming conventions applied
- [ ] Each citation matches the specific claim in text

Second-pass QA per section: Re-read against the self-check list. Spot-check each [N] citation by reading the corresponding Obsidian note to confirm the claim is accurate.

Next (between sections): Confirm section acceptance and continue.
Next (after all sections): Proceed to Step 5.5

---

## Step 5.5 - Cross-Section Consistency Check [was Step 4.5, RENAMED]

NOTE: This step runs AFTER all body sections are written and BEFORE Step 6.0 Conclusion.

Goal: Verify logical continuity, terminology consistency, and structural integrity across the full draft.

Note: For large consistency check reports (when output exceeds platform batch size from Step 0.0b), apply the Batched Output Protocol.

### Check Items
1. Section-to-section transitions: does each section conclusion lead naturally into the opening of the next?
2. Terminology consistency: is the same term used consistently (no alternating between synonyms)?
3. Logical gaps: are there unexplained jumps between topics?
4. Redundancy: is substantial content repeated across sections?
5. Figure and table numbering: sequential and matching the position markers in the framework?
6. Heading numbering: correct hierarchical sequence throughout the manuscript?
7. Reference number continuity: are [N] numbers sequential and consistent with first-appearance order?

For each issue found: state the location (section number and paragraph) and the recommended fix. User decides to fix or accept as-is.

Output: pipeline_output/05.5_cross_section_check.md

Self-check:
- [ ] All 7 consistency items checked
- [ ] All issues documented with location and recommended fix
- [ ] User decisions on each issue recorded

Second-pass QA: After fixes are applied, re-read affected transitions to confirm resolution.

Next: Proceed to Step 6.0

---

## Step 6.0 - Conclusion [UPDATED]

Structure (350-500 words):
1. 3-5 sentence synthesis of the core message - integrative statement, NOT a summary list
2. What has been resolved by the existing evidence
3. What remains unresolved (the 1-2 most urgent open questions)
4. Key bottlenecks: are they technical, model-related, or translational?
5. Limitations of this review (scope, database coverage, language restrictions)
6. Future directions with specific, actionable solution pathways

Self-check:
- [ ] Does NOT repeat body text verbatim - this is synthesis, not summary
- [ ] All 6 structural elements present
- [ ] Speculative statements clearly marked
- [ ] Length: 350-500 words
- [ ] No AI-characteristic language
- [ ] No directional arrow symbols

Second-pass QA: Re-read against the framework to verify the conclusion integrates the core message from every major section.

Output: pipeline_output/05_conclusion.md

Next: Proceed to Step 6.5

---

## Step 6.5 - Abstract [NEW]

Goal: Write the abstract after the full body text and conclusion are complete.

### 6.5.1 Ask for Abstract Type
Ask the user:
  Does the target journal require a structured or unstructured abstract?
  - Structured: separate labeled sections such as Background, Methods, Results, Conclusion - common in clinical and pharmacology journals
  - Unstructured: continuous prose paragraphs - common in basic science journals
  Check the target journal author guidelines if uncertain.

### 6.5.2 Structured Abstract Format
Background (2-3 sentences): Why this topic matters; what gap the review addresses.
Methods (1-2 sentences): Search databases, year range, article types included.
Results (3-5 sentences): Key findings organized by major theme; use specific evidence.
Conclusion (2-3 sentences): Main synthesis; most important unresolved question; future direction.
Word limit: 250-300 words or per journal specification.

### 6.5.3 Unstructured Abstract Format
Continuous prose covering the same elements as the structured format without section labels.
Word limit: 200-300 words or per journal specification.

### 6.5.4 Rules
- The abstract must stand alone: a reader who reads only the abstract must understand the key message
- Do not introduce abbreviations that are not also defined in the body text
- Do not cite references in the abstract
- Do not include claims not supported by the body text

Self-check:
- [ ] Abstract type confirmed with user
- [ ] All required elements present
- [ ] Within word limit
- [ ] No abbreviations introduced that are absent from body text
- [ ] No references cited in abstract
- [ ] All claims are present in the body text

Second-pass QA: Read the abstract against the body text. Verify every statement is supported by the manuscript.

Output: pipeline_output/05b_abstract.md

Next: Proceed to Step 6.6

---

## Step 6.6 - Keywords [NEW]

Goal: Generate a keyword list using MeSH terms, following target journal requirements.

### Process
1. Identify 5-8 key concepts from the title, abstract, and main body sections
2. For each concept, search the MeSH database (NLM) for the official MeSH term
3. Prefer MeSH-controlled vocabulary over free-text terms
4. Check whether the target journal has specific keyword requirements (count, source vocabulary, format)

### Format
Output as a comma-separated list:
  Keywords: MeSH Term One, MeSH Term Two, MeSH Term Three, MeSH Term Four, MeSH Term Five

### Rules
- Use only established MeSH terms where available
- Do not use abbreviations as keywords unless they are official MeSH entries
- Do not use the journal name or author names as keywords
- Title words should not be repeated as keywords (they are already indexed)

Self-check:
- [ ] 5-8 keywords generated
- [ ] Each keyword verified as an active MeSH preferred term
- [ ] Format matches target journal requirements
- [ ] No abbreviations used unless official MeSH entries

Second-pass QA: Cross-check each keyword against the MeSH database to confirm it is an active preferred term.

Output: pipeline_output/05c_keywords.md

Next: Proceed to Step 7.0

---

## Step 7.0 - Figure Instructions + Legends [UPDATED]

Goal: Output drawing instructions for each figure and figure legends as a separate file. Instructions are designed to be handed directly to an illustrator or AI drawing tool.

### Three Separate Outputs [UPDATED]
1. pipeline_output/06_figure_instructions.md -- drawing instructions for each figure (for illustrator/AI drawing tool)
2. pipeline_output/06_figure_legends.txt -- plain-text figure legends for reference
3. pipeline_output/06_figure_legends.docx -- standalone Word file containing ONLY the figure legends, formatted per journal spec [NEW]

The .docx legend file uses the same Word formatting as the main manuscript (Times New Roman, 10 pt body, 1.5x spacing, justified). Each legend title is bold. This file is submitted or copied independently -- it is NOT merged into the main manuscript file.

### Per-Figure Drawing Instructions (in 06_figure_instructions.md)
For each figure, provide:
1. Figure number and insertion location (matching framework position markers)
2. Core meaning: what this figure must convey in one sentence
3. Elements to include: complete checklist of all required components
4. Visual hierarchy: specify which element is primary emphasis, which is secondary, which is background context
5. Logical flow direction: state in words which concept comes first and how subsequent elements relate to it (do not use directional arrows in the instructions text)
6. Color guidance: use a color-blind-safe palette; confirm that the figure is interpretable in grayscale
7. Style requirements: academic and scientific style appropriate to pharmaceutical research; uncluttered; consistent font size across all figures
8. Content alignment: confirm that figure content directly corresponds to the argument made in the relevant body section

Figure quality principles (Dhillon 2022):
- Keep content simple and focused on one main message per figure
- Use labels and scale bars as needed
- Leave adequate white space; do not cram elements
- Consistent font within and across all figures in the manuscript

### Per-Figure Legends (in 06_figure_legends.txt)
For each figure, the legend must follow this exact format:

  Figure N. [Conclusion statement title - bold in Word]
  (A) Description of panel A. (B) Description of panel B. (C) Description of panel C.
  Abbreviations: AB, full term; CD, full term; EF, full term.
  [If statistical significance is shown] ns, not significant; *, p < 0.05; **, p < 0.01; ***, p < 0.001. (p is italic lowercase)

Rules for legend titles:
- The title MUST be a conclusion statement, not a description
  - Correct: NLRP3 Inflammasome Activation Mediates Cisplatin-Induced Renal Tubular Cell Pyroptosis
  - Incorrect: Schematic diagram of NLRP3 inflammasome pathway
- Each panel description follows the format (A) text; (B) text; ending with a period
- Abbreviation line is mandatory for every figure
- Statistical significance line is mandatory if any p-values are displayed

Output: pipeline_output/06_figure_instructions.md + pipeline_output/06_figure_legends.txt + pipeline_output/06_figure_legends.docx

Self-check:
- [ ] Drawing instructions written for every planned figure
- [ ] Each legend has a conclusion-statement title
- [ ] All legends follow the (A)...(B)... format
- [ ] Abbreviation line present for every legend
- [ ] Statistical significance legend line present where applicable
- [ ] Figure count matches the target set in Step 1.0
- [ ] Color-blind-safe and grayscale-compatible guidance provided
- [ ] Figure content matches the corresponding body section argument
- [ ] No directional arrow symbols used in drawing instructions text

Second-pass QA: Re-read each legend title and confirm it states a conclusion, not a description. Re-read drawing instructions and confirm style is academic and scientific.

Next: Proceed to Step 8.0

---

## Step 8.0 - Summary Tables [UPDATED]

Goal: Create synthesis-level tables with traceable citations. Tables are informational supplements, not data dumps.

### Design Principles [UPDATED]
- Each table must convey information that cannot be as efficiently presented in prose
- Minimalist design: include only columns that provide information not already in the body text; remove any column that merely repeats prose content
- Every row must be traceable to at least one verified reference [N]
- Table titles must be informative statements, not generic labels
  - Correct: Summary of NLRP3 Inhibitors and Their Mechanistic Targets in Preclinical Nephrotoxicity Models
  - Incorrect: Table of drugs and mechanisms
- Tables do NOT affect reference numbering order; numbering is determined by first appearance in body text

### Suggested Column Structure
For mechanism/evidence tables:
| Mechanism/Target | Key Evidence | Model System | Reference(s) | Gaps or Controversies |
|-----------------|-------------|-------------|-------------|----------------------|

For drug/compound tables:
| Drug or Compound | Dose/Concentration | Key Finding | Model | Reference(s) |
|-----------------|-------------------|------------|-------|-------------|

Adapt columns to the specific content; do not force content into a generic template.

### Citation Rule for Tables
Table citations are exempt from the single-use-per-reference rule in the body text. A reference that appears in a table may also appear in body text without counting as a duplicate. However, avoid redundancy in the same table row if the reference is already cited in the table title note.

Follow table-template.md for detailed construction guidance.

Output: pipeline_output/07_tables.md + pipeline_output/07_tables_standalone.docx [UPDATED]

The .docx tables file is a standalone Word document containing ONLY the tables, formatted per journal spec (Times New Roman, 10 pt, 1.5x spacing, justified). Table titles are formatted as captions. This file is submitted independently -- it is NOT merged into the main manuscript file.

Self-check:
- [ ] All [N] citations traceable to verified references
- [ ] Table count matches the target set in Step 1.0
- [ ] Each table is synthesis-level, not a raw data enumeration
- [ ] Table titles are informative statements
- [ ] Minimalist design: no redundant columns
- [ ] No table content contradicts or repeats body text verbatim
- [ ] Standalone tables .docx file (07_tables_standalone.docx) created with correct Word formatting

Second-pass QA: For each table row, verify the cited reference [N] supports the specific content in that row.

Next: Proceed to Step 9.0

---

## Step 9.0 - Reference Assembly + Cross-Verification [UPDATED]

Goal: Build the final reference list in the confirmed format; verify 100% traceability through three independent checks.

Note: For large reference lists (when reference count exceeds ~40-50 entries), apply the Batched Output Protocol when writing the formatted list.

### 9.1 Reference Format
Use the format locked in Step 1.0 - this is not a new decision.
- Vancouver: apply formatting rules from the internal skill file vancouver-guide.md (same narrative-review skills directory). Consult the NLM Citing Medicine guide for any entry type not covered there.
- Other format: apply the journal author instructions saved in 00_project_config.md

### 9.2 Reference Mode
Ask: Auto-assemble the reference list, or will you insert references manually?
- Auto: Claude compiles from 01_reference_list.md and 02_literature_notes.md
- Manual: Claude outputs the draft list; user formats in their reference manager

### 9.3 Reference Numbering Order
Numbers follow strict order of first appearance in body text:
- [1] is the first reference cited in the Introduction
- Proceed through sections in manuscript order
- Tables do NOT determine numbering order; body text does
- Each reference receives its number on first appearance; all subsequent appearances use the same [N]

### 9.4 Triple Verification Protocol
Run all three passes before finalizing:

Pass 1 (from Step 3.0): PMID/DOI, title, first author, journal, year verified against PDF. All unverifiable papers already excluded.
Pass 2 (from Step 5.0): Each in-text [N] was verified during writing to match the specific claim. Document any unresolved inconsistencies.
Pass 3 (this step):
- Scan all 04_draft_section_*.md files for all [N] patterns
- Every [N] in text -> must exist in reference list
- Every reference list entry -> must be cited at least once in text or table
- Every reference -> must appear in 02_literature_notes.md as verified
- PMID/DOI -> must match 01_reference_list.md
- Confirm at least 5 papers from target journal are cited

If N >= 35 (per the Step 3.1 dynamic protocol): spawn a dedicated citation QA sub-agent for Pass 3. If N < 35: run Pass 3 in a single pass without a sub-agent.

### 9.5 Citation Content Alignment Check
For each in-text [N], verify: does the cited paper actually support this specific claim?
- Check all conclusion-level claims (claims forming the basis of a section argument)
- Check all mechanism-level claims (each step in a described pathway)
- Resolve any mismatch before finalizing

Output: pipeline_output/08_references_final.md

Self-check:
- [ ] Format matches locked format from Step 1.0
- [ ] Numbering is sequential by first body-text appearance
- [ ] All three passes completed and documented
- [ ] 100% traceability: every [N] has a reference, every reference is cited
- [ ] Zero unverifiable references in final list
- [ ] PMID/DOI verified for all entries
- [ ] At least 5 target journal self-citations confirmed
- [ ] Citation content alignment checked for all key claims

Second-pass QA: Read the final reference list against 01_reference_list.md entry by entry. Flag any formatted entry that does not exactly match the source metadata.

Next: Proceed to Step 10.0

---

## Step 10.0 - Final Assembly + Output [UPDATED]

Goal: Compile everything, generate abbreviations table, apply Word formatting, deliver with output file summary.

Note: When assembling the full manuscript, apply the Batched Output Protocol if the total manuscript length exceeds platform batch size from Step 0.0b.

### 10.1 Assemble Manuscript
Merge all components in this order:
1. Title (finalized after optional second-pass revision in 10.2)
2. Abstract (05b_abstract.md) - note: written in Step 6.5, placed here in assembly order
3. Keywords (05c_keywords.md)
4. Body sections (all 04_draft_section_*.md in framework order)
5. Conclusion (05_conclusion.md)
6. Acknowledgments placeholder (if required by target journal)
7. Tables (07_tables.md) -- Note: 07_tables_standalone.docx is a separate standalone submission file and is NOT merged here.
8. Figure legends (06_figure_legends.txt) -- Note: 06_figure_legends.docx is a separate standalone submission file and is NOT merged here.
9. References (08_references_final.md)

### 10.2 Title Second-Pass Revision [NEW]
After assembly, offer:
  Now that the full manuscript is complete, would you like to revise the title to better reflect the actual content and conclusions?
If yes: revise, confirm, update 00_project_config.md.

### 10.3 Abbreviations Table [UPDATED]
Scan the full assembled text for ALL abbreviations of the following types:
1. General acronyms and initialisms (e.g., NF-kB, NLRP3, ROS) -- include only if appearing > 3 times OR if they are established proper-noun abbreviations
2. Abbreviated gene names (e.g., TP53, BRCA1) -- include ALL gene symbols used in the text regardless of frequency
3. Abbreviated protein names (e.g., NRF2, CASP1) -- include ALL protein symbols used in the text regardless of frequency
4. Units and measurement abbreviations if used consistently (e.g., mg/kg, IC50)

Output as a table sorted alphabetically:
| Abbreviation | Full Term | Type | First Appearance |
|-------------|-----------|------|-----------------|
| BRCA1 | Breast Cancer gene 1 | Gene (human) | Section 1.2 |
| NRF2 | Nuclear factor erythroid 2-related factor 2 | Protein (human) | Section 2.1 |
| ROS | Reactive oxygen species | Acronym | Introduction |

Save as:
- pipeline_output/10_abbreviations.md -- plain text version
- pipeline_output/10_abbreviations.docx -- standalone Word file [NEW]

The .docx abbreviations file is formatted as a Word table (Times New Roman 10 pt, 1.5x spacing, justified). This file is submitted independently -- it is NOT merged into the main manuscript file.

### 10.4 Word (.docx) Formatting
If docx skill is available and user requests Word output, apply to ALL .docx files generated:
- Font: Times New Roman throughout
- Body text: 10 pt
- Section headings (all levels): 12 pt
- Line spacing: 1.5x
- Paragraph spacing before: 0 pt
- Paragraph spacing after: 0 pt
- Paragraph alignment: justified (both left and right edges aligned)

Save as: pipeline_output/09_final_manuscript.docx
Plain text always saved as: pipeline_output/09_final_manuscript.txt

Standalone output files (also apply the formatting above):
- pipeline_output/06_figure_legends.docx -- figure legends only
- pipeline_output/07_tables_standalone.docx -- tables only
- pipeline_output/10_abbreviations.docx -- abbreviations table only

### 10.5 Final Acceptance Checklist
- [ ] All citations from verified, user-provided literature - ZERO fabricated
- [ ] All headings are conclusion statements with numbered hierarchy (1., 1.1., etc.)
- [ ] Conclusion: synthesis, resolved, unresolved, bottlenecks, limitations, future directions
- [ ] Evidence-based reasoning throughout; no overconfident language
- [ ] No laundry-list style; critical synthesis present in every section
- [ ] Figure legends in 06_figure_legends.txt; each title is a conclusion statement
- [ ] Figure legends follow format: bold title; (A)...(B)...; Abbreviations:; p-value legend if applicable
- [ ] Tables are minimalist and synthesis-level with traceable [N]
- [ ] Abbreviations table complete: all gene/protein symbols included regardless of frequency; general acronyms included if appearing > 3 times or established proper nouns
- [ ] 100% [N] traceability; all three verification passes completed
- [ ] At least 5 target journal self-citations confirmed
- [ ] Abstract complete (structured or unstructured per journal requirement)
- [ ] Keywords: 5-8 MeSH terms
- [ ] Gene and protein symbols follow nomenclature rules
- [ ] No AI-characteristic language
- [ ] No directional arrow symbols in body text
- [ ] Word formatting applied (TNR, 10 pt body, 12 pt headings, 1.5x spacing, 0 pt paragraph spacing, justified paragraph alignment)
- [ ] Word count, figure count, and table count within specifications

Second-pass QA: Re-read the full assembled manuscript against the checklist above. Verify every item passes independently before delivering. If any item fails, fix it before proceeding to 10.6 Output File Summary.

### 10.6 Output File Summary Table [UPDATED]
| File | Path | Contents |
|------|------|----------|
| Run log | pipeline_output/run_log.md | Full session log: user inputs, actions, timestamps, interruptions |
| Language setting | pipeline_output/00_language.md | Interaction language choice |
| Pre-flight check | pipeline_output/00_preflight_check.md | Skills, network status, model/platform |
| Project config | pipeline_output/00_project_config.md | All parameters, title, journal, format, platform, batch size |
| Search strategy | pipeline_output/01_search_strategy.md | Full reproducibility record: query strings, databases, dates, counts |
| Reference list | pipeline_output/01_reference_list.md | All references with PMID/DOI and file names |
| Literature notes | pipeline_output/02_literature_notes.md | Verified notes, conflict matrix, exclusions |
| Obsidian vault | obsidian_vault/ | Complete knowledge graph |
| Framework | pipeline_output/03_framework.md | Locked outline with reference estimates |
| Section drafts | pipeline_output/04_draft_section_*.md | One file per section including Section Brief |
| Consistency check | pipeline_output/05.5_cross_section_check.md | Cross-section consistency report |
| Conclusion | pipeline_output/05_conclusion.md | Conclusion draft |
| Abstract | pipeline_output/05b_abstract.md | Abstract draft |
| Keywords | pipeline_output/05c_keywords.md | MeSH keyword list |
| Figure instructions | pipeline_output/06_figure_instructions.md | Drawing instructions per figure |
| Figure legends txt | pipeline_output/06_figure_legends.txt | Plain-text figure legends |
| Figure legends docx | pipeline_output/06_figure_legends.docx | Standalone Word file -- legends only [NEW] |
| Tables md | pipeline_output/07_tables.md | Summary tables in markdown |
| Tables docx | pipeline_output/07_tables_standalone.docx | Standalone Word file -- tables only [NEW] |
| Final references | pipeline_output/08_references_final.md | Final formatted reference list |
| Final manuscript txt | pipeline_output/09_final_manuscript.txt | Complete plain-text manuscript |
| Final manuscript docx | pipeline_output/09_final_manuscript.docx | Word-formatted manuscript (main body only) |
| Abbreviations md | pipeline_output/10_abbreviations.md | Abbreviations table in markdown |
| Abbreviations docx | pipeline_output/10_abbreviations.docx | Standalone Word file -- abbreviations table only [NEW] |
| Self-check log | pipeline_output/10_selfcheck_log.md | All QA passes and gate confirmations |

### 10.7 Deliver
- Present each output file path
- Log all checklist results to pipeline_output/10_selfcheck_log.md

Output: pipeline_output/09_final_manuscript.txt + (optional) .docx + pipeline_output/10_selfcheck_log.md + obsidian_vault/

Next: All complete. To make changes, specify the step number - e.g., return to Step 4.0 to revise the framework.

---

## Common Mistakes [UPDATED]

| Mistake | Fix |
|---------|-----|
| Skipping scope checklist (Step 1.0) | Mandatory gate - topic not validated = stop |
| Writing before framework is locked (Step 4.0) | No writing until user types LOCK |
| Laundry-list style in sections | Each paragraph must synthesize >= 2 studies and include critical evaluation |
| Overconfident language | Replace clearly demonstrates, undoubtedly, proves with suggests, indicates, supports |
| Citing a review instead of the original paper | Trace back to the original research article; use the review only if no primary source exists |
| Reference [N] mismatch between text and list | Cross-verify in Step 9.0 Pass 3 |
| Figure legend is a description, not a conclusion | Rewrite as one-sentence core finding |
| Forgetting the abbreviations table | Step 10.3 auto-generates it |
| Loading all PDFs into context at once | Use Obsidian vault reading path: MOC -> themes -> specific paper notes only |
| Directional arrows in body text | Remove; describe direction in words |
| AI-characteristic expressions in writing | Scan and remove before delivering each section |
| Citing a preprint or conference abstract | Step 2.3 filters exclude these; if found in reference list, remove |
| Not verifying gene/protein symbols | Always verify against HGNC/GeneCards for genes, UniProt for proteins before writing |
| Abbreviating terms that appear <= 3 times | Only abbreviate terms appearing > 3 times, except established proper-noun abbreviations |
| Skipping Section Brief before writing | Section Brief is mandatory; it forces articulation of writing logic before drafting |
| Not checking word count per section | Flag if outside 80-110% of section budget before advancing |
| Forgetting target journal self-citations | Verify >= 5 target journal papers in reference list before final assembly |

---

## Red Flags - STOP and Fix

- Unsure if a reference is real -> re-verify in Step 3.0 before using it
- Framework heading is a topic label, not a conclusion statement -> rewrite before LOCK
- A section reads like Author A found X. Author B found Y. -> restructure as synthesis before saving
- Using search-engine results without database verification -> return to Step 2.0
- References cited in text but missing from final list -> return to Step 9.0
- Any reference that cannot be confirmed from a user-provided PDF -> EXCLUDE, do not retain
- Verification rate below 90% -> return to Step 2.0 for replacement papers
- Word count per section is outside 80-110% of budget -> flag and resolve before proceeding
- Figure legend title describes what is shown rather than states what it means -> rewrite as conclusion
- Same reference cited in multiple unrelated paragraphs across different sections -> consolidate to single best location
- Top-journal or original-source paper missing for a key concept-level claim -> locate and add before finalizing

Any red flag: pause, fix the issue, re-verify before proceeding.

---

## Quick Reference [UPDATED]

| Step | Output File(s) | Key Action |
|------|---------------|------------|
| 0.0 | 00_language.md | Choose interaction language [NEW] |
| 0.0b | 00_project_config.md (platform) | Model and platform selection [NEW] |
| 0.1 | (screen only) | NR vs SR introduction |
| 0.5 | 00_preflight_check.md | Scan skills + network check |
| 0.9 | 00_project_config.md (title) | Confirm title [NEW] |
| 1.0 | 00_project_config.md | Parameters: word/fig/table/ref count, format, journal |
| 2.0 | 01_search_strategy.md + 01_reference_list.md | Platform, year range, article types, search + PMID list |
| 3.0 | 02_literature_notes.md | PDF verify + notes + conflict matrix + exclusions |
| 3.5 | obsidian_vault/ | Knowledge graph |
| 4.0 | 03_framework.md | Numbered outline with ref estimates -> LOCK |
| 5.0 | 04_draft_section_*.md | Section Brief + writing per section |
| 5.5 | 05.5_cross_section_check.md | Cross-section consistency [was Step 4.5] |
| 6.0 | 05_conclusion.md | Synthesis + limitations + future directions |
| 6.5 | 05b_abstract.md | Abstract (structured or unstructured) [NEW] |
| 6.6 | 05c_keywords.md | MeSH keywords [NEW] |
| 7.0 | 06_figure_instructions.md + 06_figure_legends.txt + 06_figure_legends.docx | Drawing instructions + plain-text legend + standalone Word legend |
| 8.0 | 07_tables.md | Minimalist synthesis tables |
| 9.0 | 08_references_final.md | Format + triple verification + content alignment |
| 10.0 | 09_final_manuscript.txt/.docx + 10_selfcheck_log.md | Final assembly + formatting + output file summary |

---

## Requirements Traceability

The following table maps each user requirement to the step(s) where it is implemented:

| Req | Summary | Implemented In |
|-----|---------|---------------|
| 1 | Language selection at start | Step 0.0 [NEW] |
| 2 | Structured vs unstructured abstract | Step 6.5 [NEW] |
| 3 | Reference format at start, default Vancouver | Step 1.0 + Step 9.0 |
| 4 | Network check + tool confirmation before search | Step 0.5 + Step 2.4 |
| 5 | Custom search platforms, default PubMed | Step 2.1 |
| 6 | Path explanation + default templates for non-coders | Step 1.1 |
| 7 | Year range + article type filter (no preprints/conferences) | Step 2.2 + Step 2.3 |
| 8 | Academic style, first author only, declarative sentences | Core Rules + Step 5.0 |
| 9 | Word formatting: TNR, 10/12 pt, 1.5x spacing, justified paragraph alignment | Step 10.4 |
| 10 | Numbered headings 1., 1.1., etc. | Step 4.0 + Step 5.0 |
| 11 | Abbreviate only if > 3 times | Core Rules + Step 10.3 |
| 12 | Keywords with MeSH terms | Step 6.6 [NEW] |
| 13 | Gene/protein naming conventions (HGNC, MGI, UniProt) | Core Rules + Step 5.0 |
| 14 | Figure legend separate txt, conclusion title, (A)(B) format, p-value | Step 7.0 |
| 15 | Academic drawing instruction style | Step 7.0 |
| 16 | Remove AI-characteristic language | Core Rules + Step 5.0 |
| 17 | No directional arrows; minimal tables | Core Rules + Step 8.0 |
| 18 | No filler; logic-based argument | Core Rules |
| 19 | Output file summary table | Step 10.6 [NEW] |
| 20 | Incorporate all design fixes | All steps |
| 21 | 90+ ref hallucination risk (batch verification) | Step 3.1 + Multi-Agent Strategy |
| 22 | Each reference cited once in body text | Core Rules + Step 5.0 |
| 23 | Table citations exempt; ref order by body text | Step 8.0 + Step 9.3 |
| 24 | Reference count at start, default 100 | Step 1.0 |
| 25 | Per-section reference estimate in framework | Step 4.0 |
| 26 | Title confirmation step + post-writing revision | Step 0.9 [NEW] + Step 10.2 |
| 27 | Prefer original/top-journal citations | Core Rules + Step 3.6 + Step 5.0 |
| 28 | Internal second-pass QA at every step | Every step self-check |
| 29 | Citation content must match cited paper | Core Rules + Step 9.5 |
| 30 | Target journal inquiry + special issues + 5 self-citations | Step 1.2 + Step 9.4 |
| 31 | Triple verification for references | Step 3.0 + Step 5.0 + Step 9.4 |
| 32 | Writing based on actual literature content | Core Rules |
| 33 | Multi-agent for 1M context management | Multi-Agent Strategy [NEW] |
| 34 | Section Brief (writing logic + core argument + evidence) | Step 5.0 [NEW] |

Design Fix 1: Step 4.5 renamed to Step 5.5 (runs after all sections written)
Design Fix 2: Step 6.5 Abstract added [NEW]
Design Fix 3: Obsidian reading path specified in Step 5.0
Design Fix 4: Unverifiable PDF protocol added in Step 3.3
Design Fix 5: Section word count check added in Step 5.0
Design Fix 6: Introduction special handling added in Step 5.0
Design Fix 7: Continue prompts delivered in chosen language (Step 0.0 controls this)
Design Fix 8: Reference format uses Step 1.0 locked choice in Step 9.0 (not defaulting to Vancouver)

## v2.1 New Requirements (v2.1 Additions)

| Req | Summary | Implemented In |
|-----|---------|---------------|
| 35 | Figure legends, tables, abbreviations table as standalone Word files; abbreviations include gene and protein names | Step 7.0, Step 8.0, Step 10.3, Step 10.4 |
| 36 | Model/platform selection at start | Step 0.0b [NEW] |
| 37 | Batched output for max-token limits (DeepSeek ~384t, Claude app/terminal) | Batched Output Protocol [NEW] + Steps 3.0, 5.0, 9.0, 10.0 |
| 38 | Vancouver reference format uses project-specific style file + NLM guide | Step 1.4 [UPDATED], Step 9.1 [UPDATED] |
| 39 | Full search reproducibility record (date, database versions, queries, counts) | Step 2.8 [NEW] |
| 40 | Full session run log file (user inputs, actions, timestamps, interruptions) | Step 0.0 [created here], all steps [appended] |

Abbreviations table extended to include abbreviated gene and protein names in addition to general acronyms (Req 35 detail).
Vancouver formatting source: internal skill file vancouver-guide.md (no external path dependency); NLM Citing Medicine guide consulted for entry types not covered internally (Req 38 detail).
Run log path: pipeline_output/run_log.md -- created at Step 0.5, appended at every step (Req 40 detail).

