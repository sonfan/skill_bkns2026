---
name: content
description: "SEO content creation, topic clusters, and blog publishing pipeline. Use for /seo (SEO-optimized article), /article (blog post), /brief (content brief), /cluster (topic cluster strategy), /competitor (competitor analysis), /refresh (content refresh), /internal-link (link optimization), /schema (structured data), /audit-content (content SEO audit). Triggers on: SEO, bài viết, article, blog, content, viết bài, keyword, từ khóa, cluster, schema, competitor."
---

# Content Skill — SEO Content Engine v2 + Topic Clusters + Schema (v7.0)

> 📂 Chi tiết bổ sung: `content/references/seo-advanced.md`

---

## /cluster [topic]
> Topic cluster strategy — pillar page + supporting content

```
STEP 1 — TOPIC RESEARCH:
  □ Define pillar topic (broad, high-search-volume)
  □ Identify 8-15 subtopics (long-tail, specific angles)
  □ Map search intent per subtopic (info/nav/transactional/commercial)
  □ Competitor cluster analysis: ai đã cover topic này?

STEP 2 — CLUSTER MAP:
  □ Pillar page: comprehensive guide (2000-4000 words)
  □ Cluster pages: focused articles (1000-2000 words each)
  □ Internal linking plan: every cluster → pillar (và ngược lại)
  □ Content calendar: publish order (pillar first, then clusters)

  CLUSTER MAP FORMAT:
  ┌─────────────────────────────────┐
  │     PILLAR: [Main Topic]        │
  │     (Comprehensive Guide)       │
  ├───────┬───────┬───────┬────────┤
  │ Sub 1 │ Sub 2 │ Sub 3 │ Sub 4  │
  │ (How)  │ (Why) │ (Best)│(Compar)│
  ├───────┼───────┼───────┼────────┤
  │ Sub 5 │ Sub 6 │ Sub 7 │ Sub 8  │
  │(Guide)│(Tools)│(Tips) │(Cases) │
  └───────┴───────┴───────┴────────┘

STEP 3 — PRIORITIZE:
  □ Difficulty vs opportunity matrix
  □ Which subtopics have lowest competition?
  □ Which have highest commercial intent?
  □ Recommended publish sequence

OUTPUT: Cluster map + content calendar + internal linking strategy
```

---

## /competitor [url]
> Deep competitor content analysis

```
ANALYSIS DIMENSIONS:

  CONTENT INVENTORY:
    □ Total published articles (estimate)
    □ Publish frequency
    □ Content types: blog / guide / case study / tool / video
    □ Average word count
    □ Top-performing pages (by estimated traffic)

  SEO ANALYSIS:
    □ What keywords do they rank for?
    □ Content gaps: keywords they DON'T cover
    □ Backlink profile: authority sources
    □ Featured snippets they own
    □ Schema markup usage

  CONTENT QUALITY:
    □ E-E-A-T signals: author bios, citations, expertise
    □ Visual content: images, infographics, videos
    □ Internal linking strategy
    □ Update frequency (last updated dates)
    □ User engagement signals (comments, shares)

  OPPORTUNITIES:
    □ Topics they cover poorly (thin content)
    □ Topics they haven't covered yet
    □ Better format possibilities (video, interactive)
    □ Outdated content they haven't refreshed

OUTPUT: Competitor analysis report + opportunity list + action recommendations
```

---

## /refresh [url]
> Content refresh workflow — update outdated articles for SEO boost

```
REFRESH CHECKLIST:

  CONTENT AUDIT:
    □ When was this last updated?
    □ Are facts/stats still accurate? Source dates?
    □ Are outbound links still alive? (check 404s)
    □ Has search intent changed for target keyword?
    □ New information available since publish?
    □ Competitor content: have they overtaken us?

  UPDATE ACTIONS:
    □ Update title + meta description (new year/data)
    □ Add new sections covering recent developments
    □ Replace outdated stats with current data
    □ Fix broken outbound + internal links
    □ Add new internal links to recent articles
    □ Improve images (WebP, better alt text)
    □ Add/update FAQ section (People Also Ask)
    □ Add/update Schema markup

  POST-REFRESH:
    □ Update "Last Updated" date prominently
    □ Request re-indexing in Google Search Console
    □ Share on social media (với "Updated" tag)
    □ Monitor ranking changes (2-4 weeks)

OUTPUT: Refresh diff + updated content + re-index instruction
```

