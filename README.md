# Team File Share

A drag-and-drop file sharing interface for small teams, with instant preview, upload progress, and per-file timestamps. Built with plain HTML, CSS and JavaScript — no frameworks, no build step.

**Live demo:** https://asifur-rahman-ai.github.io/team-file-share/
*(update the repo name in the URL if you name it differently)*

**More demos:** [AI Requisition Slip](https://asifur-rahman-ai.github.io/requisition-slip-demo/) — a requisition form generator with auto amount-in-words, print and PDF export.

> **Demo mode:** the hosted version runs entirely in your browser. Files you drop are never uploaded anywhere and disappear when you refresh. All names and sample files are fictional.

---

## Features

- **One box per person** — drag a file onto someone's card, or click to browse
- **Multi-file upload** with a live progress toast for each file
- **Instant preview** — images and PDFs open in a modal; other types show a clear fallback
- **Serial numbers and timestamps** — `#1, #2, …` in upload order, with "Today / Yesterday / date" times
- **Delete your own uploads** — the delete button only appears on files added in the current session
- **Fully responsive** — works on phone, tablet and desktop; long file names truncate cleanly
- **Keyboard friendly** — `Esc` closes the preview

## Tech stack

| Layer | Technology |
|-------|-----------|
| Frontend | Vanilla HTML / CSS / JavaScript, single file |
| Styling | CSS variables, glass-style cards, sharp corners, system font stack |
| Demo storage | In-memory JS object + `URL.createObjectURL` |
| Reference backend | PHP 7.4+ (4 small endpoints) |

## Repository structure

```
team-file-share/
├── index.html            ← the complete demo (open it directly or host on GitHub Pages)
├── backend-reference/
│   ├── api/
│   │   ├── config.php    ← people list, limits, shared helpers
│   │   ├── upload.php    ← POST   person + file          → { success, filename, size }
│   │   ├── list.php      ← GET    ?person=               → { success, files: [...] }
│   │   ├── download.php  ← GET    ?person=&file=         → file stream
│   │   └── delete.php    ← POST   person + file          → { success }
│   └── storage/
│       └── .htaccess     ← blocks direct browser access to stored files
└── README.md
```

## Run locally

No install needed.

```bash
git clone https://github.com/asifur-rahman-ai/team-file-share.git
cd team-file-share
open index.html        # or just double-click the file
```

## Deploy to GitHub Pages

1. Push this repository to GitHub
2. **Settings → Pages**
3. Source: **Deploy from a branch** → branch `main`, folder `/ (root)` → **Save**
4. After a minute the site is live at `https://<your-username>.github.io/<repo-name>/`

GitHub Pages serves static files only, so it can run the demo but not the PHP backend.

## How the demo differs from the full version

| | Demo (this page) | Full version |
|---|---|---|
| Storage | Browser memory | Server filesystem |
| Upload | Simulated progress, no network | Real `XMLHttpRequest` with progress events |
| Who sees the files | Only you | Everyone using the page |
| Delete permission | Files added in this session | Files uploaded from the same browser |
| Refresh | Files are lost | Files persist; list auto-refreshes |

## Backend reference (self-hosting)

`backend-reference/` contains the PHP endpoints the full version talks to. To self-host:

1. Upload `backend-reference/` to any PHP 7.4+ host
2. Edit the people list in `api/config.php` (IDs must match the IDs in the frontend)
3. Make sure `storage/` is writable by PHP (permissions `775`)
4. Point the frontend at your API base URL and swap the simulated upload/list/delete functions for `fetch` / `XMLHttpRequest` calls to the endpoints above

**Built-in safeguards**

- Filename sanitising and path-traversal protection on every endpoint
- Executable types (`.php`, `.exe`, `.sh`, …) are rejected at upload
- `storage/.htaccess` denies direct URL access, so every download goes through `download.php`
- Server-side file size limit

## Design notes

- Accent colour `#2596be` on a deep navy background
- Cards use a subtle backdrop blur (kept low for performance on mobile)
- Initial data loading is deferred until after first paint, and polling pauses when the tab is hidden (full version)
- Layout uses flexible card heights rather than fixed ones, so long file lists never break the grid on small screens

## Limitations and ideas

- No authentication — the full version relies on the page URL staying private. For anything sensitive, add real login and server-side ownership checks.
- Delete ownership in the full version is tracked client-side, so it is a convenience, not a security boundary.
- Possible next steps: cloud storage integration (e.g. S3 or Microsoft Graph), folder-level permissions, virus scanning, expiring links.

## More projects

Part of a small set of single-file web tools built with the same approach (vanilla HTML/CSS/JS, no build step, mobile responsive, shared visual style).

| Project | What it does | Demo |
|---------|--------------|------|
| **Team File Share** (this repo) | Drag-and-drop file sharing with preview, progress and timestamps | [Open](https://asifur-rahman-ai.github.io/team-file-share/) |
| **AI Requisition Slip** | Requisition and disbursement form with automatic amount-in-words, print and PDF download | [Open](https://asifur-rahman-ai.github.io/requisition-slip-demo/) |

All demos use fictional data and run entirely in the browser.

## License

Add a license of your choice (MIT is a common default for portfolio projects).
