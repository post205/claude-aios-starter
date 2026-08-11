# Connections

Registry of every system your AIOS can reach. Filled by `/onboard` from your Q4-Q7 answers, then expanded as you wire new tools. `/audit` reads this file to score domain coverage and freshness.

| # | Domain | Tool | Mechanism | Auth | Last checked |
|---|---|---|---|---|---|
| 1 | Revenue / Financials | _filled by /onboard_ | not yet connected | — | — |
| 2 | Customer interactions | _filled by /onboard_ | not yet connected | — | — |
| 3 | Calendar | _filled by /onboard_ | not yet connected | — | — |
| 4 | Communication | _filled by /onboard_ | not yet connected | — | — |
| 5 | Project / task tracking | _filled by /onboard_ | not yet connected | — | — |
| 6 | Meeting intelligence | _filled by /onboard_ | not yet connected | — | — |
| 7 | Knowledge / files | _filled by /onboard_ | not yet connected | — | — |

**Mechanism options:** `cli` (a thin command or `curl` you call on demand — the token-light default), `script` (Python/Bash hitting an API, kept in `scripts/`), `mcp` (MCP server — heavier, loads its toolset into every session), `export` (a CSV/JSON dump pipeline), `key+ref` (a `.env` key plus a `references/{tool}-api.md` guide), `not yet connected`.

**Prefer `cli` or `script` over `mcp`.** An MCP pays a token tax on every conversation whether you use it or not. A command you call on demand only costs context when it runs. Pay per use, not rent. (The Shift, Move 3.)

Every time you wire a new tool, do two things: add its row above, and save `references/{tool}-api.md` capturing the endpoints, the auth flow, and the two or three queries you actually use. Research it once, keep it forever — every skill you build after that inherits the work.
