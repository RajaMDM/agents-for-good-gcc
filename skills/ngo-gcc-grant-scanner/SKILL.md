---
name: ngo-gcc-grant-scanner
description: Scans GCC-region grant, CSR, and foundation funding opportunities matching a nonprofit's cause, geography, and stage. Use when the user wants a short-list of active funding calls to pursue. Produces a ranked list with source URLs, deadlines, and a brief first-pass fit assessment. Does not invent grants or claim a deadline is active without verification. Requires web search capability configured in Hermes (Tavily, Parallel, or similar).
version: 1.0.0
metadata:
  hermes:
    tags: [nonprofit, fundraising, grants, research, gcc]
    category: nonprofit
  author: raja-shahnawaz-soni
  license: MIT
required_environment_variables:
  - TAVILY_API_KEY  # or PARALLEL_API_KEY — depending on which search backend is configured
---

# GCC Grant Scanner

## When to Use

Use this skill when:

- The user's organisation is looking for grant or CSR funding opportunities
- They can describe their cause, geography, and stage clearly
- They want a short-list of current opportunities to assess, not a long list of historical grants
- They understand this skill is doing research, not guaranteeing eligibility

Do NOT use this skill for:

- Producing the actual grant application (use a drafting skill once available, and always with human review)
- Anything that assumes eligibility without the user verifying it with the funder
- Funders outside the GCC region unless the user explicitly asks for wider scope

## Quick Reference

**Inputs the skill needs:**
- Cause category: e.g., `migrant-worker-welfare`, `education`, `women-and-children`, `health`, `environment`, `animal-welfare`, `faith-based-relief`, `youth-development`
- Primary country(ies) of operation within the GCC
- Stage: `seed`, `early`, `scaling`, `established`
- Grant size sought: rough USD range (e.g., USD 10k-50k)
- Organisation type: `registered-nonprofit`, `association`, `foundation`, `community-group-unregistered`
- Any specific exclusions: funders to avoid (e.g., "no alcohol-industry CSR")
- Time horizon: `due-this-month`, `due-this-quarter`, `due-this-year`

**Output:**
- A ranked list of 5-10 opportunities
- For each: funder name, opportunity name, URL, deadline, typical grant size, fit assessment
- A "not yet verified" section for leads that need confirmation
- A note on sources used and what was searched

## Procedure

1. **Build a search plan.** Before running any searches, list the types of sources to check:
   - Official government regulators' grant programmes (e.g., UAE Community Development Authority, KSA Ministry of Human Resources)
   - Sovereign foundation programmes (e.g., Emirates Foundation, Al Jalila Foundation, King Khalid Foundation)
   - Major corporate CSR funds
   - Embassy-linked community funds for migrant community support
   - Regional Islamic finance and zakat-based programmes
   - Multilateral or bilateral funders with GCC country offices
   - Verify each source type is applicable to the user's cause; skip non-applicable types

2. **Run targeted web searches.** For each source type:
   - Use specific queries including the cause, country, and "grant" / "funding" / "call for proposals"
   - Cross-reference multiple searches before accepting a lead
   - Prefer results dated within the last 6 months — older calls may be closed

3. **For each candidate opportunity, extract:**
   - Funder name (official name, not media shorthand)
   - Opportunity / programme name
   - Source URL (the actual page, not a news summary)
   - Opening and closing dates (if stated)
   - Stated typical grant size
   - Stated eligibility — country, org type, cause
   - Stated application requirements — audited financials, registration proof, cofunding, etc.

4. **Verify the opportunity is active.** An opportunity that is mentioned in a news article from 18 months ago is not usable. Ways to verify:
   - Visit the funder's official page
   - Look for an explicit "applications open until" or similar
   - Check if there's a newer article describing winners of the last cycle (the next cycle may or may not be open)
   - If active status is uncertain, flag it clearly in the output — do not bury the uncertainty

