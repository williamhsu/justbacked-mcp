<p align="center"><img src="logo.png" width="96" alt="JustBacked"></p>

# JustBacked MCP Server

Search and track open roles at venture-backed startups that raised in the last six months, from Claude, ChatGPT, Cursor or any MCP client.

[JustBacked](https://justbacked.com) lists every open role at startups that just raised a round, with the round, the lead investors and the date each role first appeared. This MCP server gives your AI assistant the same data plus your application tracker, company lists and saved searches.

This is a **hosted remote server**. There is nothing to install or run: point your client at the URL below.

| | |
|---|---|
| Endpoint | `https://justbacked.com/api/mcp` |
| Transport | Streamable HTTP (stateless, JSON responses) |
| Auth | `Authorization: Bearer jb_live_...` (JustBacked member API key) |
| Registry name | `com.justbacked/jobs` ([official MCP registry](https://registry.modelcontextprotocol.io)) |
| Protocol versions | 2025-06-18, 2025-03-26, 2024-11-05 |

`initialize` and `tools/list` work without a key. `tools/call` needs a key from a JustBacked membership: create one at [justbacked.com/account](https://justbacked.com/account#api).

## Connect

**Claude Code**

```bash
claude mcp add --transport http justbacked https://justbacked.com/api/mcp \
  --header "Authorization: Bearer jb_live_YOUR_KEY"
```

**Claude.ai, ChatGPT and other clients that only take a URL**: put the key in the path.

```
https://justbacked.com/api/mcp/jb_live_YOUR_KEY
```

**Cursor** (`~/.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "justbacked": {
      "url": "https://justbacked.com/api/mcp",
      "headers": { "Authorization": "Bearer jb_live_YOUR_KEY" }
    }
  }
}
```

Step-by-step guides for each assistant: [justbacked.com/agents](https://justbacked.com/agents).

## Tools

| Tool | Access | What it does |
|---|---|---|
| `search_jobs` | read | Open roles at startups that raised in the last six months. Filters: function, seniority, city, remote, funding stage, raise size, investors, pay, posted within. |
| `get_job` | read | Full description, pay, the company's round and investors, hiring velocity and the apply link. |
| `get_application_form` | read | The role's application questions from the company's public Greenhouse, Lever or Ashby board, so you can draft answers. Never submits. |
| `get_company` | read | Latest round, amount, lead investors, headcount, HQ and every open role at one startup. |
| `track_application` | write | Add a role to your tracker or set its status (saved, applied, interviewing, offer, ...). |
| `list_applications` | read | Your tracked roles with status, dates and notes. |
| `update_application` | write | Change status or add a dated note. |
| `list_lists` / `add_to_list` / `remove_from_list` | read / write | Target-company lists; lists with alerts email you when a company posts a role or raises. |
| `list_saved_searches` / `save_search` / `delete_saved_search` | read / write | Saved searches that email you new matching roles. |
| `get_account` | read | Membership and API usage today. |

Writes only touch your own tracker, lists and searches. Limit: 1,000 requests a day per member.

## Example prompts

- "Find senior product designer roles in New York at Series A startups paying over $150K."
- "Which startups that raised in the last 30 days are hiring backend engineers remotely?"
- "Get the application questions for that role and help me draft answers."
- "Save that one to my tracker as applied, and set an alert for similar roles."

## Docs

- Full reference (MCP and REST): [justbacked.com/developers](https://justbacked.com/developers)
- Support: support@justbacked.com

## License

The contents of this repository (docs and `server.json`) are MIT licensed. The server itself is hosted by JustBacked.
