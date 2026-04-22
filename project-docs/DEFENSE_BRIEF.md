# Defense Brief

Cumulative talking points for defending the technical and positioning choices in this repo. When someone asks "why did you choose X over Y?" — the answer lives here.

Updated after every significant decision. Include alternatives considered and why they were rejected.

---

## Positioning choices

### "Why did you build this as a skills library rather than a consulting offering?"

**Answer:** Because a library scales and a person does not. If one small nonprofit in Qatar adopts a skill, I want the next ten to be able to adopt the same skill without a call with me. A consulting model makes the installer the bottleneck; a library model makes the skills the product.

**Alternatives considered:**
- Paid consulting with a sliding scale for small NGOs — rejected because it creates a dependency relationship and limits reach
- A hosted SaaS that NGOs sign up for — rejected because it puts PII on my infrastructure and concentrates risk
- A LinkedIn presence with free advice — rejected because advice without shipped tools is not what this sector needs

### "Why Hermes and not OpenClaw?"

**Answer:** Hermes was chosen because (a) it is actively maintained by Nous Research, an organisation with a clear identity and roadmap; (b) its learning loop and skill persistence model match how NGOs actually use tools — the same workflow recurring monthly for years; (c) Hermes has a `hermes claw migrate` command, so NGOs that start on OpenClaw can migrate without losing work. The skills themselves are agentskills.io-format, so they run on either.

**Alternatives considered:**
- OpenClaw as primary — rejected because of documented third-party skill security incidents and the project's more volatile branding history (renamed twice in four months)
- Build on a proprietary platform (ChatGPT, Claude.ai, Gemini) — rejected because it creates vendor lock-in and data residency issues for GCC nonprofits
- Write for LangChain or CrewAI — rejected because these are developer frameworks, not end-user agent runtimes; the whole point is that a non-developer can install and run the tool

### "Why problem-first, not tool-first?"

**Answer:** Because NGOs do not have agentic-tool problems. They have donor stewardship problems, impact reporting problems, and grant discovery problems. Leading with the tool treats NGOs as a market to be educated; leading with the problem treats them as people with a job to do. The second framing is more useful and more honest.

### "Why did you mention your father's NGO career?"

**Answer:** Because it's true, because it is the real reason the repo exists, and because not mentioning it would leave an obvious motivational question unanswered. The framing is deliberate: lived proximity, no operational claim. I grew up near the sector. I have not done the work. That distinction matters, and saying it plainly is more credible than pretending to be something I am not.

### "Why GCC specifically, not Middle East or MENA?"

**Answer:** Because the regulatory, linguistic, and funding landscape in the GCC (UAE, KSA, Bahrain, Kuwait, Qatar, Oman) is coherent enough to write for, and I live in it. A skill for Lebanon has different regulator requirements, different donor patterns, different operational realities. Scope is a feature. If the repo succeeds, adding MENA-adjacent skills as a separate track is plausible — but not in v0.1.

---

## Technical choices

### "Why agentskills.io format, not a Hermes-proprietary schema?"

**Answer:** Portability. The same format runs on Hermes, OpenClaw, GitHub Copilot's skills system, and any future open agent runtime. NGOs that start on Hermes and later move to something else do not have to rewrite. The small cost is not using Hermes-specific extensions; the benefit is future-proofing.

**Alternatives considered:**
- Hermes-native YAML with Hermes-only fields — rejected because it would lock the repo to one runtime
- A custom schema of our own — rejected because no one else would adopt it

### "Why no build system, no CI/CD, no Docker image?"

**Answer:** The audience is nonprofit staff, often non-technical. Every additional technical layer raises the adoption barrier. Plain markdown files that can be inspected in any editor is the lowest possible bar. Future versions may add optional tooling — CI for skill validation, a packaging convention for the skills-hub — but the default path stays `git clone` + `cp -r`.

**Alternatives considered:**
- A one-click installer that sets up Hermes, drops in skills, configures the model — rejected because it hides the thing from the user, and the user needs to understand what is happening to hand it over responsibly
- A Docker image — rejected for the same reason, plus it makes data residency harder to reason about

### "Why not ship a GUI or a web dashboard?"

**Answer:** Hermes already has a TUI and supports messaging gateways (Telegram, Slack, WhatsApp, Signal). Building another UI on top duplicates effort for no clear gain. If a skill's UX is bad, the fix is to rewrite the skill's prompt, not wrap it in a web form.

**Alternatives considered:**
- A simple web app per skill — rejected because it adds hosting and maintenance burden without clear value for the user
- A Streamlit-style data app for the impact report skill — tempting, but would fork the maintenance path

### "Why open-source, MIT?"

**Answer:** Two reasons. First, the audience — nonprofits — needs to be able to fork, adapt, and redeploy without licensing friction. Second, the skills themselves embed operational patterns that the sector benefits from sharing widely. MIT is the least restrictive practical choice. AGPL would be wrong here — it would block adoption inside orgs with cautious legal teams.

---

## Scope choices

### "Why did you refuse to ship a beneficiary intake or child safeguarding skill?"

**Answer:** Because these are tasks where confident-wrong answers cause real harm, and because current LLMs cannot meet the reliability bar these tasks require. The `docs/03-when-not-to-use.md` document names these as hard stops. Not refusing would be irresponsible.

**Alternatives considered:**
- Ship the skill with heavy warnings — rejected because warnings are routinely ignored, and the liability is not reduced by them
- Ship a "triage assistant" that only recommends urgency levels for human review — is in the stub list; implementation requires serious data-protection and safeguarding review before any code is written

### "Why stub the compliance packet skill rather than ship it?"

**Answer:** Because regulator requirements vary by emirate, by year, and by organisation category. I could not verify the current UAE CDA annual return format at the time of v0.1 release. Shipping a skill that uses stale templates would actively harm NGOs. The stub describes the problem and what a contributor would need to do; it does not pretend to be a solution yet.

### "Why are there no paid integrations?"

**Answer:** Paid integrations (Salesforce Nonprofit Cloud, DonorPerfect, specific WhatsApp Business API providers) introduce cost and lock-in that small NGOs cannot absorb. The repo defaults to open or free-tier tools. If an organisation has the budget for paid tooling, they have choices this repo does not need to address.

---

## Future defences to prepare (placeholder)

Things that are likely to come up later and should have prepared answers when they do:

- "Why don't you use LlamaIndex / LangChain / CrewAI / AutoGen under the hood?" — Because those are developer frameworks. The target user is an NGO staff member.
- "Why don't you charge for training / workshops?" — If an NGO asks for paid support, fine; but the repo is a library, not a funnel.
- "Hermes had a major version bump and my skills broke." — Expected risk; see TECH_MEMORY for Hermes version drift notes; affected skills get patched as issues are filed.
- "An NGO is using this and something went wrong." — See `docs/03-when-not-to-use.md` for the boundary that should have prevented it. Learn from the incident, document it here, amend the relevant skill or doc.

---

## Rules for updating this document

- Add an entry when a defence is needed that didn't exist before
- Include the alternatives considered — not just the choice made
- Do not remove entries when choices change; add a superseding entry
- If the answer to a "why" question is genuinely "I don't know yet," say so — don't fabricate a defence
