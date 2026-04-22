---
name: ngo-bilingual-thankyou
description: Drafts a donor thank-you message in Arabic and English for a GCC nonprofit. Use when the user provides donor details (name, amount, campaign, language preference) and wants a short, warm, jurisdiction-aware acknowledgement. Produces parallel AR/EN text with appropriate honorifics, Hijri-calendar awareness during Ramadan, and a clean separation between standard text and organisation-specific details.
version: 1.0.0
metadata:
  hermes:
    tags: [nonprofit, communications, arabic, bilingual, donor-stewardship, gcc]
    category: nonprofit
  author: raja-shahnawaz-soni
  license: MIT
---

# NGO Bilingual Donor Thank-You

## When to Use

Use this skill when:

- A donor has contributed to a GCC-based nonprofit and the organisation wants to send a short thank-you message
- The organisation operates in a context where Arabic and English are both expected (UAE, KSA, Bahrain, Kuwait, Qatar, Oman)
- The message needs to be warm and specific but does not need to be a formal receipt (for zakat receipts specifically, use the separate `ngo-zakat-receipt` skill once available)

Do NOT use this skill for:

- Formal contractual acknowledgements (use legal review)
- First-contact communications with donors you have not engaged before (those need a real human touch)
- Condolence or bereavement-related donations — those require direct, human drafting

## Quick Reference

**Inputs the skill needs:**
- Donor name (first name, family name if known, preferred title if known)
- Donation amount and currency
- Campaign or programme the donation supports
- Donor's preferred language: `arabic`, `english`, or `both` (default: `both`)
- Formality level: `formal`, `warm`, or `plain` (default: `warm`)
- Channel: `email`, `whatsapp`, `sms`, or `letter` (default: `email`)
- Organisation name (fictitious for testing; real only in production)
- Season awareness flag: whether the message should acknowledge Ramadan, Eid, or other relevant context

**Output:**
- A single message block with AR and EN in the requested format
- A brief rationale note for the sender: what the message does and doesn't say, and any edits they should consider before sending

## Procedure

1. **Clarify missing inputs.** Ask the user for any of the required inputs above that are not provided. Ask all missing items in one message — do not interrogate across multiple turns.

2. **Determine the honorific.** For Arabic output:
   - If donor name is recognisably male → السيد / الأستاذ (Mr. / Ustaadh)
   - If donor name is recognisably female → السيدة / الأستاذة (Mrs. / Ustaadha)
   - If ambiguous → ask the user; do not guess
   - If donor holds a title (Sheikh, Sheikha, Dr., Eng., His/Her Excellency) and it was provided → use it; do not invent titles

3. **Determine the seasonal framing.** Check whether the current date falls within:
   - Ramadan → open with Ramadan-appropriate greeting; reference the spirit of giving
   - Eid al-Fitr / Eid al-Adha → open with Eid greeting; acknowledge the season
   - The first ten days of Dhul Hijjah → acknowledge the spirit of the days
   - UAE National Day, Saudi National Day, or other GCC national day → optional, if donation timing suggests relevance
   - Otherwise → no seasonal framing

   Verify the current Hijri date if unsure. Do not invent seasonal context.

4. **Draft in English first.** Structure:
   - Greeting with name and (if applicable) title
   - Explicit acknowledgement of the donation amount and what it supports
   - One specific line on what the donation enables (avoid generic "makes a difference" language)
   - Closing with organisation name and (if known) signatory
   - Maximum 80 words for email/letter, 40 words for WhatsApp/SMS

5. **Draft in Arabic as a parallel translation, not a word-for-word rendering.** Arabic donor communications have their own conventions:
   - Open with بسم الله الرحمن الرحيم only if the organisation's house style uses it consistently — otherwise omit
   - Use formal supplications appropriate for donor acknowledgement: جزاكم الله خيراً, بارك الله فيكم, تقبل الله منكم
   - Keep tone elevated but not stiff
   - Use MSA (Modern Standard Arabic), not Gulf dialect — donors of any Arabic-speaking background should read it comfortably

6. **If channel is WhatsApp or SMS**, produce shorter versions (40 words max each language). Do NOT include signatures or org name repetition — the channel tells the recipient who sent it.

7. **Append a sender's note** clarifying:
   - What the message assumes (e.g. "assumes donor is male based on name — verify before sending")
   - What it deliberately does not claim (e.g. "no claim of tax-deductibility made — add if your jurisdiction supports it")
   - Suggested customisations the user should consider

8. **Return** the drafts in a clear layout:
   ```
   === ENGLISH ===
   [English message]

   === العربية ===
   [Arabic message]

   === SENDER'S NOTE ===
   [rationale and suggestions]
   ```

## Pitfalls

- **Guessing gender from names.** Many Arabic names are unambiguous; many are not. Names common in the Subcontinent, East Africa, and the Philippines are frequently misread. When unsure, ask.

- **Machine-translated Arabic.** LLMs in 2026 produce Arabic that is usually grammatical and often feels slightly off — stilted syntax, odd register mixing, or unnecessary formality. Always have the first few uses reviewed by a fluent Arabic speaker in your team. Refine the skill's examples based on their feedback.

- **Inventing tax-deductibility claims.** Tax treatment of donations varies by jurisdiction and by the donor's residency. This skill does NOT claim deductibility. Do not edit it to do so unless you have verified the claim is correct for the specific donor.

- **Wrong Hijri date.** Do not state a Hijri date unless you have verified it. If the current Hijri date is needed, either use a verified source or leave it out.

- **Ramadan timing.** Ramadan dates shift by ~11 days each year. Do not hardcode. If seasonal framing is requested, check the current date against the known Ramadan start date for the current Hijri year.

- **Real brand names in examples.** All examples and test fixtures in this skill use fictitious organisation names. Do not edit in real names during testing — it leaks into agent memory.

## Verification

After drafting, the user should check:

1. **Name is spelt correctly.** Arabic spellings of transliterated names vary; if the donor has a preferred spelling, use that.
2. **Amount and currency are correct.** Mismatched currency is a common error in bilingual drafts.
3. **Seasonal framing matches reality.** If the skill drafted a Ramadan greeting, verify the current date actually falls within Ramadan.
4. **Arabic renders right-to-left in the channel being used.** Some WhatsApp clients and email clients handle mixed-direction text poorly. If the output looks broken, copy into a simple text editor first.

## Test this skill

Sample input:

> Draft a warm thank-you email, both languages, for:
> - Donor name: Fatima Al-Hosani (female, use "Ustaadha")
> - Amount: AED 2,500
> - Campaign: Back-to-school programme for Grade 1-3 students
> - Organisation: Al-Noor Charitable Foundation (fictitious example)
> - Signatory: Programme Director
> - Seasonal framing: none (not currently Ramadan)

Expected shape of output: An English paragraph of roughly 50-70 words using "Ustaadha Fatima" and referencing the back-to-school programme specifically (not generically). An Arabic parallel using الأستاذة فاطمة, the donation amount, and a supplication-style closing. A sender's note that does not flag any assumptions because all inputs were explicit.

A fluent Arabic speaker reviewing the output should be able to say "I would send this without edits" or "change X to Y." If that bar is not being met, the skill's Procedure section needs tuning — open an issue.
