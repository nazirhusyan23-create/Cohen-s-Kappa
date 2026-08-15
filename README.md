# Kappa Calc — Cohen's Kappa Inter-Rater Reliability Calculator

A single-purpose, zero-backend web tool that calculates Cohen's Kappa (inter-rater
reliability) from a confusion matrix, entirely client-side. Built to rank for
long-tail, low-competition academic-utility search queries and to pass Google
AdSense review quickly.

## Why this niche

"Cohen's kappa calculator" and its long-tail variants (e.g. "inter-rater reliability
calculator online free", "kappa statistic calculator with confidence interval") get
steady search demand from grad students, clinical researchers, and qualitative coders,
but the top results are either paywalled stats suites, buried inside general
"statistics calculator" mega-sites, or don't report a confidence interval. That gap is
exactly what this tool fills — a fast, free, focused answer to one specific query.

## What's in this repo

```
index.html               → Cohen's Kappa Calculator (2 raters, ~500 words SEO content + FAQ schema)
fleiss-kappa.html          → Fleiss' Kappa Calculator (3+ raters)
percent-agreement.html      → Percent Agreement Calculator (paste two rater lists, no matrix needed)
compare.html                → Decision guide: which statistic fits your data (links all 3 tools)
about.html                   → About page (trust signal for AdSense + users)
privacy.html                  → Privacy policy (required by AdSense; noindexed on purpose)
contact.html                  → Contact page
styles.css                    → shared design system (no external CSS framework, no font requests)
ads.txt                       → AdSense publisher authorization file
robots.txt                     → allows crawling, points to sitemap
sitemap.xml                   → lists all 7 pages
vercel.json                    → clean URLs + cache headers for static hosting
```

All four content pages (Cohen's Kappa, Fleiss' Kappa, Percent Agreement, and the comparison
guide) are cross-linked via nav bar and "Related Tools" sections — a small SEO content
cluster: each targets a different long-tail keyword and passes authority to the others via
internal links, which tends to help all four rank faster than one isolated page would.

Each calculator also includes a **citation box** with an APA-style citation and a
one-click copy button — a small trust/credibility signal aimed at the academic audience,
who are more likely to link back to a tool they can cite properly in a methods section.

## Before you deploy — required edits

1. **Replace the placeholder domain.** Every file uses `https://cohen-s-kappa.vercel.app/` in
   `<link rel="canonical">`, Open Graph tags, and `sitemap.xml`/`robots.txt`. Find-and-replace
   that with your actual domain once you know it (your Vercel URL, or a custom domain).
2. **`contact.html`** — replace `hello@REPLACE-WITH-YOUR-DOMAIN.com` with a real inbox.
3. **`privacy.html`** — fill in the "Last updated" date and the analytics disclosure
   once you know exactly what scripts (AdSense, analytics, etc.) you're running.
4. **Add a real `og-image.png`** (1200×630) if you want rich social previews, and add
   `<meta property="og:image" content="...">` back into `index.html`'s `<head>` — it was
   left out here since no image asset exists yet.

## Deploying to GitHub + Vercel

### 1. Push to GitHub
```bash
cd kappa-calculator
git init
git add .
git commit -m "Initial commit: Cohen's Kappa calculator"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/kappa-calculator.git
git push -u origin main
```

### 2. Deploy on Vercel
- Go to [vercel.com/new](https://vercel.com/new) and import the GitHub repo.
- Framework preset: **Other** (it's a static site — no build command, no output
  directory override needed; Vercel will serve the root as-is).
- Click **Deploy**. You'll get a live URL in under a minute (e.g. `kappa-calculator.vercel.app`).
- Optional: add a custom domain under Project → Settings → Domains, then update the
  placeholder domain references (step 1 above) and redeploy.

### 3. Verify indexability
- Visit `/robots.txt` and `/sitemap.xml` on your live domain to confirm they load.
- Submit the sitemap in [Google Search Console](https://search.google.com/search-console)
  (Sitemaps → enter `sitemap.xml` → Submit).
- Use Search Console's URL Inspection tool to request indexing of the homepage directly
  — this is the single biggest lever for the "1–2 weeks to index" goal; don't just wait
  for Google to find it organically.

## Setting up Google AdSense

Your publisher ID (`ca-pub-2006445566626425`) is already wired in:

- The AdSense verification `<script>` is in the `<head>` of every page.
- All three ad slots in `index.html` (leaderboard, in-feed, rectangle) have real
  `<ins class="adsbygoogle">` units pointing at your publisher ID.
- `ads.txt` is included at the repo root with your publisher ID.
- `contact.html` uses `nh6639741@gmail.com`.

**One thing still to do:** each `<ins>` tag has `data-ad-slot="XXXXXXXXXX"` — that's a
placeholder. Once your AdSense account is approved, create ad units in the AdSense
dashboard (Ads → By ad unit → create one for each of the three slots) and swap in the
real slot IDs it gives you. Ads will not serve until those are real values.

Steps in order:
1. Deploy the site (see above) so you have a live URL.
2. Apply at [adsense.google.com](https://www.google.com/adsense/) with that domain.
3. AdSense reviewers check for: real, useful content (this tool + the ~500-word guide +
   FAQ qualify), a working About/Privacy/Contact page (included), and no placeholder/lorem
   ipsum text — double-check `privacy.html`'s "Last updated" date is filled in before you apply.
4. Once approved, create your three ad units and paste their slot IDs into `index.html`.
5. Note: **new AdSense accounts are frequently held to a "low traffic" review period.**
   Getting approved and getting your first real ad impressions are two separate
   milestones — budget for both.

## A note on the "hidden SEO text" ask

The original brief asked for a hidden keyword-rich text block. That's implemented here
as **visible, on-page content** instead (the "What Is Cohen's Kappa" article section),
not hidden via `display:none` or off-screen positioning. Cloaked or hidden text is a
violation of Google's spam policies and can trigger a manual action that tanks rankings
site-wide — the opposite of the goal. Real, visible, useful content targeting the same
keywords achieves the SEO goal without that risk.

## Extending the cluster further (optional)

Three tools are already live and cross-linked. If you want to keep compounding authority,
good next additions in the same niche are a Krippendorff's Alpha calculator (handles missing
data and ordinal/interval scales, a common ask from content-analysis researchers) or an
Intraclass Correlation Coefficient (ICC) calculator for continuous ratings rather than
categorical ones. Follow the same pattern: copy `styles.css`, reuse the nav/footer markup,
add the new page to `sitemap.xml`, and link it from the "Related Tools" section on the
existing three pages.
