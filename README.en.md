<p align="center"><img src="docs/assets/logo.svg" alt="vxtop" width="236"></p>


**A read-only 3D observatory of your computer.** Every folder is a cube of 27 cells, every open program another cube, and what is being used *right now* lights up and moves — by you, by other programs, or by an AI agent such as Claude Code.

[Español](README.md) · **English** · [Guía (ES)](docs/guia.md) · [Guide (EN)](docs/en/guide.md) · [Architecture](docs/architecture.md)

![vxtop: folders and programs as cubes, live](docs/assets/demo.gif)

| Selected folder | Tree view |
|---|---|
| ![](docs/assets/selected.png) | ![](docs/assets/tree.png) |

## Why

File managers show *where* things are. vxtop shows *what is happening*: which folders are being written, which program is touching them, what an AI agent is reading or editing, and how big and how old everything is — at a glance, in one space you can orbit, zoom and click.

It only **observes**. It never creates, changes or deletes anything it looks at and never acts on processes or the system.

## Highlights

- **Folders as data cubes** — 27 cells: file type × depth × age. Size, recency and activity are visible without opening anything.
- **Live** — only what is in use now: a folder appears when something touches it and fades out 8 s after the last activity. Every moving dot is a real file event, coloured by who did it: amber for Claude, teal for you, grey-blue for other programs.
- **Programs as cubes** — size is memory, lit cells are CPU, with the real app icon. The one in front of you gets an amber halo.
- **Hover preview** — point at a folder to see, in miniature, the windows of the programs using it and the images, videos and texts being touched.
- **AI aware** — follows Claude Code sessions: what they read, search and write, file by file.
- **Five views** — Space, System (processes and network), Tasks (a 3D task manager), Tree (like `tree`, every folder a cube) and a file viewer (code, images, video, audio, PDF, 3D models).
- **Indexes for whole drives** — millions of files, kept up to date in the background.
- **MCP server** — an AI can open folders as cubes and observe them.
- **No dependencies, offline** — plain Node.js and a bundled three.js. Nothing leaves your machine.

## Quick start

Requirements: [Node.js](https://nodejs.org) 18.15+ and Chrome or Edge. Windows is the most complete platform; Linux works; macOS is untested.

```bash
npx github:vxtop/vxtop            # live view of the whole machine
npx github:vxtop/vxtop C:\code\my-project --expand
```

Or clone it:

```bash
git clone https://github.com/vxtop/vxtop.git
cd vxtop
node server.js            # opens http://127.0.0.1:4827/
```

On Windows, double-click **`vxtop.vbs`** for a console-free app window that closes everything when you close it.

| Option | |
|---|---|
| `[folder ...]` | open these folders as cubes (default: live view) |
| `--expand` | also open their subfolders |
| `--port 4827` | port to listen on (127.0.0.1 only) |
| `--no-open` | don't open the browser |
| `--no-live` | no live view (don't watch the drives) |

**Controls:** one click selects, centres and opens · hover shows what is in use · drag to orbit, right-drag to pan, wheel to zoom · `H` frame all · `V` System · `T` Tasks · `A` Tree · `?` help.

## For AI agents (MCP)

```bash
claude mcp add vxtop -- node /path/to/vxtop/mcp.js
```

Tools include `vxtop_open`, `vxtop_observe`, `vxtop_cube`, `vxtop_file`, `vxtop_system` and `vxtop_focus`. See the [guide](docs/en/guide.md#for-an-ai-mcp).

## Privacy and safety

- Listens on `127.0.0.1` only. Every API call needs a per-session token; cross-origin requests are refused.
- Read-only: the only folder it writes to is its own (`~/.vxtop`: indexes, scenes, token).
- Live images of your windows are **off** until you allow them, and never leave your machine.
- Runs without administrator rights. Clicking the *read-only* badge restarts it with admin rights (Windows asks) to see the DNS cache and per-process open files.
- Side effects of the OS itself: reading a file updates its last-access time, and OneDrive downloads cloud-only files that are read.

More in [SECURITY.md](SECURITY.md).

## Development

```bash
npm test             # smoke test, no browser
npm run test:e2e     # interaction test in headless Chrome
npm run check        # syntax check
npm run demo         # a fictional studio to try or show vxtop without your own files
```

The client is a single ES module split into ordered files (`public/js/NN-*.js`); the server concatenates them with a source map — no build step. See [architecture](docs/architecture.md) and [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[Apache License 2.0](LICENSE) © 2026 virtuanista. You may use, modify and share vxtop, also commercially, as long as you keep the copyright and the [NOTICE](NOTICE) file — that is, credit the author — and state what you changed.
