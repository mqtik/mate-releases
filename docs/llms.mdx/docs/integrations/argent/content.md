# Agentic Mobile (/docs/integrations/argent)



Agentic Mobile in Gent is powered by Argent, the MCP toolkit from Software Mansion. It gives agents a real mobile-app control surface instead of limiting them to source-code edits.

An agentic toolkit to control, debug, and profile iOS and Android applications. Your agent can navigate your app, explore the component tree, inspect network requests, and trace performance problems in your mobile apps.

Gent bundles Argent as `@swmansion/argent`, so you can enable it from the connector library without manually installing the package.

## What agents can do [#what-agents-can-do]

Agentic Mobile is useful when the agent needs to work against the running app:

* Navigate iOS and Android screens
* Tap, swipe, pinch, rotate, and type
* Launch, restart, reinstall, or reload the app
* Take screenshots and compare screen states
* Explore the React Native component tree
* Inspect native view hierarchy
* Read network logs and request details
* Start and analyze React or native profiler sessions
* Connect symptoms in the UI to source files, requests, and performance traces

The workflow is simple: the agent changes code, runs the app, drives the app, observes what happened, and keeps going.

## Example prompts [#example-prompts]

```text
Open the app, go through onboarding, and tell me why the continue button never enables.
```

```text
Navigate to checkout, inspect the failing network request, and patch the client-side validation.
```

```text
Profile the feed screen while scrolling and identify which components are causing the slow commits.
```

```text
Reproduce the login bug on Android, capture screenshots, inspect the component tree, and propose the smallest fix.
```

## Platform requirements [#platform-requirements]

Agentic Mobile runs from the desktop agent session. Your phone can control the Gent session remotely, but the simulator/emulator tooling runs on the paired desktop.

| Platform | Requirement                                                                          |
| -------- | ------------------------------------------------------------------------------------ |
| macOS    | Xcode for iOS simulators; Android SDK platform-tools and an emulator/AVD for Android |
| Linux    | Android SDK platform-tools and an emulator/AVD                                       |
| Windows  | Android SDK platform-tools and an emulator/AVD                                       |

iOS simulator control requires macOS and Xcode. Android requires `adb` plus a running emulator or configured AVD.

## Enabling Agentic Mobile [#enabling-agentic-mobile]

1. Open the Connectors UI
2. Find **Argent**
3. Enable it for the agent session
4. Start or restart the agent chat so the CLI receives the MCP server config

Argent does not require API credentials. It talks to local simulator/emulator tooling on your development machine.

## Permissions [#permissions]

Some Argent tools only read state, such as screenshots, hierarchy inspection, logs, and profiler queries. Other tools perform actions, such as tapping, swiping, launching apps, reloading Metro, or starting recordings.

Review action prompts the same way you would review shell commands: the agent is controlling a local simulator or emulator on your machine.

## Mobile app vs Agentic Mobile [#mobile-app-vs-agentic-mobile]

Gent's iOS and Android apps let you control desktop sessions from your phone. Agentic Mobile is different: it lets the desktop agent control iOS and Android simulators/emulators for app development.

Those two pieces work well together. You can start an agent task from your phone, let it drive a simulator on your desktop through Argent, and get the result back in the same Gent chat.

## Related [#related]

* [Agent Chat](/docs/features/agent-chat)
* [Mobile Usage](/docs/remote/mobile)
* [Connector Setup](/docs/integrations/connector-setup)
