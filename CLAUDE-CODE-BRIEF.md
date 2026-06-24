# nayangoenka.me — Architecture & Claude Code Handoff Brief

## What's in this repo (deployable today)

A hand-coded static site with clean folder-based URLs:

```
/
├── index.html                  # Homepage (executive design, full SEO + JSON-LD Person)
├── 404.html                    # Branded fallback
├── sitemap.xml
├── robots.txt
├── CNAME                        # custom domain binding (nayangoenka.me)
└── blog/
    ├── index.html              # Blog listing (5 posts)
    ├── post-template.html       # Reusable post template (full BlogPosting schema)
    ├── today-im-a-believer/index.html
    ├── officially-yes-personally-no/index.html
    ├── my-leap-of-faith/index.html
    ├── entrepreneurial-nirvana/index.html
    └── life-is-all-about-keep-walking/index.html
```

Design: navy (#1a3a52) / cream (#f8f6f2), Playfair Display headings + Source Sans 3 body. SEO-complete.

---

## Deploying (Cloudflare Pages — recommended)

1. Cloudflare → Workers & Pages → Create → Pages → Connect to Git → select `nayan576/nayangoenka.me`
2. Build settings: framework = None, build command = blank, output directory = `/`
3. Custom domains → add `nayangoenka.me` (and `www` if wanted) → follow DNS instructions
4. SSL auto-provisions

GitHub Pages also works (the CNAME file is already in place): Settings → Pages → Source = main / root.

---

## Writing new posts (no CMS needed)

1. Draft with Claude — get a complete filled-in `index.html`
2. Drop it at `/blog/<slug>/index.html`
3. Add a line to `sitemap.xml`, add a card to `/blog/index.html`
4. Commit → auto-deploys

Git is the CMS. The post-template.html has all the SEO scaffolding pre-built.

---

## The Claude Code brief: migrate to Astro

**Goal:** Convert this hand-coded static site to an Astro project where blog posts are markdown files, preserving the exact visual design and URL structure.

**Requirements:**
1. Preserve design 1:1 — same palette, Playfair Display headings, Source Sans 3 body. Pull CSS from existing files into shared layout components.
2. Layouts: one BaseLayout.astro (header, footer, SEO head slots), one PostLayout.astro (article-header + body, BlogPosting JSON-LD from frontmatter).
3. Content collection: src/content/blog/*.md. Frontmatter: title, description, date, slug, optional dateModified. Body in markdown.
4. Routes: / (homepage), /blog/ (auto-generated listing sorted by date desc), /blog/[slug]/ (rendered from markdown). Match existing URLs exactly.
5. Auto-generate: sitemap.xml (@astrojs/sitemap), RSS feed at /rss.xml (@astrojs/rss), robots.txt.
6. SEO: per-page canonical, Open Graph, Twitter card, Person schema on homepage, BlogPosting schema per post — all driven from frontmatter/props.
7. Migrate the 5 existing posts into markdown.
8. Output: static build (astro build, output dir dist), deployable to Cloudflare Pages.

**Stretch:** /now page, reading-time estimates, RSS-to-newsletter hook.

---

## Editorial note (blog curation)

The original Google Sites blog had 14 posts. This rebuild keeps 5, on purpose:
- **Kept:** Today I'm a Believer (high SEO traffic, dad's recovery story), Entrepreneurial Nirvana, Life is All About Keep Walking, My Leap of Faith.
- **Reworked:** Officially Yes, Personally No — matured from a "be ruthless" business piece into a leadership essay on conviction and accountability.
- **Cut (political/religious — liability for executive search):** The PM We Never Had, My Take on Ram Mandir Issue, Letter to Pakistani Youth, Pen is Mightier or Sword.
- **Cut (dated/off-brand):** My Take on Net Neutrality (argued for Airtel Zero, which TRAI banned), 5 Things No One Should Pay For, Life – A Journey, First Sight, A Walk to Secure Future (prologue fragment).

If any cut post should return, fetch it from the original Google Sites export and run it through post-template.html.

---

## Links confirmed
- LinkedIn: https://linkedin.com/in/nayan576
- GitHub: https://github.com/nayan576
- Email: ping@nayangoenka.me

## Post-deploy SEO
Add property in Google Search Console → submit https://nayangoenka.me/sitemap.xml → request homepage indexing.
