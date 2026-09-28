# Contractor SOW Marketplace

This public Factory marketplace provides a vendor-neutral skill for collecting
contractor engagement facts through a structured intake form and automatically
preparing draft Statements of Work.

It does **not** contain a company's agreement, legal playbook, approval routing,
internal identifiers, or HR/payroll integration. Users should provide their own
approved agreement or SOW template and have the output reviewed by qualified
counsel before use.

## Install

```bash
droid plugin marketplace add https://github.com/morganwozniak-code/contractor-sow-marketplace
droid plugin install contractor-sow@contractor-sow-marketplace --scope user
```

For local development:

```bash
droid plugin marketplace add /path/to/contractor-sow-marketplace
droid plugin install contractor-sow@contractor-sow-marketplace --scope user
```

Start a new session and say:

> I need a contractor SOW. Start the intake form and automatically generate the
> draft when the required fields are complete.

You can also start the workflow directly with:

```text
/contractor-sow
```

The skill keeps the form state across replies, reports missing or blocked fields,
validates rates and caps, and generates the draft in chat when the status reaches
`READY TO DRAFT`. It does not upload, sign, approve, or route the document.

## Scope and safety

The skill can prepare:

- a draft SOW from user-supplied business facts;
- a package based on a user-supplied approved agreement;
- a review record and list of unresolved issues.

It does not determine worker classification, guarantee enforceability, provide
jurisdiction-specific legal advice, sign or send documents, or update external
systems.

## Repository structure

```text
contractor-sow-marketplace/
  .factory-plugin/marketplace.json
  plugins/
    contractor-sow/
      .factory-plugin/plugin.json
      commands/
        contractor-sow.md
      skills/
        contractor-sow-drafter/
          SKILL.md
          intake-form.md
```

## Publishing checklist

Before making changes public:

- remove organization-specific names, addresses, emails, agreement text, and
  approval details;
- scan for secrets and real contractor/customer data;
- run the manifest and markdown checks;
- review the legal disclaimer and supported jurisdictions;
- publish through a public repository and pin installs to a tagged release when
  stability matters.

## License

MIT. See [`LICENSE`](./LICENSE).
