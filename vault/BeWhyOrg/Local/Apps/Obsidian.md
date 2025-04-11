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

## Plugins
- Intro
	- [level 0](https://youtu.be/gafuqdKwD_U?si=j6Q1j0Y26pZvVqKy)
	- [level 1](https://www.youtube.com/watch?v=d2BkvqbTPjk)
	- [level 2](https://www.youtube.com/watch?v=c6qfrRVUOO8)
	- [level 3](https://www.youtube.com/watch?v=Ehw3hUZNF1M)
- Tasks
	- [Tutorial](https://www.youtube.com/watch?v=quXNtjTe5WE)
	- [Documentação](https://publish.obsidian.md/tasks/Scripting/Task+Properties)
- Calendar
- Dataview
	- [Tutorial](https://youtu.be/Yzi1o-BH6QQ?si=BX50ogkTssOHMKdR&t=717)
- Templater
- Full Calendar
	- [Documentação](https://obsidian-community.github.io/obsidian-full-calendar/)
- Quick Add
	- [Tutorial](https://youtu.be/Yzi1o-BH6QQ?si=nYDJbF0UJ_yvpju1)

## Outra documentação
- Documentação da Comunidade, [plugins](https://publish.obsidian.md/hub/00+-+Start+here) e mais 
- [Vault](https://github.com/s-blu/obsidian_dataview_example_vault/tree/main/20%20Dataview%20Queries) com exemplos de querries para [tasks](https://github.com/obsidian-tasks-group/obsidian-tasks/tree/main/resources/sample_vaults/Tasks-Demo) e [dataview](https://s-blu.github.io/obsidian_dataview_example_vault/)
- css snippet [collections](https://github.com/r-u-s-h-i-k-e-s-h/Obsidian-CSS-Snippets?tab=readme-ov-file)
## Ideias descardadas
- Kanban
	- *ainda poderei testar que cria actividade ficheiro*
- [Daily Agenda](https://publish.obsidian.md/tasks/Advanced/Daily+Agenda#Instruction+contains+unexpanded+template+text)
- Project
- [Tracker](https://www.youtube.com/watch?v=W_leEJHBZW4)
- Database [File](https://youtu.be/ubkzPh29qyw?si=DyQjg-HnuzaA_H9v&t=1057)|
	- *com outros Plugins*
## Ideas
- O [Obsidian](https://docs.dhtmlx.com/vault/angular_integration.html) pusha em [[Angular]]???
 - Como é que se adicionam cores ao graph, o css falhou
 - Homepage *não estou a perceber*
 - Git ou Remotely Save 
 - Passar as tasks para o topo dos projectos, com filtros pelas tags
 - Tal como o Editor Toolbar um multi Quick-Add?
 - Plugins a ponderar
	 -  Kanban **needs full testing**
	 - Stacked Tabs - **needs full testing**
		 - Vertical Tabs?
	 - Footnotes shortcuts
	 - Hider (vs Commander)
	 - Themes
	 - quick-switcher++
	 - Mind Map 
	 - Caret => LLM
	 - Relay => Multi-User
- Ainda não percorremos as Tasks recorrentes, pode ser útil
```bash
tasks
not done
is recurring
due before tomorrow
```