---
name: contractor-sow-drafter
description: Presents a structured contractor intake form, validates the answers, and automatically prepares a draft Statement of Work or agreement package using an approved user-provided template. Use for net-new contractors and existing-contractor renewals or changes. This produces drafts for qualified human legal review, not legal advice or final contracts.
allowed-tools: []
enabled: true
user-invocable: true
disable-model-invocation: false
license: MIT
compatibility: droid
version: 0.5.0
metadata:
  owner: contractor-sow-marketplace
  department: general
---

# Contractor SOW Drafter

## Purpose and boundary

Help a requester collect complete business facts and prepare a draft Statement of
Work (SOW) or contractor agreement package for a net-new contractor or an update to
an existing contractor engagement. The output is a drafting aid for human review.
It is not legal advice, a classification determination, a guarantee of
enforceability, tax advice, or proof that any approval or signature exists.

This skill is intentionally vendor-neutral. It does not connect to, write to, or
claim synchronization with an HR, payroll, contract-lifecycle, ticketing, signing,
or document-management system.

Use the requester's approved agreement, SOW template, policy, or playbook when one
is provided. Do not invent a company's legal terms or imply that this generic skill
is an organization's approved form.

The companion `intake-form.md` is the structured form for this skill. It is a
conversational form: the requester may paste a completed copy, answer one section
at a time, or provide the facts in ordinary language. The skill must normalize the
answers into the form fields and retain them across follow-up turns.

## First-response behavior

When the requester says only “I need a contractor SOW,” “help me hire a contractor,”
or similar:

1. Ask whether this is a `net-new`, `renewal`, `scope change`, `fee change`, or
   `replacement SOW` request. Do not draft contract language yet.
2. Explain that the skill will present an intake form, validate the business facts,
   identify review flags, and then prepare a draft for human review.
3. Start with the three routing questions below. Do not dump the full form in the
   first response.
4. If the requester answers only part of the form, ask only for the remaining
   fields.
5. Before drafting, show a normalized fact summary and review flags.
6. When all required fields are complete and no blocking condition remains,
   automatically generate the draft in that response. Do not ask the requester to
   issue a separate “generate” command.
7. If the summary contains a contradiction or the requester says a fact is wrong,
   pause and ask for the correction before drafting.

Use this opening:

```text
I can help with that. I will ask a few questions at a time, keep track of what is
complete, and prepare the draft automatically when the required facts are ready.

First:
1. Is this a new contractor, a renewal, a scope change, a fee change, or a
   replacement SOW?
2. Do you need a full agreement package, an SOW-only update, or a neutral draft?
3. Do you already have the approved agreement or SOW template?
```

### Progressive intake

Do not display all of `intake-form.md` at once unless the requester asks for the
full form. Ask only the next relevant section and show a compact progress marker:

```text
Contractor request progress: 2 of 5 sections complete
Next: contractor and client details
Still needed: scope, schedule, compensation, risk review
```

Use this order:

1. **Route the request:** request type, package mode, and approved source.
2. **Identify the parties:** contractor, signatory, client entity, requester, and
   business owner.
3. **Define the work:** project, services, deliverables, acceptance criteria,
   schedule, location, access, and term.
4. **Confirm money:** fee type, rate or amount, cap, expenses, invoicing, and
   renewal terms when applicable.
5. **Screen risk:** classification, data, export/government work, IP, subcontractors,
   international work, equity, and required reviewers.

Skip fields that do not apply, label them `Not applicable`, and explain why. For an
existing engagement, ask for the current agreement/SOW identifier and the requested
delta before asking for new-contract details. For a full package, ask for the
approved template before drafting. After each answer, echo only the newly captured
facts and the remaining items.

Do not skip intake because the requester calls the engagement “standard.” A
standard request still needs the fields in `intake-form.md`.

## Engagement types and package modes

This skill supports both net-new contractors and updates to existing contractor
engagements:

- For `net-new`, prepare a full agreement package when an approved agreement is
  provided, or a neutral draft SOW when it is not.
- For `renewal`, `scope change`, `fee change`, or `replacement SOW`, normally
  prepare an SOW-only update tied to the existing agreement. Identify whether the
  base agreement must be re-executed instead of assuming the replacement SOW is
  sufficient.
- A `neutral draft SOW` is allowed for either type only when it is clearly labeled
  as an unapproved generic draft.

For an existing engagement, collect the existing agreement or SOW identifier and
effective date, preserve the relationship to the base agreement, and do not create
a second engagement record merely because the scope or fees changed.

