# Citation and versions

## What a citation contains

Every legal statement carries, next to it or in a short list of sources at the end:

1. **The document**: its title as returned by `lex_get_catalog` (or, if you did not fetch the catalog, its identifier), with the country or community.
2. **The provision**: the article number for a customs code; the tariff code for a tariff line; the heading code for the Harmonized System; the category and identifier for a valuation instrument.
3. **The version of the document**: `year` for a customs code, `edition_year` for a tariff, `version` for the Harmonized System. These fields come from the catalog entry of the document.
4. **The status**, only when it is `staging`: say that the document is not yet validated for publication in Lex Duana.

Short examples of form (the content is illustrative):

- Customs code: "Customs Code of Togo (2018), article 20 bis."
- Tariff: "ECOWAS Common External Tariff (2022 edition), line 0101.21.00.00."
- Harmonized System: "Harmonized System 2022, heading 01.01, explanatory note."
- Valuation: "WCO advisory opinion 1.1."

Keep `content_hash` out of the prose unless the user asks for a verifiable reference; give it then, exactly as returned.

## Rules

- **No source, no statement.** If you did not read it in a tool result during this conversation, do not present it as the law. You may add general background from your own knowledge only if you label it clearly as such and keep it apart from the cited text.
- **Quote, then explain.** Quote the decisive sentence in its original language, in quotation marks, then explain it in the user's language. Do not translate a legal text and present the translation as the text. Keep quotations short: quote the sentences that answer the question, not the whole article.
- **Read before you quote.** A search snippet locates a text; it is not a quotation. Read the article, heading or instrument before quoting.
- **Say what you did not find.** "No article on this point was found in the Customs Code of X (2018)" is a valid and useful answer. Do not replace a missing text with a text from another country without saying so.
- **Only the official text is authoritative.** Lex Duana reproduces published texts as a reading aid. For a decision with legal or financial consequences, the user must check the official publication (official journal, customs administration) and, where needed, ask the customs administration or a licensed professional.

## Versions

- The text you read is the version held by Lex Duana, identified by the catalog fields above. It may have been amended since. Never write "the law in force" without the version; write "as published in the 2018 code".
- If the user asks about a date before or after the version you read, say that you can only answer for the version available.
- If the catalog lists several versions of the same code, state which one you used and why (most recent, or the one the user named).
- If you did not fetch the catalog and cannot tell the version, cite the document by its identifier and say that the version was not checked, or spend one call on `lex_get_catalog` when the date matters to the user.

## Things the tools do not do

Say so plainly rather than improvise:

- They do not compute duties and taxes, and do not know exemptions, preferential origin or national taxes outside the tariff.
- They do not issue a classification decision or a customs value.
- They do not cover every country or every text: the catalog is the list of what exists.
