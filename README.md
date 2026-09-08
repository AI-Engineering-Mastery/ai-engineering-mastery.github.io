# ai-engineering-mastery.github.io

Landing page for **Production-Ready RAG & Backend Architecture** by Ganesh Sah.
Static site, no build step, no dependencies. Deployed with GitHub Pages.

## Deploy

This repo **must** be named `ai-engineering-mastery.github.io` and live in the
`AI-Engineering-Mastery` organization for the root URL to work.

```bash
git init -b main
git add .
git commit -m "Landing page"
git remote add origin git@github.com:AI-Engineering-Mastery/ai-engineering-mastery.github.io.git
git push -u origin main
```

Then: **Settings → Pages → Source = Deploy from a branch → `main` / `(root)` → Save.**
Live in 1–2 minutes at https://ai-engineering-mastery.github.io

## Before going live

1. **Paddle client token.** Open `index.html`, find the `PADDLE CONFIG` block near the
   bottom, and replace `REPLACE_WITH_YOUR_PADDLE_CLIENT_TOKEN`.
   Get it from Paddle → Developer Tools → Authentication → Client-side tokens.
   Use `PADDLE_ENV = "sandbox"` with a `test_` token while testing.
2. **Approve the domain in Paddle.** Paddle → Checkout → Website approval →
   add `ai-engineering-mastery.github.io`. Checkout will not open without this.
3. **Social share image.** Save the exported Canva creative as `assets/og.png` (1200×675).
4. **Contact email.** Replace `hello@example.com` in the footer of `index.html`.
5. **Fallback price** (optional). Set `FALLBACK_PRICE` in the config block so a price
   still shows if Paddle's PricePreview call fails.

## Delivering the files after purchase

Paddle Billing does **not** host your PDF. See `fulfillment-worker/` — a Cloudflare
Worker that verifies the purchase with Paddle's API and serves the files from a
private R2 bucket behind 30-minute signed links.

After deploying it, set `WORKER` at the top of the script in `thanks.html` to the
worker's URL.

**Never commit the PDF or DOCX to this repo — it is public.**

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire landing page — HTML, CSS and JS in one file |
| `thanks.html` | Post-checkout success page (Paddle `successUrl`) |
| `assets/` | Four sample figures from the book |
| `.nojekyll` | Stops GitHub Pages running Jekyll over the files |
| `robots.txt`, `sitemap.xml` | Basic SEO |

## Price

Price ID `pri_01m1zddc0qk7xx33j0w8z8jw6j` is set in `index.html`.
The displayed price is fetched live from Paddle via `PricePreview`, so it is localised
per visitor and you never have to edit the page when you change the price.
