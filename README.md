# webclaw

Static site of free, browser-based developer tools. No backend, no build step, no tracking.

## Local preview

```bash
cd webclaw
python -m http.server 5173
# open http://127.0.0.1:5173
```

## Project layout

```
webclaw/
├── index.html              # homepage (tool grid)
├── about.html
├── privacy.html            # required for AdSense approval
├── robots.txt
├── sitemap.xml
├── assets/
│   └── styles.css          # shared styles for all pages
└── tools/
    └── json-formatter/
        └── index.html      # first tool — fully self-contained
```

## Deployment — Cloudflare Pages (recommended)

Free, global CDN, free SSL, custom domains. Steps:

1. **Buy a domain** — Namecheap / Cloudflare Registrar / Porkbun (`webclaw.com` ~$10/yr).
2. **Push this folder to a new GitHub repo** (`webclaw`).
3. Go to https://dash.cloudflare.com → Workers & Pages → **Create** → **Pages** → **Connect to Git**.
4. Select the `webclaw` repo. Build settings:
   - Framework preset: **None**
   - Build command: *(leave empty)*
   - Build output directory: `/`
5. Click **Save and Deploy**. You get a `*.pages.dev` URL in ~30s.
6. In Pages → **Custom domains**, add `webclaw.com` and `www.webclaw.com`. Cloudflare auto-issues SSL.

Alternative hosts (also fine, all free): GitHub Pages, Netlify, Vercel.

## Search Console + Sitemap (do this before AdSense)

1. Open https://search.google.com/search-console → **Add property** → enter `https://webclaw.com`.
2. Verify ownership via DNS TXT record (Cloudflare panel → DNS).
3. In Search Console → **Sitemaps** → submit `https://webclaw.com/sitemap.xml`.
4. Wait 1–2 weeks for Google to index pages. Check **Pages** report to confirm indexing.

## Google AdSense (after indexing)

> Don't apply too early. AdSense reviewers look for: original useful content, clear navigation, About + Privacy pages, traffic. We already have the structural pieces — just need indexing + a bit of organic visits.

1. Apply at https://adsense.google.com.
2. After approval, replace the placeholder in every HTML `<head>`:
   ```html
   <!-- AdSense placeholder: replace ca-pub-XXXXXXXXXXXXXXXX after approval -->
   ```
   With:
   ```html
   <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-YOUR_ID" crossorigin="anonymous"></script>
   ```
3. Insert ad units into the reserved `<div class="ad-slot">` blocks on tool pages.

## Adding the next tool

1. Create `tools/<tool-slug>/index.html`. Copy the JSON formatter as a starting template.
2. Add a card to `index.html` (replace one of the `coming` placeholders).
3. Add a `<url>` entry in `sitemap.xml`.
4. Each tool page needs:
   - unique `<title>` and `<meta description>` targeting its keyword
   - canonical link
   - JSON-LD `SoftwareApplication` block
   - an `.article` section with 200+ words of original explanation (helps SEO and AdSense review)

## Roadmap

- [x] JSON Formatter & Validator
- [ ] Image Compressor (browser Canvas API)
- [ ] PDF Merge & Split (pdf-lib in browser)
- [ ] Base64 Encoder/Decoder
- [ ] QR Code Generator
- [ ] Timestamp Converter
