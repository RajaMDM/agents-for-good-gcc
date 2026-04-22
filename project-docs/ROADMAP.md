# Roadmap

Where this repo is heading, what's currently blocked, and what triggers the next phase.

Not a commitment document. A working map for the next 12 months.

---

## Now (v0.1 — shipped April 2026)

Three working skills, six stubs, seven framing documents, full project-docs scaffolding. The repo is a usable, defensible library for NGOs that match one of the documented archetypes.

**What "now" means:** the repo exists and works. An NGO can install Hermes, copy a skill, and use it. A contributor can pick up a stub and turn it into a skill.

---

## Next (v0.2 — target Q2–Q3 2026)

### Turn two stubs into full skills

Priority order:

1. **`ngo-zakat-receipt`** — useful year-round, spikes during Ramadan, minimal external dependencies. The technical work is mostly research (per-jurisdiction requirements), not engineering.
2. **`ngo-social-media-bilingual`** — high utility, low risk, adjacent to the existing bilingual thank-you skill, shares infrastructure.

**Trigger to start:** at least one NGO reports useful adoption of an existing skill, or a contributor volunteers to pick up one of the stubs.

### Run one real pilot

Find one small nonprofit — preferably in Dubai or Abu Dhabi — willing to install Hermes and one skill for a six-week pilot. Document what went right, what went wrong, and amend the repo based on what was learned.

**Trigger to start:** an NGO director reads the repo and reaches out.

**Blocker:** UAE volunteering regulations need to be clarified first. The right path is probably to pilot through a licensed NGO and have them publish the lessons, not me.

### Arabic translation of top-level docs

The framing documents (README, who-is-this-for, when-not-to-use, handover-playbook) should be available in Arabic. Machine translation is insufficient — these documents carry ethical and legal weight and need fluent review.

**Trigger to start:** a contributor volunteers to translate, OR budget is found for paid professional translation.

---

## Later (v0.3+ — target Q4 2026 and beyond)

### Turn remaining stubs into skills

Specifically:
- `ngo-whatsapp-volunteer-coordinator` — depends on clarifying Meta's WhatsApp Business Policy for nonprofit automation
- `ngo-beneficiary-intake-triage` — depends on resolving the PII-handling constraints; may end up as a hybrid local-model skill
- `ngo-compliance-packet-uae-cda` — depends on getting current regulator templates from a practitioner
- `ngo-donor-stewardship-cadence` — depends on the other donor-facing skills being stable

### Add an Abu Dhabi / Sharjah compliance track

UAE is not one regulator. Dubai has CDA; Abu Dhabi has DCD; Sharjah has its own. A single `ngo-compliance-packet-uae` skill may need to split into three.

### Expand beyond UAE

If the UAE skills prove useful, replicate the compliance, grant discovery, and donor-stewardship skills for KSA (primary target), then Bahrain, Qatar, Kuwait, Oman. Each expansion needs a local practitioner collaborator — not something I can do alone.

### Integrate with common NGO tools

Optional integrations with free-tier versions of: Google Workspace, Airtable, Notion, Mailchimp free plan. Only if there is demonstrated pull from real NGOs — not built speculatively.

### Publish selected skills to the Hermes skills hub

Once a skill has been used successfully by two or more NGOs and has not had a material bug in 90 days, it becomes a candidate for the official Hermes skills hub (`hermes skills install owner/repo-name` path). This is promotion, not a rewrite — the skills stay open in this repo.

---

## What's currently blocked

### Legal clarifications I need to resolve personally

- **UAE volunteering framework:** public self-description as a volunteer offering tech services to NGOs may require registration with a licensed channel. Until this is verified, any promotion of the repo should frame it as a pro bono library — not a volunteer-services offering.
- **Employer IP terms:** need to confirm that a public open-source repo in the nonprofit-automation space does not conflict with employment agreements. Moving slowly on public promotion until this is resolved.

### Technical blockers

- **Arabic output quality on budget models** is inconsistent; until either Hermes ships with better Arabic handling, or a cost-effective Arabic-specialist model is widely available, the bilingual skills will carry a "review Arabic with a fluent speaker" caveat.
- **WhatsApp channel for agent-initiated messages** is constrained by WhatsApp Business Policy. A nonprofit-friendly path exists but is not simple.

### Human blockers

- No active contributors yet. The repo is a solo effort at v0.1. Moving to v0.2 benefits from at least one additional contributor — ideally someone with operational NGO experience in the GCC.

---

## Things that will trigger a rewrite of this roadmap

- A major Hermes release that breaks the skill format
- A new open agent runtime that makes Hermes less useful — the repo's tool-agnostic stance means a migration is an annoyance, not an emergency
- GCC regulatory changes that significantly alter the legal landscape for AI tools handling personal data
- A serious incident — mine or someone else's — involving agentic tools in the nonprofit sector. If that happens, the `when NOT to use` document grows and the scope of what this repo ships contracts.

---

## Anti-roadmap: things this repo will not become

Putting limits on ambition is as important as stating ambition.

- **Not a SaaS.** There will be no hosted version, no signup, no multi-tenant platform. Every NGO runs the skills themselves.
- **Not a consultancy.** No paid services tied to the repo.
- **Not a brand-building exercise.** The author is not trying to become an "AI for good" thought leader. If the repo disappears from the top of his GitHub profile because he built something else he is more excited about, that is fine.
- **Not a replacement for sector expertise.** The repo supplies tools. The work of running an NGO stays with the people doing it.

---

## Rules for updating this roadmap

- Review quarterly
- Move items from Next to Now when they start; move from Later to Next when Next empties
- Add blockers as they emerge; close them when they resolve
- If a goal has not moved in 18 months, delete it — either honestly reframe or let it go
