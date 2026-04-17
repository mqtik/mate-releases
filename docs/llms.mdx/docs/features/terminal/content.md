# Terminal (/docs/features/terminal)



Mate's terminal is a real PTY shell — not a simplified command runner. It uses full xterm emulation backed by a native PTY, so everything you expect from a terminal works: colors, cursor addressing, interactive programs, shell completion, and full Unicode support.

## Local terminals [#local-terminals]

A local terminal runs your default shell (zsh, bash, fish, or whatever you have configured) directly on the machine. Each terminal tab is an independent session with its own working directory and environment.

You can open as many terminal tabs as you need. Each one is a separate shell process.

### What works [#what-works]

* Full ANSI color and formatting (256-color and truecolor)
* Interactive programs: `vim`, `nano`, `top`, `htop`, `less`, and more
* Shell features: tab completion, history, aliases, custom prompts
* Mouse support in programs that use it
* Scrollback buffer for reviewing previous output
* Copy and paste with standard keyboard shortcuts

## Remote terminals [#remote-terminals]

When you select a paired remote device in the sidebar, terminal tabs show that device's sessions. Remote terminals connect over WebSocket and behave identically to local ones — same PTY, same scrollback, same interactive program support.

From a remote device (like your phone), you can:

* View and interact with terminals running on the desktop
* Create new terminal sessions on the desktop
* Use the same shell with full input support

<Callout type="info">
  Remote terminal sessions are owned by the desktop. Creating a terminal from your phone actually creates it on the paired desktop — your phone is just the viewer and controller.
</Callout>

## Working with multiple terminals [#working-with-multiple-terminals]

The tab bar shows all open terminals. You can:

* **Open** a new terminal with the + button or keyboard shortcut
* **Switch** between terminals by clicking tabs or using keyboard shortcuts
* **Reorder** tabs by dragging
* **Close** a terminal by clicking the tab's X button

## Terminal within projects [#terminal-within-projects]

Terminals can be organized inside [Projects](/docs/features/projects). When you create a terminal within a project, it starts in the project's working directory and is grouped with the project's other sessions.
