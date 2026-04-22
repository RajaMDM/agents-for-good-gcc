# Agents for Good — GCC

A library of open-source agent skills for nonprofits operating in the Gulf.

This repo is for the people running small, under-resourced nonprofit teams in the GCC who spend most of their day on admin work instead of programme work. It gives you working [Hermes Agent](https://github.com/NousResearch/hermes-agent) skills — drop-in markdown files that make your agent do real, specific jobs — plus the docs you'll need to decide whether this is for you, what it'll cost, and how to hand it off so you don't end up dependent on the person who installed it.

It is not a pitch deck. It is not a framework. It is skills you can install today, plus honest notes on where they fall short.

---

## The problems this repo addresses

If you work at a nonprofit in the UAE, KSA, Bahrain, Kuwait, Qatar, or Oman, there is a very good chance you are losing hours every week to at least three of these:

- Donors expecting thank-yous, receipts, and Ramadan updates in Arabic *and* English, on time, with the right tone
- Monthly or quarterly impact reports that need to pull numbers from a spreadsheet somebody else owns and turn them into something a board will read
- Grant opportunities scattered across regulator portals, corporate CSR pages, and foundation announcements that nobody has time to track
- A volunteer base that only communicates through WhatsApp, in four languages, across time zones
- Beneficiary intake forms that arrive in bursts — especially during Ramadan — and need triage faster than your caseworkers can do by hand
- Annual compliance packets for the UAE CDA, KSA regulator, or your local authority that eat two weeks of staff time
- Zakat receipts that have to be right for both the donor's records and the jurisdiction's rules

Each of these is a problem that a well-scoped agent skill can absorb. That is what this repo tries to provide.

---

## What's here today

The repo ships three full skills and six stubs. Full skills are ready to install and use. Stubs describe the problem, the shape of the solution, and what's needed to complete them — they're honest placeholders, not vaporware.

| Problem | Skill | Status |
|---|---|---|
| Bilingual donor thank-yous (Arabic / English) | [`ngo-bilingual-thankyou`](./skills/ngo-bilingual-thankyou/) | Ready |
| Monthly impact reports from a spreadsheet | [`ngo-monthly-impact-report`](./skills/ngo-monthly-impact-report/) | Ready |
| Grant discovery across GCC funders | [`ngo-gcc-grant-scanner`](./skills/ngo-gcc-grant-scanner/) | Ready |
| WhatsApp volunteer coordination | `ngo-whatsapp-volunteer-coordinator` | [Stub](./skills/_stubs/) |
| Beneficiary intake triage | `ngo-beneficiary-intake-triage` | [Stub](./skills/_stubs/) |
| Zakat receipt generation | `ngo-zakat-receipt` | [Stub](./skills/_stubs/) |
| Bilingual social media drafting | `ngo-social-media-bilingual` | [Stub](./skills/_stubs/) |
| UAE CDA annual compliance packet | `ngo-compliance-packet-uae-cda` | [Stub](./skills/_stubs/) |
| Donor stewardship cadence | `ngo-donor-stewardship-cadence` | [Stub](./skills/_stubs/) |

Contributing a stub is a great place to start — see [CONTRIBUTING.md](./CONTRIBUTING.md).

---

## Start here

1. Read [`docs/03-when-not-to-use.md`](./docs/03-when-not-to-use.md) **first**. There are real situations where an agent is the wrong tool. It is important you recognise yours before investing time.
2. If you're still in, read [`docs/02-who-is-this-for.md`](./docs/02-who-is-this-for.md) to see which of the NGO archetypes your team resembles. The skills map to those archetypes.
3. Install Hermes Agent using [`docs/06-installing-hermes.md`](./docs/06-installing-hermes.md). The single install command is [`curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash`](https://github.com/NousResearch/hermes-agent), but there is more to understand before you run it.
4. Pick **one** skill. Not three, not all of them. One. Use it for two weeks on one real, recurring task. Measure whether it saved time.
5. Read [`docs/07-handover-playbook.md`](./docs/07-handover-playbook.md) before you bring in a second person. The point is capability, not dependency.

---

## Before you install, understand the trade-offs

This is not free-as-in-no-cost. Hermes itself is free and open source. The costs are:

- **LLM API calls** — every task the agent runs costs something. Budget roughly USD 10–70 per month for light to moderate use on cost-efficient models (Gemini Flash, DeepSeek, Qwen). Frontier models cost significantly more. [`docs/05-cost-reality.md`](./docs/05-cost-reality.md) has numbers and the budget path.
- **Data protection** — you are running an agent that sees beneficiary, donor, and sometimes case data. UAE, KSA, and other GCC jurisdictions have real data protection law. [`docs/04-data-protection-gcc.md`](./docs/04-data-protection-gcc.md) walks through what matters. Read it before you connect anything sensitive.
- **Someone has to own it** — somebody in your team has to be able to run `hermes doctor`, understand what a skill is, and know how to disable one when it goes wrong. If no one on staff will take that, don't start.

---

## Why I built this

My father spent his entire career in the NGO sector. I grew up close to that world without ever working in it myself.

I am a technologist, not an NGO practitioner. I have worked for twenty years in enterprise data — master data, governance, integration — and I spend my weekends building things. This repo is what happens when those two facts meet: someone who can build systems but doesn't pretend to know what it feels like to run a refugee intake desk, a migrant worker hotline, or a cancer patient support service.

So this is not a consulting offer. It is a library. If a skill here saves you an afternoon, good. If you need more, raise an issue and tell me what's missing — I'd rather add the skill than be on a call.

> *Anyone can describe a system. I'd rather hand you a working one and say — here, try it.*

— Raja Shahnawaz Soni · [LinkedIn](https://linkedin.com/in/raja-shahnawaz/) · Dubai

---

## Repo structure

```
agents-for-good-gcc/
├── README.md                     # This file
├── LICENSE                       # MIT
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── CHANGELOG.md
├── docs/                         # How to think about using this
│   ├── 01-why-this-repo.md
│   ├── 02-who-is-this-for.md
│   ├── 03-when-not-to-use.md
│   ├── 04-data-protection-gcc.md
│   ├── 05-cost-reality.md
│   ├── 06-installing-hermes.md
│   └── 07-handover-playbook.md
├── skills/                       # The actual artefact
│   ├── README.md                 # Skills index
│   ├── ngo-bilingual-thankyou/
│   ├── ngo-monthly-impact-report/
│   ├── ngo-gcc-grant-scanner/
│   └── _stubs/                   # Problems with solution shapes, not yet built
└── project-docs/                 # Living documents for the repo itself
    ├── PROJECT_HISTORY.md
    ├── TECH_MEMORY.md
    ├── DEFENSE_BRIEF.md
    └── ROADMAP.md
```

---

## Contributing

Contributions welcome from two kinds of people:

- **Nonprofit staff** — tell me what's broken in the skills I've shipped, or raise a problem you want a skill for. Use the [NGO Problem Request](./.github/ISSUE_TEMPLATE/ngo-problem-request.md) template.
- **Technologists** — take a stub and turn it into a working skill. Use the [Skill Contribution](./.github/ISSUE_TEMPLATE/skill-contribution.md) template. See [CONTRIBUTING.md](./CONTRIBUTING.md).

All skills follow the [agentskills.io](https://agentskills.io) open standard, which means they run on Hermes, OpenClaw, and any other compatible agent runtime — not locked to a single vendor.

---

## License

MIT. See [LICENSE](./LICENSE). Skills are yours to fork, adapt, and ship inside your own NGO tooling.
