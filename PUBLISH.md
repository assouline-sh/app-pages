# Publishing the shared docs site to GitHub Pages

This folder (`~/app-pages`) is its **own** git repo — separate from your app source repos (those
stay private). One public repo hosts privacy + support pages for **all** your apps, each in its
own subfolder.

## Layout
```
style.css            ← shared by every app
index.html           ← landing page linking to each app
ayfm/                ← AYFM's pages (privacy.html, support.html)
hobbygo/             ← HobbyGo's pages
innerleaf/           ← Innerleaf's pages
_template/           ← copy this to add a new app (not linked from anywhere)
```

## Step 1 — create a new public repo
Browser: https://github.com/new → name it `app-pages` → **Public** → don't add a README → **Create**.

## Step 2 — push these files
This folder is already a git repo (`main` branch). From `~/app-pages`:
```bash
cd ~/app-pages
git add .
git commit -m "App docs: privacy & support pages"
git remote add origin git@github.com:assouline-sh/app-pages.git
git push -u origin main
```
*(gh CLI alternative, from `~/app-pages`: `git add . && git commit -m "App docs" && gh repo create assouline-sh/app-pages --public --source=. --push`)*

## Step 3 — enable GitHub Pages
Repo → **Settings → Pages** → Source: **Deploy from a branch** → **main** / **/(root)** → **Save**.
Wait ~1 min for the first build.

## URLs for App Store Connect
**AYFM**
- Privacy: `https://assouline-sh.github.io/app-pages/ayfm/privacy.html`
- Support: `https://assouline-sh.github.io/app-pages/ayfm/support.html`

**HobbyGo**
- Privacy: `https://assouline-sh.github.io/app-pages/hobbygo/privacy.html`
- Support: `https://assouline-sh.github.io/app-pages/hobbygo/support.html`

**Innerleaf**
- Privacy: `https://assouline-sh.github.io/app-pages/innerleaf/privacy.html`
- Support: `https://assouline-sh.github.io/app-pages/innerleaf/support.html`

All three apps answer App Store Connect's **App Privacy** questionnaire the same way: **Data Not
Collected** — no analytics, no third-party SDKs, no backend.

## Adding another app later
1. `cp -r _template app-four` (use a short, permanent slug — it becomes part of the public URL).
2. Edit `app-four/privacy.html` and `app-four/support.html` — replace the `APP NAME`, email, and
   body text.
3. Add a block for it in `index.html` so the landing page links to it.
4. Commit and push. Its URLs will be
   `https://assouline-sh.github.io/app-pages/app-four/privacy.html` (and `/support.html`).

That's it — no new repo or Pages setup per app. Push once and all apps' docs update together.
