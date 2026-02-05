You are generating a workflow-specific assumptions DELTA file.

Baseline assumptions are already finalized in:
templates/enumeration_assumptions_baseline.md

Your job is NOT to rewrite the baseline.
Your job is ONLY to create a delta file for this workflow:
validations/<WF_NAME>/enumeration_assumptions.md

Inputs I will provide:
1) PowerCenter Workflow XML
2) PowerCenter Mapping XML(s)
3) Enumerated Platform JSONs (dataset.json and/or pipeline.json)
4) Platform JSON schema/template (if needed for clarifying what is representable)

Task:
1) Read the baseline assumptions (treat as global truth).
2) Analyze the workflow + mapping + enumerated JSONs.
3) Identify ONLY:
   A) Deviations from baseline assumptions for this workflow
   B) Additional assumptions that were required specifically for this workflow
   C) Unknowns / items requiring confirmation (cannot be inferred confidently)
4) DO NOT include anything that is already covered by the baseline.
5) If there are no deviations, explicitly say “No workflow-specific deviations identified.”

Output file requirements:
- Create the file at: validations/<WF_NAME>/enumeration_assumptions.md
- Content MUST be valid Markdown
- Keep it short and high-signal (max ~15 bullets total)

Use this exact structure:

# Enumeration Assumptions — <WF_NAME>

This workflow follows the baseline assumptions defined in:
templates/enumeration_assumptions_baseline.md

## Workflow-Specific Deviations
- <only deviations from baseline; or say “None”>

## Workflow-Specific Additional Assumptions
- <only additional assumptions needed to enumerate JSONs>

## Unknowns / Needs Confirmation
- <anything not inferable from inputs; use “UNKNOWN:” prefix>

## Notes (Optional)
- <only if needed; keep 2-3 bullets max>

Rules / Constraints:
- Do NOT restate baseline bullets.
- Do NOT invent values.
- If unsure, mark as UNKNOWN and put it under “Unknowns / Needs Confirmation”.
- Do NOT modify enumerated JSONs.
- Do NOT propose solutions or future enhancements.
- Focus only on what was assumed during enumeration and what is uncertain.
