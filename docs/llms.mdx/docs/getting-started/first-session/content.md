# First Session (/docs/getting-started/first-session)



When you launch Mate for the first time, you land in the workspace — the main area where all your sessions live. Let's walk through the basics.

## The workspace [#the-workspace]

The workspace has three main areas:

* **Sidebar** (left): Lists your local device and any paired remote devices. Tap a device to switch context.
* **Tab bar** (top): Shows your open sessions — terminals, editor tabs, agent chats, web previews, and more.
* **Session area** (center): The active session's content fills this space.

## Open a terminal [#open-a-terminal]

Mate starts with a terminal tab by default. If you need another one:

1. Click the &#x2A;*+** button in the tab bar
2. Select **Terminal** from the dropdown
3. A new terminal session opens with your default shell

Each terminal is a full PTY session — it runs your actual shell (zsh, bash, fish, etc.) with complete support for colors, cursor movement, and interactive programs like `vim` or `top`.

## Working with tabs [#working-with-tabs]

Tabs appear along the top of the workspace. You can:

* **Reorder** tabs by dragging them
* **Close** a tab by clicking the X or using the keyboard shortcut
* **Create** new tabs with the + button — choose from Terminal, Editor, IDE, Web Preview, or Project

<Callout type="info">
  Each tab type has its own purpose. Terminals run shells, the IDE opens project folders, Web Previews show localhost ports, and Agent Chat connects to AI coding assistants. See [Features](/docs/features/terminal) for details on each.
</Callout>

## Tab types at a glance [#tab-types-at-a-glance]

| Tab         | What it does                                  |
| ----------- | --------------------------------------------- |
| Terminal    | Full PTY shell session                        |
| Agent Chat  | AI assistant (Claude Code, Codex, Copilot)    |
| IDE         | Multi-file editor with file tree              |
| Editor      | Single-file editor                            |
| Web Preview | View a localhost port through a reverse proxy |
| Project     | Organize related sessions together            |

## Try an AI agent [#try-an-ai-agent]

If you have Claude Code, Codex, or Copilot CLI installed, you can start an agent chat:

1. Click &#x2A;*+** in the tab bar
2. Select **Agent Chat**
3. Pick your preferred CLI from the dropdown
4. Type a message and watch the agent work

The agent can read files, run commands, search your codebase, and make edits — all within Mate's interface. See [Agent Chat](/docs/features/agent-chat) for the full guide.

## Next steps [#next-steps]

* [Pair a mobile device](/docs/getting-started/pairing-devices) to access your sessions from your phone
* [Set up integrations](/docs/integrations/overview) to connect GitHub, Slack, databases, and more
* [Explore features](/docs/features/terminal) to see everything Mate can do
