# Agent Chat (/docs/features/agent-chat)



Agent Chat lets you work with AI coding assistants directly inside Mate. Instead of switching between your terminal and a separate chat window, the agent runs alongside your other sessions — reading your files, executing commands, and making edits, all visible in real time.

## Supported CLIs [#supported-clis]

| CLI         | Multi-turn             | How it connects                                                 |
| ----------- | ---------------------- | --------------------------------------------------------------- |
| Claude Code | Yes (long-lived stdin) | Spawns process, sends messages via `--input-format stream-json` |
| Codex       | One-shot               | Spawns a new process per message                                |
| Copilot     | One-shot               | Spawns a new process per message                                |

<Callout type="info">
  Claude Code keeps a persistent process running, so follow-up messages are instant. Codex and Copilot spawn fresh processes for each message, which takes a few seconds.
</Callout>

## Available models [#available-models]

Each CLI gives you access to different models:

| CLI         | Models                                 |
| ----------- | -------------------------------------- |
| Claude Code | Haiku 4.5, Sonnet 4.6, Opus 4.6        |
| Codex       | Codex Mini, GPT-5.2 Codex, o4-mini, o3 |
| Copilot     | GPT-4o, Claude 3.5 Sonnet, o3-mini     |

Select your preferred model from the dropdown in the chat header. The model affects response quality, speed, and cost.

## Starting a chat [#starting-a-chat]

1. Click &#x2A;*+** in the tab bar and select **Agent Chat**
2. Choose your CLI (Claude Code, Codex, or Copilot) from the dropdown
3. Type your message and press Enter

The agent streams its response in real time. You will see text output as it is generated, and tool use appears as interactive chips showing what the agent is doing.

## Tool use [#tool-use]

When the agent calls tools — reading files, running commands, searching code — Mate shows each tool invocation with meaningful context:

* **Read file** shows the filename being read
* **Run command** shows the actual shell command
* **Search** shows the query being searched
* **Edit file** shows which file is being modified

Tool calls that modify files (edits, writes) are highlighted so you can review what changed. Mate generates inline diffs for file modifications.

### Tool approval [#tool-approval]

Some tools require your approval before the agent can execute them. When the agent wants to run a potentially destructive action (like writing a file or running a shell command), Mate shows a permission prompt. You can:

* **Approve** the individual tool call
* **Approve all** for that tool type during the session
* **Reject** to deny the action

### Auto-approval and permission modes [#auto-approval-and-permission-modes]

For trusted workflows, you can configure auto-approval in the chat settings. This lets the agent run tools without asking — useful when you are watching the output and want a faster feedback loop. You can set permission modes per tool category (e.g., always approve file reads, always ask before shell commands).

### Effort level [#effort-level]

Claude Code supports an effort setting that controls how thorough the agent is. Lower effort means faster, more concise responses. Higher effort means the agent spends more time thinking, reading more files, and producing more detailed output. Adjust this in the chat header.

## Conversations [#conversations]

Each agent chat is a persistent conversation. You can:

* **Continue** a conversation by sending more messages
* **Fork** a conversation to branch off from a specific point — useful when you want to try a different approach without losing the original thread
* **Resume** a previous conversation from the sidebar

Conversation history is stored locally on your desktop. Nothing is sent to any cloud service beyond what the underlying CLI itself sends to its API.

### Forking [#forking]

Conversation forking creates a new conversation that starts with the same history up to the point you forked. The original conversation is untouched. This lets you explore "what if" scenarios — try a different approach, and if it doesn't work out, go back to the original.

## Rich content [#rich-content]

### Markdown rendering [#markdown-rendering]

Agent responses render full Markdown with syntax highlighting for code blocks, tables, lists, and inline formatting. Code blocks show the language label and can be copied with one click.

### Canvas artifacts [#canvas-artifacts]

When an agent produces self-contained HTML/JS/CSS, Mate can display it in a Canvas panel alongside the chat. This is useful for visual content — charts, diagrams, interactive prototypes — that the agent generates during the conversation.

### File and image attachments [#file-and-image-attachments]

Drag and drop files or images into the composer, or paste them from your clipboard. The agent receives the file content as part of the message context. This works with code files, screenshots, logs, or any text-based content you want the agent to see.

## Slash commands [#slash-commands]

Type `/` in the composer to see available slash commands. These come from installed [skills](/docs/integrations/skills) and built-in commands. Slash commands let you trigger specific workflows without typing out full prompts.

## MCP connectors in agent chat [#mcp-connectors-in-agent-chat]

If you have [MCP connectors](/docs/integrations/overview) configured, the agent can use them as tools. For example, with the GitHub connector enabled, Claude Code can create pull requests, read issues, and manage repositories directly from chat.

Mate generates an MCP config file that the CLI reads at startup, so all your connected integrations are available to the agent automatically.

## Remote agent chat [#remote-agent-chat]

Agent chat works from paired remote devices. When you select a remote device in the sidebar, you see its running agent chat sessions and can interact with them. The CLI process runs on the desktop — the remote device sends input and receives streamed output over the network.

## Tips [#tips]

* Long-running agent tasks keep working even if you switch to another tab
* Use conversation forking when you want to try a different approach without losing the original thread
* The agent respects your project's working directory when running commands
* Use [voice input](/docs/features/voice-input) to dictate prompts instead of typing