---

## /internal-link [site]
> Internal linking optimization strategy

```
ANALYSIS:
  □ Crawl site structure (map all pages)
  □ Identify orphan pages (no internal links pointing to them)
  □ Identify hub pages (most internal links)
  □ Check anchor text diversity
  □ Map topic clusters → verify linking between cluster members

OPTIMIZATION RULES:
  □ Every page should be ≤3 clicks from homepage
  □ Pillar pages should have most internal links
  □ Anchor text: descriptive, varied, not exact-match spam
  □ New articles MUST link to 2-3 existing relevant articles
  □ Old articles SHOULD be updated to link to new related content
  □ No broken internal links

OUTPUT: Link map + orphan pages + recommended link additions
```

---

## /schema [type]
> Generate Schema.org structured data

```
SCHEMA TYPES:

  Article:        BlogPosting / NewsArticle / TechArticle
  FAQ:            FAQPage (rich snippet → more SERP real estate)
  HowTo:          Step-by-step guide (rich snippet)
  Product:        Price, availability, reviews
  LocalBusiness:  Address, hours, phone, reviews
  Organization:   Logo, social profiles, contact
  BreadcrumbList: Navigation path (SEO + UX)
  WebSite:        Sitelinks search box
  Person:         Author bio (E-E-A-T signal)
  VideoObject:    Video content on page

GENERATION PROTOCOL:
  □ Identify appropriate schema type for content
  □ Generate JSON-LD format (preferred by Google)
  □ Validate with schema.org spec
  □ Test with: https://search.google.com/test/rich-results

OUTPUT: JSON-LD code block ready to paste into <head>
```

---

## /brief [topic or keyword]
> Research và lập content brief trước khi viết

```
RESEARCH PHASE:
  □ Keyword analysis: search volume, difficulty, intent
  □ SERP analysis: top 10 results đang cover gì?
  □ Content gap: gì họ có nhưng thiếu? Gì họ không có?
  □ Search intent: informational / navigational / transactional / commercial?
  □ Related keywords: LSI, long-tail variations
  □ People Also Ask: questions to answer
  □ Featured snippet opportunity? (paragraph/list/table)

BRIEF STRUCTURE:
  Target keyword: [primary]
  Secondary keywords: [list 5-10]
  Search intent: [type]
  Target audience: [persona]
  Word count target: [range based on SERP analysis]
  Required sections: [H2 list]
  Must-answer questions: [People Also Ask]
  Tone: [technical/casual/professional]
  CTA: [what action after reading?]
  Schema type: [Article/FAQ/HowTo/Product]
  Internal links: [existing pages to link to]
```

---

## /article [topic or brief]
> Viết bài chuẩn SEO, E-E-A-T, đúng format WordPress

```
PRE-WRITING:
  □ /brief đã chạy? Nếu không → chạy brief trước
  □ /cluster: bài này thuộc cluster nào? (internal linking context)
  □ INSTINCTS.md: có pattern viết bài liên quan?

CONTENT FORMATS (chọn phù hợp search intent):
  □ How-to guide:     Step-by-step, numbered, actionable
  □ Listicle:         "Top N [topic]" — scannable, ranked
  □ Comparison:       "A vs B" — table, pros/cons
  □ Ultimate guide:   Pillar page, comprehensive, 3000+ words
  □ Case study:       Problem → Solution → Results
  □ Review:           Product/tool review, rating

STRUCTURE (SEO-optimized):
  □ Title (H1): target keyword trong 60 chars, compelling
  □ Meta description: 150-160 chars, include keyword, có CTA
  □ Introduction (150-200 words):
      - Hook: câu hỏi / stat / pain point
      - Problem acknowledgment
      - Promise: bài này giải quyết gì
      - NO keyword stuffing trong 2 câu đầu

  □ Body (H2/H3 structure):
      - H2s chứa secondary keywords tự nhiên
      - Mỗi section: 200-400 words
      - Bullet points / numbered lists cho scanability
      - Internal linking: 3-5 links relevant (cluster-aware)
      - External linking: 2-3 authoritative sources
      - Images: descriptive alt text với keyword

  □ Conclusion:
      - Tóm tắt key points
      - CTA rõ ràng (comment / share / next article)
      - FAQ section (rich snippet potential → /schema FAQ)

E-E-A-T SIGNALS (Google quality rater focused):
  □ Experience: practical examples, screenshots, personal insight
  □ Expertise: technical depth, accurate terminology
  □ Authoritativeness: cite authoritative sources, link to research
  □ Trust: transparent, up-to-date, no misleading claims

READABILITY:
  □ Flesch-Kincaid: grade 8-12
  □ Sentence length: avg <25 words
  □ Paragraph: max 3-4 sentences
  □ Transition words: 30%+
  □ Active voice: 80%+

VIETNAMESE SEO SPECIFICS:
  □ Keyword trong tiếng Việt: có dấu + không dấu variants
  □ Title: đặt keyword đầu, compelling, Unicode correct
  □ URL slug: không dấu, hyphens, no stop words
  □ Content: natural Vietnamese, avoid translated feel
```

