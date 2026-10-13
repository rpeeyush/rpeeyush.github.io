# Peeyush's interview notebook

A GitHub Pages blog for `rpeeyush.github.io`. Upload notes; the publishing workflow builds the site automatically.

## Publish once

1. Copy the **contents** of this `blog` folder into the root of `rpeeyush/rpeeyush.github.io`. Include the hidden `.github` folder. Keep any existing files you need; review changes before committing.
2. Commit and push to `main`.
3. In the repository, open **Settings → Pages → Build and deployment → Source → GitHub Actions**.
4. Open **Actions → Publish interview blog**. Wait for a successful run. If the initial run failed before Pages was enabled, rerun it.
5. Visit https://rpeeyush.github.io/.

## Add notes

Use these folders (nested subfolders also work):

```
content/
  GAPS/
  Threat Hunting/
  Place Holder 1/
  Place Holder 2/
  Place Holder 3/
```

On GitHub, open a folder and choose **Add file → Upload files**, select your `.md`, `.docx`, or `.pdf` files, and commit to `main`. You can also push them using Git. Every push rebuilds the folder lists and note pages. Renaming or deleting files updates the next build too.

- **Markdown:** headings, tables, code blocks, lists, and relative links/images. A first level-one heading supplies the page title; otherwise the filename is used. Front matter is optional and skipped.
- **Word:** `.docx` content is converted into a readable article, including images and tables. Exact Word pagination and advanced formatting are not preserved. Old `.doc` files must first be saved as `.docx`.
- **PDF:** displayed in the browser's PDF viewer with an original download link. Browsers without a viewer show an open/download fallback.
- **Search:** searches note titles, folders, and the first 180 characters of Markdown/Word content. PDF text is not indexed.

There is no upload form on the public blog. Uploads happen in your GitHub repository. A file must be committed and the workflow must finish before it appears. Only upload material you intend to publish publicly. Keep note images next to the Markdown file and use relative image paths.

## Run locally

Requires Python 3.13 (matching the workflow).

```
python -m venv .venv
# Windows:
.venv\Scripts\python -m pip install -r requirements.txt
.venv\Scripts\python -m unittest discover -s tests
.venv\Scripts\python build.py
.venv\Scripts\python -m http.server 8000 --directory dist
```

On macOS/Linux use `.venv/bin/python`. Open http://localhost:8000. `dist/` is generated and should not be committed. The layout uses Google Fonts when available and system fonts offline.
