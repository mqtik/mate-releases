# Installation (/docs/getting-started/installation)



Gent runs on macOS, Windows, and Linux. Mobile apps for iOS and Android are available for remote access to a paired desktop.

## System requirements [#system-requirements]

| Platform | Minimum OS                 | Architecture           |
| -------- | -------------------------- | ---------------------- |
| macOS    | 12.0 Monterey              | Intel or Apple Silicon |
| Windows  | 10 (64-bit)                | x86\_64                |
| Linux    | Ubuntu 22.04 or equivalent | x86\_64, ARM64         |
| iOS      | 16.0                       | iPhone, iPad           |
| Android  | 10 (API 29)                | ARM64, x86\_64         |

## Download [#download]

Grab the latest release for your platform from GitHub:

<Cards>
  <Card title="Download Gent" href="https://github.com/mqtik/mate-releases/releases">
    All platforms — macOS .dmg, Windows .zip, Linux .tar.gz
  </Card>
</Cards>

## Install by platform [#install-by-platform]

<Tabs items="[&#x22;macOS&#x22;, &#x22;Windows&#x22;, &#x22;Linux&#x22;]">
  <Tab value="macOS">
    1. Download the `.dmg` file from the releases page
    2. Open the `.dmg` and drag **Gent** into your Applications folder
    3. Launch Gent from Applications — if macOS shows a security warning, go to **System Settings > Privacy & Security** and click **Open Anyway**
    4. Gent bundles its own Node.js runtime, so you do not need Node installed separately
  </Tab>

  <Tab value="Windows">
    1. Download the `.zip` file from the releases page
    2. Extract the zip to a folder of your choice (e.g. `C:\Program Files\Gent`)
    3. Run `Gent.exe` to launch
    4. Node.js is bundled — no separate installation needed
  </Tab>

  <Tab value="Linux">
    1. Download the `.tar.gz` file from the releases page
    2. Extract it: `tar xzf mate-linux-*.tar.gz`
    3. Run the `mate` binary from the extracted folder
    4. Node.js is bundled with the app
  </Tab>
</Tabs>

## Mobile apps [#mobile-apps]

iOS and Android apps are available for pairing with a desktop running Gent. Mobile devices act as remote mirrors — they connect to your desktop over the local network and let you interact with your sessions from your phone or tablet.

<Callout type="info">
  Mobile devices do not run terminals or AI agents locally. They connect to a paired desktop that does the heavy lifting. See [Pairing Devices](/docs/getting-started/pairing-devices) for setup instructions.
</Callout>

## Verify the installation [#verify-the-installation]

After launching Gent, you should see the workspace with a default terminal tab. Try typing a command to confirm everything works:

```bash
echo "Gent is ready"
```

If the terminal responds, you are good to go. Head to [First Session](/docs/getting-started/first-session) to learn the basics.
