# Remote Sessions (/docs/remote/overview)



Mate's remote feature lets you access your desktop's sessions from any paired device on the same network. Understanding the architecture helps you get the most out of it.

## The mental model [#the-mental-model]

Your **desktop** (Mac, Windows, or Linux) is the source of truth. It runs the server and owns all session state:

* Terminal processes (PTY shells)
* Agent chat sessions (CLI subprocesses)
* IDE and editor state
* Web preview proxies
* File storage
* MCP connector processes

A **remote device** (phone, tablet, or another computer) is a paired mirror client. It does not run its own sessions. Instead, it connects to the desktop over the local network and presents a live view of the desktop's sessions.

<Callout type="info">
  Remote sessions are not copies. They are live mirrors. When you type in a terminal on your phone, the keystrokes go to the desktop's shell process, and the output streams back to your phone in real time.
</Callout>

## What remote devices can do [#what-remote-devices-can-do]

From a remote device, you can:

* **View and interact** with all terminal sessions on the desktop
* **Chat with AI agents** running on the desktop
* **Browse and edit files** through the IDE
* **Preview web apps** running on the desktop's localhost
* **Create new sessions** — these are created on the desktop, not on the remote device
* **Send and receive files** between devices

## How it connects [#how-it-connects]

Mate uses direct TCP connections over your local network. The default port is **53317**. Device discovery happens automatically via multicast UDP — no manual IP configuration needed.

The connection flow:

1. Both devices run Mate on the same network
2. Multicast discovery finds nearby devices automatically
3. Selecting a device in the sidebar establishes a TCP connection
4. All session data flows directly between devices — no cloud relay

## Device switching [#device-switching]

The sidebar lists your local device and all paired remote devices. Tapping a device switches the workspace to show that device's sessions:

* **Local device selected**: workspace shows your local terminals, chats, editors
* **Remote device selected**: workspace shows that remote device's sessions

Every UI component — tabs, projects, terminal lists — filters based on which device is currently selected.

## Security [#security]

All communication happens on your local network. No data leaves your network, no accounts are required, and no cloud services are involved. Device pairing is based on trust within your local network.

## Platform capabilities [#platform-capabilities]

| Capability            | Desktop              | Mobile                               |
| --------------------- | -------------------- | ------------------------------------ |
| Run terminal sessions | Yes (local)          | No (remote mirror only)              |
| Run AI agent CLIs     | Yes (local)          | No (remote mirror only)              |
| Edit files            | Yes (local)          | Yes (remote, edits saved to desktop) |
| Web preview           | Yes (local + remote) | Yes (remote)                         |
| File transfer         | Yes (send + receive) | Yes (send + receive)                 |
| Create sessions       | Yes (local)          | Yes (created on paired desktop)      |
