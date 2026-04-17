# Integrations Overview (/docs/integrations/overview)



Mate ships with a full library of integrations built on the &#x2A;*Model Context Protocol (MCP)**. These connectors let your AI agents interact with external services — GitHub, Slack, databases, cloud providers, and more — directly from agent chat.

## What is MCP? [#what-is-mcp]

The Model Context Protocol is an open standard for connecting AI assistants to external tools. Each MCP connector runs as a local process that speaks a standardized protocol over stdin/stdout. The connector exposes "tools" that the AI agent can call — like creating a GitHub issue, querying a database, or sending a Slack message.

## How connectors work in Mate [#how-connectors-work-in-mate]

When you enable a connector in Mate:

1. Mate stores your credentials locally (API keys, tokens) in encrypted storage on your device
2. When you start an agent chat, Mate spawns the connector process and passes it to the CLI as an MCP server
3. The AI agent discovers the connector's tools and can call them during the conversation
4. The connector process runs locally on your machine — credentials never leave your device

<Callout type="info">
  Mate bundles its own Node.js runtime, so most connectors work out of the box without you needing to install Node.js separately. The bundled runtime handles `npx` commands that connectors use to start.
</Callout>

## What connectors enable [#what-connectors-enable]

With connectors, your AI agent can:

* **Read and write code** on GitHub, GitLab, or Bitbucket
* **Manage projects** in Linear, Jira, Asana, or Trello
* **Query databases** like Postgres, MySQL, MongoDB, or Redis
* **Search the web** via Brave Search, Exa, or Tavily
* **Send messages** on Slack, Discord, or Telegram
* **Manage infrastructure** on AWS, Cloudflare, Vercel, or Kubernetes
* **Generate images** with DALL-E, Stable Diffusion, or fal.ai
* And much more — see the [full connector list](/docs/integrations/connector-list)

## Transport types [#transport-types]

Most connectors use **stdio** transport — Mate spawns a local process and communicates over stdin/stdout. A few built-in connectors (like Mate Canvas) are handled directly by the app without spawning a separate process.

## Next steps [#next-steps]

* [Set up a connector](/docs/integrations/connector-setup) — step-by-step guide
* [Browse all connectors](/docs/integrations/connector-list) — full list by category
* [Claude Code integration](/docs/integrations/claude-code) — detailed guide for the most popular CLI
* [Custom connectors](/docs/integrations/custom-connectors) — add your own MCP servers
