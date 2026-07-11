# Final Acceptance Checklist (v2.1)

Run this checklist at Step 10.0 before delivering the final manuscript.
Every item must pass. Sourced from Step 10.5 of the narrative-review v2.1 skill.

## Anti-Hallucination
- [ ] All citations from user-provided, verified literature -- ZERO fabricated
- [ ] Every PMID/DOI verified against actual PDF content
- [ ] Zero unverifiable references in the final list
- [ ] All three verification passes completed and documented:
      Pass 1 (Step 3.0): PMID/DOI, title, first author, journal, year vs PDF
      Pass 2 (Step 5.0): each in-text citation matches specific claim during writing
      Pass 3 (Step 9.0): full cross-check of in-text [N] vs reference list vs notes
- [ ] At least 5 papers from the target journal included in reference list

## Structure and Headings
- [ ] All framework headings are conclusion statements, not descriptive labels
- [ ] All headings use numbered hierarchy: 1., 1.1., 1.2., 2., etc.
- [ ] Logical chain continuous from Introduction through Conclusion
- [ ] Figure and table positions marked in text matching framework markers
- [ ] Step 5.5 cross-section consistency check passed

## Content Quality
- [ ] No laundry-list style -- every section synthesizes across studies
- [ ] Critical evaluation present for key cited studies
- [ ] Balanced coverage -- conflicting evidence addressed, not ignored
- [ ] Evidence-based reasoning throughout; no overconfident language
- [ ] Original research cited, not reviews of reviews
- [ ] No AI-characteristic language anywhere in manuscript
- [ ] No directional arrow symbols in body text

## Conclusion
- [ ] 3-5 sentence synthesis -- integrative statement, not a summary list
- [ ] Limitations of this review stated
- [ ] Resolved vs unresolved questions identified
- [ ] Future directions with specific, actionable solution pathways
- [ ] Length: 350-500 words

## Abstract and Keywords
- [ ] Abstract complete: structured or unstructured per journal requirement
- [ ] Abstract stands alone; no abbreviations introduced not in body text
- [ ] No references cited in abstract
- [ ] Keywords: 5-8 MeSH preferred terms
- [ ] Keywords match journal requirements

## Gene and Protein Nomenclature
- [ ] Human gene symbols: ALL CAPS, italics -- verified against HGNC/GeneCards
- [ ] Mouse/rat gene symbols: First letter cap, rest lower, italics -- verified against MGI
- [ ] Human protein symbols: ALL CAPS, non-italic -- verified against UniProt
- [ ] Mouse/rat protein symbols: First letter cap, rest lower, non-italic -- verified against UniProt

## Figures
- [ ] Figure count matches Step 1.0 specification
- [ ] Each figure legend is a conclusion statement, not a description
- [ ] All legends follow format: bold title; (A)...; (B)...; Abbreviations:...
- [ ] Statistical significance legend line present where p-values are shown:
      ns, not significant; *, p < 0.05; **, p < 0.01; ***, p < 0.001
- [ ] Abbreviation line mandatory for every figure
- [ ] Color-blind-safe and grayscale-compatible guidance provided
- [ ] Figure legends output to 06_figure_legends.txt (plain text)
- [ ] Figure legends output to 06_figure_legends.docx (standalone Word file)

## Tables
- [ ] Table count matches Step 1.0 specification
- [ ] Tables are minimalist and synthesis-level with traceable [N] citations
- [ ] Table titles are informative conclusion statements
- [ ] No redundant columns that repeat prose content
- [ ] Tables output to 07_tables.md (markdown)
- [ ] Tables output to 07_tables_standalone.docx (standalone Word file)

## References
- [ ] 100% citation traceability: every [N] has a reference, every reference is cited
- [ ] Reference numbering sequential by first appearance in body text
- [ ] Format matches the format locked in Step 1.0 (default: Vancouver)

## Abbreviations Table
- [ ] All gene symbols included regardless of frequency
- [ ] All protein symbols included regardless of frequency
- [ ] General acronyms included if appearing > 3 times or established proper nouns
- [ ] Units and measurement abbreviations included if used consistently
- [ ] Table sorted alphabetically with columns: Abbreviation, Full Term, Type, First Appearance
- [ ] Abbreviations output to 10_abbreviations.md (markdown)
- [ ] Abbreviations output to 10_abbreviations.docx (standalone Word file)

## Word Formatting (applied to all .docx files)
- [ ] Font: Times New Roman throughout
- [ ] Body text: 10 pt
- [ ] Section headings: 12 pt
- [ ] Line spacing: 1.5x
- [ ] Paragraph spacing before: 0 pt
- [ ] Paragraph spacing after: 0 pt
- [ ] Paragraph alignment: justified
- [ ] Word count within user-specified limit
- [ ] Figure count within specification
- [ ] Table count within specification

## Output File Completeness
- [ ] pipeline_output/run_log.md -- complete session log
- [ ] pipeline_output/09_final_manuscript.txt -- plain text manuscript
- [ ] pipeline_output/09_final_manuscript.docx -- Word manuscript (main body)
- [ ] pipeline_output/06_figure_legends.docx -- standalone figure legends
- [ ] pipeline_output/07_tables_standalone.docx -- standalone tables
- [ ] pipeline_output/10_abbreviations.docx -- standalone abbreviations table
- [ ] pipeline_output/10_selfcheck_log.md -- QA pass documentation
