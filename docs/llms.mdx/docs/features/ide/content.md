# IDE (/docs/features/ide)



Mate includes a built-in IDE for editing code without leaving the app. It is not a replacement for VS Code or JetBrains — it is a lightweight, always-available editor that is especially useful when you are working remotely from your phone or tablet.

## Opening the IDE [#opening-the-ide]

1. Click &#x2A;*+** in the tab bar
2. Select **IDE**
3. Choose a folder to open

The IDE shows a file tree on the left and an editor pane on the right. Click any file to open it.

## File tree [#file-tree]

The file tree is git-aware. It uses `git ls-files` to list tracked files, which means it automatically respects your `.gitignore` and skips build artifacts, `node_modules`, and other ignored directories. For non-git projects, it falls back to a standard directory listing.

You can:

* Navigate folders by expanding/collapsing them
* Open files by clicking
* Search files by name using the search bar at the top of the tree

## Editor [#editor]

The editor supports syntax highlighting for 100+ languages through the re\_editor package. Features include:

* Syntax highlighting with language auto-detection based on file extension
* Line numbers
* Find and replace
* Undo/redo
* Standard keyboard shortcuts for editing

<Callout type="info">
  The IDE is designed for quick edits and code review, not as a full development environment. For heavy editing sessions, pair it with your preferred desktop editor and use Mate's IDE for on-the-go changes.
</Callout>

## Single-file editor [#single-file-editor]

If you just need to edit one file without a full project tree, use the **Editor** tab type instead. It opens a single file in an editor with the same syntax highlighting and editing features.

## Remote editing [#remote-editing]

The IDE works from paired remote devices. When you open an IDE tab on a remote session, you are browsing and editing files on the desktop. Changes are saved directly to the desktop's filesystem.

This is particularly useful for:

* Quick fixes from your phone while away from your desk
* Reviewing code that an AI agent just modified
* Editing configuration files on a remote machine

## File browser [#file-browser]

The file browser modal lets you navigate your filesystem to find files or folders. It supports:

* Breadcrumb navigation
* Quick search with fuzzy matching
* Git-aware file listing that filters out ignored files
