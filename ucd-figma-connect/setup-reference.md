# Figma Console MCP - setup reference

Condensed from https://docs.figma-console-mcp.southleft.com/setup. Check that page when something here does not match what the user sees; it is the source of truth.

The token placeholder is always `figd_YOUR_TOKEN_HERE`. The user replaces it themselves. Never ask for the real value.

## Modes

| Mode | Good for | Needs Node.js | Needs plugin | Can write |
|---|---|---|---|---|
| NPX (recommended) | Full design creation and editing, automatic updates | Yes, 18+ | Yes | Yes |
| Local Git | Pinning a version, contributing | Yes, 18+ | Yes | Yes |
| Cloud mode | Web clients, machines without Node.js | No | Yes, paired by code | Yes, smaller tool set |
| Remote read-only | Evaluating, extracting design data | No | No | No |

Only NPX and Local Git support real-time selection tracking and console log streaming.

## Prerequisites

- Node.js 18 or higher: `node --version`
- Figma Desktop (the browser version cannot run the bridge plugin): https://www.figma.com/downloads/
- An MCP client: Claude Code, Claude Desktop, Cursor, Windsurf, VS Code with Copilot, or similar

## Personal access token

1. In Figma: account menu > Settings > Security > Personal access tokens > Generate new token.
2. Name it `Figma Console MCP`.
3. Scopes:
   - File content: Read only
   - Variables: Read only (available on Enterprise plans only; skip if not offered)
   - Comments: Read and write
   - Everything else: No access
4. Copy the token straight away. It starts with `figd_` and is shown once.

## Add the server (NPX)

### Claude Code

One command, run by the user in their own terminal:

```bash
claude mcp add figma-console -s user -e FIGMA_ACCESS_TOKEN=figd_YOUR_TOKEN_HERE -e ENABLE_MCP_APPS=true -- npx -y figma-console-mcp@latest
```

The entry is stored in `~/.claude.json` (macOS, Linux) or `%USERPROFILE%\.claude.json` (Windows).

### Claude Desktop

Settings > Developer > Edit Config, or open the file directly:

- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

### Cursor, Windsurf and other clients

Same JSON in the client's MCP config file:

```json
{
  "mcpServers": {
    "figma-console": {
      "command": "npx",
      "args": ["-y", "figma-console-mcp@latest"],
      "env": {
        "FIGMA_ACCESS_TOKEN": "figd_YOUR_TOKEN_HERE",
        "ENABLE_MCP_APPS": "true"
      }
    }
  }
}
```

If the file already lists other servers, add `figma-console` inside the existing `mcpServers` object. Check for trailing commas and curly "smart" quotes. Then quit and reopen the client completely.

### VS Code with GitHub Copilot (1.102+)

Create `.vscode/mcp.json` with a `servers` key holding the same command and args. Keep the token in an env file referenced with `envFile` so it stays out of version control. Start the server from the Command Palette: "MCP: List Servers".

## Desktop Bridge plugin

1. Open Figma Desktop.
2. Plugins > Development > Import plugin from manifest…
3. Pick `~/.figma-console-mcp/plugin/manifest.json` (Windows: `%USERPROFILE%\.figma-console-mcp\plugin\manifest.json`). The server copies the plugin there the first time it starts, so the MCP client must have run once.
4. Open the design file and run Plugins > Development > Figma Desktop Bridge.
5. The plugin shows a status pill: `Local · ready`, `Cloud · ready` or `Local + Cloud · ready`. Keep the plugin window open while working.

If the manifest path does not exist: run `npx figma-console-mcp@latest --print-path`, or read the `pluginPath` field from the status tool.

Figma caches plugin files. Re-import the manifest only when the plugin shows an update banner or release notes say so.

Ports: each MCP server takes the next free port from 9223 to 9232, and the plugin scans all of them. A fallback port is normal when several sessions are open.

## Cloud mode

1. Add `https://figma-console-mcp.southleft.com/mcp` as a custom connector in the client's settings, with the Figma token as the bearer token.
2. Run the Desktop Bridge plugin in the Figma file.
3. Ask the assistant to connect to the Figma plugin. It returns a 6-character pairing code, valid for 5 minutes.
4. In the plugin: turn on Cloud Mode, enter the code, click Connect.

## Remote read-only

- OAuth endpoint: `https://figma-console-mcp.southleft.com/sse`. In Claude Desktop: Settings > Connectors > Add custom connector.
- Claude Code: `claude mcp add figma-console -s user -- npx -y mcp-remote@latest https://figma-console-mcp.southleft.com/sse`

## Verify

After restarting the client the server should show as connected. Then:

1. "Check Figma status" - reports an active WebSocket transport and the connected file.
2. "Search for button components" - returns results from the open file.
3. Optional, with the user's agreement: create one small frame, confirm it appears, delete it.

## Troubleshooting

| Symptom | Fix |
|---|---|
| Failed to connect to Figma Desktop | The plugin is not running. Run Plugins > Development > Figma Desktop Bridge in the file |
| FIGMA_ACCESS_TOKEN not configured | Token missing or mistyped in the config. It must start with `figd_` |
| Command not found: node | Install Node.js 18+ |
| Tools do not appear | Quit the client fully and reopen it |
| Port 9223 in use | Nothing to do. The server falls back to 9224-9232 |
| Plugin shows "MCP scanning" | Start the MCP client. The plugin retries on its own |
| Plugin shows "No MCP server found" | No client is running, or stale processes hold the ports. Restart the client |
| An old version runs | Use `figma-console-mcp@latest` explicitly in the command |
| Cryptic start-up errors such as "parseArgs not exported" | Node.js is older than 18. With a version manager, point the config at the absolute path of a newer `node` |
| Claude Desktop ignores the config | Invalid JSON. Check trailing commas and smart quotes |
| Cloud pairing code expired | Ask for a new one. Codes last 5 minutes |
| Cloud Mode toggle missing in the plugin | Re-import the plugin manifest |
| Import from manifest: file not found | The server has not started yet. Start the client once, then look again, or use `--print-path` |
| Connected, but to the wrong file | Run the plugin in the intended file, then check status again |
| Variables cannot be read | The Variables scope needs an Enterprise plan through the REST API. The plugin connection reads variables on any plan, so make sure the plugin is running |

When asking for help upstream (GitHub issues of `southleft/figma-console-mcp`), include: setup mode, exact error text, `node --version`, and the client name.
