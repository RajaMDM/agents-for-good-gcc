# Skill stubs

These are problems that deserve a skill but don't yet have one. Each stub describes the problem, the shape of the solution, and what a contributor would need to pick it up. Start here if you want to contribute.

---

## `ngo-whatsapp-volunteer-coordinator`

### The problem

Every NGO in the GCC runs its volunteer base on WhatsApp groups. Coordinator roles — shift allocation, reminders, event RSVPs, last-minute changes — consume hours of staff time. For events like Ramadan iftar drives, the volume spikes beyond what staff can handle manually.

### Shape of the solution

A Hermes skill invoked through the WhatsApp gateway. Behaviours:

- Accept RSVPs from volunteers in a group or direct message (numbered replies: "1" for yes, "2" for no, "3" for maybe)
- Maintain a roster for each event, keyed to the event date and shift
- Send reminders at a defined cadence (three days before, one day before, four hours before)
- Handle substitutions (when a volunteer cancels, ask other volunteers on the shortlist)
- Multi-language reminders — English and Arabic by default, other languages configurable
- Send a summary to the coordinator ahead of each event

### Dependencies

- Hermes messaging gateway configured for WhatsApp. **Important:** WhatsApp Business Policy has explicit rules about automated messaging. A nonprofit using this at any scale must verify compliance with Meta's terms. This is not optional.
- A small persistent store (can be a JSON file in the skill directory) for the roster
- Cron integration for scheduled reminders

### Open questions

- How are volunteer phone numbers added to the roster? Manual input, CSV upload, or invite-code based self-service?
- How is the shortlist of substitutes chosen? By geography, skill tag, past reliability?
- What happens when the agent gets an unrecognised reply in a group chat — does it ignore, ask for clarification, or escalate to the coordinator?

### Why this is complex

