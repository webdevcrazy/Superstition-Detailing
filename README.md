# Superstition Detailing — Website

Single-page static site. No build step, no dependencies — just HTML/CSS.

## Deploy to GitHub Pages

1. Create a new repository on GitHub (e.g. `superstition-detailing`).
2. Upload everything in this folder (`index.html`, `assets/`, `.nojekyll`) to the repo root.
   ```bash
   git init
   git add .
   git commit -m "Superstition Detailing site"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/superstition-detailing.git
   git push -u origin main
   ```
3. In the repo: **Settings → Pages → Source: Deploy from a branch → Branch: main / (root) → Save**.
4. Your site goes live at `https://YOUR_USERNAME.github.io/superstition-detailing/` within a minute or two.

Tip: to use a custom domain later, add it under Settings → Pages → Custom domain.

## SEO setup included

- `robots.txt` — allows all search engines **and** AI crawlers (GPTBot, ClaudeBot, PerplexityBot, etc.)
- `sitemap.xml` — submit this at [Google Search Console](https://search.google.com/search-console) after deploying
- `llms.txt` — a plain-language business summary that AI assistants can read
- JSON-LD structured data in `index.html` — LocalBusiness (AutoDetailing) + FAQ schema

### Custom domain: superstitiondetailing.com

All URLs in the site already point to `https://superstitiondetailing.com/` and a
`CNAME` file is included, so GitHub Pages will pick up the domain automatically.
To finish the hookup:

1. In the repo: **Settings → Pages → Custom domain** → enter `superstitiondetailing.com` → Save, and check **Enforce HTTPS** once available.
2. At your domain registrar, add these DNS records:
   - **A records** for `superstitiondetailing.com` pointing to GitHub Pages IPs:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - **CNAME record** for `www` pointing to `YOUR_USERNAME.github.io`
3. DNS can take up to a few hours to propagate; HTTPS certificate issues automatically after that.

### To actually rank #1 (the stuff a website alone can't do)

1. **Claim/verify your Google Business Profile** and add this website URL to it — this is the single biggest factor for "near me" searches and AI recommendations.
2. **Get more Google reviews** — ask every happy customer. Volume + recency matter more than anything on the page.
3. Submit the site to **Google Search Console** and **Bing Webmaster Tools** (Bing powers ChatGPT's search).
4. Keep name/phone identical everywhere (Google, Instagram, site) — consistency builds trust with both search engines and AI.
