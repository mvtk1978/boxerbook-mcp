# Boxerbook MCP server

**Boxerbook** ([boxerbook.com](https://boxerbook.com)) is an open catalog of professional boxing worldwide: boxers, bouts, cards, results with sources, world titles, publisher rankings (WBC, WBA, IBF, WBO, The Ring, TBRB), the Boxerbook rating and a pre-fight forecast. The data is open under [ODbL](https://opendatacommons.org/licenses/odbl/) with attribution "Boxerbook".

This repository holds the public metadata of the **remote MCP server** and the **free JSON API**. The product code lives elsewhere; nothing here needs to be installed.

## Connect

| | |
|---|---|
| Endpoint | `https://mcp.boxerbook.com/mcp` |
| Transport | Streamable HTTP, stateless |
| Auth | none (no key, no sign-up) |
| Limits | 300 tool calls per minute per IP; lists are capped (schedule 30 days, results 14 days, search 20) |
| Registry name | `com.boxerbook/boxing` (official MCP Registry) |
| JSON API | [boxerbook.com/developers](https://boxerbook.com/developers) · OpenAPI 3.1: [`/v1/openapi.json`](https://boxerbook.com/v1/openapi.json) |

### Claude Code

```bash
claude mcp add --transport http boxerbook https://mcp.boxerbook.com/mcp
```

### Claude Desktop / claude.ai

Settings → Connectors → *Add custom connector* → URL `https://mcp.boxerbook.com/mcp`.

### Cursor

`.cursor/mcp.json`:

```json
{ "mcpServers": { "boxerbook": { "url": "https://mcp.boxerbook.com/mcp" } } }
```

### ChatGPT (developer mode) and other clients

Add a remote MCP server with the URL above; no authentication.

## Tools

| Tool | What it answers |
|---|---|
| `boxing_schedule` | upcoming cards (today, tonight, weekend, 30 days) with start times, broadcasters, forecast and market consensus |
| `boxing_results` | completed bouts of the last N days with sources (`days=2` is last night and today) |
| `boxer` | a boxer's card by name, slug or id: record, division, next fight, last result, rating |
| `next_fight` | a boxer's next bout with start time, broadcasters and odds |
| `bout` | one bout in full (sides' records going in, forecast, market, sources, fight-week notes) |
| `where_to_watch` | the broadcasters of a bout or card by country |
| `rankings` | the top 15 of a division: Boxerbook rating or a publisher (WBC, WBA, IBF, WBO, The Ring, TBRB) |
| `search_boxers` | boxers by name (pick by country, division and record when names collide) |
| `search`, `fetch` | any boxer, bout ("Inoue vs Nakatani"), card or division, and its document |

Resources: `boxerbook://schedule/today`, `boxerbook://results/last-night`, `boxerbook://status` (data freshness), `boxerbook://about`. Prompts: `fight_night_guide`, `boxer_briefing`, `weekend_results`.

Every answer carries a `url` field (a boxerbook.com page) to cite. `start_utc` is the start of the card, not of each bout. `forecast` is the Boxerbook model's probability that side A wins; `market` is the no-vig bookmaker consensus (via The Odds API). Neither is betting advice.

## Data and licence

Records are counted from open and official sources: athletic commissions (California, Nevada, Texas, Japan), sanctioning bodies, Wikidata, Wikipedia, the press. Data: [ODbL](https://opendatacommons.org/licenses/odbl/), attribution "Boxerbook". This README, `server.json` and the examples: MIT.

Questions and corrections: [info@boxerbook.com](mailto:info@boxerbook.com) · every bout page has a "report a discrepancy" link.
