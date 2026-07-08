# PATCH — Agency site

Single-file marketing landing page for **PATCH**, a UK field-marketing agency.
_"Every patch covered."_

The whole site lives in **`index.html`** — HTML, CSS, JS, SVG icons and imagery all in
one self-contained file. No build step, no framework, no dependencies.

---

## Run locally
Just open the file:

```bash
open index.html          # macOS
```

…or serve it (nicer for testing, avoids any file:// quirks):

```bash
python3 -m http.server 5173
# then visit http://localhost:5173
```

---

## Connect this folder to the GitHub repo
Repo: **https://github.com/johnpbell7/Patch-Agency**

From inside this folder:

```bash
git init
git add .
git commit -m "PATCH landing page"
git branch -M main
git remote add origin https://github.com/johnpbell7/Patch-Agency.git
git push -u origin main
```

If the remote already has commits (e.g. a README created on GitHub), pull first:

```bash
git pull origin main --allow-unrelated-histories
# resolve any conflicts, then:
git push -u origin main
```

Day-to-day after that:

```bash
git add -A && git commit -m "your message" && git push
```

### Staging-first (recommended)
```bash
git checkout -b staging      # work + review on staging
git push -u origin staging   # get a Vercel preview URL for this branch
# happy? merge to production:
git checkout main && git merge staging && git push
```

---

## Deploy (Vercel)
Import the GitHub repo in Vercel once, then every push to the production branch
rebuilds automatically.

- Framework preset: **Other**
- Build command: _(none)_
- Output directory: _(root)_

It's a static `index.html`, so Vercel serves it with no configuration.

---

## Before you go live — quick checklist
- [ ] **Fonts:** paste your Adobe Fonts (Typekit) kit URL into the commented
      placeholder in `<head>` and uncomment it, to get real Proxima Nova. Until then
      it falls back to Montserrat.
- [ ] **Images:** currently embedded as base64 (keeps the file portable, ~500KB). For
      production you can move them to hosted assets and swap the `src`s if you prefer a
      lighter HTML file.
- [ ] Real copy / links / form endpoint wired up on the contact form.

## Editing
Brand colours and fonts are CSS variables at the top of the `<style>` block
(`:root`) — re-skin the whole site from there. See `CLAUDE.md` for full conventions.
