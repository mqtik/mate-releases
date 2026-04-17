# Projects (/docs/features/projects)



Projects let you group related sessions together. Instead of having a flat list of terminal tabs, editor tabs, and agent chats, you can organize them by project — keeping your frontend work separate from your backend work, or your personal projects separate from work.

## Creating a project [#creating-a-project]

1. Click &#x2A;*+** in the tab bar
2. Select **Project**
3. Choose a working directory for the project

The project opens as a container tab. Inside it, you can create terminals, editors, and agent chats that are scoped to that project's directory.

## What projects contain [#what-projects-contain]

A project can hold:

* **Terminals** that start in the project's working directory
* **Agent chats** scoped to the project's codebase
* **IDE tabs** that open the project's folder
* **Web previews** for dev servers running in the project

## Working directory [#working-directory]

Every session created within a project inherits the project's working directory. When you open a new terminal inside a project, it starts in the project root. When you start an agent chat, the AI assistant has context about the project's files.

This means you do not need to `cd` into your project directory every time you open a new terminal — the project handles that for you.

## Switching between projects [#switching-between-projects]

Projects appear as tabs in the main tab bar, just like terminals and editors. Click a project tab to switch to it and see its sessions.

<Callout type="info">
  Projects are a local organizational tool. They do not create any files in your project directory or modify your repository in any way.
</Callout>

## When to use projects [#when-to-use-projects]

Projects are most useful when you are working on multiple codebases at once. Instead of managing a sea of unlabeled terminal tabs, you can group everything by context:

* **Monorepo work**: One project for the frontend, another for the backend, another for infrastructure
* **Multi-repo development**: Separate projects for related but distinct repositories
* **Context switching**: Keep your side project's sessions separate from your work sessions
