# Skills (/docs/integrations/skills)



Skills are reusable prompt templates and commands that you install into your AI coding CLIs. They add slash commands, specialized behaviors, and domain-specific knowledge to your agent chat sessions — like plugins for your AI assistant.

For example, a "code review" skill might add a `/review` command that instructs the agent to follow a specific review checklist. A "testing" skill might add `/test-spec` that generates tests from a specification file. Skills encode best practices into repeatable, shareable commands.

## How skills work [#how-skills-work]

When you install a skill, Mate places it in the appropriate directory for each CLI:

| CLI         | Skill directory    |
| ----------- | ------------------ |
| Claude Code | `.claude/skills/`  |
| Codex       | `.codex/skills/`   |
| Copilot     | `.copilot/skills/` |
| Shared      | `.mate/skills/`    |

Skills installed through Mate are symlinked across CLI directories, so a single skill works with all your agents without duplication. Install it once, use it everywhere.

Each skill is a markdown file that contains the prompt template and metadata the CLI uses to register it as a slash command.

## Browsing the marketplace [#browsing-the-marketplace]

<Steps>
  ### Open Settings [#open-settings]

  Go to the **Settings** tab in Mate.

  ### Navigate to Skills [#navigate-to-skills]

  Find the **Skills** section. This shows the marketplace — a browsable list of available skills organized by category.

  ### Browse and preview [#browse-and-preview]

  Each skill shows its name, description, and what slash commands it adds. You can preview the full prompt template before installing.

  ### Install [#install]

  Tap **Install** on any skill. Mate downloads it and symlinks it into the appropriate CLI directories. The skill is immediately available in your next agent chat session.
</Steps>

## Using skills in chat [#using-skills-in-chat]

Once installed, skills appear as slash commands in agent chat. Type `/` in the composer to see available commands. Select one to invoke the skill — the prompt template is sent to the agent, which follows its instructions.

Some skills are fire-and-forget (run a single task), while others are interactive (the agent asks follow-up questions based on the skill's template).

## Skill structure [#skill-structure]

A skill is a markdown file with frontmatter metadata:

```markdown
---
name: review-code
description: Review code changes with a structured checklist
---

Review the staged changes in this repository. For each file, check:
1. Are there any obvious bugs?
2. Is error handling adequate?
3. Are there any security concerns?

Provide your review as a structured list.
```

The CLI reads the frontmatter to register the slash command, and uses the body as the prompt template when invoked.

## Managing installed skills [#managing-installed-skills]

In the Skills section of Settings, you can see all installed skills and:

* **Uninstall** a skill to remove it from all CLI directories
* **Update** a skill if a newer version is available in the marketplace
* **View details** to see the full prompt template

## Custom skills [#custom-skills]

You can create your own skills by placing markdown files directly in `.mate/skills/` or the CLI-specific skill directories. Custom skills follow the same format as marketplace skills and appear alongside them in the slash command list.

This is useful for team-specific workflows — write a skill once, share the file, and everyone on the team gets the same commands.
