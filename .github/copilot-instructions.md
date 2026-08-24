# OnLex Website - Static One-Pager

OnLex Website is a Polish business website: a single-page, plain HTML/CSS/JS static site (no build step, no framework). It scrolls top-to-bottom through Hero, Services, How we work, FAQ, and Contact sections, plus two standalone legal pages (Privacy Policy, Terms of Service). Deployed to GitHub Pages via GitHub Actions.

## Structure

```
index.html          # one-pager: hero, services, process, faq, contact
privacy.html         # standalone legal page
terms.html           # standalone legal page
css/style.css        # all styling (Luxury Gold theme: black background, gold accents, serif headings)
js/main.js           # mobile nav toggle, active-section nav highlighting, scroll-reveal animations
favicon.svg
CNAME                # custom domain: onlex.net
```

There is no `content/`, `layouts/`, `themes/`, or Hugo config anymore — the site was migrated off Hugo/HugoBlox to plain static files.

## Local preview

No build step. Serve the repo root with any static file server, e.g.:

```
npx serve .
```

Then open the printed local URL (e.g. `http://localhost:3000`).

## Editing content

Edit the HTML directly in `index.html`, `privacy.html`, `terms.html`. Styling lives entirely in `css/style.css` (CSS custom properties at the top control the color palette). Behavior (mobile menu, scroll animations) is in `js/main.js`.

## Deployment

`.github/workflows/deploy-pages.yml` uploads the repository root as a Pages artifact and deploys it on every push to `main` (also runnable manually via workflow_dispatch). No Node/Hugo setup step is needed since there's no build.

## Important notes

- Keep the site framework-free unless a real need arises — it's intentionally a plain static site.
- `CNAME` at the repo root must stay in place for the `onlex.net` custom domain to keep working on GitHub Pages.
- Animations in `js/main.js` respect `prefers-reduced-motion`.
