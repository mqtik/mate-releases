# Custom Adapters (/docs/integrations/custom-adapters)



Gent talks to AI coding CLIs (Claude Code, Codex, Copilot, …) through **adapters**. An
adapter describes how to launch a CLI, what to show in its model / effort / slash-command
pickers, how to label its tools, and how to turn its output into Gent's chat. Most of an
adapter is **data, not code** — so you can add a new CLI by writing a JSON file.

<Callout type="warn">
  Custom adapters are part of Gent's runtime-extensible adapter system. This page documents
  the authoring format; availability ships with the rollout of the new adapter engine.
</Callout>

## How it works [#how-it-works]

Two things are always true:

* **The desktop host runs the adapter.** A paired phone is a viewer — it never spawns a
  CLI; it just mirrors what the host produces. Get it working on your Mac/PC and it works
  on your phone automatically.
* **Pure-data adapters can't execute anything.** When a CLI genuinely needs parsing code,
  that code runs in a sandbox (WASM) or as a signed first-party driver — never as
  unsandboxed downloaded code.

## Pick a tier [#pick-a-tier]

How you build the adapter depends on how the CLI talks.

<Cards>
  <Card title="Declarative (most CLIs)" description="The CLI prints a simple format (e.g. one JSON object per line). You write only a JSON spec. No app build." />

  <Card title="Sandboxed WASM" description="The CLI needs real parsing code. You ship a JSON spec plus a .wasm module that runs in a sandbox on the host. No app build." />

  <Card title="Bundled driver" description="Rare: a protocol needing full host trust. Requires a first-party code change shipped in an app release." />
</Cards>

## Write a declarative adapter [#write-a-declarative-adapter]

<Steps>
  ### Create the spec [#create-the-spec]

  A complete, working adapter for a CLI that emits one JSON object per line:

  ```json
  {
    "id": "acme-cli",
    "name": "Acme Coder",
    "version": "1.0.0",
    "schemaVersion": 1,
    "minAppVersion": "0.0.49",

    "spawn": {
      "command": "acme",
      "args": [
        { "flag": "--model", "value": "{model}", "when": { "var": "model", "op": "set" } },
        { "flag": "--json" },
        { "value": "{prompt}" }
      ],
      "oneShot": false
    },

    "models": [
      { "id": "acme-small", "label": "Acme Small" },
      { "id": "acme-large", "label": "Acme Large" }
    ],

    "tools": {
      "categories": { "edit": ["write_file"], "read": ["read_file"], "bash": ["run_shell"] },
      "display": { "read_file": { "label": "Read $path" } }
    },

    "driver": { "type": "stdio_json_lines" },
    "parsing": [
      { "match": { "jsonPath": "type", "equals": "assistant_text" },
        "extract": { "text": ["text"] },
        "emit": { "event": "assistantDelta", "text": "$text" } },
      { "match": { "jsonPath": "type", "equals": "tool_call" },
        "extract": { "toolName": ["tool"], "input": ["args"] },
        "emit": { "event": "toolStart", "toolName": "$toolName", "input": "$input" } },
      { "match": { "jsonPath": "type", "equals": "tool_result" },
        "extract": { "id": ["call_id"], "output": ["result"] },
        "emit": { "event": "toolDone", "toolId": "$id", "output": "$output" } }
    ]
  }
  ```

  ### Install it with Add Adapter [#install-it-with-add-adapter]

  Open **Add Adapter** in Gent, paste your adapter JSON (or a GitHub repo URL). Gent
  validates it and — if it spawns a command — shows you the exact command before anything
  runs. Approve to install.

  ### Test it [#test-it]

  Start a new agent chat with your adapter selected and send a prompt. Your model picker,
  tools, and messages should appear just like a built-in CLI.
</Steps>

## Models, effort, and slash commands [#models-effort-and-slash-commands]

These are **catalogs** — lists that drive the pickers. The picker shows the `label`; the
`id` is what gets sent to the CLI. Omit a catalog and its picker disappears.

```json
"models": [
  { "id": "acme-large", "label": "Acme Large", "contextWindow": 200000 }
],
"effortLevels": [
  { "id": "low",   "label": "Low",        "flag": "--effort" },
  { "id": "high",  "label": "High",       "flag": "--effort" },
  { "id": "xhigh", "label": "Extra High", "flag": "--effort" }
],
"slashCommands": [
  { "command": "/review", "description": "Review the current diff",
    "action": "prompt", "promptStarter": "/review " }
]
```

When the user picks a model or effort, its `id` becomes the variable `{model}` / `{effort}`.
You choose where it goes — and that depends on the CLI:

<Tabs items="[&#x22;As a launch flag&#x22;, &#x22;Per-turn (JSON-RPC CLIs)&#x22;]">
  <Tab value="As a launch flag">
    Most CLIs take model/effort as command-line arguments. Reference the variable in
    `spawn.args`. Changing the selection respawns the process.

    ```json
    "args": [
      { "flag": "--model",  "value": "{model}",  "when": { "var": "model",  "op": "set" } },
      { "flag": "--effort", "value": "{effort}", "when": { "var": "effort", "op": "set" },
        "validValues": ["low", "medium", "high", "xhigh", "max"] }
    ]
    ```

    `validValues` rejects an unknown effort; `when` skips the flag when nothing is selected.
  </Tab>

  <Tab value="Per-turn (JSON-RPC CLIs)">
    CLIs like Codex/Copilot accept model/effort with each turn, so they can change
    mid-session without restarting. Set `perTurnSettings` and put the variables in the
    message template instead of the spawn args.

    ```json
    "capabilities": { "perTurnSettings": true },
    "encoding": {
      "mode": "jsonrpc",
      "userMessage": {
        "method": "turn/start",
        "paramsTemplate": { "model": "{model}", "effort": "{effort}", "prompt": "{prompt}" }
      }
    }
    ```
  </Tab>
</Tabs>

<Callout type="info">
  The `models` list is a fallback. If your CLI can report its real models at runtime, the
  driver uses those and overrides the list.
</Callout>

## Turning output into chat [#turning-output-into-chat]

The `parsing` rules run against each line of the CLI's output; the first match wins. The
vocabulary is small on purpose — `match`, `extract`, `emit`, a shallow `setFlag`, and
`escalate`:

* `match` — pick lines by JSON path, value, regex, or field presence.
* `extract` — pull named fields (with ordered fallbacks).
* `emit` — produce a Gent event (`assistantDelta`, `toolStart`, `toolDone`, `turnComplete`, …).
* `escalate` — for anything stateful, hand off to a WASM or bundled driver instead of
  growing the rules.

If your CLI needs real, cross-line parsing logic, that's the cue for a **sandboxed WASM
adapter** (`driver.type: "wasm"` with a hash-pinned module) rather than stretching the
declarative rules.

## Publish to the registry [#publish-to-the-registry]

To share an adapter with everyone, open a pull request to &#x2A;*`mqtik/mate-adapters`** adding
your `specs/<id>.json` (and the `.wasm` for a WASM adapter). Once merged and signed, every
Gent install picks it up on the next refresh — no app update. Fixes ship as a new immutable
version, so rollback is a one-line change.

## Tips [#tips]

* Namespace your `id`; the built-in `claude` / `codex` / `copilot` ids are protected.
* Put every tool the CLI emits into `tools.categories`, or it shows up uncategorized.
* Tool categories can tighten approval, never relax it — unknown tools always ask.
* A bad or missing adapter degrades to a clear "needs update" state; it can't break the app.

See also: [Custom Connectors](/docs/integrations/custom-connectors) for adding MCP servers
(a different extension point — tools for an agent, rather than a new CLI).
