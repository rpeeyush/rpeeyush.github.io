# Peeyush's Commonplace Book

A collection of passages, ideas, observations, and reflections worth keeping and returning to. This book brings together what I read in fiction and non-fiction, discover on the internet, and explore through Hinduism.

**Read:** https://rpeeyush.github.io/  
**Repository:** https://github.com/rpeeyush/rpeeyush.github.io

## Purpose

Collect what catches my attention, record where it came from, and add my own understanding. Entries can be short quotations, reading notes, questions, connections between books, or longer reflections. This is a personal reference and a growing conversation with what I read, rather than an interview-preparation notebook.

## Current transition status

The content folders have been reorganized, but the website builder still has the old interview-blog configuration. Updating this README does not change the website's layout or publishing logic.

Before adding entries for publication:

1. Update `FOLDERS` in `build.py` to match the categories below:

   ```python
   FOLDERS = ['Fiction', 'Non-fiction', 'From Internet', 'Hinduism']
   ```

2. Update the old interview wording in the generated page title, header/footer, and homepage copy. The homepage folder count is currently hard-coded to `5`; it should reflect the configured categories.
3. Add a note or `.gitkeep` inside `content/Hinduism/` so Git retains that currently empty folder. The other three categories already contain `.gitkeep` files.

The workflow is currently still named **Publish interview blog**. That existing name is the one to look for in Actions until it is renamed. It already runs on pushes to `main`.

## Organization

```text
content/
  Fiction/
  Non-fiction/
  From Internet/
  Hinduism/
```

| Category | What belongs here |
| --- | --- |
| Fiction | Passages, characters, themes, and reflections from novels and stories |
| Non-fiction | Ideas and reading notes from essays, history, biography, and other non-fiction |
| From Internet | Links, short sourced excerpts, articles, and ideas encountered online |
| Hinduism | Notes on texts, philosophy, traditions, interpretations, and personal reflections |

Nested subfolders can organize authors, books, or themes. The current builder groups their entries under the configured top-level category; it does not provide separate child-folder filters. When adding or renaming a top-level category, also update `FOLDERS` in `build.py`.

## A suggested entry

Use a descriptive filename, such as `book-title-on-attention.md`. A first level-one heading supplies the page title; otherwise the filename is used. Front matter is optional and is skipped by the builder.

```markdown
# A thought worth keeping

## Source

- Author / speaker:
- Book / article / text:
- Page, chapter, verse, or URL:
- Translator / edition, where relevant:
- Date noted:

## Passage or idea

> A short excerpt, clearly distinguished from my own writing.

## My reflection

Why did this stay with me? What does it connect to? What do I question?

## Related notes

- [Another entry](another-entry.md)
```

The template is a suggestion, not a requirement. Keep exact quotations separate from paraphrases and personal comments. Include source details that help you find the original again. For translations, distinguish the text from a translator's or commentator's interpretation. For internet material, keep a source link and your own notes rather than reproducing entire articles.

## Supported files

- **Markdown (`.md`):** headings, tables, lists, fenced code, relative document links, and images.
- **Word (`.docx`):** converted into readable articles, including supported images and tables. Exact Word layout and pagination are not preserved. Save older `.doc` files as `.docx` first.
- **PDF (`.pdf`):** embedded browser viewer with an original download link; browsers without a viewer offer an open/download fallback.
- **Search:** note titles, categories, and the first 180 characters of Markdown/Word text. PDF contents are not indexed.

Keep images beside the entry or in a relative subfolder, then reference them with a relative path. The root README is repository documentation; it is not rendered as a commonplace entry.

**Everything published by this repository is public.** This blog currently has no special draft/staging-folder exclusion. Files anywhere under `content/` may be copied into the generated site's original-file area, even if their category is not listed in `FOLDERS`. Keep unpublished/private drafts outside `content/` and do not commit material you want kept private.

## Working folder on this laptop

```text
C:\Users\Shashi-Peeyush\Downloads\rpeeyush-blog\repository
```

This is the actual Git clone. Edit entries inside its `content/` directory. The surrounding `Downloads\rpeeyush-blog` directory may contain an old extracted copy; it is not the working folder for this blog.

## Add entries using Git

Open PowerShell and download the latest changes before editing:

```powershell
cd "$env:USERPROFILE\Downloads\rpeeyush-blog\repository"
git pull --ff-only
```

Add or edit entries in a category under `content/`, then:

```powershell
git status
git add content
git commit -m "Add commonplace entries"
git push origin main
```

`git add content` includes additions, edits, and deletions beneath `content/`. For documentation or site changes, stage the relevant files explicitly, for example `git add README.md build.py`. Review `git status` before committing.

Moving or deleting an entry updates the next build. Renaming an entry or changing its folder changes its generated page URL, so existing bookmarks to it may stop working.

## Upload through GitHub's website

