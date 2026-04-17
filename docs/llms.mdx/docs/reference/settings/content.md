# Settings (/docs/reference/settings)



Access settings by clicking the gear icon or pressing `Cmd + ,` (macOS) / `Ctrl + ,` (Windows/Linux).

## General [#general]

### Port [#port]

The TCP port Mate uses for device communication. Default is **53317**. Change this if the default port conflicts with another application. All paired devices must use the same port.

### Theme [#theme]

Choose between light, dark, or system theme. System follows your OS appearance setting.

### Language [#language]

Mate supports multiple interface languages. The default follows your system language.

## Terminal [#terminal]

### Default shell [#default-shell]

The shell used for new terminal sessions. Mate detects your system's default shell automatically (e.g., zsh on macOS, bash on Linux). You can override this to use a different shell.

### Font size [#font-size]

The terminal font size in points. Adjustable via settings or with keyboard shortcuts (`Cmd + =` / `Cmd + -`).

### Scrollback buffer [#scrollback-buffer]

The number of lines kept in the terminal's scrollback history. Higher values use more memory but let you scroll back further through command output.

## Connectors [#connectors]

### Enabled connectors [#enabled-connectors]

Toggle individual MCP connectors on or off. Each connector shows its name, category, and connection status.

### Credentials [#credentials]

Manage API keys and tokens for connectors. Credentials are stored in platform-native secure storage (Keychain on macOS, Credential Manager on Windows, Secret Service on Linux).

### Command verification [#command-verification]

Mate checks that the required command for each connector (usually `npx`) is available before enabling it. If a command is not found, Mate shows installation guidance.

## Network [#network]

### Device name [#device-name]

The name other devices see when they discover your device on the network. Defaults to your computer's hostname.

### Auto-discovery [#auto-discovery]

Toggle multicast UDP discovery on or off. When enabled, Mate automatically finds other devices on the same network. When disabled, you need to connect manually.

## Agent Chat [#agent-chat]

### Default CLI [#default-cli]

The AI CLI to use when creating new agent chat sessions. Options depend on which CLIs are installed on your system (Claude Code, Codex, Copilot).

### MCP config generation [#mcp-config-generation]

Mate automatically generates MCP configuration files that agent CLIs read at startup. This section shows which connectors will be passed to agent sessions and lets you configure additional settings.

<Callout type="info">
  Settings are stored locally on your device. They are not synced between devices — each device has its own configuration.
</Callout>
