# PDF Tools

A small offline PDF toolkit. Everything runs entirely inside the browser tab — no file is ever uploaded to a server.

- **index.html** — Landing page / grid of tools (this is what GitHub Pages serves by default)
- **unlock.html** — Remove an existing password from a PDF
- **lock.html** — Add a new AES-256 password to a PDF
- **merge.html** — Combine two or more PDFs into one, in a chosen order
- **images.html** — Export every page of a PDF as a PNG or JPEG, bundled into a ZIP
- **images-to-pdf.html** — Combine one or more photos (JPEG/PNG) into a single PDF
- **compress.html** — Shrink a PDF's file size, either by downsizing embedded images (keeps live text) or by rasterizing every page (works on anything, at the cost of selectable text)

## How it works
All tools use [MuPDF](https://mupdf.readthedocs.io/) compiled to WebAssembly (`mupdf.js`) to open/rewrite the PDF entirely in-browser.

## Deploying to GitHub Pages
1. Create a new **public** GitHub repository.
2. Upload all files in this folder (`index.html`, `unlock.html`, `lock.html`, `mupdf.js`, `mupdf-wasm.js`, `mupdf-wasm.wasm`) to the repo root.
3. Settings → Pages → set Source to the branch/folder containing these files.
4. Open `https://<username>.github.io/<repo-name>/` in Safari — you'll land on the tool picker.
5. Optional: Share icon → **Add to Home Screen** for a one-tap app-like icon.

## Adding more tools later
Duplicate `lock.html` or `unlock.html` as a starting template, and add a new card in `index.html`'s `.grid` pointing to it. All tools share the same `mupdf.js` / `mupdf-wasm.wasm` engine files, so there's no extra weight per tool beyond the new HTML file itself.

## Notes
- First load downloads the ~10 MB WASM engine; after that, Safari caches it.
- Locking uses AES-256 with the same password set for both "owner" and "user" passwords.
- Passwords containing a comma (`,`) are rejected — that character conflicts with how options are passed to the underlying library.
- MuPDF is licensed AGPL-3.0 — fine for personal use; if you ever redistribute a modified version publicly, that license applies.