1. Open this repository while signed in as **rpeeyush**.
2. Navigate to the destination category under `content/`.
3. Choose **Add file → Upload files**.
4. Upload your files and commit to `main`.

If GitHub creates a separate branch, merge its pull request into `main` to publish it. After a website upload, run `git pull --ff-only` in the local clone before making further local edits. There is no upload form on the public blog itself.

## Publishing

The GitHub Actions workflow installs dependencies, runs the tests, builds `dist/`, and deploys that generated site. Every push to `main` triggers it; **Run workflow** is only needed for an initial deployment or manual retry.

Set **Settings → Pages → Build and deployment → Source → GitHub Actions**. Do not use branch publishing alongside the custom workflow: it can serve repository documentation instead of the generated homepage.

Wait for both build and deploy to succeed, then refresh the site. Use **Ctrl + F5** if your browser shows an older version. The generated homepage is `dist/index.html`; it does not need to be created manually at the repository root.

## Two blogs, two GitHub accounts

| Site | Purpose | Local working folder |
| --- | --- | --- |
| `rpeeyush.github.io` | This commonplace book | `Downloads\rpeeyush-blog\repository` |
| `peeyushrao.github.io` | Security notebook | `Downloads\peeyushrao-blog` |

Run Git commands from the intended blog's working folder. Check its destination with `git remote -v`.

For this commonplace book, select the correct account once per clone:

```powershell
git remote set-url origin https://rpeeyush@github.com/rpeeyush/rpeeyush.github.io.git
git config user.name "Peeyush"
git config user.email "EMAIL_FOR_RPEEYUSH"
```

Replace the email placeholder with the account's verified email or GitHub-provided private commit email. Name/email settings control commit attribution; the account in the remote URL helps select the login. Complete sign-in as **rpeeyush** when prompted. A saved login may be reused without a prompt. Never put a password or token in the URL.

## Use another laptop

Push your latest work from the old laptop first. Install [Git for Windows](https://git-scm.com/install/windows), reopen PowerShell, and clone this repository:

```powershell
cd "$env:USERPROFILE\Documents"
git clone https://rpeeyush@github.com/rpeeyush/rpeeyush.github.io.git
cd rpeeyush.github.io
git config user.name "Peeyush"
git config user.email "EMAIL_FOR_RPEEYUSH"
```

The new working folder is `Documents\rpeeyush.github.io`; use that folder instead of the Downloads path on this laptop. Continue with pull → edit → status → add → commit → push.

To manage the separate security blog on that laptop too:

```powershell
cd "$env:USERPROFILE\Documents"
git clone https://peeyushrao@github.com/peeyushrao/peeyushrao.github.io.git
```

Configure its commit identity inside its own clone and sign in as **peeyushrao** when pushing. You do not need the original ZIP, installer, Python, or another Pages setup to publish from another laptop. Python is only needed for local preview. Push before switching laptops and pull before editing on the other one.

## Repository files and optional preview

| Path | Purpose |
| --- | --- |
| `content/` | Entries, original documents, and related images |
| `build.py` | Category configuration and static-site generation |
| `assets/` | Layout styles and search/filter behavior |
| `tests/` | Automated builder checks; retain this folder |
| `.github/workflows/pages.yml` | Build and deployment automation |
| `requirements.txt` | Python dependencies |
| `dist/` | Generated site, excluded from Git |

For a local preview, use Python 3.13, matching the workflow:

```powershell
python -m venv .venv
.venv\Scripts\python -m pip install -r requirements.txt
.venv\Scripts\python -m unittest discover -s tests
.venv\Scripts\python build.py
.venv\Scripts\python -m http.server 8000 --directory dist
```

Open http://localhost:8000. On macOS/Linux use `.venv/bin/python`. Do not commit `.venv/`, `__pycache__/`, or `dist/`.

## Troubleshooting

Start with `git status`, `git remote -v`, and `git log -1 --oneline` from this clone.

| Symptom | Check |
| --- | --- |
| New categories do not appear | Match their exact names in `build.py`'s `FOLDERS`; see the transition checklist above. |
| Empty category missing from GitHub | Add an entry or `.gitkeep`; Git does not track empty directories. |
| Working tree clean but expected changes missing | Confirm you edited this clone rather than the surrounding extracted copy. |
| Branch ahead of `origin/main` | Commit is local; run `git push origin main`. |
| Permission denied / HTTP 403 | Confirm the remote selects `rpeeyush` and authenticate with that account. |
| Pull or push rejected | Inspect local changes and remote updates; do not discard edits or force-push. |
| Workflow failed | Open the failed step in Actions and read its error. |
| Old layout or README shown on the live site | Confirm Pages uses GitHub Actions, check the latest deployment, then Ctrl + F5. |

References: [cloning repositories](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository), [multiple GitHub accounts](https://github.com/git-ecosystem/git-credential-manager/blob/main/docs/multiple-users.md), and [Pages publishing settings](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).
