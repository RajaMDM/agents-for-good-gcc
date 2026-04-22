# Changelog

All meaningful changes to this repo. Not git-commit-level — meaningful changes only.

Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

## [0.1.0] — 2026-04-22

### Added
- Initial scaffold of the `agents-for-good-gcc` repo.
- Three working Hermes skills:
  - `ngo-bilingual-thankyou` — Arabic / English donor thank-you drafting
  - `ngo-monthly-impact-report` — monthly impact report drafting from a spreadsheet
  - `ngo-gcc-grant-scanner` — grant opportunity discovery across GCC funders
- Six stubs in `skills/_stubs/` covering WhatsApp volunteer coordination, beneficiary intake triage, zakat receipts, bilingual social media, UAE CDA compliance packets, and donor stewardship cadence.
- Seven framing documents under `docs/`:
  - Why this repo exists
  - Who it's for (GCC NGO archetypes)
  - When NOT to use agentic tools
  - Data protection for GCC jurisdictions
  - Cost reality and budget-first model choices
  - Installing Hermes Agent for non-developers
  - Handover playbook (capability, not dependency)
- Living project documents: PROJECT_HISTORY.md, TECH_MEMORY.md, DEFENSE_BRIEF.md, ROADMAP.md
- Issue templates for NGO problem requests and skill contributions
- MIT license, Contributor Covenant-style Code of Conduct, CONTRIBUTING.md

### Decisions locked
- Repo is **problem-first**, Hermes-centric (not tool-comparison-first).
- Tool-agnostic skills format (agentskills.io standard) — portable to other compatible runtimes.
- No real NGO, donor, or beneficiary names in any example or test fixture.
- Maintainer makes no claim of NGO operational experience; framed as a technologist contributing pro bono tooling.

### Flagged for follow-up
- Verify UAE volunteering regulations before publicly describing Raja as a "volunteer" to NGOs (moved from repo framing into personal comms).
- Review employment IP terms before publishing (no internal systems, no work data referenced — should be clean, but verify).
- Arabic-first UX is currently weak in both Hermes and OpenClaw. Flagged in each skill's Pitfalls section.
