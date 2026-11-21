# Errors and limits

## Limits by plan

Each tool call costs 1 call. Two limits apply to the user's Lex Duana account, depending on its plan:

| Plan | Requests per minute | Tool calls per day |
|---|---|---|
| Free | 60 | 100 |
| Pro | 300 | 2000 |

The daily counter resets at midnight UTC. On the Free plan, the number of questions a user can ask in a day is the daily limit divided by the calls you spend per question: this is why the workflows are short.

## Errors and what to tell the user

A tool error comes back as `{"error": {"code": ..., "message": ..., "type": ...}}`. Read `code`.

| What you see | Meaning | What to do | What to tell the user |
|---|---|---|---|
| HTTP 401, or the tool asks to sign in | Not connected, or the connection expired | Do not retry in a loop | "The Lex Duana connector needs you to sign in again with your Lex Duana account." |
| `ACCOUNT_REQUIRED` | The call carried no account | Stop calling | Same message as above |
| `QUOTA_EXCEEDED` | Daily quota used up. The error gives `limit`, `used`, `reset_at`, `plan_id`, `upgrade_available` | Stop calling for today. Answer from what you already hold, and say what is missing | "Your daily quota of Lex Duana calls is used up; it resets at midnight UTC." If `upgrade_available` is true, add that a subscription raises the limit. |
| `RATE_LIMITED` (HTTP 429, header `Retry-After`) | Too many requests in one minute | Wait the number of seconds given, then retry once | Nothing, unless it happens again |
| `RATE_LIMIT_UNAVAILABLE` (HTTP 503), `QUOTA_UNAVAILABLE`, `SERVICE_UNAVAILABLE` | Temporary failure on the server side | Retry once after a short wait, then stop | "Lex Duana is temporarily unavailable; please try again in a moment." |
| `INVALID_INPUT` | A parameter is wrong | Fix the parameter using `tools-and-fields.md`; do not resend the same call | Nothing |
| `NOT_FOUND` | The identifier, article or code does not exist in that document | Check the identifier with the catalog or a search; do not guess variants one by one | Say what was not found, and where you looked |
| `NO_RESULTS` | The search matched nothing | Rephrase once (other words, language of the document), then stop | Say that nothing was found on this point |
| `SERVER_ERROR` | Unexpected failure | Retry once, then stop | Same as temporary failure |

Never hide an error behind an answer from memory. If you could not read the text, say so.

## Staying within the quota

- Plan the calls before the first one; follow `workflows.md`.
- One call per need: `lex_hs_lookup` for a tariff code, `lex_get_articles_by_numbers` for several articles.
- Never repeat a call with the same arguments. Never call `lex_ping` or `lex_list_domains` as a warm-up.
- Fetch a catalog once per domain and reuse it for the rest of the conversation.
- After `NOT_FOUND` or `NO_RESULTS`, at most one corrected attempt.
- For a broad request, tell the user roughly how many calls it takes and propose a narrower scope.
- When `QUOTA_EXCEEDED` arrives, do not try other tools: every tool draws on the same counter.
