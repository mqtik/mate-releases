# Voice Input (/docs/features/voice-input)



Voice Input adds speech-to-text to the agent chat composer. Instead of typing out a detailed prompt, tap the microphone icon and talk. Your speech gets transcribed into text in the composer, ready to send or edit before submitting.

This is especially useful on mobile devices where typing long prompts is tedious, or when you are describing a problem and just want to think out loud.

## STT Engines [#stt-engines]

Mate supports four speech-to-text engines, each with different tradeoffs:

| Engine       | Runs locally?        | Setup                   | Best for                             |
| ------------ | -------------------- | ----------------------- | ------------------------------------ |
| Native       | Yes                  | None                    | Quick dictation with zero setup      |
| Whisper      | Yes (after download) | One-time model download | Offline use, privacy-sensitive work  |
| Cloud STT    | No                   | API key                 | High accuracy, many languages        |
| Azure Speech | No                   | API key                 | Enterprise environments, Azure users |

### Native [#native]

Uses your platform's built-in speech recognition — Siri on Apple devices, Google Speech on Android. No setup required, works immediately. Accuracy depends on your platform's implementation, but it is solid for English and most major languages.

### Whisper [#whisper]

Runs OpenAI's Whisper model locally on your device. The first time you use it, Mate downloads the model (\~150MB). After that, everything runs offline — no network requests, no API keys, no data leaving your machine.

Whisper handles accents and background noise well, and supports dozens of languages out of the box.

### Cloud STT [#cloud-stt]

Uses a cloud-based speech-to-text API for transcription. Requires an API key configured in Settings. Offers high accuracy and broad language support, with the tradeoff that audio is sent to an external service for processing.

### Azure Speech [#azure-speech]

Microsoft's Azure Speech Services. Requires an Azure subscription and speech resource key. A good fit if you are already in the Azure ecosystem or need enterprise-grade speech recognition with compliance guarantees.

## How to use it [#how-to-use-it]

<Steps>
  ### Open an Agent Chat tab [#open-an-agent-chat-tab]

  Voice input works in the agent chat composer — the text field where you type messages to the AI agent.

  ### Tap the microphone icon [#tap-the-microphone-icon]

  You will see a mic icon in the composer bar. Tap it to start recording. If this is your first time, Mate may ask for microphone permission.

  ### Speak your message [#speak-your-message]

  Talk naturally. The transcription appears in the composer as you speak. When you are done, tap the mic icon again to stop.

  ### Review and send [#review-and-send]

  The transcribed text appears in the composer. Edit it if needed, then send it to the agent like any other message.
</Steps>

## Choosing an engine [#choosing-an-engine]

Open **Settings** and look for the **Speech-to-Text** section. You can select your preferred engine and configure any required credentials. The engine selection persists across sessions.

<Callout type="info">
  If you want fully offline voice input with no setup beyond the initial download, Whisper is the way to go. For zero-setup convenience, start with Native and switch later if you need better accuracy.
</Callout>

## Language support [#language-support]

All four engines support multiple languages. The available languages depend on the engine:

* **Native**: Whatever your OS supports — typically 30+ languages on modern devices
* **Whisper**: 99 languages (full list on OpenAI's Whisper documentation)
* **Cloud STT**: Varies by provider, typically 50+ languages
* **Azure Speech**: 100+ languages and variants

English variants (US, UK, Australian, etc.) are supported across all engines.

## Platform availability [#platform-availability]

Voice input works on all platforms where Mate runs: macOS, Windows, Linux, Android, and iOS. The Native engine uses platform-specific APIs, so the experience varies slightly — Siri's speech recognition on Apple devices, Google's on Android, and platform speech APIs on desktop. Whisper, Cloud STT, and Azure Speech behave identically across all platforms.