WhatsApp integration involves platform-specific tokens, a Business Account, and compliance with Meta's messaging rules. This skill needs careful design before implementation. Anyone picking it up should start by reading [Meta's WhatsApp Business Policy](https://www.whatsapp.com/legal/business-policy) and the [Hermes WhatsApp channel setup documentation](https://hermes-agent.nousresearch.com/docs) before writing any SKILL.md.

---

## `ngo-beneficiary-intake-triage`

### The problem

Intake forms arrive in bursts — through a web form, over WhatsApp, through a hotline that a volunteer transcribed. A small NGO team can receive 50-100 new intake entries during a Ramadan appeal period. Caseworkers have to triage by hand: who is urgent, who is already in the system, who doesn't match eligibility criteria.

### Shape of the solution

A skill that takes a batch of intake entries (CSV, JSON, or natural-language list) and produces:

- A triage ranking: `urgent`, `priority`, `routine`, `ineligible`, `duplicate-suspect`
- A rationale for each classification in one sentence
- A flag for any entry that mentions safeguarding concerns (child, domestic violence, self-harm indicators) — these get routed to a named human, never handled by the agent

### Dependencies

- Clear definitions of urgency and eligibility — each NGO will configure these differently; the skill needs to accept these as configuration
- A way to check against existing beneficiary records for duplicate detection — can be a simple name/phone match, but needs a sensible ruleset
- Strong human review before any action is taken on an agent classification

### Open questions

- How is the eligibility ruleset expressed? A natural-language document loaded as a reference file? A structured YAML?
- How is duplicate detection grounded? Is there a way to do this without passing beneficiary PII to a cloud LLM (see `docs/04-data-protection-gcc.md`)?
- What's the fallback when the agent is unsure? It must NEVER guess on an uncertain case — the default has to be "escalate to human."

### Why this is sensitive

This skill touches beneficiary PII and potentially safeguarding signals. It cannot be written or deployed without serious data protection review. Contributors to this skill should be prepared to engage with the boundaries in `docs/03-when-not-to-use.md` and `docs/04-data-protection-gcc.md`. If those boundaries preclude a useful implementation for a given NGO, the skill should explicitly say so, not paper over it.

---

## `ngo-zakat-receipt`

### The problem

Zakat donations have specific receipt requirements that vary by donor and jurisdiction. Some donors need a receipt for their own zakat calculation records, some need it for regulator reporting, some need a specific format for their family foundation. Generating these manually during Ramadan, when volume is highest, is painful.

### Shape of the solution

A skill that takes donation details and produces a properly formatted zakat receipt:

- Donor name, donation amount, date (Gregorian and Hijri)
- Correct receipt language: Arabic, English, or both
- Proper religious framing (e.g., تقبل الله منكم) if and only if the donor context permits
- Organisation's registration number and any regulator-required language
- Optional: a breakdown of how zakat funds are distributed (if the organisation publishes this)

### Dependencies

- Organisation's registration details (configurable)
- Accurate Hijri date conversion (needs a library, not hallucinated dates)
- Template variations for different donor types

### Open questions

- Which GCC regulators require specific receipt formats? This needs research per jurisdiction — UAE CDA, KSA NPO regulator, Zakat, Tax and Customs Authority in KSA for commercial zakat.
- Is there a standard receipt format that would work across most jurisdictions, or does every jurisdiction really need its own template?
- How is the Gregorian-to-Hijri conversion done? LLMs are unreliable at this; a deterministic library call is needed.

### Why this matters

A badly formatted zakat receipt can cause real problems for a donor — at tax time, at regulator review, at succession. It is worth doing well.

---

## `ngo-social-media-bilingual`

### The problem

Smaller NGOs struggle to maintain consistent social media presence across Instagram, Twitter/X, LinkedIn, and Facebook, especially when posts need to go out in both Arabic and English.

### Shape of the solution

A skill that takes a single content brief — an announcement, a campaign, a beneficiary story (anonymised, with consent) — and produces:

- An Instagram caption (English and Arabic versions)
- A Twitter/X thread (English; Arabic thread as separate posts if requested)
- A LinkedIn post (professional tone, English and Arabic)
- Suggested hashtags relevant to the cause and region
- Image prompts (if the user wants to generate accompanying visuals)

### Dependencies

- No mandatory external dependencies for text drafting
- Optional image generation requires a provider (FAL, OpenAI Images, etc.) — skill should function without it

### Open questions

- How is the organisation's voice guide expressed? Does the user provide a short style sample, or does the skill ask for tone descriptors?
- How is consent for beneficiary stories handled? The skill itself cannot verify consent, but it should prompt the user to confirm.

### Why this is not trivial

Bilingual social media drafting is superficially simple but surprisingly hard to get right. Arabic social media has its own conventions — hashtag style, formality, emoji use, line breaks. Direct translation sounds wrong. Parallel composition is the right approach, and the skill's prompt needs to reflect that.

---

## `ngo-compliance-packet-uae-cda`

### The problem

UAE nonprofits regulated by the Community Development Authority (CDA) in Dubai, or by equivalent authorities in other emirates, have to produce annual compliance packets. Governance documents, financial attestations, programme reports, beneficiary data summaries. Typically two weeks of staff time.

### Shape of the solution

A skill that takes the organisation's raw operational data and produces first drafts of the required packet components:

- Programme activity narratives (from programme logs and reports)
- Board composition and governance summary (from organisational records)
- A beneficiary impact summary (from anonymised data)
- Finance section placeholders that explicitly say "requires accountant"

The skill does not produce the financial statements themselves — those need qualified accounting review. It produces everything else, saving days of drafting time.

### Dependencies

- Templates for the current year's CDA packet format (need to be sourced from the CDA or from practitioners)
- Strong understanding of what the regulator actually requires vs what organisations sometimes add

### Open questions

- What is the current CDA annual return format? This changes. Contributors must source the current template, not use outdated guidance.
- How does this map to equivalent authorities in Abu Dhabi (DCD), Sharjah, and the other emirates? Is this one skill or a family?
- Is a separate skill needed for KSA regulator? Probably yes.

### Why this is regulatory

Regulatory filings have real consequences if wrong. This skill must produce a draft that a staff member reviews carefully, not a final output. The Verification section must emphasise this. Before merging, a contributor should consult someone who has actually filed a CDA annual return in the last 12 months.

---

## `ngo-donor-stewardship-cadence`

### The problem

Small NGOs lose donors by going silent between asks. Proper stewardship — the rhythm of thank-yous, updates, quiet-season engagement, Ramadan touchpoints, year-end appeals — is a full-time job nobody has.

### Shape of the solution

A skill that takes a donor list (with consent flags, donation history, communication preferences) and produces:

- A 12-month stewardship calendar respecting Ramadan, Eid, UAE National Day, and similar touchpoints
- For each donor segment, recommended touchpoints with a draft for each
- A flag for any donor whose engagement is declining (based on donation history)
- An explicit note on which touchpoints should be personalised by a human vs automated

### Dependencies

- Access to donation history (anonymised where possible)
- Accurate GCC calendar including Islamic dates
- Integration with the bilingual thank-you skill for actual drafting

### Open questions

- How is donor segmentation done? By giving size, by cause, by recency?
- How does this handle lapsed donors vs active ones — they need different touchpoints
- What's the right cadence? Monthly is too much for some donors; quarterly is too little for others. Is this per-segment configurable?

### Why this is subtle

Stewardship is a human skill that an agent can support but not replace. The output of this skill should scaffold the stewardship work, not automate it. Getting this balance wrong will alienate exactly the donors the NGO is trying to retain.

---

## Picking one up

Comment on the relevant GitHub issue or open a new one saying you want to pick it up. Include:

- Which stub you're taking
- Any clarifications you need on the open questions
- An estimated timeline

Once you've started, the stub gets moved to "in progress" in the main README table. When the PR merges, the stub entry moves to the "ready to install" section.
