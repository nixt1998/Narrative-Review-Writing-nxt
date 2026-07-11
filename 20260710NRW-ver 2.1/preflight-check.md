# Pre-flight Environment Check

## Check Logic

At Step 0.5, scan the current environment for installed skills, confirm search capability,
and verify network connectivity. Results feed into Step 2.0 tool selection.

## Dependency Matrix

| Skill | Required | Check Method | Purpose |
|-------|----------|-------------|---------|
| pdf | Yes | Check that ~/.claude/skills/pdf/SKILL.md exists | Read/verify PDF content in Step 3.0 |
| docx | Optional | Check that ~/.claude/skills/docx/SKILL.md exists | Generate Word output in Step 10.0 |
| web-search or equivalent | Required for assisted search | Attempt a test search call | Execute database search in Step 2.0 |

Obsidian (desktop app, obsidian.md): Recommended but not required. Without it, vault notes
remain usable as plain markdown files. The knowledge graph view in Step 3.5 second-pass QA
requires Obsidian to be installed. Document availability in the preflight output.

## Network Connectivity Check

Before any database search in Step 2.0:
1. Attempt a minimal test query to the primary target database (default: PubMed)
2. If connectivity confirmed: PASS, continue
3. If connectivity fails: WARN the user and switch to manual search mode in Step 2.0
4. Record the result in pipeline_output/00_preflight_check.md

## Run Log Note

The session run log (pipeline_output/run_log.md) is created at the start of Step 0.0.
At Step 0.5, append retroactive entries for Steps 0.0, 0.0b, 0.1, and 0.5 since those
steps executed before the first natural log checkpoint. From Step 0.9 onward, the global
log rule applies: append at end of every step without exception.

## Outcomes

### All Required Present -- PASS

Pre-flight Status: PASS
Required skills:   pdf [FOUND]
Search capability: web-search [FOUND or NOT FOUND -- manual search mode]
Optional skills:   docx [FOUND or NOT FOUND -- Word output unavailable, TXT only]
Obsidian:          [FOUND or NOT FOUND -- vault notes available as plain markdown]
Network:           [CONNECTED or UNAVAILABLE -- manual search mode]

Ready to proceed.

### Required Skill Missing -- BLOCKED

Pre-flight Status: BLOCKED
Required skill MISSING: pdf

The PDF skill is required to verify literature content in Step 3.0.
Without it, this skill cannot guarantee zero fabricated references.
Please install the pdf skill and restart.

### Optional Skill Missing -- WARNING

Pre-flight Status: WARNING
docx skill not found.
Word output unavailable; TXT output will still be generated.
Standalone Word files for figure legends, tables, and abbreviations will also be unavailable.

Continue in degraded mode? (y/n)

### Network Unavailable -- WARNING

Pre-flight Status: WARNING (degraded mode)
Network connectivity check failed.
Step 2.0 will operate in manual search mode.
Claude will output the search strategy; user executes the search independently.

## Scan Implementation

Check each dependency in sequence:
1. pdf skill:          ls ~/.claude/skills/pdf/SKILL.md
2. docx skill:         ls ~/.claude/skills/docx/SKILL.md
3. web-search:         attempt a minimal test call to the search tool
4. Obsidian:           check if obsidian.md is installed on the system
5. Network:            attempt a minimal test query to PubMed or the target database

Report FOUND or MISSING for each item; CONNECTED or UNAVAILABLE for network.

## Output

Save results to pipeline_output/00_preflight_check.md with:
- Date and time of check
- All skills scanned: found or missing with verdict
- Obsidian availability
- Network connectivity status
- Overall verdict: PASS / BLOCKED / WARNING
- If BLOCKED: specific install instructions
- Retroactive run log entries for Steps 0.0, 0.0b, 0.1, and 0.5
