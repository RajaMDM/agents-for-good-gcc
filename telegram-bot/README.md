# HERMES Telegram Bot

A Telegram bot that gives you mobile access to the HERMES agents-for-good skill
library. Runs locally on your machine (macOS, Apple Silicon). No cloud hosting
required.

## What it does

Each HERMES skill becomes a Telegram command. You can invoke agents by command or
just type naturally — the bot routes your message to the right agent automatically.

| Command | Agent | What it does |
|---------|-------|-------------|
| `/thankyou` | Bilingual Donor Thank-You | Draft warm donor acknowledgements in Arabic + English |
| `/report` | Monthly Impact Report | Turn programme data into a board-ready narrative report |
| `/grants` | GCC Grant Scanner | Find active grant and CSR opportunities across the GCC |
| `/triage` | Beneficiary Intake Triage | Classify intake entries by urgency for caseworkers |
| `/social` | Social Media Bilingual Content | Create bilingual posts for Instagram, Twitter, LinkedIn |
| `/help` | HERMES Assistant | General guidance and skill navigation |
| `/status` | — | Show current session and active agent |
| `/reset` | — | Clear session context and start fresh |

## Prerequisites

- Python 3.11 or later
- A Telegram bot token (from [@BotFather](https://t.me/BotFather))
- An Anthropic API key ([console.anthropic.com](https://console.anthropic.com))

## Setup

### 1. Create and activate a virtual environment

```bash
cd ~/Documents/agents-for-good-gcc/telegram-bot
python3 -m venv .venv
source .venv/bin/activate
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure secrets

```bash
cp .env.example .env
```

Open `.env` and fill in:
- `TELEGRAM_BOT_TOKEN` — from @BotFather
- `ANTHROPIC_API_KEY` — from [console.anthropic.com](https://console.anthropic.com)
- `ADMIN_USER_IDS` — your Telegram user ID (find it by messaging [@userinfobot](https://t.me/userinfobot))

### 4. Run the bot

```bash
python bot.py
```

You should see:
```
Starting HERMES Telegram Bot…
Model (agents): claude-sonnet-4-6
Model (router): claude-haiku-4-5-20251001
Admin user IDs: {your_id}
Bot is running. Press Ctrl+C to stop.
```

Open Telegram and send `/start` to your bot.

### 5. Keep it running (optional)

To run in the background and auto-restart:

```bash
# Using nohup (simple)
nohup python bot.py > hermes-bot.log 2>&1 &

# Or using screen
screen -S hermes-bot
python bot.py
# Detach with Ctrl+A, D
```

## Usage

### Slash commands
Type `/thankyou`, `/report`, `/grants`, `/triage`, or `/social`. The bot activates
the relevant agent and tells you what information it needs.

### Natural language
Just type what you need:
- *"I need to write a thank you to a donor who gave AED 5,000"* → routes to `/thankyou`
- *"Help me write the board report for March"* → routes to `/report`
- *"Find us some grant funding for education in the UAE"* → routes to `/grants`

### File uploads (CSV for reports)
For the `/report` agent, you can upload a `.csv` or `.tsv` file directly. The bot
reads it and passes the content to the report agent. Excel files: export as CSV first.

### Session management
- Each user session maintains conversation context (up to 20 messages).
- Switching agents via command clears the previous context.
- `/reset` clears everything and returns to neutral.

## Model selection

The bot uses two Claude models:

| Role | Default model | Notes |
|------|--------------|-------|
| Skill agents | `claude-sonnet-4-6` | Good Arabic quality, reasonable cost |
| Intent router | `claude-haiku-4-5-20251001` | Fast and cheap — only classifies intent |

To improve Arabic output quality, change `CLAUDE_MODEL=claude-opus-4-7` in `.env`.
Expect higher API costs (~5–10x vs Sonnet).

**Estimated cost:** Light personal use (< 50 messages/day) = USD 2–8/month on Sonnet.

## Security

- The bot is admin-whitelisted — only Telegram user IDs in `ADMIN_USER_IDS` can interact.
- `.env` is gitignored and must never be committed.
- Beneficiary PII: the triage agent explicitly instructs users to use anonymised
  descriptors. No data is stored beyond the in-memory session (which clears on restart).
- All outputs are drafts for human review — the bot does not send anything on your behalf.

## Architecture

```
bot.py          Telegram handlers and message routing
agents.py       Agent definitions — system prompts derived from SKILL.md files
router.py       Intent classification via Claude Haiku
config.py       Environment variable loading and validation
```

Message flow:
1. Telegram message arrives → `bot.py` handler fires
2. If a command: switch agent, send welcome message
3. If natural language: `router.py` classifies intent via Claude Haiku
4. If a specialist agent detected: auto-switch and invoke
5. `agents.py` sends message + conversation history to Claude via Anthropic SDK
6. Reply split into chunks if needed, sent back to Telegram

## Data protection

This bot is intended for single-admin use by the account owner. Before using with
beneficiary data, review:
- `docs/03-when-not-to-use.md` — hard stops and soft cautions
- `docs/04-data-protection-gcc.md` — GCC-specific legal frameworks

The triage agent contains explicit safeguards: any safeguarding signal (child,
domestic violence, self-harm) is flagged for human review only.

## Troubleshooting

**Bot doesn't respond**
- Check the terminal for error messages
- Confirm your Telegram user ID is in `ADMIN_USER_IDS`
- Verify `TELEGRAM_BOT_TOKEN` is correct

**API errors from Anthropic**
- Confirm `ANTHROPIC_API_KEY` is valid and has credit
- Check [status.anthropic.com](https://status.anthropic.com) for outages

**Arabic text renders incorrectly in Telegram**
- This is a Telegram client rendering issue with mixed-direction text
- Copy the Arabic text into a plain text editor and it should render correctly
- On iOS/Android Telegram clients, rendering is generally fine

---
*Part of the [agents-for-good-gcc](https://github.com/raja-soni/agents-for-good-gcc) repository.*
*Built by Raja Shahnawaz Soni.*
