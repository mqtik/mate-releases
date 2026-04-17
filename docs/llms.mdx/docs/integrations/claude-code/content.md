# Claude Code Integration (/docs/integrations/claude-code)



Claude Code is the most deeply integrated AI CLI in Mate. Unlike Codex and Copilot (which run one-shot), Claude Code maintains a persistent process with multi-turn conversation support, making it feel like a native part of the app.

## How it works [#how-it-works]

When you start an agent chat with Claude Code:

1. Mate spawns the `claude` CLI with `--input-format stream-json` for streaming communication
2. The process stays alive for the entire conversation — follow-up messages go through stdin
3. Responses stream back in real time with text, tool calls, and results
4. MCP connectors are passed via a generated config file

This long-lived process model means there is no multi-second delay between messages. After the initial startup, follow-ups are instant.

## Requirements [#requirements]

You need the Claude Code CLI installed on your system:

```bash
npm install -g @anthropic-ai/claude-code
```

Mate detects available CLIs automatically. If `claude` is in your PATH, it appears as an option when creating an agent chat.

## Features in Mate [#features-in-mate]

### Streaming responses [#streaming-responses]

Text and tool use stream in real time. You see the agent's thinking as it happens, not just the final result.

### Tool use visualization [#tool-use-visualization]

When Claude Code calls tools, Mate shows them as interactive chips with context:

* **File reads** show the filename
* **Shell commands** show the actual command being run
* **Searches** show the query
* **File edits** show the file being modified, with inline diffs

### Conversation persistence [#conversation-persistence]

Conversations persist across app restarts. You can close Mate, reopen it, and resume where you left off.

### Conversation forking [#conversation-forking]

Fork a conversation at any point to explore a different approach without losing the original thread. This is useful for trying alternative solutions.

### MCP connector passthrough [#mcp-connector-passthrough]

All enabled [MCP connectors](/docs/integrations/overview) are automatically available to Claude Code. Mate generates an MCP config file that the CLI reads at startup, giving the agent access to GitHub, databases, search engines, and every other connector you have configured.

<Callout type="info">
  Mate handles the MCP config file generation automatically. You do not need to manually configure Claude Code's MCP settings — just enable connectors in Mate's settings and they are available in every agent chat.
</Callout>

### Tool approval [#tool-approval]

Some tool calls require your approval before execution. Mate shows a permission prompt for sensitive operations, letting you review and approve or deny before the agent proceeds.

## Remote usage [#remote-usage]

Claude Code sessions are accessible from paired remote devices. The CLI process runs on the desktop, and the remote device sends input and receives output over the network. You can start a conversation on your Mac and continue interacting with it from your phone.

## Tips [#tips]

* Use conversation forking when you want to try a different approach
* Enable relevant MCP connectors before starting a chat so the agent has access to your tools from the first message
* Long-running tasks continue working even when you switch to another tab
