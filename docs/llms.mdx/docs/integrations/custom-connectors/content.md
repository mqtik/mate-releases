# Custom Connectors (/docs/integrations/custom-connectors)



Beyond the built-in connectors, you can add any MCP-compatible server as a custom connector. If you have built your own MCP server or want to use one from the community that is not in Mate's registry, you can configure it manually.

## What you need [#what-you-need]

A custom connector requires:

* An **MCP server** that speaks the Model Context Protocol over stdio (stdin/stdout)
* A **command** to start it (e.g., `npx`, `node`, `python`, or a binary path)
* Any **arguments** the command needs
* Any **environment variables** for configuration (API keys, etc.)

## Adding a custom connector [#adding-a-custom-connector]

Custom connectors are configured as MCP servers that Mate passes to the agent CLI at startup.

<Steps>
  ### Prepare your MCP server [#prepare-your-mcp-server]

  Make sure your server runs correctly from the command line. Test it independently first:

  ```bash
  echo '{"jsonrpc":"2.0","method":"initialize","id":1,"params":{"capabilities":{}}}' | npx your-mcp-server
  ```

  ### Configure in Mate [#configure-in-mate]

  Add the connector configuration in Mate's settings. You will need to provide:

  * **Name**: A display name for the connector
  * **Command**: The command to run (e.g., `npx`, `node`, `python`)
  * **Arguments**: Command arguments (e.g., `-y @your-org/mcp-server`)
  * **Environment variables**: Any API keys or config values the server needs

  ### Test the connector [#test-the-connector]

  Open a new agent chat and ask the agent to list available tools. Your custom connector's tools should appear in the list.
</Steps>

## Examples [#examples]

### Node.js MCP server via npx [#nodejs-mcp-server-via-npx]

If your server is published to npm:

* **Command**: `npx`
* **Args**: `-y @your-org/your-mcp-server`
* **Env**: Any required variables like `API_KEY`

### Local Node.js script [#local-nodejs-script]

If your server is a local file:

* **Command**: `node`
* **Args**: `/path/to/your/server.js`
* **Env**: Any required variables

### Python MCP server [#python-mcp-server]

If your server is written in Python:

* **Command**: `python`
* **Args**: `-m your_mcp_server`
* **Env**: Any required variables

<Callout type="info">
  Mate bundles Node.js, so `npx` and `node` commands work without a system Node.js installation. For Python-based servers, you need Python installed on your system.
</Callout>

## Building your own MCP server [#building-your-own-mcp-server]

If you want to build a custom MCP server, the protocol is straightforward:

1. Read JSON-RPC messages from stdin
2. Process tool calls and return results
3. Write JSON-RPC responses to stdout

The [MCP specification](https://modelcontextprotocol.io) has full details on the protocol, tool definitions, and message formats. There are SDKs available for TypeScript, Python, and other languages that handle the protocol boilerplate.

## Sharing connectors [#sharing-connectors]

If you build a connector that others might find useful, consider publishing it to npm (for Node.js) or PyPI (for Python). The MCP ecosystem is growing, and community servers are easy to distribute as packages.
