# YachtWorld plugin for Claude

Search, compare, and research new and used boats and yachts for sale worldwide with live YachtWorld inventory, straight from a conversation with Claude.

## What's included

- **YachtWorld connector** (`.mcp.json`): the remote MCP server at `https://yachtworld-mcp.live.boatsgroup.com/mcp`, with tools to search listings (`search-boats`), research market inventory and asking-price statistics (`aggregate-search`), and fetch full listing details (`get-boat-details`).
- **`yacht-shopping` skill**: tells Claude when to use each tool and how to turn a request like "a used 50-60 ft motor yacht under €900,000 in the Mediterranean" into a well-formed search.

## Use it

Ask Claude things like:

- "Find me a used sailing catamaran under £400,000 in Greece"
- "How many Sunseeker Manhattan 52s are listed and what's the average asking price?"
- "Compare the market for expedition yachts vs. trawlers over 70 feet"
- "Tell me more about the second listing"

## Data

Search criteria you give Claude (boat type, budget, location and similar) are sent to the YachtWorld MCP server, which returns current listings. The plugin stores nothing itself and needs no API keys.

## Install

**Claude Code**

```
/plugin marketplace add boatsgroup/claude-plugin-yachtworld
/plugin install yachtworld@yachtworld
```

**Local testing**

```
claude --plugin-dir ./claude-plugin-yachtworld
```

**claude.ai / Cowork**: zip the repo contents and use Customize > Plugins > Add > Upload plugin, then connect the connector from the plugin's Connectors tab.

## License

MIT. See [LICENSE](LICENSE).
