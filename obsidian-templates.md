# Obsidian Note Templates

## Paper Note Template

Each verified paper gets a note at `obsidian_vault/papers/NNN_AuthorYear_Keyword.md`:

```markdown
---
pmid: "XXXXXXX"
doi: "10.xxxx/xxxx"
authors: "Author A, Author B, Author C"
year: 2024
journal: "Journal Name"
tags: [mechanism, pathway, clinical, methodology, review-value-high]
---
# NNN: [First Author] ([Year]) -- [Short Title]

## Core Findings
- Finding 1 (with specific data: direction, magnitude, significance)
- Finding 2
- Finding 3

## Methodology
- Model: [in vitro/in vivo/species/cell line]
- Key technique: [Western blot, RNA-seq, CRISPR, etc.]
- Sample size: [n = X]
- Key reagents: [drug concentration, antibody, inhibitor]

## Key Mechanisms/Pathways
- [[Molecular Target A]]: [effect direction, mechanism]
- [[Pathway B]]: [upstream/downstream relationship]

## Related Studies
- [[002_Author2022_Topic]]: [relationship -- supports/contradicts/extends]
- [[005_Author2020_Topic]]: [relationship]

## Strengths
- [e.g., multiple in vivo models, large sample size, rigorous controls]

## Limitations
- [e.g., single cell line, no in vivo validation, retrospective design]

## Value to This Review
- [Which section(s) of the framework this paper supports]
- [Key figure/quote/data to cite]
```

## Theme Note Template

Auto-generated for high-frequency keywords at `obsidian_vault/themes/ThemeName.md`:

```markdown
---
tags: [theme, mechanism]
related_papers: [001, 003, 007, 012]
---
# [Theme Name]

## Overview
One-paragraph synthesis of what is collectively known about this theme.

## Supporting Evidence
- [[001_Author2024]]: [specific finding]
- [[003_Author2022]]: [specific finding]

## Contradictory Evidence
- [[007_Author2021]]: [contrary finding and possible explanation]

## Consensus Position
What most evidence supports, with key caveats.

## Open Questions
- Question 1
- Question 2
```

## MOC (Map of Content) Template

`_MOC_Overview.md`:
```markdown
# Narrative Review: [Title]

## Structure
1. [[_MOC_Mechanisms|Mechanisms]]
2. [[_MOC_Clinical_Translation|Clinical Translation]]
3. [[_MOC_Controversies|Controversies]]

## Paper Index
| # | File | Key Theme |
|---|------|-----------|
| 1 | [[papers/001_Author2024|001]] | Theme A |
| 2 | [[papers/002_Author2023|002]] | Theme B |
```
