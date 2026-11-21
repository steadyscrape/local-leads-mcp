# Local Leads MCP (SteadyScrape)

A remote MCP server for local business research: find businesses on Google Maps by category and area with lead filters, read their recent reviews, and get complaint and praise themes. Business and review data comes from DataForSEO under licence.

**Endpoint (Streamable HTTP):**

```
https://leads.mcp.steadyscrape.dev/mcp
```

The same server is also served at `https://mcp.steadyscrape.dev/leads/mcp`. It is hosted on the [SteadyScrape MCP gateway](https://leads.mcp.steadyscrape.dev). Tools run in your own [Apify](https://apify.com/steady-scrape) account. Nothing to install or host.

## Tools

All tools are read-only.

| Tool | What it does |
|---|---|
| `find_local_businesses` | Businesses on Google Maps for 1–5 categories in an area (city, postal code, country, or coordinates and radius), with optional lead filters: no website, unclaimed profile, low rating, few reviews, or newly listed. |
| `business_reviews` | Recent reviews of 1–5 businesses from Google Maps, Trustpilot or Tripadvisor, with rating stats and a monthly trend. Reviewer names, profiles and photos are never returned. |
| `review_summary` | Complaint and praise themes, suggested actions, rating distribution, trend and owner reply rate for 1–3 businesses. No reviewer names. |
| `get_results` | Fetch results of a call that returned a `run_id` because it took longer than about two minutes. Free. |

Each call is billed by Apify to your own account at the Store price of the underlying SteadyScrape Actor (see the [server page](https://leads.mcp.steadyscrape.dev) for prices and free-plan limits). Errors and refused calls are free; listing tools and connecting cost nothing.

## Authentication

Sign in with your own Apify account (free to create). Clients that support MCP OAuth (Claude, VS Code, Cursor, ChatGPT developer mode) open the Apify sign-in the first time. Apify runs the sign-in (OAuth 2.1 with PKCE); SteadyScrape never sees your Apify password. You can revoke access any time in Apify Console → Settings → API & Integrations.

## Client setup

**Claude.ai / Claude Desktop:** Settings → Connectors → *Add custom connector* → paste the endpoint URL → Connect, then sign in to Apify.

**Claude Code:**

```bash
claude mcp add --transport http steadyscrape-leads "https://leads.mcp.steadyscrape.dev/mcp"
```

**Cursor, Windsurf** and other clients that use `mcpServers`:

```json
{
  "mcpServers": {
    "steadyscrape-leads": { "url": "https://leads.mcp.steadyscrape.dev/mcp" }
  }
}
```

**VS Code** (`.vscode/mcp.json`):

```json
{
  "servers": {
    "steadyscrape-leads": { "type": "http", "url": "https://leads.mcp.steadyscrape.dev/mcp" }
  }
}
```

**Clients that only speak stdio:**

```json
{
  "mcpServers": {
    "steadyscrape-leads": { "command": "npx", "args": ["-y", "mcp-remote", "https://leads.mcp.steadyscrape.dev/mcp"] }
  }
}
```

## Example prompts

- "Find plumbers in Austin, TX with no website and fewer than 20 reviews."
- "What do customers complain about most at these three dental clinics?"
- "List restaurants in Denver first listed on Google Maps in the last 30 days."

## Links

- Server page: https://leads.mcp.steadyscrape.dev
- Privacy: https://mcp.steadyscrape.dev/privacy
- Support: https://mcp.steadyscrape.dev/support
- Terms: https://steadyscrape.dev/terms
- Official MCP Registry: `dev.steadyscrape/local-leads` ([`server.json`](server.json))
- Glama: https://glama.ai/mcp/connectors/dev.steadyscrape/local-leads ([`glama.json`](glama.json))

## License

MIT. This repo contains configuration and docs only; the tools are paid services on Apify.
