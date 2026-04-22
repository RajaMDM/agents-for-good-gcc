# Who this is for

This is not a universal toolkit. It's aimed at specific kinds of organisations, with specific kinds of problems. If none of the archetypes below describe your team, this repo is probably not for you — and that's a useful thing to know before you invest an afternoon installing something.

## The archetypes

### 1. Small migrant-worker welfare NGOs

You work with construction workers, domestic workers, delivery riders, or seafarers. Your team is small — often under fifteen people. Your caseload spikes unpredictably. You communicate in at least three languages: English, Arabic, and one or more of Urdu, Hindi, Tagalog, Malayalam, Bengali, Tigrinya, Amharic, Nepali.

**Where an agent helps:**
- Triaging incoming case queries by urgency
- Drafting standard multilingual replies (shelter contacts, legal aid next steps)
- Compiling anonymised monthly caseload reports for funders
- Generating referral letters in the right language

**Where it doesn't:**
- Actual casework. A caseworker listens, reads body language over a video call, and makes judgment calls about whether someone is safe. That is not what an LLM does.

---

### 2. Faith-based charity and zakat organisations

You distribute zakat, sadaqah, and relief funds. Your donor base includes family foundations, zakat committees, and corporate CSR. Ramadan is your peak season — volume multiplies, and everyone wants updates in Arabic *and* English.

**Where an agent helps:**
- Generating zakat receipts in the correct format for donor jurisdictions
- Drafting Ramadan donor communications — thank-yous, updates, appeals
- Coordinating iftar drive logistics across volunteer groups
- Producing end-of-Ramadan impact summaries for donor presentations

**Where it doesn't:**
- Shariah-compliance decisions on fund distribution. An agent does not replace a scholar, a fatwa council, or internal compliance review.

---

### 3. Education, orphan-sponsorship, and youth-development organisations

You match sponsors to beneficiaries. You send quarterly updates. You produce annual reports. Parents, schools, and sponsors all expect communications in their own language.

**Where an agent helps:**
- Drafting sponsor update letters from a structured input (marks, attendance, milestones)
- Generating bilingual annual report narratives from a data file
- Producing grant applications to foundations
- Event coordination for sponsor visits, graduation ceremonies, school supply drives

**Where it doesn't:**
- Child safeguarding decisions. Never automate or assist decisions about risk to a child. That stays human.

---

### 4. Women's support, domestic violence, and crisis shelters

You take calls that are often the worst call of the caller's life. You work under confidentiality rules that are legal as well as ethical. Your tolerance for technical error is zero.

**Where an agent *may* help** (with heavy caution and good governance):
- Anonymised statistical reporting to regulators and funders
- Drafting generic resource summaries (rights, hotline numbers, legal channels)
- Scheduling non-sensitive volunteer rota work

**Where it must not help:**
- Anything touching a beneficiary record, case note, or first contact.
- Anything in the caller-facing path.

Read [`../docs/03-when-not-to-use.md`](./03-when-not-to-use.md) before doing anything in this category.

---

### 5. Health, disability, and people-of-determination support

You support patients, families, and individuals with disabilities. Your work is programmatic but also individual. Your funders include hospitals, foundations, and corporate CSR.

**Where an agent helps:**
- Drafting sponsor and donor impact stories (anonymised)
- Grant opportunity scanning across GCC health foundations
- Translating awareness campaign materials (AR/EN)
- Monthly impact reports

**Where it doesn't:**
- Clinical decisions. Medical advice. Treatment guidance. Do not let an agent near these.

---

### 6. Animal welfare and rescue

You coordinate foster families, adoptions, and emergency pickups. Social media is a major fundraising channel. Volunteers are plentiful in theory and hard to coordinate in practice.

**Where an agent helps:**
- Adoption application triage and matching
- Bilingual social media drafting (posting profiles, campaigns)
- Volunteer foster-rota coordination via WhatsApp
- Drafting supplier follow-ups (vets, food suppliers)

**Where it doesn't:**
- Decisions about which animals to accept when capacity is full. That is a hard human call.

---

### 7. Environment and sustainability nonprofits

You run awareness campaigns, school programmes, and partnerships with corporations for CSR activations. Event coordination is a constant load.

**Where an agent helps:**
- Event logistics follow-up (beach clean-ups, school workshops)
- Grant application drafting
- Corporate partnership proposal generation
- Monthly activity reports

**Where it doesn't:**
- Scientific claims. If an agent drafts an awareness post that claims a specific figure, verify the figure before it goes out. LLMs are confident about numbers that are sometimes wrong.

---

### 8. Expat community mutual-aid groups

You are an informal or semi-formal network supporting a diaspora community. Indian, Pakistani, Filipino, Bangladeshi, Sri Lankan, Nepali, East African. You coordinate emergency response, community events, and cultural programmes.

**Where an agent helps:**
- Event coordination via WhatsApp
- Community newsletter drafting
- Emergency response coordination (within limits — see below)
- Translating official communications into the community language

**Where it doesn't:**
- Anything involving unverified claims of crisis or fraud. Manual verification stays with people who know the community.

---

## If you're not in any of these

You might still get value from specific skills. The bilingual thank-you skill works for any org that has donors who read Arabic or English. The monthly impact report skill works for any org with a spreadsheet. But the repo is shaped around the archetypes above, so the framing may fit less well.

## A harder question

**Do you have a person on staff who will own this?**

Not "someone who is technical." Someone who will:

- Run `hermes doctor` when something acts weird
- Read the logs when an answer looks wrong
- Know how to disable a skill and what happens when they do
- Explain to a colleague what the agent is and isn't allowed to touch

If that person does not exist on your team, and you cannot identify a volunteer who will take the role for at least three months, do not start. You will end up dependent on whoever installed it, and that is the opposite of what this repo is trying to enable.

[Next: When NOT to use this →](./03-when-not-to-use.md)
