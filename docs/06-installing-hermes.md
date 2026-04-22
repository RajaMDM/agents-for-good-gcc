# Installing Hermes Agent

This document is written for someone in an NGO who is comfortable with a computer but has never installed a developer tool. If you are a developer, skip to the [official Hermes docs](https://hermes-agent.nousresearch.com/docs) — they are faster.

## Before you begin

You need:

1. **A computer running macOS, Linux, or Windows with WSL2** — Hermes itself [installs on Linux, macOS, and WSL2](https://hermes-agent.org/) with a single command. Windows users need to set up [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install) first.
2. **An internet connection** — for install and for LLM API calls afterwards.
3. **An API key from at least one LLM provider.** Easiest starting point: create an [OpenRouter](https://openrouter.ai) account. OpenRouter gives you access to many models through one key. Budget USD 20 to top up.
4. **An hour of uninterrupted time.** Do not try to install this while also doing anything else.

## Step 1 — Install Hermes

Open your Terminal (macOS / Linux) or your WSL shell (Windows) and run:

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

This is [the official install command from the Hermes repo](https://github.com/NousResearch/hermes-agent). It installs `uv`, Python 3.11, Node.js, ripgrep, and ffmpeg for you.

The install will print a lot of text. This is normal. Wait for it to finish. When it's done, you should be able to type:

```bash
hermes --version
```

…and see a version number. If you see "command not found," close the terminal, open a new one, and try again. If that still fails, the install log will have told you what's missing — copy-paste the error into the [Hermes GitHub issues](https://github.com/NousResearch/hermes-agent/issues) before asking anywhere else.

## Step 2 — Run the setup wizard

Hermes ships with a setup wizard that configures your model provider, your messaging channels (if you want them), and your tools in one go:

```bash
hermes setup
```

When it asks which model provider you want to use, start with **OpenRouter**. Paste the API key you created earlier. Select a default model — for a first install, pick:

- `google/gemini-2.5-flash` — very cheap, good for most drafting
- OR `deepseek/deepseek-chat` — also cheap, slightly different strengths
- OR `anthropic/claude-haiku-4-5` — more expensive but high quality on bilingual work

You can change this later with `hermes model`. You are not locked in.

## Step 3 — Test it

Open a chat:

```bash
hermes
```

Type a simple instruction:

> Write a short thank-you email in English for a donor who contributed AED 1,000 to our back-to-school programme. Keep it under 80 words.

The agent should draft something reasonable. If the response is empty, failing, or nonsensical, your model or API key is probably misconfigured. Run `hermes doctor` — it checks the install and tells you what's wrong.

## Step 4 — Install the skills from this repo

Clone this repo somewhere on your machine:

```bash
git clone https://github.com/rajamdm/agents-for-good-gcc.git
cd agents-for-good-gcc
```

(The URL above is a placeholder. Replace it with the actual repo URL when this repo is published.)

Copy the skill you want into your Hermes skills directory:

```bash
mkdir -p ~/.hermes/skills
cp -r skills/ngo-bilingual-thankyou ~/.hermes/skills/
```

Restart Hermes:

```bash
hermes
```

Type `/skills` in the chat — you should see `ngo-bilingual-thankyou` in the list. That means Hermes has loaded the skill.

You can now invoke it by typing `/ngo-bilingual-thankyou` followed by the information it needs.

## Step 5 — Decide what you will run and what you will not

You now have a working agent. Before you start using it for real work, go back and read:

- [`docs/03-when-not-to-use.md`](./03-when-not-to-use.md) — the hard stops
- [`docs/04-data-protection-gcc.md`](./04-data-protection-gcc.md) — the legal boundaries
- [`docs/07-handover-playbook.md`](./07-handover-playbook.md) — how to set this up so you are not the single point of failure

## Step 6 (optional) — Connect a messaging channel

Hermes can connect to Telegram, Discord, Slack, WhatsApp, Signal, and email so you can chat with the agent from your phone without opening a terminal. This is powerful and it's also where things get more complicated — channel setup involves platform-specific tokens and sometimes business accounts.

Do not do this on day one. Use the terminal chat for two weeks first. If you want to add a messaging channel after that, the [Hermes messaging gateway guide](https://hermes-agent.nousresearch.com/docs) walks through each platform.

Special note on WhatsApp: WhatsApp's terms and API have real restrictions on business / bot use. Do not connect a WhatsApp channel to an agent for beneficiary-facing interactions without understanding Meta's WhatsApp Business Policy. It is worth asking a lawyer.

## Common things that go wrong

**"hermes: command not found" after install.** Close the terminal, open a new one. If still broken, the install script couldn't add Hermes to your PATH — follow its printed instructions or run `hermes doctor`.

**The agent replies with nothing or says "error."** Ninety percent of the time this is an API key problem or an out-of-credit problem. Log into your LLM provider dashboard and check.

**The skill I copied doesn't show up in `/skills`.** The directory name must match the `name:` field inside `SKILL.md` exactly. If you renamed the directory, rename the name field — or vice versa. [This is enforced by the skill loader](https://code.visualstudio.com/docs/copilot/customization/agent-skills).

**The agent gets the answer confidently wrong.** Expected. That is why the skill's "Verification" section exists. Always verify.

**It's too slow.** Switch to a faster model with `hermes model`. Some cheaper models are also faster.

## Before you close this doc

Write down, somewhere you will find again:

- The LLM provider you signed up with
- The default model you chose
- Where your OpenRouter API key is stored (ideally in a password manager, not in a text file)
- Which colleague is the backup person for this install

If those four things aren't written down, the person who installed Hermes *is* the documentation, which is the opposite of what we're trying to do.

[Next: The handover playbook →](./07-handover-playbook.md)
