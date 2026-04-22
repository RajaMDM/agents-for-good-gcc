# When NOT to use this

Read this before you install anything. If any of the conditions below apply to your organisation, stop and get professional advice before running agentic tools on your systems.

This is not a disclaimer to cover my back. It is a list of situations where the wrong tool will cause real harm.

## Hard stops

Do not run any agent from this repo, or from anywhere else, in these situations:

### 1. Cases involving children at risk

Safeguarding decisions — whether a child is in danger, whether to escalate to authorities, whether a particular piece of communication is appropriate — are not tasks for an LLM. Full stop. Not to triage, not to summarise, not to draft communications. Human safeguarding leads only.

### 2. Trafficking, asylum, and survivor cases

An agent that holds a case note about a trafficking survivor, or a record of an asylum application, is a liability. These records can be subpoenaed, can be breached, can be exposed through prompt injection attacks, and can endanger the people in them. If your work involves any of these categories, the default is: no agent touches the record, no agent is in the loop of first contact, no agent has read access to the case management system.

The [UAE Personal Data Protection Law (Federal Decree-Law No. 45 of 2021)](https://u.ae/en/about-the-uae/digital-uae/data/data-protection-laws) and its executive regulations treat sensitive personal data — including data revealing ethnic origin, political opinions, and health — with stricter requirements. Case notes on vulnerable beneficiaries almost certainly fall into this category. Legal advice is not optional.

### 3. Undocumented migrants

Even information that feels procedural — "where can this person find shelter tonight?" — becomes dangerous if it is recorded in a system that is legally discoverable. If your organisation supports undocumented individuals, an agent on your server that logs conversations can become a problem no one anticipated.

### 4. Unattended high-stakes communication

Any outbound communication that carries legal weight — formal grant submissions, regulator correspondence, compliance attestations, donor agreements, press releases — must be reviewed and approved by a human before it leaves your system. Do not configure an agent to send these autonomously, no matter how tempting the time savings.

### 5. Financial disbursement

An agent should never decide who receives money. Not zakat, not emergency relief, not grants, not reimbursements. An agent can draft the list, prepare the file, and hand it to a human. The human approves. The human disburses.

---

## Situations where you should pause and think carefully

These are not hard stops, but they demand deliberation, usually with legal or governance input.

### Storing beneficiary PII in the agent's memory

Hermes Agent's [persistent memory](https://hermes-agent.org/) is one of its main features — it remembers across sessions, builds a model of how you work. That is an advantage for a developer working alone. For an NGO, the same feature means beneficiary names, case identifiers, and contextual details can end up in the memory store. Before you start, decide:

- Which categories of data can be written to agent memory at all
- How long memory entries persist
- How you purge memory (Hermes stores conversations, long-term memory, and skills as plain files under `~/.hermes` — [this is documented](https://github.com/NousResearch/hermes-agent))
- Who has access to the machine where the agent runs

### Running on cloud LLMs (Claude, OpenAI, Gemini)

When the agent calls a hosted LLM, the content of your prompt travels to that provider. Each provider has its own data use, training, and retention policy. For GCC nonprofits handling beneficiary data:

- Read the model provider's zero-retention and no-training-on-inputs options. For [Anthropic's Claude API, zero-retention is available via Anthropic's enterprise agreements](https://www.anthropic.com/privacy).
- Consider routing sensitive workflows through local models (Ollama, vLLM) — Hermes supports this via OpenAI-compatible endpoints. You trade off quality for data sovereignty.
- Nous Research's own Portal may be another option, but it is still a third-party inference service — verify the terms.

### Skill marketplaces and community skills

Hermes lets you install skills from the community hub or from any GitHub repo with `hermes skills install owner/repo`. Treat every community skill as if it were untrusted code — because functionally, it is. A skill can include instructions that tell the agent to exfiltrate data, overwrite files, or call an unexpected API.

The OpenClaw ecosystem has already seen this: [Cisco's AI security research team found third-party skills that performed data exfiltration and prompt injection without user awareness](https://en.wikipedia.org/wiki/OpenClaw). The risk profile on Hermes is similar.

**Rule of thumb:** only install skills from the bundled set, from this repo, or from maintainers whose GitHub history you have actually looked at.

### Prompt injection through uploaded documents

If an agent reads a document uploaded by a beneficiary, donor, or volunteer, that document can contain hidden instructions that manipulate the agent. This is a well-understood attack class. Mitigations:

- Do not let the agent take destructive actions (send email, write to beneficiary records, delete files) based on the contents of an uploaded document without human approval.
- Treat uploaded documents as input *data*, not *instructions*.
- Be especially careful when the agent has access to a messaging channel — a message in a WhatsApp group can be crafted to manipulate the agent.

---

## Questions to ask before you start

1. Who on the team will *own* this tool for at least the next three months?
2. If the person who installed it leaves tomorrow, can someone else keep it running?
3. What data will never touch this system — and do all staff understand what that list means in practice?
4. What happens if the agent produces a confident, convincing, wrong answer and someone acts on it?
5. Have you told your board what you are doing?

If you cannot answer all five of those today, stop, write them down, and come back to this repo next week.

---

## A note on honesty

Nothing in this section is specific to the skills in this repo. Every point above applies to any agentic tool, from any vendor, for any nonprofit. The reason it is in *this* repo is that I want you to read it before you read anything else.

If you decide this is not for you after reading this — good. That is exactly the right call.

[Next: Data protection in the GCC →](./04-data-protection-gcc.md)
