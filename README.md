# Rauff Consulting — Production Site

Single-page marketing site for Rauff Consulting. Static HTML, no build step, deployed on Vercel.

**Live:** https://rauff-consulting.vercel.app
**Canonical domain:** https://rauffconsulting.com (see *Domain setup* below)

## Files

| File | Purpose |
|------|---------|
| `index.html` | The entire site — content, styles and behaviour in one file |
| `404.html` | Branded not-found page (Vercel serves it automatically) |
| `site.webmanifest` | PWA metadata (name, icons, theme colours) |
| `vercel.json` | Security headers, clean URLs, cache rules |
| `sitemap.xml` / `robots.txt` | Search engine essentials |
| `og.jpg` | Social share card (LinkedIn / WhatsApp), 1200×630 |
| `apple-touch-icon.png` | Home-screen / bookmark icon, 180×180 |

## Site configuration — one block

Everything configurable lives in the `CONFIG` object inside `index.html` (search for `CONFIG`):

```js
var CONFIG = {
  whatsapp: "27744815163",               // WhatsApp number, digits only (country code, no +)
  email:    "team@businesshustle.co.za", // ⚠️ swap for Rauff's own inbox before launch
  endpoint: ""                           // optional form endpoint (Apps Script /exec URL); empty = mailto fallback
};
```

- **email** — currently the developer's inbox. Replace with Rauff's address *and* update the matching `"email"` field in the JSON-LD block near the top of `index.html`.
- **endpoint** — leave empty to keep the working mailto fallback, or paste a Google Apps Script / Formspree URL to receive enquiries in a spreadsheet.
- The WhatsApp float button, footer links, form button and the scoping tool all read from `CONFIG` — change it once and every touchpoint updates.

## Domain setup (rauffconsulting.com)

The site's canonical URL, sitemap, robots.txt and Open Graph tags already point at `rauffconsulting.com`. To make it live:

1. Vercel dashboard → project → **Settings → Domains** → add `rauffconsulting.com` and `www.rauffconsulting.com`.
2. At the domain registrar, point DNS at Vercel: `A` record `@ → 76.76.21.21`, `CNAME` record `www → cname.vercel-dns.com`.
3. Vercel provisions SSL automatically. canonical/OG/sitemap then resolve correctly with no code changes.

## Deploying

Any push to `main` auto-deploys to production via Vercel. To ship an update:

```bash
git add .
git commit -m "Describe the change"
git push
```

## Pre-launch checklist

- [ ] Swap `CONFIG.email` (and JSON-LD email) to Rauff's inbox
- [ ] Connect `rauffconsulting.com` in Vercel + DNS
- [ ] Install analytics (GA4 or Plausible) before launch day
- [ ] Confirm softened clay palette sign-off (Daily practice section)
- [ ] Test enquiry form, WhatsApp links and scoping tool on a phone