5. **Assess fit.** For each verified opportunity, write a one-paragraph fit assessment covering:
   - **Cause alignment** — does it match the user's cause clearly, or is it a stretch?
   - **Geography** — does the funder work in the user's country?
   - **Stage** — is the funder known for seed/early grants, or only for established orgs?
   - **Size** — does the typical grant size match what the user is seeking?
   - **Process** — is the application process lightweight or does it require audited financials and a three-year track record?
   - **Risk flags** — anything that might make it a bad fit (political sensitivity, exclusion criteria, conflict with org values)

6. **Rank the list.** Order by overall fit (strongest first). Use a simple rubric:
   - Strong fit: all alignment factors match, process proportional to grant size
   - Moderate fit: 3 of 5 alignment factors match, process manageable
   - Weak fit: 2 or fewer alignment factors match, or process is very heavy relative to grant size

7. **Produce a "leads to verify" section.** Any opportunity that came up in search but couldn't be confirmed active goes here, with a note on what verification step the user should take.

8. **State the sources used.** List the searches run and the number of results reviewed. Be transparent about what was searched and what wasn't. This is how the user knows whether to run the skill again with different parameters.

## Pitfalls

- **Hallucinated grants.** This is the single biggest risk in this skill. LLMs will confidently describe grant programmes that don't exist, mix up funders, or quote deadlines that passed months ago. Every opportunity in the output MUST have a real, verifiable URL. If you cannot find a URL that confirms the opportunity exists and is active, it does not go in the list — it goes in "leads to verify" with an explicit verification step.

- **Stale news articles as primary source.** A news article from 2024 describing a grant programme is not evidence the programme is running in 2026. Always follow through to the funder's official page.

- **Mixing up similar names.** Several GCC foundations have similar names. "Foundation X" and "X Foundation" and "The X Charitable Foundation" may be three different organisations. Do not assume — verify the exact legal name.

- **Regional eligibility confusion.** A GCC-headquartered funder may only fund projects in its own country. A "Middle East and North Africa" fund from a Western donor may have eligibility restrictions that exclude GCC countries. Read the eligibility text, don't infer from the fund's name.

- **Zakat / Islamic finance confusion.** Not every zakat-funded programme accepts applications from all types of organisations. Some are restricted by school of jurisprudence, some are restricted by the type of beneficiary. Do not assume a Muslim-serving nonprofit is automatically eligible for every zakat-funded programme.

- **Language of the funder.** Some GCC funders accept applications only in Arabic. Flag this in the fit assessment — it changes the effort required.

## Verification

After running the skill, the user should:

1. Click every URL in the output. Every one. If a link 404s or goes to a parked domain, the skill hallucinated or the programme is dead.
2. For the top 3 opportunities, visit the funder's home page and confirm the programme is listed there (not just on a third-party aggregator).
3. For any opportunity the user plans to apply to, email or call the funder to confirm status before committing effort.
4. Cross-check at least one opportunity with a colleague familiar with the sector — the reality check often catches subtle fit issues the skill will miss.

## Test this skill

Sample input:

> Cause: migrant-worker welfare
> Country: UAE, with secondary focus on KSA
> Stage: early
> Size sought: USD 25k-100k
> Org type: registered-nonprofit
> Exclusions: none
> Time horizon: due this quarter

Expected shape of output:

- A ranked list of 5-10 candidate opportunities
- Every opportunity has a funder name, programme name, URL, deadline, size, and fit paragraph
- A "leads to verify" section with any opportunities whose active status was uncertain
- A sources summary at the bottom listing what was searched

If the output contains any URL that 404s, any deadline that is in the past without being flagged, or any opportunity that is demonstrably not real on the funder's own website — the skill failed. File an issue.

## Maintenance note

GCC grant and CSR landscapes change. Foundations restructure, government programmes get renamed, corporate CSR priorities shift after leadership changes. This skill is not a replacement for building relationships with local intermediaries who track this for a living. Think of it as a starting point, not the end of the research.
