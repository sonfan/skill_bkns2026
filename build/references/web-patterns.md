# Build References — Web Development Patterns (v7.0)

---

## Web Project Starters

### Static Website (HTML + CSS + JS)
```
STRUCTURE:
  index.html          — Main page
  css/index.css       — Global styles (tokens first)
  css/components/     — Component styles
  js/main.js          — Core logic
  assets/images/      — Optimized images (WebP)
  assets/fonts/       — Self-hosted fonts

CHECKLIST:
  □ CSS: design tokens → reset → globals → components
  □ Meta tags: title, description, OG tags, viewport
  □ Favicon: multiple sizes (16, 32, 180, 512)
  □ Performance: lazy loading, font preload, minify
  □ SEO: sitemap.xml, robots.txt, canonical URL
```

### Vite + React/Vue SPA
```
INIT: npx -y create-vite@latest ./ --template react-ts
STRUCTURE:
  src/components/     — Reusable UI components
  src/pages/          — Page/route components
  src/hooks/          — Custom hooks
  src/utils/          — Helper functions
  src/styles/         — CSS + tokens
  src/assets/         — Static assets

CHECKLIST:
  □ Router: react-router-dom / vue-router
  □ State: zustand / pinia (avoid Redux for small projects)
  □ CSS strategy: CSS Modules or vanilla CSS (no Tailwind unless requested)
  □ Build: vite.config.ts optimized (code splitting, tree shaking)
```

### Next.js Fullstack
```
INIT: npx -y create-next-app@latest ./ --ts --app --no-tailwind
STRUCTURE:
  app/                — App router pages
  app/api/            — API routes
  components/         — UI components
  lib/                — Business logic
  public/             — Static files

CHECKLIST:
  □ Server Components default (client only when need interactivity)
  □ Loading states: loading.tsx + Suspense
  □ Error handling: error.tsx per route
  □ SEO: metadata API (generateMetadata)
  □ Images: next/image (auto-optimized)
```

---

## Component-First Development

```
ORDER:
  1. Design tokens (CSS custom properties) → index.css
  2. Atoms: Button, Input, Badge, Icon, Text
  3. Molecules: Card, FormField, SearchBar, NavItem
  4. Organisms: Header, Footer, Sidebar, HeroSection
  5. Templates: layout composition
  6. Pages: data + templates

EACH COMPONENT:
  □ Single responsibility
  □ Uses only design tokens (no hardcoded values)
  □ Responsive from mobile-first
  □ Dark mode compatible
  □ Keyboard accessible
  □ Loading/error states
```

---

## Landing Page Architecture

```
SECTIONS (top to bottom):
  1. HERO          — Headline + CTA + visual (above fold)
  2. SOCIAL PROOF  — Logos, stats, or testimonials
  3. FEATURES      — 3-6 features with icons
  4. HOW IT WORKS  — 3 steps, visual flow
  5. BENEFITS      — Detailed value propositions
  6. TESTIMONIALS  — Customer quotes with photos
  7. PRICING       — Plans comparison (if applicable)
  8. FAQ           — Common questions (rich snippet)
  9. CTA           — Final call to action
  10. FOOTER       — Links, social, newsletter

CONVERSION OPTIMIZATION:
  □ CTA visible without scrolling
  □ One primary action per page
  □ Trust signals near CTA (reviews, guarantees)
  □ Fast load (LCP ≤2.5s)
  □ Mobile-optimized form
```

---

## Image Optimization Pipeline

```
FORMATS:
  WebP:  primary format (30% smaller than JPEG)
  AVIF:  next-gen (50% smaller, less browser support)
  JPEG:  fallback

RESPONSIVE IMAGES:
  <img
    src="image-800.webp"
    srcset="image-400.webp 400w, image-800.webp 800w, image-1200.webp 1200w"
    sizes="(max-width: 768px) 100vw, 50vw"
    loading="lazy"
    alt="Descriptive alt text"
    width="800" height="600"
  />

OPTIMIZATION CHECKLIST:
  □ Max width: 1200-1600px (no larger)
  □ Quality: 80% (WebP), 75% (AVIF)
  □ Lazy loading: all images below fold
  □ Aspect ratio: set width/height to prevent CLS
  □ Alt text: descriptive, include keywords naturally
```

---

## Deployment Checklist

### VPS (nginx + pm2)
```
□ Build: npm run build (check exit code 0)
□ Upload: rsync or git pull on server
□ Dependencies: npm ci --production
□ pm2: pm2 restart ecosystem.config.js
□ nginx: config correct, reload
□ SSL: certbot certificate valid
□ Health check: curl localhost:PORT
□ External check: curl https://domain.com
```

### Vercel/Netlify
```
□ Build: verify build passes locally first
□ Environment variables: all set in dashboard
□ Deploy preview: test before promoting
□ Custom domain: DNS configured
□ HTTPS: auto-provided
□ Headers: _headers file or vercel.json
```
