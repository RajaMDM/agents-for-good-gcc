# Skills index

Every skill in this repo follows the [agentskills.io](https://agentskills.io) open standard. That means the skill's `SKILL.md` will run on Hermes, OpenClaw, GitHub Copilot's skills system, or any other compatible agent runtime. You are not locked into a single vendor.

## Ready to install

Full working skills. Install, test, use.

### [`ngo-bilingual-thankyou`](./ngo-bilingual-thankyou/)

Draft donor thank-you messages in Arabic and English for a GCC nonprofit. Handles honorifics, seasonal framing (Ramadan, Eid), and channel-specific length (email vs WhatsApp).

**Install:**
```bash
cp -r skills/ngo-bilingual-thankyou ~/.hermes/skills/
```

Then restart Hermes and invoke with `/ngo-bilingual-thankyou`.

---

### [`ngo-monthly-impact-report`](./ngo-monthly-impact-report/)

Turn a structured spreadsheet of monthly programme data into an honest impact report for a board or funder. Includes a mandatory "Things We Do Not Yet Know" section to prevent overclaiming. Optional Arabic executive summary.

**Install:**
```bash
cp -r skills/ngo-monthly-impact-report ~/.hermes/skills/
```

**Dependencies:** Spreadsheet-reading tools (built into most Hermes installs). No external API keys required.

---

### [`ngo-gcc-grant-scanner`](./ngo-gcc-grant-scanner/)

Scan active grant and CSR opportunities across GCC funders for a given cause, country, and stage. Returns a ranked list with verified URLs and fit assessments. Explicitly refuses to invent grants.

**Install:**
```bash
cp -r skills/ngo-gcc-grant-scanner ~/.hermes/skills/
```

**Dependencies:** Web search capability. Hermes supports [Tavily](https://tavily.com) and [Parallel](https://parallel.ai) out of the box. Configure an API key before installing.

---

## Stubs — problems described, solutions not yet built

Six more problems that deserve skills. Each has a description of the problem, the shape of the solution, and what a contributor would need to build it. See [`_stubs/README.md`](./_stubs/).

- `ngo-whatsapp-volunteer-coordinator`
- `ngo-beneficiary-intake-triage`
- `ngo-zakat-receipt`
- `ngo-social-media-bilingual`
- `ngo-compliance-packet-uae-cda`
- `ngo-donor-stewardship-cadence`

## Adding your own skill

See [CONTRIBUTING.md](../CONTRIBUTING.md) at the repo root. Short version:

1. Create a directory under `skills/` with the exact name of your skill
2. Write `SKILL.md` with YAML frontmatter matching the directory name in the `name:` field
3. Include sections: When to Use, Quick Reference, Procedure, Pitfalls, Verification, Test
4. Open a PR
