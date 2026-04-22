---
name: Skill Contribution
about: Propose a new skill, pick up a stub, or improve an existing skill.
title: "[Skill] "
labels: skill-contribution, needs-triage
assignees: ''
---

## What you are proposing

- [ ] Picking up an existing stub (which one: __________)
- [ ] Proposing a new skill not currently in the stubs list
- [ ] Improving an existing skill (which one: __________)

## The skill (or improvement)

Briefly describe what the skill does, or what the improvement addresses.


## Who is this for

Which of the NGO archetypes in `docs/02-who-is-this-for.md` benefits? If it doesn't map to one, explain who does benefit.


## Shape of the solution

What will the skill do? Keep it to the shape — not full implementation detail. The SKILL.md is where the detail goes.

**Inputs:**


**Outputs:**


**Tools / APIs required:**


## Data protection considerations

Does this skill touch:

- [ ] Beneficiary PII
- [ ] Donor PII
- [ ] Financial records
- [ ] Health data or other sensitive categories
- [ ] Children's data
- [ ] None of the above

If any of the first five are ticked, reference `docs/04-data-protection-gcc.md` and explain how the skill addresses those constraints.


## Dependencies

Does the skill need:

- External API keys (which?):
- Specific Hermes tools (web search, browser, subagents):
- A messaging channel (which platform?):
- Local model support:
- Anything else:


## Open questions

List anything that isn't decided yet. If you need help from another contributor to decide, say so here.


## Timeline

Rough estimate of when you expect to have a PR ready. "Two weekends," "one month," "unclear — asking for a collaborator" are all fine.


## PR checklist (to be completed before merging)

- [ ] Skill directory name matches the `name:` field in SKILL.md
- [ ] Frontmatter has all required fields
- [ ] All five structured sections present (When to Use, Quick Reference, Procedure, Pitfalls, Verification)
- [ ] A working test case at the bottom of SKILL.md
- [ ] No real NGO, donor, or beneficiary names anywhere
- [ ] No secrets hardcoded
- [ ] CHANGELOG.md updated
- [ ] Skill listed in `skills/README.md` and main `README.md`
