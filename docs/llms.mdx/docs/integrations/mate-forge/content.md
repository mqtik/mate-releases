# Gent Forge (/docs/integrations/mate-forge)



Gent Forge is `/connect anything` for agents. If Gent does not already ship the exact connector you need, ask for it. The agent can generate a local MCP server, register it with Gent, and make that new toolset available to future agent sessions.

The point is not "fill out a connector form." The point is:

```text
/connect printingpress.dev
```

or:

```text
/connect our internal billing admin
```

or:

```text
/connect the deployment checklist in this repo
```

Gent gives the agent the Forge guide, a local workspace under `~/.mate/mcps`, and a built-in `mate-forge.register` tool. The agent does the boring work: understand the target, design the MCP tools, implement the server, compile it, and register it.

## What Forge can generate [#what-forge-can-generate]

Forge is for generating MCP servers, not only API wrappers. A generated connector can expose tools for many kinds of targets:

| Target                  | Example tools                                                |
| ----------------------- | ------------------------------------------------------------ |
| SaaS products           | create project, read status, update customer, send message   |
| Public APIs             | search records, fetch details, submit requests               |
| Private/internal APIs   | run admin action, query account state, trigger workflow      |
| Websites                | fetch structured page data, submit forms, watch status pages |
| Local workflows         | run release checklist, package assets, prepare handoff       |
| Repo-specific utilities | validate config, inspect generated files, normalize data     |

If the agent can understand the interface and implement a safe MCP server around it, Forge can turn it into a Gent connector.

## Starting with `/connect` [#starting-with-connect]

Type `/connect` followed by the thing you want agents to use:

```text
/connect printingpress.dev
```

Gent expands that into a structured build task:

1. Read the Forge guide from `~/.mate/mcps/.template/GUIDE.md`
2. Create a project under `~/.mate/mcps/<service>/`
3. Design a small set of useful MCP tools
4. Implement the server
5. Install dependencies and compile it
6. Call `mate-forge.register` with the absolute path to `dist/index.js`

After registration, Gent can enable that generated connector for agent sessions.

## Give the agent context [#give-the-agent-context]

The best Forge prompts tell the agent what the connector should actually help with:

```text
/connect printingpress.dev so agents can create print jobs, check quote status, and download proof links
```

Useful context can include:

* API docs
* OpenAPI specs
* Example requests and responses
* Screenshots of an admin flow
* A README from the repo
* Environment variable names
* Captured request examples, if that is the easiest way to explain the API

Those are just inputs. The core workflow is: describe what you want to connect, and the agent builds the MCP.

## What `register` accepts [#what-register-accepts]

The Forge register tool validates a generated connector before Gent records it.

| Field         | Purpose                                                                    |
| ------------- | -------------------------------------------------------------------------- |
| `id`          | Lowercase connector ID with hyphens, such as `printingpress`               |
| `name`        | Display name shown in Gent                                                 |
| `description` | One sentence explaining what the connector does                            |
| `path`        | Absolute path to the compiled `dist/index.js` file                         |
| `credentials` | Optional credential fields shown in Gent's connector UI                    |
| `env`         | Optional environment variables, including `$KEY` references to credentials |

The compiled server path must be under `~/.mate/mcps`. That keeps generated connector registration scoped to Gent's MCP workspace.

## Credential flow [#credential-flow]

Forge-generated connectors can declare credential fields. Gent shows those fields in the Connectors UI, stores values locally, and injects them as environment variables when the MCP server starts.

Example credential declaration:

```json
{
  "key": "PRINTINGPRESS_API_KEY",
  "label": "PrintingPress API key",
  "required": true,
  "helpText": "Create an API key from your PrintingPress account settings"
}
```

Then the generated connector can reference it in `env`:

```json
{
  "PRINTINGPRESS_API_KEY": "$PRINTINGPRESS_API_KEY"
}
```

## Good generated connectors are small [#good-generated-connectors-are-small]

Forge works best when the generated MCP has a focused tool surface. Do not mirror an entire product API unless the agent really needs it.

Better:

* `create_print_job`
* `get_quote_status`
* `download_proof`
* `cancel_job`

Worse:

* 80 raw endpoints copied from an OpenAPI file with no workflow design

Small tool surfaces are easier for agents to choose correctly and cheaper to keep in context.

## Review generated code [#review-generated-code]

Forge makes connector creation fast, but generated code still deserves review:

* Test the connector with a real agent session
* Review tool names and descriptions for clarity
* Keep schemas narrow and explicit
* Avoid hardcoding secrets in generated files
* Prefer read-only tools first when connecting sensitive systems

## Related [#related]

* [Custom Connectors](/docs/integrations/custom-connectors)
* [Connector Setup](/docs/integrations/connector-setup)
* [Integrations Overview](/docs/integrations/overview)
