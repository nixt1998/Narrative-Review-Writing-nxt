# Pre-flight Environment Check

## Check Logic

At Step 0.5, scan the current environment for installed skills. Use the `Skill` tool and check `~/.claude/skills/` directory.

## Dependency Matrix

| Skill | Required? | Check Method | Purpose |
|-------|-----------|-------------|---------|
| `pdf` | **Yes** | Check `~/.claude/skills/pdf/` exists | Read and verify PDF content in Step 3.0 |
| `docx` | Optional | Check `~/.claude/skills/docx/` exists | Generate Word output in Step 10.0 |

## Outcome

### All Required Pass
```
Pre-flight Status: PASS

Required skills: pdf [FOUND]
Optional skills: docx [FOUND / NOT FOUND -- Word output will be unavailable]

Ready to proceed.
```

### Required Skill Missing
```
Pre-flight Status: BLOCKED

Required skill MISSING: pdf

The PDF skill is required to verify literature content (Step 3.0).
Without it, this skill cannot guarantee zero fabricated references.

Please install: [installation instructions]

Then restart this skill.
```

### Recommended but Missing
```
Pre-flight Status: WARNING

docx skill not found -- Word (.docx) output will be unavailable.
TXT output will still be generated.

Continue in degraded mode? (y/n)
```

## Scan Implementation

```bash
ls ~/.claude/skills/pdf/SKILL.md && echo "pdf: FOUND" || echo "pdf: MISSING"
ls ~/.claude/skills/docx/SKILL.md && echo "docx: FOUND" || echo "docx: MISSING"
```

## Output

Save results to `pipeline_output/00_preflight_check.md` with:
- Date/time of check
- All skills scanned (found/missing)
- Verdict: PASS / BLOCKED / WARNING
- If BLOCKED: specific install instructions
