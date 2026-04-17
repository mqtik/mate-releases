# Pairing Devices (/docs/getting-started/pairing-devices)



Mate lets you access your desktop sessions from any device on the same network. Your desktop is the server — it runs the terminals, AI agents, and editors. Paired devices are live mirrors that connect directly, with no cloud involved.

## How pairing works [#how-pairing-works]

Mate uses multicast UDP for automatic device discovery on your local network. When two devices running Mate are on the same Wi-Fi or LAN, they find each other automatically. No manual IP entry, no account creation, no cloud relay.

<Steps>
  ### Launch Mate on both devices [#launch-mate-on-both-devices]

  Open Mate on your desktop and on the device you want to pair (phone, tablet, or another computer).

  ### Wait for discovery [#wait-for-discovery]

  Devices on the same network appear automatically in the sidebar within a few seconds. You will see the other device's name show up under the device list.

  ### Tap to pair [#tap-to-pair]

  Select the discovered device in the sidebar. The first connection establishes the pairing. Once paired, the device remembers the connection for future sessions.
</Steps>

## What paired devices can do [#what-paired-devices-can-do]

Once paired, the remote device can:

* View and interact with all terminal sessions running on the desktop
* Chat with AI agents that are running on the desktop
* Browse and edit files through the IDE
* Preview web apps running on the desktop's localhost
* Send and receive files

<Callout type="warn">
  Mobile devices (iOS/Android) do not run sessions locally. All terminals, agent chats, and IDE sessions live on the desktop. The mobile app is a remote viewer and controller.
</Callout>

## Network requirements [#network-requirements]

* Both devices must be on the **same local network** (same Wi-Fi or LAN)
* Mate uses TCP port **53317** by default for communication (configurable in Settings)
* Multicast UDP must not be blocked by your router — most home and office networks allow it
* No internet connection is required for pairing

## Troubleshooting pairing [#troubleshooting-pairing]

If devices don't discover each other:

1. Confirm both devices are on the same Wi-Fi network
2. Check that no firewall is blocking port 53317 (TCP) or multicast (UDP)
3. On macOS, ensure Mate has local network permission in **System Settings > Privacy & Security > Local Network**
4. Try restarting Mate on both devices — this triggers a fresh multicast scan
5. If automatic discovery fails, check [Remote Troubleshooting](/docs/remote/troubleshooting) for manual connection options

## Multiple devices [#multiple-devices]

You can pair multiple devices with the same desktop. Each paired device appears in the sidebar, and switching between them shows that device's remote sessions. Your local device is always listed first.
