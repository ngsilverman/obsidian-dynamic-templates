# Obsidian Dynamic Templates Plugin

⚠️ **This plugin is in early development.** It may be subject to breaking changes. Use it at your own risk.

**The main goal of this plugin is to offer a templating system where the generated content can be updated when state changes AND exists as plain Markdown.** Should you stop using the plugin, or Obsidian altogether, you will not lose the dynamic content that has already been generated in your notes. And, because the templates produce plain Markdown, they are fully compatible with [Obsidian Publish](https://obsidian.md/publish).

- A dynamic template reference can be inserted as a section anywhere in a Markdown note.
- Templates are backed by a JavaScript file which outputs Markdown.
- [Dataview](https://github.com/blacksmithgu/obsidian-dataview)'s JavaScript API can be used.
- The content generated by the templates is saved as regular Markdown.
- In reading view, or if the note is published, only the generated content is visible.

## Basic Usage

In order to remain invisible in reading view, the dynamic template syntax uses [Markdown comments](https://help.obsidian.md/Editing+and+formatting/Basic+formatting+syntax#Comments) to write _template references_:

```
%%{ template: 'templates/foobar.js' }%%
```

Where `templates/foobar.js` is the _template script_, a JavaScript file in your vault which returns arbitrary Markdown, for example:

```js
// File: templates/foobar.js
const date = new Date().toLocaleDateString();
return `## Header
- Foo
- Bar
- Date: ${date}`;
```

**When a template reference is _invoked_ (using a shortcut, for example), the note is automatically edited and our original template reference turns into:**

```
%%{ template: 'templates/foobar.js' }%%
## Header
- Foo
- Bar
- Date: 2/21/2024
%% %%
```

`%%{ template: … }%%` marks the beginning of the templated section, and `%% %%` its end. Because they're Markdown comments, they don't show in reading view, but the header and the list do. **Each time the template is invoked, its current generated content is replaced with the new one.** For example, if we invoke this template the next day, this section of the note will be updated to:

```
%%{ template: 'templates/foobar.js' }%%
## Header
- Foo
- Bar
- Date: 2/22/2024
%% %%
```

## Full Documentation

For more, including how to use arguments and Dataview, see the full [Obsidian Dynamic Templates Documentation](https://nates.foo/obsidian-dynamic-templates-plugin).

## Installation

This plugin is not yet available via the community plugins interface of Obsidian, but you can install it manually:

1. Clone this repository in `YourVault/.obsidian/plugins`
2. Make sure your NodeJS is at least v16 (`node --version`)
3. `npm i` or `yarn` to install dependencies
4. `npm run build` to build the project
5. Enable it from Obsidian settings > Community plugins > Installed plugins
