# Project History

A chronological, plain-language account of how this repo came to be and how it evolved. Written for anyone — trustees, funders, collaborators — who wants to understand the project without reading code.

---

## April 2026 — Origin

The author (Raja Shahnawaz Soni) installed Hermes Agent on his personal laptop to understand how self-hosted agentic tools behave in practice. Hermes is an open-source autonomous agent released by Nous Research in February 2026 — it runs on your own machine, remembers what it learns across sessions, and can be reached through messaging platforms like Telegram, Discord, and WhatsApp.

Around the same time, the author noticed two things:

1. His father had spent an entire career working with NGOs. The work was always under-resourced, always buried under administrative load — and he had never had tools like this available.
2. Small nonprofits in the GCC face problems that off-the-shelf agent skills don't address: bilingual Arabic-English donor communications, grant landscapes specific to the region, compliance filings to local regulators, and a communication culture that runs almost entirely through WhatsApp.

The decision was to build a public library of skills that address those specific problems, shipped as portable agentskills.io-format files so they work on Hermes today and on any compatible open agent runtime later.

## April 22, 2026 — Repo scaffold published

The first public version (`0.1.0`) shipped with:

- Three working skills covering bilingual donor acknowledgements, monthly impact reports, and GCC-specific grant discovery
- Six stubs describing other NGO problems and what would be needed to turn them into skills
- Seven framing documents explaining who the repo is for, what it costs, what the data protection landscape in the GCC looks like, and — importantly — when not to use agentic tools at all
- An internal-ops document template for any NGO that wants to adopt a skill and hand it over cleanly to a named staff owner

The framing was deliberately chosen to be problem-first rather than tool-first. The repo is not about promoting Hermes or OpenClaw. It is about helping NGOs with specific recurring problems, with Hermes as one viable runtime.

## Principles that shaped the first release

Five principles guided the initial build; they are recorded here because every future decision should be checked against them.

**1. Capability, not dependency.** Every skill is accompanied by the pieces an NGO needs to own it — documentation, tests, a handover playbook. If an NGO ends up dependent on the installer, the installer has not done the work.

**2. Honesty about limits.** The `when NOT to use` document sits near the front of the repo, not buried in the README. Agentic tools are genuinely useful for specific tasks and genuinely dangerous for others. We name both.

**3. Builder-first, not consultant-first.** The repo is a library, not a marketing funnel. No commercial offering is attached. Every skill is MIT-licensed so any NGO can fork and adapt it.

**4. No claim of NGO operational experience.** The author has lived proximity to the sector through his father's career, but never direct operational work. The repo is framed as a technologist contributing tooling, not as a sector insider.

**5. No real names.** No real NGOs, donors, or beneficiaries appear anywhere in the repo — not in examples, not in test fixtures, not in screenshots. This is a legal and ethical boundary, not a preference.

---

## Entries going forward

New entries in this file should be added when:

- A new skill reaches working status (moving out of stubs)
- An NGO reports back on a deployment and the lessons change how the repo is framed
- A framing document is substantially rewritten
- An external event (regulatory change, tool deprecation, major Hermes release) changes what the repo recommends

Each entry should be short, dated, and written in plain language that a non-technical reader can follow.
