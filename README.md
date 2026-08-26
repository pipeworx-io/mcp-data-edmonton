# mcp-data-edmonton

DataEdmonton MCP — Edmonton open data (data.edmonton.ca, Socrata SODA API).

Part of [Pipeworx](https://pipeworx.io) — an MCP gateway connecting AI agents to 1476+ live data sources.

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

### What this endpoint actually serves

`tools/list` at `https://gateway.pipeworx.io/data-edmonton/mcp` returns the tools in the table
above **plus the shared Pipeworx meta-tools** — `ask_pipeworx`,
`discover_tools`, `search_within`, `remember`/`recall` and the rest of the
gateway-wide set. So the tool count you see is larger than this table: a
single-pack endpoint currently lists roughly 30 shared tools alongside the
pack's own. The connection's `initialize` response states its exact scope, and
is the authoritative answer for a given day.

This is deliberate, not multiplexing by accident. The meta-tools are what let a
scoped connection answer a question this pack does not cover — via
`ask_pipeworx`, which routes across the whole catalog — without you adding a
second MCP server. There is currently no way to mount a pack endpoint without
them; if the extra schemas cost you more context than the routing is worth,
connect to the full gateway once rather than to several pack endpoints.

Or connect to the full Pipeworx gateway to get every pack's tools listed
directly, instead of just this one's:

```json
{
  "mcpServers": {
    "pipeworx": {
      "url": "https://gateway.pipeworx.io/mcp"
    }
  }
}
```

Both URLs reach the same gateway and the same 1476+ data sources. The
only difference is which pack's tools are listed **directly**; `ask_pipeworx`
reaches all of them from either one.

## Using with ask_pipeworx

Instead of calling tools directly, you can ask questions in plain English —
this works on the pack endpoint above as well as on the full gateway:

```
ask_pipeworx({ question: "your question about Data Edmonton data" })
```

The gateway picks the right tool and fills the arguments automatically.

## More

- [Docs and guides](https://pipeworx.io/docs)
- [pipeworx.io](https://pipeworx.io)

## License

MIT
