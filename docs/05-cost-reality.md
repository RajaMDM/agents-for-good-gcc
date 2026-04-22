# Cost reality

Hermes Agent is free. The LLM calls the agent makes are not. This document gives you a practical sense of what you will actually pay, what drives the cost, and how to keep it under control.

All prices below are **indicative only** and based on published rates as of this repo's creation. Verify current pricing before budgeting — LLM API costs move almost every month.

## The short version

For a small nonprofit running one or two skills a day on cost-efficient models, you should budget **USD 10–40 per month** in LLM costs.

For a moderately active install — several users, a few skills running daily, some multi-step agentic workflows — budget **USD 40–100 per month**.

If you route everything through a frontier model like Claude Opus or GPT-5 on a heavy agentic workload, budgets can escalate quickly; [reports cite heavy use on Claude Opus reaching USD 131 per day in extreme cases](https://dev.to/jangwook_kim_e31e7291ad98/hermes-agent-review-self-improving-open-source-ai-agent-3kk3). That is not a nonprofit budget. Stay on the cost-efficient tier unless you have a specific reason not to.

## What drives cost

A small number of factors control almost all your spend.

### 1. Which model you use

Hermes is model-agnostic. You configure a provider and a model, and the agent uses it for everything unless you override per-task. Rough cost hierarchy, cheapest to most expensive:

| Tier | Example models | Relative cost | When to use |
|---|---|---|---|
| Local (zero API cost) | Ollama with Llama 3, Qwen, Mistral | Free (your electricity) | Sensitive data, development, simple tasks |
| Budget cloud | Gemini Flash, DeepSeek V3, Qwen 2.5, GPT-4o-mini | 1× | Default for most NGO work |
| Mid-tier | Claude Haiku, GPT-4o, Gemini Pro | 3–10× budget | When quality matters for end-user-facing text |
| Frontier | Claude Opus, GPT-5, Gemini Ultra | 30–100× budget | Rare — only for specific tasks |

**Recommendation for NGO installs:** start on a budget cloud model. Route specific high-quality tasks (grant applications, formal donor letters) to a mid-tier model if needed.

### 2. Context size per call

Agents send a lot of context on every call — system instructions, conversation history, tool schemas, loaded skills. This is why agentic workloads cost more per-task than a simple chatbot exchange of the same length.

Mitigations built into Hermes:

- Skills use **progressive disclosure** — [only names and descriptions are in the system prompt; full skill content loads only when needed](https://hermes-agent.nousresearch.com/docs/guides/work-with-skills)
- Conversation summarisation — older history is summarised rather than sent verbatim
- Subagents — [isolated subagents for sub-tasks, which run with their own context and don't add to the main conversation's token count](https://hermes-agent.nousresearch.com/)

You do not need to tune this manually — the defaults are reasonable. Just be aware it's why a "simple" agent task can cost more than a simple chatbot reply.

### 3. How chatty you let the agent be

The agent is a tool. If you let it ask for clarification three times before starting, you pay for all three turns. If you give it a clear, complete instruction in one message, you pay for fewer round trips. This is user-level behaviour, not a tuning knob.

### 4. Scheduled / cron tasks

Hermes can run scheduled tasks — daily reports, weekly digests. Each run costs what that run's tokens cost. If you set up a scheduled task that runs every hour and pulls in a lot of context, the monthly bill adds up. Cron is useful but audit it regularly.

## Budget paths by NGO profile

### Profile A: One skill, one user, cost-efficient

- Model: DeepSeek V3 or Gemini Flash via OpenRouter
- Usage: 20–30 light tasks per day
- Expected monthly cost: **USD 5–20**
- Suitable for: single-skill installs like bilingual thank-yous only

### Profile B: Two or three skills, small team, mixed model

- Primary model: Gemini Flash or Claude Haiku for most tasks
- Escalation model: Claude Sonnet or GPT-4o for grant drafting and formal letters
- Usage: 50–100 tasks per day across team
- Expected monthly cost: **USD 30–80**
- Suitable for: most small NGO installs

### Profile C: Heavy agentic workflow, multi-step tasks, messaging gateway

- Primary model: Claude Sonnet or GPT-4o
- Scheduled tasks running daily
- Team using WhatsApp / Telegram gateway
- Expected monthly cost: **USD 80–200**
- Suitable for: orgs that have decided this is core operational tooling
- **Caveat:** at this level, you need a named owner and a monthly review of usage

## Alternatives to hosted LLMs

Local model inference via Ollama or vLLM runs on your own hardware. No per-call cost. Trade-offs:

- **Quality** — local open-weights models in 2026 are good for many NGO tasks (summarisation, translation, drafting) but still behind frontier models on complex reasoning and long-context work.
- **Hardware** — running a useful local model needs a machine with a decent GPU or an Apple Silicon Mac with enough unified memory. A second-hand M1/M2 Mac Mini is a workable starting point.
- **Maintenance** — somebody needs to update the local model, keep the Ollama server running, and debug it when it stops.

**When local is the right call:**

- Workflows with beneficiary PII that cannot leave your jurisdiction
- Organisations with a volunteer who can maintain a local install
- Orgs where the monthly API bill is genuinely unaffordable

Hermes supports both in the same install — you can route sensitive tasks to a local model and non-sensitive tasks to a cloud model. This is the pattern most mature installs end up using.

## How to keep the bill under control

1. **Start on the cheapest usable model.** Upgrade only when a specific task's output quality is unacceptable.
2. **Set a monthly budget cap** on your LLM provider account. OpenRouter, Anthropic, and OpenAI all support this. Set it and walk away.
3. **Review usage monthly.** Not quarterly. Monthly. The provider dashboards show you which tasks are burning tokens.
4. **Audit scheduled tasks quarterly.** Kill any that aren't earning their cost.
5. **Be skeptical of "the agent figured it out autonomously over 47 tool calls"** narratives. That is expensive. A well-scoped skill that does the job in 3–5 tool calls is what you want.

## What I would do

If I were installing this for a small NGO from scratch, with a limited budget, today:

1. Install Hermes on an existing laptop (Mac or Linux).
2. Sign up for OpenRouter with the free tier plus a USD 20 top-up.
3. Configure Hermes to use `google/gemini-2.5-flash` or `deepseek/deepseek-chat` as the default model.
4. Install one skill. Run it for two weeks on one real workflow. Measure hours saved.
5. Check OpenRouter dashboard. Calibrate expectations on cost per task.
6. Only then decide whether to install a second skill, add a messaging gateway, or start scheduling.

Keep it small until it earns the right to be bigger.

[Next: Installing Hermes →](./06-installing-hermes.md)
