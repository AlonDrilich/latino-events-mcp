# Latino Events MCP server (events.lat)

A hosted [Model Context Protocol](https://modelcontextprotocol.io) server for [events.lat](https://events.lat), a catalogue of upcoming concerts, festivals, conferences and cultural events across Latin America (Mexico, Brazil, Argentina, Colombia, Chile, Peru).

Ask your AI assistant things like *"What salsa concerts are on in Mexico City next month, and where can I buy tickets?"* and it searches the live catalogue.

> This repository holds documentation and the registry manifest only. The server is hosted by events.lat; its source code is not public.

## Connect

| | |
|---|---|
| Endpoint | `https://ojlsoqhibryhvuyltwpi.supabase.co/functions/v1/mcp` |
| Transport | Streamable HTTP |
| Authentication | OAuth 2.1 with dynamic client registration. Your client opens the events.lat sign-in the first time you connect. |
| Official MCP Registry | `lat.events/latino-events` ([server.json](server.json)) |

An unauthenticated request returns `401` with `WWW-Authenticate: Bearer resource_metadata=…`, which is how OAuth-capable clients discover the sign-in flow.

### Claude (claude.ai and desktop)

Settings → Connectors → **Add custom connector**, then paste the endpoint URL.

### Claude Code

```bash
claude mcp add --transport http latino-events https://ojlsoqhibryhvuyltwpi.supabase.co/functions/v1/mcp
```

### Cursor, VS Code and other clients

```json
{
  "mcpServers": {
    "latino-events": {
      "url": "https://ojlsoqhibryhvuyltwpi.supabase.co/functions/v1/mcp"
    }
  }
}
```

## Tools

| Tool | What it does | Access |
|---|---|---|
| `search_events` | Search upcoming public events by text, country, category, city and date range (`YYYY-MM-DD`). Up to 50 results. | Read-only |
| `get_event` | Fetch one event by id, including venue, date, price and the events.lat page where tickets can be bought. | Read-only |
| `list_saved_events` | List the events the signed-in user has bookmarked. | Read-only |
| `save_event` | Bookmark an event to the signed-in user's saved list. | Write (idempotent, not destructive) |

Where a seller doesn't publish a reliable price, events.lat says so instead of showing a guessed number.

## Other ways to get the data

- Website: https://events.lat (English, Spanish, Portuguese)
- Free iCal calendars per city, e.g. https://events.lat/cal/mexico-city.ics
- Machine-readable overview: https://events.lat/llms.txt

## Links

- Terms and privacy: https://events.lat/terms
- Contact: hello@events.lat

The documentation in this repository is MIT-licensed.