## Structured intake form

Use `intake-form.md` as the canonical field list. The form reflects the fields
commonly needed by a complete contractor workflow, including:

- request type, requested package, approved source-template status, and existing
  agreement/SOW identifier when applicable;
- contractor legal/entity name, contractor type, title, email, mailing address, and
  authorized signatory;
- client legal entity, requester, business owner, department, and client
  representative;
- project description, services, deliverables, schedule of work, work location,
  desired start date, initial term number/unit, and requested system access;
- worker-classification confirmations and notes;
- fee type, project fee, hourly rate, maximum chargeable amount, maximum-hours cap,
  expenses, invoicing, and currency;
- equity grant type, share count, vesting schedule, custom vesting, and approval
  status; and
- preexisting IP, third-party/open-source materials, subcontractors, regulated
  information, government work, international work, and additional notes.

### Form status and automatic generation

After every response, merge new answers into the form and report one status:

- `NEEDS INFORMATION` - one or more required fields are missing. Show only the
  missing fields and ask for them.
- `BLOCKED` - a required source, qualified reviewer, or risk decision is missing.
  Do not draft contract text.
- `READY TO DRAFT` - all required facts are present and no blocking condition
  remains. Show the normalized summary and review flags, then automatically produce
  the draft agreement package or SOW in the same response.

“Automatically generate” means generate the draft text in the current conversation.
It does not mean upload, sign, approve, route, or create a record in an external
system.

For every request, require at minimum: request type, contractor identity and
contact data, project/services, deliverables and acceptance criteria, client
representative, start date, term or completion event, work location, fee/cap
information, expense and invoicing terms, approved template status, and risk-screen
answers. For a net-new request, confirm that the contractor is new to the
organization. For an existing engagement, require the existing agreement or SOW
identifier, effective date, requested change, and the base agreement or template.
Apply the conditional fields for equity, renewals, IP, subcontractors,
international work, regulated data, and system access.

For an hourly or daily fee, validate that the rate, maximum hours, and maximum
chargeable amount are present and mathematically consistent. For project or
milestone fees, validate the amount and payment-triggering acceptance event. For
equity, require grant type, quantity, vesting, plan/document status, and qualified
review.

## Required intake

Collect or mark as `Unknown`:

### Parties and engagement

- Contractor's complete legal name.
- Individual or entity status.
- Contractor country, state/province, and work location.
- Contractor notice address and email.
- Authorized contractor signatory name and title, if applicable.
- Requester, business owner, department, and client point of contact.
- Request type: `net-new`, `renewal`, `scope change`, `fee change`, or
  `replacement SOW`.
- Requested package: `full agreement package`, `SOW-only`, or `neutral draft SOW`.
- Existing agreement/SOW identifier and effective date for an existing engagement.

### Services and schedule

- Project or engagement name.
- Specific services.
- Deliverables and measurable acceptance criteria.
- Milestones, dependencies, delivery method, and client inputs.
- Start date and end date, or an objective completion event.
- Expected hours and any total-hours cap.
- Work location, remote/on-site status, travel, and requested access.

### Commercial terms

Select one primary fee structure unless an authorized reviewer approves a combined
structure:

1. Fixed/project fee, including the payment-triggering completion or acceptance
   event.
2. Hourly or daily rate, including maximum hours and maximum dollar exposure.
3. Milestone-based fees, including each milestone amount and acceptance event.
4. Equity or other non-cash compensation, including plan, grant type, quantity,
   vesting, approval status, and grant-document treatment.

Also collect:

- Expense categories, advance-approval rule, and receipts.
- Invoice cadence, billing date, time records, payment term, and billing contact.
- Currency and tax treatment if relevant.

### Legal and operational review flags

Ask whether any of these apply. If the requester does not know, record `Unknown`
and route the item for review instead of treating it as `No`:

- Worker classification, employment-like control, exclusivity, or benefits.
- Personal data, sensitive data, regulated data, or data processing on the client's
  behalf.
- Confidential information, source code, production systems, or privileged content.
- Export-controlled, defense, classified, controlled, or regulated information.
- Government customers, officials, public-sector work, lobbying, or anticorruption
  concerns.
- International parties, cross-border work, sanctions, tax, or local-law issues.
- Subcontractors, employees, agents, or other people performing the services.
- Preexisting intellectual property, third-party content, open-source software, or
  licensed tools.
- Equity, insurance, indemnity, unusual termination, non-compete, non-solicit, or
  other nonstandard terms.
