# Ink

**Your thoughts, connected.** Ink is a local-first notes workspace delivered as a single `index.html` file. It runs directly in a modern browser and does not need a server, account, API key, build step, or network connection.

## Run Ink

Open `index.html` in a modern desktop or mobile browser or simply use [this link](https://vanish-coder.github.io/Ink/). For local development, you can also serve the directory with any static file server, for example:

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## Features

- Create, edit, search, favorite, pin, duplicate, and trash notes.
- Rich-text editing for headings, emphasis, lists, quotes, code, and links.
- Organize notes with folders and tags.
- Create daily notes using your local calendar date and a configurable template.
- Link notes by typing `[[Note title]]`; the graph and backlinks resolve matching titles.
- Browse a canvas graph of notes and their links.
- Import Markdown files and export individual notes as Markdown.
- Export and merge a versioned JSON workspace archive.
- Choose light, dark, or system theme and set an accent color.
- Use `Ctrl/Cmd+K` for the command palette and `Ctrl/Cmd+N` for a new note.

## Local storage and backups

Notes, folders, tags, and preferences are saved in this browser's local storage. Data does not sync to other devices. Clearing the browser's site data or removing its profile can erase the workspace.

To make a backup, open **Settings → Export JSON** and store the downloaded file somewhere safe. To restore or merge a backup, use **Settings → Import JSON**. Import validates the archive and adds its notes to the current workspace; conflicting note IDs are assigned new IDs. Markdown files can be imported from Settings as well.

The application does not currently store binary attachments, provide cloud backups, or use IndexedDB. Browser storage capacity and retention depend on the browser.

## Project structure

The application is intentionally contained in `index.html`:

- HTML provides the application root and browser metadata.
- CSS contains the visual system, desktop layout, and responsive rules.
- Inline JavaScript implements the workspace UI, editing, local persistence, search, organization, links, graph, and import/export.

There is no package manager or compilation step.

## Validation

The embedded JavaScript syntax can be checked with Node.js:

```sh
python3 -c "from pathlib import Path; s=Path('index.html').read_text(); Path('/tmp/ink-check.js').write_text(s.split('<script>',1)[1].split('</script>',1)[0])"
node --check /tmp/ink-check.js
```

No automated browser or end-to-end test suite is included.

## Deployment

Deploy `index.html` to any static file host. No environment variables or server-side services are required. If deployed over HTTPS, browsers generally allow installation-like shortcuts and more predictable local storage behavior. Each browser profile retains its own independent workspace.
