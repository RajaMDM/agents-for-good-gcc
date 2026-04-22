# The handover playbook

Capability, not dependency.

If this repo produces one outcome, it should be this: the person who installed an agent in a nonprofit can walk away, and the organisation continues to use the tool responsibly without them. If you can't hand this over, you haven't done the work.

## What "handover" actually means

Handover is not a single event. It is a state the organisation needs to reach before the installer reduces their involvement. The state has five components.

### 1. A named owner inside the organisation

Not a volunteer. Not the installer. Someone on the organisation's staff who:

- Accepts the role in writing
- Has the access credentials they need
- Is paid for the time they spend on this, or has this task explicitly allocated in their job

Without a named owner, handover is fiction. The installer remains the tool.

### 2. Documentation the owner actually uses

A README nobody reads is worse than no README, because it creates an illusion of handover. Useful handover documentation is:

- **Short** — one page per skill, one page for the install, one page for "what to do when it breaks"
- **Task-oriented** — "how to change which model is used" not "architecture of the provider layer"
- **Written for the person who will actually read it** — usually a programme officer or operations manager, not a developer
- **Kept in the organisation's own space** — not only in this repo

A template for the organisation's internal ops doc is in [Appendix A](#appendix-a--internal-ops-document-template) below.

### 3. A test they can run themselves

Before handover, the owner runs each installed skill on a sample input while the installer watches. If the skill produces the wrong output, the owner needs to be able to tell. If they can't tell, the skill is not ready to hand over.

For each skill, write a one-page test document:

- Sample input that exercises the main path
- Sample input that exercises an edge case
- What a good output looks like
- What a bad output looks like
- Who to tell when output is bad

### 4. A rollback plan

What happens if everything breaks?

- How to disable a specific skill: remove it from `~/.hermes/skills/` and restart Hermes
- How to disable Hermes entirely: stop the daemon, don't delete it yet
- Where the backup of the skills directory lives
- Who outside the organisation can help if the owner is unavailable (this person should be reachable, and should not be the installer — pick someone else)

Every rollback should be tested at least once before handover.

### 5. A budget and a ceiling

The owner must know:

- What the agent is costing per month
- What the budget ceiling is
- What they do if costs exceed the ceiling
- How to reduce costs if needed (switch model, disable a skill, reduce scheduled tasks)

Without a documented budget process, the agent will silently burn money that the organisation did not plan for. [See `docs/05-cost-reality.md`](./05-cost-reality.md) for how to set this up.

## The handover sequence

A proposed sequence. Adjust to your install.

### Week 0 — installer alone

Install Hermes. Configure the first skill. Test it on real data (with consent). Fix anything that's broken.

### Week 1–2 — installer plus owner, installer leading

The owner watches the installer use the skill for real work. The installer narrates what they're doing and why. The owner is not expected to do anything yet — they are learning the shape of the tool.

End of week 2: the owner can, unaided, explain what the skill does and when it should be used.

### Week 3–4 — owner leading, installer on call

The owner runs the skill themselves. The installer is available for questions but does not intervene unless asked. Problems the owner hits become FAQ entries for the ops doc.

End of week 4: the owner has run the skill on at least ten real tasks without help.

### Week 5 onwards — installer reduces

The installer is available for serious incidents only. The owner handles day-to-day. Monthly check-ins to review cost, usage, and any issues. Quarterly reviews to decide whether to add a new skill, change the model, or unwind.

### Month 6 — review whether the installer is still needed

Honestly answer: does the organisation depend on the installer to keep this running?

- If yes: the installer's role is not done. Go back to documentation, testing, and owner training.
- If no: the installer is no longer required for the install to function. Handover is complete. The installer stays on the credits but not on the critical path.

## Red flags that mean you have not handed over

- The owner says "I'll just ask [installer]" when anything goes wrong
- The owner does not know the name of the LLM provider being used
- The owner cannot disable a skill on their own
- The monthly bill is going to an address the owner does not control
- The installer's personal API key is still in use

If any of these are true, the install has not been handed over, no matter how long it has been running.

## What to do at the end

When handover is complete:

1. Revoke any personal access credentials the installer had
2. Move the skill repo fork, if there is one, to the organisation's GitHub account
3. Move API keys to the organisation's own accounts
4. Delete the installer's local working copy of the organisation's configuration
5. Note the date of handover in the project-docs/PROJECT_HISTORY.md inside the organisation's fork of this repo
6. Celebrate — actually. Handovers are rare and they matter.

---

## Appendix A — Internal ops document template

Copy this into a Google Doc or your internal wiki. Fill it in.

```
# [Organisation name] — Hermes Agent ops document

Owner: [name, email, phone]
Backup owner: [name, email, phone]
Installed by: [name, contact, relationship to org]
Install date: [date]
Handover date: [date]

## What this agent does for us
[One paragraph, plain language]

## Which skills are installed
- [skill name]: [what it does] — test: [link to test doc]
- [skill name]: [what it does] — test: [link to test doc]

## Which skills are deliberately NOT installed
- [skill name]: [why]
- [skill name]: [why]

## Model provider and default model
Provider: [OpenRouter / Anthropic / etc.]
Default model: [model id]
Where the API key lives: [password manager entry / vault reference]
Monthly budget cap: [amount]
Who to tell if costs exceed budget: [role / person]

## Data that never touches this agent
- [e.g. beneficiary case notes]
- [e.g. undocumented migrant records]
- [e.g. anything about children]

## How to do common things
- Check the agent is running: [command]
- Disable a skill: [step by step]
- Add a new skill from the repo: [step by step]
- Change the default model: [step by step]
- Export all agent memory for review: [step by step]
- Delete all agent memory (nuclear option): [step by step]

## Who to contact
- Our owner: [name]
- The installer (escalation only): [name, response SLA]
- The community (for generic Hermes questions): [link to issues]

## Review cadence
Monthly: cost review, skill-by-skill usage check
Quarterly: decide whether to add/remove skills
Annually: full review against data protection changes
```

Without this document, there is no handover.
