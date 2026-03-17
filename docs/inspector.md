# MCP Inspector usage

This project uses [@modelcontextprotocol/inspector](https://github.com/modelcontextprotocol/inspector) for testing and debugging the MCP server. The Inspector provides a React-based web UI and a Node.js proxy for browser interaction.

**API reference (Context7):** [MCP Inspector – Context7](https://context7.com/modelcontextprotocol/inspector).

## Package

- **Package:** `@modelcontextprotocol/inspector`
- **Install:** In `devDependencies`. Run `npm install`.

---

## UI mode (default)

Starts the Inspector web UI (default: http://localhost:6274) and an MCP proxy (default port 6277). Run your MCP server under the Inspector via stdio.

```bash
npm run inspect
```

Equivalent to:

```bash
npx @modelcontextprotocol/inspector tsx src/index.ts
```

Or with built output:

```bash
npx @modelcontextprotocol/inspector node build/index.js
```

### UI options

| Option | Description |
|--------|-------------|
| **Default ports** | Client UI: 6274, Proxy: 6277 (T9: MCPI / MCPP). |
| **Custom ports** | `CLIENT_PORT=8080 SERVER_PORT=9000 npx @modelcontextprotocol/inspector node build/index.js` |
| **Env vars for server** | `npx @modelcontextprotocol/inspector -e API_KEY=your-key -e DEBUG=true node build/index.js --debug` |

---

## CLI mode

CLI mode allows programmatic interaction (scripting, automation, coding assistants). Enable with `--cli`.

### Parameters (official API)

| Parameter | Type | Description |
|-----------|------|-------------|
| `--cli` | boolean | **Required.** Enables CLI mode. |
| `--config` | string | Path to config file (e.g. `mcp.json`). |
| `--server` | string | Server name from config. |
| `--method` | string | Method to call: `tools/list`, `tools/call`, `resources/list`, `prompts/list`. |
| `--tool-name` | string | Name of the tool to call. |
| `--tool-arg` | string | Tool arguments. Use `key=value` or JSON. Can be repeated. |
| `--transport` | string | Transport: `sse`, `http`, `stdio`. Default SSE for remote. |
| `--header` | string | Custom header, e.g. `"X-API-Key: your-api-key"`. |

### Examples

List tools (local):

```bash
npx @modelcontextprotocol/inspector --cli tsx src/index.ts --method tools/list
```

Call a tool (key-value):

```bash
npx @modelcontextprotocol/inspector --cli tsx src/index.ts --method tools/call --tool-name hello --tool-arg key=value
```

Call a tool (JSON argument):

```bash
npx @modelcontextprotocol/inspector --cli tsx src/index.ts --method tools/call --tool-name hello --tool-arg 'options={"format":"json"}'
```

With config file:

```bash
npx @modelcontextprotocol/inspector --cli --config path/to/config.json --server myserver --method tools/list
```

Remote server (SSE default):

```bash
npx @modelcontextprotocol/inspector --cli https://my-mcp-server.example.com --method tools/list
```

Remote with Streamable HTTP and header:

```bash
npx @modelcontextprotocol/inspector --cli https://my-mcp-server.example.com --transport http --method tools/list --header "X-API-Key: key"
```

List resources / prompts:

```bash
npx @modelcontextprotocol/inspector --cli tsx src/index.ts --method resources/list
npx @modelcontextprotocol/inspector --cli tsx src/index.ts --method prompts/list
```

---

## Config file (mcp.json)

Example for multiple servers:

```json
{
  "mcpServers": {
    "default-server": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-everything"]
    },
    "hello-world-mcp": {
      "command": "tsx",
      "args": ["src/index.ts"]
    }
  }
}
```

---

## NPM scripts in this repo

| Script | Command | Description |
|--------|---------|--------------|
| `npm run inspect` | `npx @modelcontextprotocol/inspector tsx src/index.ts` | Run Inspector UI with this server. |
| `npm run inspect:cli` | `npx @modelcontextprotocol/inspector --cli tsx src/index.ts --method tools/list` | List tools via CLI. |
