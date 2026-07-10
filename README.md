# The Sunday Folder

A working prototype website for **thesundayfolder.org** — free student ministry curriculum, plus affordable consulting for small churches (custom curriculum builds, custom graphics, AI coaching, and volunteer/leader training resources).

## What this is

A **single self-contained HTML file** — no build step, no framework, no dependencies. All HTML, CSS, and JavaScript live in one file (including the curriculum logo images, which are embedded as base64 data so nothing external needs to load).

- `curriculum-site.html` — the entire site

## Running it locally

Just open the file directly in a browser:

```
open curriculum-site.html
```

Or serve it with any static file server, e.g.:

```
npx serve .
```

No `npm install`, no build command — it's plain HTML/CSS/JS.

## Deploying to Vercel

Since there's no build step, keep the Vercel project config simple:

1. **Framework Preset:** `Other` (no framework detected / no build command needed)
2. **Build Command:** leave blank
3. **Output Directory:** the folder containing the HTML file (repo root, if that's where it lives)

**Important:** Vercel serves `index.html` by default at your domain root. This file is currently named `curriculum-site.html`, so you'll want to either:
- Rename it to `index.html` before pushing, **or**
- Add a `vercel.json` with a rewrite so requests to `/` resolve to `curriculum-site.html`

If your domain is showing the wrong branch or an old version after deploying, check **Settings → Git → Production Branch** and **Settings → Domains → (your domain) → Edit → Git Branch** in your Vercel project — both need to point at the branch you're actually pushing to.

## Site structure (what's in the file)

- **Header** — logo + cart button
- **Hero** — headline, CTAs, preview of the three flagship curriculum series
- **Trust strip** — three quick reassurance points
- **Tab navigation** — swaps between 7 views without page reload:
  - Free Student Ministry Curriculum (Inspired, Grindset, We Ball, Rent-Free)
  - Consulting (Custom Curriculum Build, Custom Graphics, AI Coaching, Fire Code & Hazmat)
  - Volunteer Resources ($7 each: Boundaries & Safety, Red Flags & Mandated Reporting, "What If a Student Says...?", Yearly Strategy)
  - AI Tools for Ministry
  - What We Believe
  - Our Scope & Sequence
  - Why This Exists
- **Cart drawer** — in-memory only (resets on page refresh; no localStorage, per Claude Artifacts restrictions)
- **Lesson/resource preview modal** — shows a "Week 1" or "page 1" sample for each product
- **Footer**

## Known placeholders — replace before going live

- **Email:** `hello@thesundayfolder.org` throughout — confirm this is a real, monitored inbox
- **Checkout:** UI-only. The cart works, but "Continue to checkout" just shows a note — no real payment processor is connected (would need Stripe, Gumroad, etc.)
- **Booking buttons:** "Book a call" shows a placeholder note asking people to email instead — no real scheduling tool is wired in (would need Calendly or similar)
- **Pricing & business names:** confirm all prices, service names, and the Chad Anderson / Fire Code consultation listing are exactly what you want live before launch

## Notes for future edits

- The whole file can get edited directly — it's plain HTML/CSS/JS, no compiled assets to worry about
- Product data (curriculum + volunteer resources + AI tools) lives in JS objects near the top of the `<script>` tag — `products`, `aiProducts`
- Lesson/resource preview content lives in `lessonPreviews` and `resourcePreviews` objects just below that
