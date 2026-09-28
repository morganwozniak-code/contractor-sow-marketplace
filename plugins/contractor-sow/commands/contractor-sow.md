---
description: Start the contractor intake form and automatically generate a draft SOW or agreement package when required fields are complete
---

Run the `contractor-sow-drafter` skill. Start with the three routing questions,
then ask only the next relevant section from
`skills/contractor-sow-drafter/intake-form.md`. Merge the requester's answers across
turns, show a compact progress marker plus `NEEDS INFORMATION`, `BLOCKED`, or
`READY TO DRAFT`, and automatically generate the full agreement package, SOW-only
update, or neutral draft SOW when the form is complete. Preserve all of the skill's
engagement-type, legal-review, source-template, and external-system safeguards.