- Requested changes to the approved agreement or SOW template.

## Approved-template handling

### When an approved agreement or SOW template is provided

1. Read it completely before drafting.
2. Identify fillable fields and substantive clauses separately.
3. Preserve substantive clauses unless an authorized reviewer expressly approves a
   change.
4. Populate only verified facts.
5. For a net-new engagement, include the full approved agreement plus the completed
   SOW if the requester asks for an agreement package or the template requires it.
6. For a renewal, scope change, fee change, or replacement SOW, prepare the
   requested SOW update and identify whether the base agreement must be re-executed.
7. State any template version, effective date, or source-file uncertainty.

### When no approved template is provided

Prepare a neutral, clearly labeled draft SOW only if the requester has supplied
enough facts. Do not present it as an approved agreement or as a complete legal
contract. Recommend review by qualified counsel in the relevant jurisdictions.

## Blocking checks

Do not produce completed contract text when:

1. The contractor's legal identity or contracting party is incomplete.
2. Services, deliverables, acceptance criteria, dates, or client point of contact
   are materially incomplete.
3. The fee structure lacks its rate/amount, payment trigger, or maximum exposure
   where applicable.
4. The requester asks for a full agreement package but no approved agreement or
   organization-specific template is available.
5. Worker classification, international work, regulated data, government work,
   export controls, equity, subcontractors, or other material risk is present and
   the required qualified reviewer is not identified.
6. Preexisting IP, third-party materials, or open-source software is involved but
   the items, rights, and license/permission owner are not identified.
7. The requester asks to alter a substantive approved term without identifying the
   clause and authorized approver.
8. The requester asks the skill to approve, sign, send, upload, or mark a contractor
   active without a connected, authorized system and explicit user confirmation.

When blocked, return:

```text
Status: BLOCKED - additional information or qualified review required
Blocking items:
- [specific missing fact, source, or reviewer]
No completed contract text has been generated.
```

## Drafting procedure

1. Classify the request and choose `full agreement package`, `SOW-only`, or
   `neutral draft SOW`.
2. Normalize the facts and show them to the requester for correction.
3. Calculate review flags from the answers. Unknown answers remain flagged.
4. Run all blocking checks.
5. Draft from the approved source when available. Keep legal clauses separate from
   internal review notes.
6. Select exactly one fee structure and remove unused alternatives, sample
   vesting choices, and drafting instructions.
7. Reconcile the SOW with the agreement, especially scope, IP, confidentiality,
   data protection, term, termination, notices, governing law, and amendment rules.
8. Check arithmetic for rates, hours, milestone totals, and caps. Do not silently
   resolve inconsistencies.
9. Replace every fillable field with a verified value. Do not leave unexplained
   brackets, template tokens, sample text, or invented signature details.
10. Keep signature dates blank unless an actual execution date is already verified.
11. State that the output remains a draft pending required review and execution.

## Required output

Return exactly these sections after the form reaches `READY TO DRAFT`:

### 1. Intake result

- Status: `READY TO DRAFT`.
- Normalized field summary.
- Review flags and required reviewers.

### 2. Draft agreement package

For a full package:

- Complete approved agreement text, with only verified fields populated.
- Completed SOW appended in the approved location or exhibit format.
- No substantive clause changes unless explicitly approved and identified.

For SOW-only:

- Completed SOW or change order tied to the existing agreement or SOW identifier.
- Identifier and version/date of the base agreement it relies on.
- Any uncertainty about whether the base agreement must be re-executed.

For a neutral draft SOW:

- Clearly label it `Generic draft - not an approved legal form`.
- Include only the requested business terms and neutral drafting language.

### 3. Review record

- Request type and contractor legal name.
- Existing agreement/SOW identifier and effective date, when applicable.
- Package mode and source-template version, if any.
- Scope, schedule, and compensation summary.
- Maximum financial exposure.
- Review flags and required reviewers.
- Documents or approvals still needed.
- Status: `Draft for human legal review`.

### 4. Open items

List unresolved facts, source-template questions, and required reviews. Never say
that the document is legally final or approved.

## External-system boundary

This public skill does not connect to or write to external systems. If a user asks
to upload, send, sign, approve, route, or activate a contractor, stop and explain
that the generated text must be handled through the organization's approved process.
Do not claim an external action occurred.

## Data-handling guidance

Do not ask users to paste passwords, API keys, access tokens, or unnecessary
personal data. Encourage them to use approved document storage and access controls.
Do not include real customer, contractor, classified, export-controlled, or
confidential information in public skill files.