---

## /seo [topic]
> Full SEO article với Yoast/RankMath optimization

```
YOAST / RANKMATH FIELDS (tất cả phải filled):
  □ Focus Keyphrase: exact match target keyword
  □ SEO Title: keyword đầu, ≤60 chars
  □ Meta Description: keyword, benefit, CTA, ≤160 chars
  □ Slug: keyword-only, no stop words, no dates
  □ OG Image: 1200×630px, text overlay nếu cần

CONTENT ANALYSIS TARGETS:
  □ Keyphrase in first paragraph ✓
  □ Keyphrase in SEO title ✓
  □ Keyphrase density: 0.5-2.5% ✓
  □ Outbound links: ≥2 ✓
  □ Internal links: ≥3 (cluster-aware) ✓
  □ Image alt attributes ✓
  □ Word count ≥ competitor average ✓
  □ Subheadings (H2/H3) ✓
  □ Flesch reading ease ≥60 ✓
  □ Schema markup included ✓

SERP FEATURE TARGETING:
  □ Featured snippet: paragraph (40-60 words) or list format
  □ People Also Ask: answer in 2-3 sentences, then expand
  □ FAQ rich result: add FAQPage schema
  □ How-to rich result: add HowTo schema with steps

WORDPRESS REST API PAYLOAD:
  {
    title: "...",
    content: "...[formatted HTML]...",
    status: "draft",
    categories: [term_id],
    tags: [term_ids],
    meta: {
      _yoast_wpseo_title: "...",
      _yoast_wpseo_metadesc: "...",
      _yoast_wpseo_focuskw: "...",
      rank_math_focus_keyword: "..."
    },
    featured_media: wp_media_id
  }
```

---

## /audit-content [URL or post ID]
> SEO audit bài viết đã publish

```
TECHNICAL SEO:
  □ Page load <3s (Core Web Vitals: LCP, CLS, FID)
  □ Mobile-friendly (responsive layout)
  □ HTTPS active
  □ Canonical URL correct
  □ No broken links (internal + external)
  □ Images have alt text + WebP format
  □ Structured data valid (Schema.org)
  □ Sitemap inclusion check

ON-PAGE SEO:
  □ Title: keyword present, ≤60 chars, compelling
  □ Meta description: filled, ≤160 chars, include CTA
  □ H1: exists, unique, contains keyword
  □ H2/H3 structure: logical, keyword variations
  □ Content length vs top competitors
  □ Internal links: quantity, relevance, anchor diversity
  □ Keyword density: 1-2%, natural placement
  □ Featured snippet opportunity missed?

CONTENT QUALITY:
  □ Last updated: nếu >6 tháng → cần /refresh
  □ Facts/stats: còn accurate? Check source dates
  □ Outbound links: không bị broken / redirected?
  □ E-E-A-T score: author expertise clear?
  □ Better media opportunities (video, infographic)?
  □ FAQ section present? (rich snippet opportunity)

OUTPUT: Score /100 + Priority fix list + estimated traffic impact
```
