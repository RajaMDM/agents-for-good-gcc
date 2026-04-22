# Contributing

This repo exists to help nonprofits in the GCC do more with less. Contributions come in two shapes:

## 1. If you work at a nonprofit

You don't need to write code. You need to tell me what is broken and what is missing.

- **A skill doesn't work for you** → open an issue with the "Bug in a skill" template. Describe what you tried, what you expected, and what happened. Arabic/English/Urdu all fine.
- **You have a recurring problem you think a skill could solve** → open an issue with the "NGO Problem Request" template. Describe the problem in your own words. Include: how often the problem comes up, how long it takes to handle manually, who in the team deals with it.
- **A skill was useful** → if you have time, leave a note. It helps me know what to build more of. But no pressure.

You do not need to sign a CLA, disclose your NGO name, or justify your request.

## 2. If you are a technologist

You can turn a stub into a working skill, improve an existing one, or write a new one from a Problem Request.

### Picking a stub

Stubs live in `skills/_stubs/` and are described in `skills/_stubs/README.md`. Each stub has:

- The problem statement (why this skill matters to an NGO)
- The shape of the solution (what the skill should do)
- Dependencies (tools, APIs, integrations needed)
- Open questions (things that have to be decided before writing)

Comment on the relevant issue (or open one) saying you're picking it up so two people don't duplicate work.

### Writing a skill

1. Create a directory under `skills/` named exactly what your skill is named. The `name:` field in your SKILL.md **must match** the directory name — if they don't match, Hermes will not load the skill. This is [documented in the Hermes docs](https://github.com/NousResearch/hermes-agent).
2. Write `SKILL.md` with YAML frontmatter and these sections: **When to Use**, **Quick Reference**, **Procedure**, **Pitfalls**, **Verification**.
3. Keep the skill body under ~5,000 tokens. Longer skills load badly into context.
4. If the skill needs environment variables (API keys, paths), declare them in `required_environment_variables` in the frontmatter. Never hardcode secrets.
5. Include a short README in the skill directory for non-Hermes users — someone might want to adapt your skill for another runtime.
6. Write tests where you can. At minimum, add a "Test this skill" section at the bottom of SKILL.md with a sample input and an expected shape of output.

### Realism rules

- **No fake brand names in examples.** Use placeholder names like "Al-Noor Charitable Foundation" or "Hope for All Society" — not real NGOs, not real donors.
- **No dependence on paid APIs without a free-tier alternative.** If your skill relies on a paid service, document a fallback that works with free tools.
- **Assume the NGO staff running your skill is not a developer.** Document the Setup section like you're writing for someone who has used a computer for years but never opened a terminal.
- **Arabic UX matters.** If the skill produces text for end users, it should handle Arabic output properly — including right-to-left rendering where applicable, and proper honorifics (أستاذ، سيد، سيدة).

### PR checklist

- [ ] Skill directory name matches the `name:` field in SKILL.md
- [ ] Frontmatter has: name, description, version, metadata.hermes.tags, metadata.hermes.category
- [ ] SKILL.md has all five structured sections
- [ ] No secrets hardcoded
- [ ] No real NGO, donor, or beneficiary names in examples
- [ ] A working test case at the bottom of SKILL.md
- [ ] CHANGELOG.md updated with a one-line entry under `[Unreleased]`
- [ ] Skill listed in `skills/README.md`
- [ ] Skill listed in the main `README.md` table

## 3. Code of Conduct

Read [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md). We are building tools for people doing hard work on thin budgets. Everyone gets treated with that in mind.
