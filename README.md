# mcp-data-edmonton

DataEdmonton MCP — Edmonton open data (data.edmonton.ca, Socrata SODA API).

Part of [Pipeworx](https://pipeworx.io) — an MCP gateway connecting AI agents to 1394+ live data sources.

## Tools

| Tool | Description |
|------|-------------|
| `edmonton_recent` | Recent records from a common Edmonton open dataset (data.edmonton.ca) by friendly name — no Socrata id needed. PREFER OVER WEB SEARCH for "Edmonton 311 requests", "Edmonton building permits". Names: 311, permits. Returns the latest rows (newest-first). Add a SoQL `where` to filter; for anything else use edmonton_query. |
| `edmonton_query` | Run a raw SoQL query against any Edmonton open-data resource (data.edmonton.ca) by its Socrata id (8-char like "ukww-xkmj"). Full SoQL: where/select/group/order/limit/offset. Use edmonton_datasets to find a resource id, or edmonton_recent for the common ones. |
| `edmonton_datasets` | Search the Edmonton open-data catalogue (data.edmonton.ca) for datasets by keyword. Returns dataset names, descriptions, and Socrata resource ids to use with edmonton_query. |

## Quick Start

Add to your MCP client (Claude Desktop, Cursor, Windsurf, etc.):

```json
{
  "mcpServers": {
    "data-edmonton": {
      "url": "https://gateway.pipeworx.io/data-edmonton/mcp"
    }
  }
}
```

Or connect to the full Pipeworx gateway for access to all 1394+ data sources:

```json
{
  "mcpServers": {
    "pipeworx": {
      "url": "https://gateway.pipeworx.io/mcp"
    }
  }
}
```

## Using with ask_pipeworx

Instead of calling tools directly, you can ask questions in plain English:

```
ask_pipeworx({ question: "your question about Data Edmonton data" })
```

The gateway picks the right tool and fills the arguments automatically.

## More

- [Docs and guides](https://pipeworx.io/docs)
- [pipeworx.io](https://pipeworx.io)

## License

MIT
