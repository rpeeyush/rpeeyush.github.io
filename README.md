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
  Guidelines/
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

## Git guide: managing both blogs

Keep a separate local clone for each blog. The repository folder you run Git from determines which blog receives your changes.

| Blog | Folder on this laptop | Where notes belong |
| --- | --- | --- |
| `rpeeyush.github.io` | `Downloads\rpeeyush-blog\repository` | Inside `content\GAPS`, `content\Threat Hunting`, `content\Guidelines`, or another configured content folder |
| `peeyushrao.github.io` | `Downloads\peeyushrao-blog\repository` | Inside topic folders such as `CrowdStrike\CQL`, `CWPP`, or `Windows` |

Edit files inside the clone named `repository`, rather than the extracted ZIP's surrounding folder. Git publishes tracked changes in the clone. Check your destination at any time with:

```powershell
git remote -v
```

### Set the correct account for each blog (once per clone)

For the interview blog:

```powershell
cd "$env:USERPROFILE\Downloads\rpeeyush-blog\repository"
git remote set-url origin https://rpeeyush@github.com/rpeeyush/rpeeyush.github.io.git
git config user.name "Peeyush"
git config user.email "EMAIL_FOR_RPEEYUSH"
```

For the security blog:

```powershell
cd "$env:USERPROFILE\Downloads\peeyushrao-blog\repository"
git remote set-url origin https://peeyushrao@github.com/peeyushrao/peeyushrao.github.io.git
git config user.name "Peeyush Rao"
git config user.email "EMAIL_FOR_PEEYUSHRAO"
```

Replace each email placeholder with that account's verified GitHub email or its GitHub-provided private commit email. These settings are local to the clone. `user.name` and `user.email` control commit attribution; the account in the remote URL guides Git Credential Manager's login selection. Never put passwords or tokens in the URL.

### Everyday routine

Open PowerShell in the appropriate clone, then download the latest changes **before editing**:

```powershell
git pull --ff-only
```

Add or edit your Markdown, Word (`.docx`), or PDF files using File Explorer or your editor. Then review, commit, and push:

```powershell
git status
git add .
git commit -m "Update notes"
git push origin main
```

`git status` shows the pending changes. `git add .` stages additions, edits, and deletions beneath the current directory, so run it from the clone's root and check the listed files. `git commit` records them locally. `git push` sends your commits to GitHub.

If you only want to publish content changes in the interview blog, use `git add content` instead. For changes to site files such as `build.py`, JavaScript, CSS, or this README, use `git add .` or explicitly stage those files.

Choose the matching GitHub account when a login window appears. A saved login may be reused without a prompt.

### Upload directly through GitHub's website

1. Sign in to the correct account and open the correct repository.
2. Navigate to the destination folder.
3. Choose **Add file → Upload files**.
4. Select your files and commit the changes to `main`.

Both website uploads and Git pushes trigger the publishing workflow. If GitHub creates a separate branch, merge its pull request into `main` to publish those changes.

After a website upload, run `git pull --ff-only` in that blog's local clone before making further local edits. This keeps the website and local copy synchronized.

### Automatic publishing and folder behavior

- GitHub Pages uses **Settings → Pages → Source → GitHub Actions**. This is a one-time setting for each repository.
- Every push or website commit to `main` automatically builds and publishes the site.
- Routine updates do not need **Run workflow**. Use it for a manual retry or an initial deployment after changing Pages settings.
- The interview blog's workflow is **Publish interview blog**. The security blog's is **Publish security notes**.
- Wait for both build and deploy to succeed, then refresh the site. On Windows, **Ctrl + F5** forces a refresh.
- In the interview blog, the top-level folder names under `content/` must match `FOLDERS` in `build.py`; update that list when renaming a top-level folder.
- In the security blog, new and renamed topic folders are discovered automatically. With the child-folder update installed, selecting CrowdStrike includes all its notes, while selecting its CQL child includes only that subtree.
- Git does not track empty directories. Put a `.gitkeep` file in an empty folder if you want it retained.

### Move to another laptop

Push any unpushed work from the old laptop first. Install [Git for Windows](https://git-scm.com/install/windows) on the new laptop, reopen PowerShell, and clone both repositories:

```powershell
cd "$env:USERPROFILE\Documents"
git clone https://rpeeyush@github.com/rpeeyush/rpeeyush.github.io.git
git clone https://peeyushrao@github.com/peeyushrao/peeyushrao.github.io.git
```

Your new working folders are now:

```text
Documents/
  rpeeyush.github.io/
  peeyushrao.github.io/
```

Set your commit identity in each new clone, replacing the email placeholders:

```powershell
cd "$env:USERPROFILE\Documents\rpeeyush.github.io"
git config user.name "Peeyush"
git config user.email "EMAIL_FOR_RPEEYUSH"

cd "$env:USERPROFILE\Documents\peeyushrao.github.io"
git config user.name "Peeyush Rao"
git config user.email "EMAIL_FOR_PEEYUSHRAO"
```

Use the same pull → edit → status → add → commit → push routine in the chosen new folder. Authenticate with the corresponding GitHub account when asked. You do not need the original ZIP, the installer, Python, or another Pages setup to publish updates: the repositories contain the blog source and GitHub runs the builds. Python is only needed for an optional local preview.

When switching between laptops, push before leaving one and pull before editing on the other. You can also manage uploads through GitHub's website on any laptop.

### Troubleshooting

Run these from the affected clone:

```powershell
git status
git remote -v
git log -1 --oneline
```

| Message or symptom | What to do |
| --- | --- |
| `ahead of origin/main` | Your commit is local; run `git push origin main`. |
| `Everything up-to-date` | There are no unpushed commits. Check `git status` for unstaged files and confirm you edited the actual clone. |
| `nothing to commit, working tree clean` | No file changes are waiting to be committed; this alone does not prove the new version is deployed. Check the latest commit and Actions run. |
| `403` or `Permission denied to rpeeyush` for the security repository | Set its remote to `https://peeyushrao@github.com/peeyushrao/peeyushrao.github.io.git` and retry the push using the `peeyushrao` account. Do not create another commit for the same changes. |
| Git asks who you are | Set `git config user.name` and `git config user.email` in that clone, then retry the commit. |
| Push rejected because the remote contains new work | If your working tree is clean, run `git pull --rebase`, resolve any reported conflicts, then push. Preserve existing edits before attempting this; stop and ask for help if unsure. |
| `git pull --ff-only` fails | Stop and inspect `git status`. Local edits or diverging commits need attention; do not discard them or force-push. |
| Site still shows the old version | Check the correct repository's Actions tab. If no new run exists, verify your push. If the run failed, read the failed step. If it succeeded, use Ctrl + F5. |

Official references: [cloning repositories](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository), [multiple GitHub accounts with Git Credential Manager](https://github.com/git-ecosystem/git-credential-manager/blob/main/docs/multiple-users.md), and [GitHub Pages publishing settings](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).
