# Workflows

Four standard journeys. Each gives the calls to make, in order, and a budget. Stop as soon as you can answer; the budget is a ceiling, not a target. A whole question should rarely need more than 4 calls.

Before any journey: if you already hold the document identifier and the text from an earlier call in this conversation, reuse them. Do not fetch them again.

## 1. Find an article of a customs code

Budget: 1 to 3 calls.

1. Identify the code. If the user named a country or community and you do not know the `code_id`, call `lex_get_catalog` with `domain: "codes"` (once) and pick the entry by `country` and `year`. If several versions exist, take the most recent one in `production` and say which one you used.
2. Then, depending on what the user gave:
   - an article number: `lex_get_article` with `numero`;
   - several numbers: `lex_get_articles_by_numbers`;
   - a topic: `lex_semantic_search` with `code_id` and a query written in the language of the code, then `lex_get_article` (or `lex_get_articles_by_numbers`) for the one or two best hits.
3. Quote the article and cite it (see `citation-and-versions.md`).

Notes:
- A search snippet is an extract. Read the article before quoting it or drawing a conclusion from it.
- If `homonyms` or `ambiguous` comes back, choose by `contexte` and tell the user which article you kept.
- To compare the same rule in two countries, run step 2 once per code; do not search without `code_id`.

## 2. Read a tariff line and its rates

Budget: 1 to 2 calls.

1. The user gives a tariff or HS code: call `lex_hs_lookup` with `hs_code` and `tec_org` (the community of the country concerned). One call returns the lines, their rates, the meaning of each tax and the HS note.
2. The user describes goods without a code: call `lex_search_tec` with `tec_id` if you know it, then `lex_hs_lookup` on the best code.
3. Report the rates exactly as returned, with the name of each tax taken from the tax definitions. Do not compute an amount of duties unless the user asks, and if you do, show the calculation and say it is an estimate that ignores exemptions, national taxes and preferential regimes.

Notes:
- If the user does not say which tariff applies, ask or state your assumption; rates differ between communities.
- A short code (2, 4 or 6 digits) returns several lines. Present them as a list; do not pick one silently.
- `found: false` on the tariff side means the code does not exist in that tariff: say so, do not guess a neighbouring line.

## 3. Classify goods in the Harmonized System

Budget: 2 to 4 calls.

1. Call `lex_search_sh` with a description of the goods (what it is, what it is made of, what it is used for).
2. Read the one or two most plausible headings with `lex_get_sh_position` (`sh_id` and `code` come from the search results). Check the notes: they include and exclude goods explicitly.
3. If the choice between two headings depends on a General Interpretative Rule, apply the rule; read its text with `lex_get_sh_position` (`node_id` `rgi-1` to `rgi-6`) only if you need to quote it.
4. If the user also wants the duties, finish with `lex_hs_lookup` on the retained code.

Notes:
- Present the result as a reasoned proposal: heading, the note or rule that supports it, the alternatives you ruled out and why.
- Always say that only the customs administration can issue a binding classification decision.
- If the description is too vague to choose (material, use or presentation unknown), ask the user before spending more calls.

## 4. Read a customs valuation instrument

Budget: 2 calls.

1. Call `lex_search_valuation` with the question (for example royalties, related parties, commissions, transport costs).
2. Read the best instrument with `lex_get_valuation_instrument`, passing the `identifier` and the `category` returned by the search.
3. Explain what the instrument says and cite it by its category, its identifier and its title.

Notes:
- These instruments are WCO doctrine on the WTO Valuation Agreement. They guide interpretation; the applicable rule is in the national or community customs code, which you can find with journey 1.
- They never give a customs value. Do not present a computed value as coming from Lex Duana.

## Saving calls

- Batch: several articles of one code go in one `lex_get_articles_by_numbers` call.
- Prefer `lex_hs_lookup` to the sequence search, tariff line, rates.
- Do not browse (`lex_browse_code`, `lex_list_children`, `lex_browse_sh`) to find a topic; search instead. Browse only when the user asks for an outline.
- Do not re-read a text to "double-check" it: the result you hold is the published text.
- When a question is broad ("everything about transit in three countries"), tell the user how many calls it needs and agree on a scope first.
- When the quota is nearly used up or exhausted, say it and answer with what you already hold (see `errors-and-limits.md`).
