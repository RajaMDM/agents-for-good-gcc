---
name: ngo-monthly-impact-report
description: Turns a structured spreadsheet of monthly programme data into a readable, honest impact report for a GCC nonprofit board or funder. Use when the user has a CSV or XLSX file of programme metrics and wants a narrative report that summarises activity, highlights change against prior month, and flags anomalies. Produces a draft in markdown with optional Arabic summary. Does not invent data or inflate claims.
version: 1.0.0
metadata:
  hermes:
    tags: [nonprofit, reporting, data, board-reporting, gcc]
    category: nonprofit
  author: raja-shahnawaz-soni
  license: MIT
required_environment_variables: []
---

# NGO Monthly Impact Report

## When to Use

Use this skill when:

- The user has a spreadsheet (CSV, XLSX, or Google Sheets export) with monthly programme data
- They want a narrative impact report aimed at a board, a funder, or a trustee group
- The report needs to summarise what happened, compare against prior periods, and flag things worth attention
- The user has about 15-20 minutes to review the draft before sending

Do NOT use this skill for:

- Audited financial statements (those need a qualified accountant)
- Regulator-facing compliance returns (format-specific; use the applicable compliance skill once available)
- Reports that make scientific or medical claims (those need subject-matter review)
- Any report that will be published without review

## Quick Reference

**Inputs the skill needs:**
- A spreadsheet file (CSV or XLSX) with one row per metric or one row per day/week
- The reporting period (e.g., "March 2026")
- The prior period to compare against (e.g., "February 2026")
- The target audience: `board`, `funder`, `community`, or `internal`
- Optional: a short free-text prompt about context — e.g., "Ramadan fell in this month" or "we ran an emergency campaign from the 10th"
- Optional: an Arabic summary flag — produces a ~150-word executive summary in Arabic in addition to the English report

**Output:**
- A markdown report with sections: Headline, Activity Summary, Month-over-Month Change, Notable Signals, Things We Do Not Yet Know
- An optional Arabic executive summary
- A data appendix listing the metrics used, exactly as read from the file
- A list of caveats and verification items for the user to check before sending

## Procedure

1. **Read the file.** Accept CSV, XLSX, or a Google Sheets URL (the user will need to have made the sheet viewable). Extract the tabular data. If the structure is ambiguous (multiple tables in one sheet, merged cells, headers not in row 1), ask the user to clarify — do not guess.

2. **Validate the data.** Before writing anything, verify:
   - All required columns for the reporting period are present
   - All required columns for the comparison period are present
   - Numeric columns parse as numbers (flag any that don't)
   - No obvious impossible values (negative headcounts, 1500% changes that look like unit errors)

   If validation fails on any point, report the problem to the user and stop. Do not produce a report on bad data.

3. **Summarise activity.** For each metric in the data:
   - State the absolute value for the reporting period
   - State the prior-period value
   - State the absolute change and the percentage change
   - Flag metrics where the percentage change is larger than 25% in either direction

   Use only the numbers present in the file. Do not extrapolate, project, or infer numbers not in the data.

4. **Identify notable signals.** From the changes above, select the three most notable:
   - Largest positive change against prior period
   - Largest negative change against prior period
   - Any metric that flips sign (e.g., net volunteer growth goes from +10 to -5)

   Write one paragraph per signal. Name the signal, give the numbers, and note what an informed reader might want to ask next. Do NOT editorialise about whether this is "good" or "bad" unless the user's context prompt made clear.

5. **Write the headline.** One sentence. Factual. No superlatives unless clearly warranted by the data. "Activity rose across all programmes" if and only if literally all programmes saw positive movement.

6. **Write 'Things We Do Not Yet Know'.** This section is mandatory and must not be skipped. List at least two items that the data cannot answer but that a reader might wonder about. Examples:
   - "Why volunteer retention dropped 30% — the data shows the drop but not the cause"
   - "Whether the surge in beneficiary intake was driven by the Ramadan awareness campaign or by seasonal patterns — this would require intake-source data we don't track yet"

   This section exists to prevent the report from overclaiming. Its presence signals honesty to a board or funder.

7. **If Arabic summary is requested**, produce a 150-word executive summary in Modern Standard Arabic. Same content, tighter form. Do not translate the full report — it is almost always too long and loses force.

8. **Assemble a data appendix**. A short table listing every metric that appeared in the report, the value, the prior-period value, and the source cell reference from the file (if extractable). This is so the reader can trace any number in the report back to the data.

9. **Write a caveat list** for the sender. Examples:
   - "The Arabic summary is machine-drafted and should be reviewed by a fluent speaker before sending"
   - "Any monetary figures shown are as they appeared in the file — verify against accounting records"
   - "The 'Things We Do Not Yet Know' section is important — do not delete it without replacing it with its content"

## Pitfalls

- **Confidently wrong numbers.** LLMs can paraphrase numbers incorrectly, especially when units are implicit. Verify every number in the draft against the spreadsheet before sending. Always.

- **Inventing context.** If the user did not provide a context prompt, the skill should not invent context. Do not say "this growth reflects the Ramadan season" unless the user told you Ramadan fell in that month.

- **Hallucinating trend language.** "Strong growth," "significant improvement," and "notable decline" are editorial. Use them sparingly and only when the numbers clearly justify them. A 3% change is not "significant."

- **Messy source files.** Many NGO spreadsheets have merged cells, multiple tables on one sheet, and headers spread across two rows. The skill should not attempt to infer structure — it should stop and ask.

- **Arabic summary quality.** As with the bilingual thank-you skill, Arabic output needs human review. Flag this explicitly.

- **Board vs funder framing.** A board wants signals and decisions; a funder wants impact attributable to their funding. If the user selected `funder`, emphasise the programmes the funder supports and do not claim credit for activities outside those programmes.

## Verification

After drafting, the user should:

1. Open the source spreadsheet alongside the report. Pick three numbers in the report at random. Verify each one against the spreadsheet.
2. Read the "Things We Do Not Yet Know" section. Ask: would a sceptical trustee agree that these are honest gaps?
3. If the Arabic summary is included, have a fluent Arabic-speaking colleague skim it. Not full review — just skim. If anything feels off, remove it from this draft.
4. Check the data appendix. Every number should be traceable to a cell in the source file.

## Test this skill

Sample input:

> File: `sample-march-2026.csv` (structure: metric name, March 2026 value, February 2026 value, notes)
> Reporting period: March 2026
> Comparison period: February 2026
> Audience: board
> Context prompt: "Ramadan fell in the first two weeks of March. We ran a food basket distribution."
> Arabic summary: yes

Expected shape of output:

- A headline (one sentence, factual)
- Activity summary for each metric in the file
- Three notable signals with paragraphs
- A "Things We Do Not Yet Know" section with at least two items
- A 150-word Arabic executive summary
- A data appendix table
- A caveat list with at least three items

If the output contains any number not traceable to the source file, the skill failed. File an issue.
