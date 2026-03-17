# hello-world-mcp

MCP server example exposing a `hello` tool.

## Scripts

- **`npm run server:dev`** — run server with tsx (`tsx src/index.ts`).
- **`npm run server:build`** — compile TypeScript to `dist`.
- **`npm run inspect`** — run this MCP server under [MCP Inspector](https://github.com/modelcontextprotocol/inspector) (web UI for testing/debugging).
- **`npm run inspect:cli`** — run Inspector in CLI mode and call `tools/list`.

## MCP Inspector

The project uses **`@modelcontextprotocol/inspector`** (dev dependency) to test and debug the MCP server.

### Usage (official API)

- **Start Inspector with this server (UI):**
  ```bash
  npx @modelcontextprotocol/inspector tsx src/index.ts
  ```
  UI: `http://localhost:6274`.

- **CLI mode (no browser):**
  ```bash
  npx @modelcontextprotocol/inspector --cli tsx src/index.ts --method tools/list
  ```

- **Environment variables for the child process:**
  ```bash
  npx @modelcontextprotocol/inspector -e KEY=value -e KEY2=$VAR tsx src/index.ts
  ```

- **Ports (defaults):**
  - Client UI (MCPI): `6274`
  - Proxy (MCPP): `6277`
  Override: `CLIENT_PORT=8080 SERVER_PORT=9000 npx @modelcontextprotocol/inspector tsx src/index.ts`

- **Arguments and env for server:**  
  `npx @modelcontextprotocol/inspector -e key=value -- tsx src/index.ts -e server-flag`

### Docs

- [Inspector repo](https://github.com/modelcontextprotocol/inspector)
- [npm @modelcontextprotocol/inspector](https://www.npmjs.com/package/@modelcontextprotocol/inspector)
