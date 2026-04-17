# Connector Setup (/docs/integrations/connector-setup)



Setting up a connector takes about a minute. Here is the process from start to finish.

## Installation [#installation]

<Steps>
  ### Open Settings [#open-settings]

  Go to the Settings tab in Mate and find the **Connectors** section.

  ### Browse connectors [#browse-connectors]

  You will see the full list of available connectors organized by category. Each connector shows its name, description, and what credentials it needs.

  ### Select a connector [#select-a-connector]

  Click on the connector you want to enable. For example, **GitHub**.

  ### Enter credentials [#enter-credentials]

  Most connectors require an API key or token. The setup form shows:

  * What credential is needed (e.g., "Personal Access Token")
  * A link to where you can create one (e.g., GitHub's token settings page)
  * Guidance on what permissions/scopes to grant

  Enter your credentials and save. They are stored locally in encrypted storage on your device.

  ### Enable the connector [#enable-the-connector]

  Toggle the connector on. Mate verifies that the required command (usually `npx`) is available and that the connector can start.
</Steps>

## Verifying a connector [#verifying-a-connector]

After enabling a connector, you can verify it works by:

1. Opening a new **Agent Chat** tab
2. Asking the agent to use a tool from that connector

For example, with the GitHub connector enabled, ask: "List my open pull requests." If the agent successfully calls the GitHub tools, the connector is working.

## Command resolution [#command-resolution]

Connectors typically run via `npx` (Node.js package runner). Mate resolves commands in this order:

1. **Bundled runtime** — Mate includes its own Node.js, so `npx` works without a system Node.js installation
2. **System PATH** — falls back to your system's Node.js if the bundled one is unavailable

<Callout type="info">
  You do not need Node.js installed on your system. Mate bundles a complete Node.js runtime on macOS, Windows, and Linux.
</Callout>

## Credential storage [#credential-storage]

Credentials are stored locally on your device using platform-native secure storage. They are never sent to any server — only passed as environment variables to the connector process running on your machine.

To update or remove credentials, go back to the connector's settings page.

## Disabling a connector [#disabling-a-connector]

Toggle the connector off in Settings. The connector process stops, and the agent can no longer use its tools. Your credentials remain saved so you can re-enable it without re-entering them.

## Troubleshooting [#troubleshooting]

* **Connector fails to start**: Check that no firewall or security tool is blocking the `npx` process
* **Tools not appearing in chat**: Restart the agent chat session after enabling a new connector
* **Authentication errors**: Verify your API key/token is correct and has the required permissions
* **Timeout errors**: Some connectors take a few seconds to initialize on first run as `npx` downloads the package
