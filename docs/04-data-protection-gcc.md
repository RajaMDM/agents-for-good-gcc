# Data protection in the GCC

This document is orientation, not legal advice. It points you at the laws that apply, summarises the obligations that matter for an agent installation, and flags the questions you should take to a lawyer before you deploy. Regulations in this region have been moving quickly — verify anything here against current sources before relying on it.

## Why this document exists

An agent like Hermes, running on a laptop in a nonprofit office, is a processor of personal data. It reads donor lists, it writes beneficiary case summaries, it sends messages on your behalf. Every one of those actions is an act of personal data processing. The relevant law in your jurisdiction treats that seriously.

## The applicable laws

Each GCC jurisdiction has its own framework. Below is a high-level map. Confirm the current version of each with a qualified local practitioner.

### United Arab Emirates

- **Federal Decree-Law No. 45 of 2021 on the Protection of Personal Data (PDPL)** — the primary federal framework. Covers consent, lawful basis, data subject rights, and cross-border transfer.
- Sensitive personal data — including data revealing religious beliefs, ethnic origin, health data, and data about children — has stricter processing requirements.
- **DIFC Data Protection Law No. 5 of 2020** — applies if your nonprofit is incorporated in the DIFC.
- **ADGM Data Protection Regulations 2021** — applies if incorporated in the ADGM.

### Kingdom of Saudi Arabia

- **Personal Data Protection Law (PDPL) — Royal Decree M/19 of 2021**, with implementing regulations issued by the **Saudi Data and AI Authority (SDAIA)**.
- Cross-border transfer restrictions are notably strict. Sending beneficiary data to a cloud LLM hosted outside KSA is not a low-effort decision.

### Bahrain

- **Personal Data Protection Law (Law No. 30 of 2018)** — applies broadly to processing in Bahrain.

### Qatar

- **Law No. 13 of 2016** on the Protection of the Privacy of Personal Data.

### Kuwait

- **Communication and Information Technology Regulatory Authority (CITRA) Data Privacy Protection Regulation** (2021 onwards). Sector-specific rules may also apply.

### Oman

- **Personal Data Protection Law — Royal Decree 6/2022**.

**Note on accuracy:** I cannot promise none of these have been amended since writing. The author is not a lawyer in any GCC jurisdiction. Verify before publishing or deploying anything that touches regulated data.

## What this means for your agent install

### Lawful basis for processing

Before the agent touches any personal data, you need a lawful basis for that processing. In most cases this will be:

- Consent — explicit, documented, and withdrawable
- Contractual necessity — for donors, this may cover receipts and reporting
- Legitimate interests — for some routine activities, with documentation
- Public interest / charitable purpose — narrower than it sounds; verify for your jurisdiction

Donor lists, volunteer rosters, and beneficiary records are each different. Document the basis separately for each.

### Data minimisation

The agent should only see the data it needs to do the specific task. Do not connect your full donor database to the agent "just in case." Narrow access explicitly:

- Per-task data files, not whole-database pointers
- Redacted test fixtures for any experimentation
- Clear boundaries on what the agent can read vs. what it can write

### Cross-border transfer

When the agent calls a cloud LLM (Anthropic, OpenAI, Google, OpenRouter, Nous Portal), the content of your prompt and any data you include travels to that provider's infrastructure, which is almost always outside the GCC. This is a cross-border data transfer. It may be lawful, but it is lawful only if:

- The receiving jurisdiction has adequate protection, *or*
- You have appropriate safeguards in place (standard contractual clauses, explicit consent for that transfer), *or*
- An exemption applies (narrowly defined)

For the UAE PDPL specifically, cross-border transfer requires either an adequate jurisdiction determination or specific safeguards. Transferring sensitive personal data (which may include detailed beneficiary case notes) is harder.

**Practical mitigation for GCC nonprofits:**

- Use local models (Ollama, vLLM running on a machine in-country) for any workflow involving sensitive beneficiary data
- Keep cloud LLM calls to tasks where the data is either fully anonymised, public, or low-risk (donor thank-yous, grant scanning, general drafting)
- Document the decision in writing — "we use local models for beneficiary intake because of cross-border transfer restrictions" — so your board and auditor can see the reasoning

### Data subject rights

Your beneficiaries and donors have rights under the law in their jurisdiction. These typically include:

- Right of access — they can ask what data you hold
- Right to rectification — they can ask you to correct wrong data
- Right to erasure — they can ask you to delete their data
- Right to restrict processing

If personal data has been written into the agent's persistent memory, those rights apply to that memory too. You need a process to:

- Search the agent's memory for a specific individual (Hermes stores memory and conversations in plain files, so this is searchable)
- Delete or rectify entries on request
- Prove you did it

### Retention

Set an explicit retention period for agent memory. Do not leave it to accumulate indefinitely. A rolling window (e.g., delete conversation history older than ninety days) is often the right default unless a specific task requires longer retention.

## A practical checklist

Before the agent sees any personal data:

- [ ] Identified lawful basis for each data category the agent will process
- [ ] Decided which categories never go to cloud LLMs (typically: beneficiary case notes, health data, anything about children, anything involving undocumented persons)
- [ ] Set up local model routing for sensitive workflows, or decided not to run those workflows at all
- [ ] Set a retention policy for agent memory and have a way to enforce it
- [ ] Documented how to handle data subject rights requests against agent memory
- [ ] Told your board (or your equivalent governance body) what you are doing and got sign-off
- [ ] Asked a lawyer the specific question: "is this deployment lawful for our organisation in our jurisdiction?"

The last item is the one most organisations skip. Do not skip it.

[Next: Cost reality →](./05-cost-reality.md)
