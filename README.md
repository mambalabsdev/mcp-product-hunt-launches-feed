# Product Hunt Launches Feed MCP Server

An MCP server for the Mamba Labs Product Hunt Launches Feed actor on Apify. Pick the days, and get one row per Product Hunt launch with the maker names, the product's website and company domain, its X and LinkedIn links, votes, rank, and topics.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

The actor reads Product Hunt's public daily launch pages and each launch's product page through the Apify proxy, with robots.txt obeyed. The public daily page shows the day's top featured launches. With your own Product Hunt developer token (`product_hunt_token`), the daily lists come from the official Product Hunt API instead, and `include_unfeatured` adds the launches Product Hunt did not feature. Filter by topic, keyword, or minimum votes, and use `only_new` on a schedule. Each day also returns one free summary row.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-product-hunt-launches-feed": {
      "command": "npx",
      "args": ["-y", "@mambalabsdev/mcp-product-hunt-launches-feed"],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `get_product_hunt_launches` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "List yesterday's Product Hunt launches in AI with their company domains and makers."
- "Which developer tools launched on Product Hunt this week with more than 200 votes?"
- "Get the launches of 2026-10-27 into a table."

## Tool

`get_product_hunt_launches`. One tool. Example arguments:

```json
{
  "days_back": 1,
  "topics": [
    "Artificial Intelligence"
  ],
  "max_launches": 50
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `days_back` | integer | no | The last N full days, Pacific time. Default 1. |
| `dates` | array | no | Specific days as YYYY-MM-DD, up to 31. |
| `include_today` | boolean | no | Also read today's list. Default false. |
| `topics` | array | no | Product Hunt topics by name or slug. |
| `keywords` | array | no | Words to find in the name, tagline, or topics. |
| `min_votes` | integer | no | Minimum votes. Default 0. |
| `max_launches` | integer | no | Launch rows per run. Default 100. |
| `open_product_pages` | boolean | no | Read product pages for website, domain, makers, socials. Default true. |
| `only_new` | boolean | no | Skip launches an earlier run returned. Default false. |
| `state_key` | string | no | Name for the only new launches memory. |
| `product_hunt_token` | string | no | Your own Product Hunt developer token, optional. |
| `include_unfeatured` | boolean | no | With your token, add unfeatured launches. Default false. |
| `max_charge_usd` | string | no | Optional cost cap for the run. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `launch-row`, per launch delivered | $0.00425 | $0.004038 | $0.003825 | $0.003613 |
| `apify-actor-start`, per run start | $0.002 | $0.002 | $0.002 | $0.002 |

Day summary rows, input refusal rows, launches whose product page could not be read, and launches skipped with only_new are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/product-hunt-launches-feed](https://apify.com/mambalabs/product-hunt-launches-feed)

## License

MIT. See [LICENSE](LICENSE).
