---
name: seo-specialist
description: Implement SEO best practices for the project. Use this skill when the user needs meta tags, Open Graph tags, schema markup, structured data, sitemap generation, or any search engine optimization work. Ensures pages rank well and display correctly when shared on social platforms.
---

This skill guides SEO implementation. Read `requirements.md` and the existing codebase to understand what content exists, then apply appropriate SEO techniques. Derive all tags, schema types, and keywords from the actual content — never from a generic template.

## Approach

1. **Understand the content** — read the page content and requirements to determine what SEO elements are relevant
2. **Choose the right schema type** — match structured data to the actual content (Book, Product, FAQPage, Article, etc.)
3. **Write for humans first** — meta descriptions and titles should be compelling to click, not stuffed with keywords
4. **Validate everything** — schema must pass Google Rich Results Test, OG tags must render correctly in social debuggers

## Meta Tags

Every page needs at minimum:
- `<title>` — compelling, under 60 characters, primary keyword included
- `<meta name="description">` — 150–160 characters, summarizes the page value, includes a call to action
- `<link rel="canonical">` — the authoritative URL for this content
- Viewport and charset tags for proper rendering
- Language tags (`hreflang`) if the site supports multiple languages

## Open Graph & Social

- Choose the correct `og:type` based on actual content (book, product, article, website)
- Title and description can differ from meta tags — optimize for social context
- Image must be at least 1200x630px for optimal display
- Always include `og:url`, `og:site_name`, and `og:locale`
- Add Twitter Card tags (`summary_large_image` for content with strong visuals)
- Test with Facebook Sharing Debugger and Twitter Card Validator before launch

## Structured Data (JSON-LD)

- Use JSON-LD format (not microdata or RDFa)
- Choose schema types that match the actual page content
- Include all required properties for the chosen schema type
- Add optional properties where the data exists — don't fabricate data
- Multiple schema blocks are fine (e.g., Book + FAQPage on the same page)
- Validate with Google Rich Results Test

## Technical SEO

### Performance (Ranking Factor)
- Core Web Vitals: LCP < 2.5s, FID < 100ms, CLS < 0.1
- Image lazy loading with `loading="lazy"`
- WebP images with fallbacks
- CSS/JS minification and compression

### Semantic HTML
- Single `<h1>` per page, logical heading hierarchy
- Use semantic elements (`<article>`, `<section>`, `<nav>`, `<main>`, `<footer>`)
- All images have descriptive `alt` text
- `<figure>` and `<figcaption>` for meaningful images

### Crawlability
- Clean, readable URLs with hyphens
- XML sitemap covering all public pages and key images
- `robots.txt` allowing public content, blocking admin/checkout
- No orphaned pages — everything linked from navigation or content

## Content SEO

- Identify primary and secondary keywords from the domain and audience
- Place primary keywords naturally in: title, H1, first paragraph, meta description, image alt
- Short paragraphs, bullet points, and lists for scannability
- Internal anchor links for navigation within long pages

## Analytics Events

- Track meaningful conversion events, not just page views
- Key events depend on the page purpose — derive from requirements (CTA clicks, form submissions, purchases, scroll depth, etc.)
- Use descriptive event names and include context in metadata (which button, which section)
