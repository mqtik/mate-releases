# Mobile Usage (/docs/remote/mobile)



Mate on mobile gives you full access to your desktop's sessions from your phone or tablet. It is not a simplified version — you get the same terminals, agent chats, editors, and web previews, just optimized for a smaller screen.

## Getting started on mobile [#getting-started-on-mobile]

<Steps>
  ### Install Mate [#install-mate]

  Download Mate from the App Store (iOS) or Google Play (Android).

  ### Connect to your desktop [#connect-to-your-desktop]

  Make sure your phone and desktop are on the same Wi-Fi network. Open Mate on both devices. Your desktop should appear in the sidebar automatically within a few seconds.

  ### Select your desktop [#select-your-desktop]

  Tap your desktop in the sidebar. The workspace switches to show your desktop's sessions.
</Steps>

## What you can do [#what-you-can-do]

### Terminals [#terminals]

Full terminal access from your phone. The terminal renders with xterm emulation, supports scrollback, and handles interactive programs. The on-screen keyboard works for typing commands, and you can scroll through output history.

### Agent chat [#agent-chat]

Interact with AI agent sessions running on your desktop. Send messages, view streaming responses, and see tool use in real time. This is great for monitoring long-running agent tasks while away from your desk.

### IDE and editor [#ide-and-editor]

Browse your project's file tree and edit files. Changes save directly to the desktop's filesystem. The editor supports syntax highlighting and standard text editing gestures.

### Web preview [#web-preview]

View web apps running on your desktop's localhost. This is genuinely useful for mobile testing — see your responsive design on an actual phone screen, running from your actual dev server.

### File transfer [#file-transfer]

Send files from your phone to your desktop, or receive files from the desktop. Useful for sharing screenshots, photos, or documents without going through a cloud service.

## Tips for mobile [#tips-for-mobile]

* **Landscape mode** gives you more horizontal space for terminals and code editing
* **Swipe** to switch between tabs
* **Long press** for context menus on tabs and sessions
* **Create sessions** from your phone — they are created on the desktop but you can interact with them immediately

<Callout type="info">
  Your phone does not run terminals, AI agents, or the IDE locally. All processing happens on the desktop. Your phone sends input and displays output over the network connection.
</Callout>

## Creating sessions remotely [#creating-sessions-remotely]

You can create new terminals, agent chats, and other sessions from your phone. When you do, the session is created on the paired desktop — your phone just tells the desktop to start it. This means:

* New terminals use the desktop's shell and filesystem
* New agent chats use the desktop's CLI installations and MCP connectors
* New IDE tabs browse the desktop's files

## Network considerations [#network-considerations]

Mobile works best on a stable Wi-Fi connection. The app handles temporary disconnections gracefully — if you walk out of range briefly and come back, it reconnects. For persistent connectivity issues, see [Troubleshooting](/docs/remote/troubleshooting).
