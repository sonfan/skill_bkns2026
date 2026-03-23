# Content References — Advanced SEO Patterns (v7.0)

---

## Topic Cluster Template

```
PILLAR PAGE: "[Main Topic] — Complete Guide [Year]"
  Word count: 3000-5000 words
  Covers: overview of entire topic, links to ALL cluster pages
  Updates: quarterly

CLUSTER PAGES (8-15 articles):
  Format: "How to [subtopic]" / "Best [subtopic]" / "[Topic] vs [Topic]"
  Word count: 1000-2000 words each
  Links back to: pillar page + 2-3 sibling cluster pages
  Updates: when new info available

LINKING RULES:
  ✅ Every cluster → pillar (anchor = pillar keyword)
  ✅ Pillar → every cluster (anchor = cluster keyword)
  ✅ Related clusters → each other (2-3 cross-links)
  ❌ Don't force links where not relevant
  ❌ Don't use same anchor text for all links
```

---

## Content Calendar Workflow

```
MONTHLY RHYTHM:
  Week 1: Research + briefs (3-4 articles)
  Week 2: Write articles 1-2
  Week 3: Write articles 3-4 + optimize
  Week 4: Publish + promote + refresh 1 old article

QUARTERLY:
  □ Update pillar pages with new data
  □ Refresh top 5 traffic-driving articles
  □ Competitor analysis update
  □ Content performance review (GA4)
```

---

## E-E-A-T Scoring Rubric

| Dimension | Score 1-3 | Score 4-6 | Score 7-10 |
|---|---|---|---|
| **Experience** | No personal insight | Some examples | First-hand experience, screenshots, data |
| **Expertise** | Generic info | Domain knowledge shown | Deep technical accuracy, credentials |
| **Authority** | No citations | Some sources | Authoritative sources, research links |
| **Trust** | Outdated, vague | Mostly current | Current, transparent, verified facts |

---

## Schema.org Templates

### Article (BlogPosting)
```json
{
  "@context": "https://schema.org",
  "@type": "BlogPosting",
  "headline": "Title Here",
  "description": "Meta description",
  "author": { "@type": "Person", "name": "Author Name" },
  "datePublished": "2026-03-23",
  "dateModified": "2026-03-23",
  "image": "https://example.com/image.webp",
  "publisher": {
    "@type": "Organization",
    "name": "Site Name",
    "logo": { "@type": "ImageObject", "url": "https://example.com/logo.png" }
  }
}
```

### FAQ
```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Question text here?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Answer text here."
      }
    }
  ]
}
```

### HowTo
```json
{
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "How to [task]",
  "step": [
    { "@type": "HowToStep", "name": "Step 1", "text": "Description..." },
    { "@type": "HowToStep", "name": "Step 2", "text": "Description..." }
  ]
}
```

### BreadcrumbList
```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    { "@type": "ListItem", "position": 1, "name": "Home", "item": "https://example.com" },
    { "@type": "ListItem", "position": 2, "name": "Category", "item": "https://example.com/cat" },
    { "@type": "ListItem", "position": 3, "name": "Page Title" }
  ]
}
```

---

## Vietnamese SEO Patterns

```
KEYWORD HANDLING:
  Primary: "thiết kế website" (có dấu)
  Slug:    "thiet-ke-website" (không dấu)
  Alt:     "thiết kế web", "thiết kế trang web" (variations)

TITLE FORMULA:
  "[Keyword] — [Benefit/Number] | [Brand]"
  Ex: "Thiết Kế Website Chuẩn SEO — Top 10 Xu Hướng 2026 | Brand"

META DESC FORMULA:
  "[Keyword] [benefit]. [Social proof]. [CTA]. ✅ [Trust signal]"
  Ex: "Thiết kế website chuẩn SEO giúp tăng traffic 300%. 500+ dự án thành công. Tư vấn miễn phí. ✅ Bảo hành 12 tháng"

URL STRUCTURE:
  ✅ /thiet-ke-website-chuan-seo
  ❌ /thiet-ke-website-chuan-seo-2026-gia-re-tot-nhat (quá dài)
  ❌ /p=123 (non-descriptive)
```
