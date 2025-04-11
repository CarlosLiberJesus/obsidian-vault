# Introduction

Obsidian is by itself a powerful app, but since AI we will try to make it better. MCP will be a the bridge between LLMs and our personal documentation.

## First Step

Is to understand/set-up Obsidian... It will be used by 2 actors (Humans and Agents)!

### Has Humans

We can always read/right it our own brains, but we are forgetful, and use note-taking apps. I have to take the time and explain that this vault uses a lot of plugins in order to make it better, so I should refer the community plugins used:

| Plugin Name           |                         |                             |
| --------------------- | ----------------------- | --------------------------- |
| url-into-selection    | quickadd                | obsidian-outliner           |
| omnisearch            | editing-toolbar         | canvas-keyboard-pan         |
| typewriter-mode       | cmdr                    | simple-canvasearch          |
| obsidian-doubleshift  | dataview                | table-editor-obsidian       |
| recent-files-obsidian | obsidian-style-settings | obsidian-icon-folder        |
| obsidian-tasks-plugin | code-styler             | obsidian-excalidraw-plugin  |
| calendar              | callout-manager         | mononote                    |
| periodic-notes        | advanced-canvas         | emoji-magic                 |
| templater-obsidian    | callout-suggestions     | tag-wrangler                |
| nldates-obsidian      | obsidian-list-callouts  | open-in-new-tab             |
| vault-size-history    | dashboard-navigator     | obsidian-paste-image-rename |
| obsidian-annotator    | Local REST API          |                             |


So for to have a better experience, you should also install the plugins... But the vision I have as a dev, is beside having a tracing on what I have, I can try to empower LLM and MCP to use it as memory also

### Has An LLM

Each source-code part in a lego in a bigger architecture, so when I have VSCode open, I will only have context to
- [[Laravel-API]]
- [[Angular-Metronic]]

Is the folder that contains the framework/layer. So hopefully we will be able to auto-generate logs directly com VSCode Agent and grow the context it self.
- [[Releases]]
I'll try to have documentation per-release.

## Second Step

Prepare MCP, continue with [[obsidian-mcp-server]] or [[Docker]].