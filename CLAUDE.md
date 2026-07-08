# CLAUDE.md — Patch Agency site

Context for Claude Code when working in this repo.

## What this is
A single-file marketing landing page for **PATCH** — a UK field-marketing agency
("Every patch covered."). The entire site — HTML, CSS, JS, SVG icons and imagery —
lives in **`index.html`**. There is no build step, no framework, no dependencies.

## Golden rules
- **Everything stays in `index.html`.** One self-contained file. Do not split into
  separate CSS/JS/asset files unless explicitly asked.
- **Edit surgically.** Make targeted changes; don't rewrite whole sections wholesale.
- **Keep it valid.** After edits, sanity-check that tags balance and the file still
  opens cleanly in a browser before committing.
- **Bold, high-contrast, distinctive.** No generic/templated "AI-looking" defaults.
  Preserve the lime highlighter signature and the navy/paper contrast.

## Design system (re-skin from `:root` in `index.html`)
Brand tokens live at the top of the `<style>` block. Change the look from there.

```
--paper:#F5F5F0  --paper-2:#ECEBE3  --card:#FBFBF7
--ink:#16180F    --ink-2:#1E2116    --body:#43463B   --muted:#787B6D
--navy:#020A1F   --navy-2:#0A1430
--line:#E2E1D7   --line-d:#1C2740
--lime:#B3DD03   --lime-2:#C7F016   --lime-ink:#5C760A
--disp / --sans : Proxima Nova (Montserrat fallback)
--ease : cubic-bezier(.22,1,.36,1)
```

Layout: light warm "paper" body with dark navy brand sections. Page order:
nav → navy hero → services → "the field route" (#how) → navy proof/stats →
industries → app (#app, near-black) → careers (lime band) → contact → footer.

Signature: the **"Every patch covered"** highlighter — a lime marker swipe behind a
word. On dark sections it's solid lime with dark text; on light it uses multiply.

## Things worth knowing
- **Fonts:** real Proxima Nova is loaded via an Adobe Fonts (Typekit) kit. There's a
  commented placeholder in `<head>`:
  `<!-- <link rel="stylesheet" href="https://use.typekit.net/YOURKIT.css"> -->`
  Paste the real kit URL there and uncomment it. Until then it falls back to
  Montserrat (loaded from Google Fonts) — visually close, not identical.
- **Images are embedded as base64** inline in the file, so the page is fully
  self-contained/portable. This makes the file large (~500KB). For production you may
  want to move them to hosted assets (e.g. `/public` on Vercel) and swap the `src`s —
  ask before doing this, it's a deliberate trade-off.
- **Motion respects `prefers-reduced-motion`** — keep it that way when adding animation.
- **The route section** (#how) has bigger navy nodes with a lime halo, a staggered
  "signal" pulse rippling node→node, a draw-in connector line, and a centred lime
  "loop" badge. Node geometry: connector `top`/mobile `left` must equal the node radius.

## Workflow (staging-first)
Build changes on a **`staging`** branch, review the deployed staging preview, then merge
to `main` only on an explicit "launch/ship it". Don't push straight to production `main`
without that go-ahead.

## Deploy
Static site → deploys as-is. Hosted via Vercel from the GitHub repo; pushing to the
production branch triggers a rebuild. No install/build command needed (framework preset:
"Other", output = repo root).
