# Multi-Database Search Strategy Construction

## Step 1: Decompose the Topic

Extract 2-4 core concepts from the user's title/keywords.

Example: "Role of mitochondrial dysfunction in cisplatin-induced nephrotoxicity"

| Concept | MeSH Terms | Free-Text Keywords |
|---------|-----------|-------------------|
| Mitochondria | "Mitochondria"[Mesh] | mitochondrial dysfunction, mitochondrial damage, mitochondrial permeability transition |
| Cisplatin | "Cisplatin"[Mesh] | cis-diamminedichloroplatinum, CDDP |
| Nephrotoxicity | "Kidney Diseases/chemically induced"[Mesh] | nephrotoxicity, renal injury, kidney damage, acute kidney injury |

## Step 2: Build Boolean Search String

```text
(mitochondrial dysfunction OR mitochondrial damage OR mitochondrial permeability transition OR "Mitochondria"[Mesh])
AND
(cisplatin OR CDDP OR cis-diamminedichloroplatinum OR "Cisplatin"[Mesh])
AND
(nephrotoxicity OR renal injury OR kidney damage OR acute kidney injury OR "Kidney Diseases/chemically induced"[Mesh])
```

## Step 3: Select Databases

| Database | Access | Best For |
|----------|--------|----------|
| **PubMed** | Free | Primary biomedical literature; MeSH indexing |
| **Embase** | Subscription | Pharmacology/drug literature; broader international coverage |
| **Scopus** | Subscription | Citation tracking; multidisciplinary |
| **Web of Science** | Subscription | Citation network analysis; citation metrics |
| **ScienceDirect** | Subscription | Elsevier journals; clinical pharmacology content |
| **Wiley Online Library** | Subscription | Wiley journals; pharmacology and drug research |
| **Google Scholar** | Free | Gray literature; broad initial scan (use cautiously) |
| **Cochrane Library** | Free/Subscription | Clinical trials; systematic reviews |

## Step 4: Set Date Parameters

- **Default:** Past 10 years (2015-present) for most literature
- **Seminal papers:** No date restriction -- classic discoveries should be included
- **Update search:** Re-run at revision stage for newly published papers

## Step 5: Output Format

### Search Strategy Document
- Database(s) searched
- Full search string (copy-paste reproducible)
- Date range applied
- Filters (language, article type, etc.)
- Date of search
- Number of results per database

### Reference List
```
| # | PMID | DOI | Title | First Author | Year | Journal | File Name |
|---|-----|-----|-------|-------------|------|---------|-----------|
| 1 | 12345678 | 10.xxxx/xxxx | Title | Author A | 2024 | J Pharmacol | 001_Author2024_Topic.pdf |
```

## Step 6: Ask About Assisted Searching

After outputting the strategy, ask:
> "Do you need assisted searching? I can execute the search across the selected databases and return structured results, or you can perform the search independently using the strategy above."

If assisted: execute search, output structured results.
If independent: strategy document is sufficient.
