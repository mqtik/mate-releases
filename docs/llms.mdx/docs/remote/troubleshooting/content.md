# Remote Troubleshooting (/docs/remote/troubleshooting)



Most remote connection problems come down to network configuration. Here are the common issues and their fixes.

## Devices not discovering each other [#devices-not-discovering-each-other]

**Symptom**: You open Mate on both devices, but they do not appear in each other's sidebar.

**Fixes**:

1. **Same network**: Confirm both devices are on the exact same Wi-Fi network. Some routers have separate 2.4GHz and 5GHz networks — make sure both devices are on the same one.

2. **Multicast blocking**: Mate uses multicast UDP for discovery. Some enterprise networks, guest networks, and mesh routers block multicast traffic. Try a different network or check your router's settings.

3. **macOS local network permission**: On macOS, go to **System Settings > Privacy & Security > Local Network** and make sure Mate is allowed.

4. **Firewall**: Check that no firewall is blocking:
   * TCP port **53317** (or your configured port)
   * Multicast UDP traffic

5. **Restart both apps**: Close and reopen Mate on both devices. This triggers a fresh multicast scan.

## Connection drops [#connection-drops]

**Symptom**: Devices pair successfully but the connection drops intermittently.

**Fixes**:

1. **Wi-Fi stability**: Check signal strength on both devices. Weak Wi-Fi causes intermittent TCP disconnections.

2. **Sleep/standby**: When a device sleeps, the network connection drops. Mate reconnects automatically when the device wakes, but there may be a brief delay.

3. **Network switching**: If your phone switches between Wi-Fi and cellular, the connection drops. Make sure your phone stays on Wi-Fi.

<Callout type="info">
  Mate uses exponential backoff for reconnection attempts. If the connection drops, it will try to reconnect automatically — starting at 10 seconds and backing off to 80 seconds between attempts.
</Callout>

## Terminal lag [#terminal-lag]

**Symptom**: Typing in a remote terminal feels slow or laggy.

**Fixes**:

1. **Network latency**: Remote terminals depend on network round-trip time. On a typical home Wi-Fi network, latency should be under 10ms. If it feels slow, check your network quality.

2. **High output programs**: Programs that produce large amounts of output (e.g., `cat` on a huge file, `find /` without filters) can cause temporary lag as the data streams over the network.

3. **Try restarting the session**: Close the terminal tab and open a new one. Occasionally a session can get into a degraded state.

## Port conflicts [#port-conflicts]

**Symptom**: Mate fails to start or pair, with errors about port 53317.

**Fix**: Another application is using port 53317. You can change Mate's port in **Settings**. Make sure both devices use the same port.

```bash
# Check what is using port 53317 on macOS/Linux
lsof -i :53317
```

## Web preview not loading [#web-preview-not-loading]

**Symptom**: Web preview tab shows a blank page or connection error.

**Fixes**:

1. **Server running**: Make sure your dev server is actually running on the specified port on the desktop
2. **Localhost binding**: Some dev servers bind to `127.0.0.1` only. Mate's reverse proxy handles this, but check that the server is running
3. **Port number**: Double-check you entered the correct port number in the web preview tab

## Agent chat not connecting remotely [#agent-chat-not-connecting-remotely]

**Symptom**: You can see agent chat tabs from a remote device but cannot send messages or see updates.

**Fixes**:

1. **CLI installed on desktop**: The AI CLI (Claude Code, Codex, etc.) must be installed on the desktop, not the remote device
2. **Process running**: Check that the agent chat process is still running on the desktop — it may have exited due to an error
3. **Reconnect**: Switch away from the remote device in the sidebar and switch back to force a reconnection

## Still stuck? [#still-stuck]

If none of the above fixes your issue:

* Check the app logs for error messages
* Try pairing on a different network (e.g., a phone hotspot) to isolate whether the issue is network-specific
* Verify that both devices are running the same version of Mate
