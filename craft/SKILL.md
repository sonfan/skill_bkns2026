---
name: craft
description: "UI/UX implementation and design system. Use for /craft (build UI components), /design (design system from inspiration), /animate (micro-animations), /responsive (multi-device testing), /palette (AI color palette), /audit (quality audit), /tokens (design system), /e2e (browser visual testing). Triggers on: UI, component, design, giao diện, responsive, WCAG, accessibility, craft, audit giao diện, animation, palette, thiết kế."
---

# Craft Skill — Premium Web UI Design Engine + WCAG + Browser Testing (v7.0)

> 📂 Chi tiết bổ sung: `craft/references/patterns.md` | `craft/references/design-patterns.md`

---

## /design [style]
> Generate design system từ inspiration — premium, modern, production-ready

```
STYLE PRESETS:
  modern      — Clean, whitespace, Inter/Outfit font, subtle shadows
  glassmorphism — Frosted glass, blur, transparency, vibrant gradients
  premium     — Dark mode, gold accents, luxury feel, serif headings
  minimal     — Ultra-clean, monochrome, max whitespace, system fonts
  dashboard   — Data-dense, cards, charts, sidebar layout
  landing     — Hero-driven, CTA-focused, conversion-optimized
  ecommerce   — Product cards, filters, cart, price displays
  custom      — User mô tả → AI generate

DESIGN SYSTEM PROTOCOL:
  STEP 1 — INSPIRATION RESEARCH:
    □ Analyze top 5 sites trong cùng niche (Dribbble, Awwwards, UIVerse)
    □ Extract patterns: layout, colors, typography, spacing, interactions
    □ Mood board: 3-5 screenshots reference
    □ Define: "Cảm giác đầu tiên khi user thấy trang là gì?"

  STEP 2 — TOKEN GENERATION:
    □ Color palette: primary, secondary, accent, neutral, semantic
    □ Typography scale: heading (serif/sans), body, mono
    □ Spacing system: 4px base unit
    □ Border radius: consistent system (sm/md/lg/full)
    □ Shadow system: subtle → elevated → floating
    □ Motion tokens: duration, easing curves

  STEP 3 — COMPONENT LIBRARY PLAN:
    □ Atomic Design mapping: atoms → molecules → organisms → templates
    □ Core components needed (button, card, input, nav, hero, footer)
    □ Interactive states: default, hover, active, focus, disabled, loading
    □ Generate component showcase page

  STEP 4 — IMPLEMENTATION:
    □ CSS custom properties (design tokens) → index.css
    □ Components → semantic HTML + CSS
    □ Dark/light mode toggle
    □ Responsive breakpoints baked in

OUTPUT: Design system + component library → ready to compose pages
```

---

## /animate [scope]
> Thư viện micro-animations + interaction patterns

```
ANIMATION CATEGORIES:

  ENTRANCE (elements appearing):
    □ fadeIn, slideUp, slideIn, scaleIn, blurIn
    □ Stagger: children appear sequentially (delay 50-100ms)
    □ Intersection Observer trigger (scroll reveals)

  HOVER & INTERACTION:
    □ Button: scale(1.02) + shadow lift
    □ Card: translateY(-4px) + shadow increase
    □ Link: underline slide, color transition
    □ Image: zoom 1.05 within overflow:hidden container
    □ Icon: rotate, bounce, pulse on hover

  PAGE TRANSITIONS:
    □ Route change: fadeOut → fadeIn (200-300ms)
    □ Content swap: crossfade
    □ Modal: backdrop fadeIn + content slideUp
    □ Drawer: slideIn from edge

  LOADING & FEEDBACK:
    □ Skeleton screens: shimmer gradient animation
    □ Spinner: 3 styles (border, dots, bars)
    □ Progress bar: smooth width transition
    □ Toast: slideIn + auto-dismiss + slideOut
    □ Success: checkmark draw animation

  SCROLL EFFECTS:
    □ Parallax: background-attachment or transform
    □ Sticky header: shrink + shadow on scroll
    □ Progress indicator: scroll % bar
    □ Reveal sections: stagger on viewport enter

PERFORMANCE RULES:
  □ ONLY animate: transform, opacity (GPU-accelerated)
  □ prefers-reduced-motion: disable all non-essential animations
  □ Duration: 150-300ms (micro), 300-500ms (page transition)
  □ Easing: ease-out (enter), ease-in (exit), ease-in-out (move)
  □ No animation on paint-heavy properties (width, height, top, left)

→ Cookbook chi tiết: references/design-patterns.md
```

---

## /responsive [url]
> Multi-device testing matrix — 6 breakpoints × light/dark × states

```
TESTING MATRIX:

  BREAKPOINTS (6):
    □ Mobile S:     320px  (iPhone SE)
    □ Mobile L:     375px  (iPhone 14)
    □ Tablet:       768px  (iPad)
    □ Laptop:       1024px (MacBook Air)
    □ Desktop:      1280px (Standard)
    □ Wide:         1536px (Ultrawide)

  FOR EACH BREAKPOINT:
    □ Screenshot light mode
    □ Screenshot dark mode (if applicable)
    □ Check: text readable? Images scaled? Layout intact?
    □ Touch targets ≥44×44px on mobile
    □ No horizontal overflow (scroll-x)
    □ Navigation: hamburger menu works on mobile?
    □ Tables: scrollable or stacked on mobile?
    □ Forms: input fields full-width on mobile?

  PRIORITY ISSUES:
    🔴 Critical: content hidden, layout broken, text unreadable
    🟡 Warning: spacing off, images oversized, touch targets small
    🟢 Info: minor alignment, could be tighter

OUTPUT: 12 screenshots (6 breakpoints × light/dark) + issue list
```

---

## /palette [theme]
> AI-generated color palette — harmonious, contrast-checked, production-ready

```
THEME OPTIONS:
  warm      — Amber, orange, coral tones
  cool      — Blue, teal, indigo tones
  neon      — Vibrant, electric, high-saturation
  pastel    — Soft, muted, approachable
  earth     — Brown, olive, terracotta, natural
  mono      — Single hue, 10 shades
  brand     — Start from brand color → generate system
  auto      — AI picks based on project type

PALETTE GENERATION:
  □ Primary:   main brand/action color
  □ Secondary: complementary or analogous
  □ Accent:    highlight, CTA, attention
  □ Neutral:   gray scale for text, borders, backgrounds
  □ Semantic:  success (green), warning (amber), error (red), info (blue)

  EACH COLOR → 10 shades (50-900):
    --color-primary-50:  lightest (backgrounds)
    --color-primary-100: light (hover states)
    --color-primary-200-400: mid tones
    --color-primary-500: base (buttons, links)
    --color-primary-600-700: dark (hover, active)
    --color-primary-800-900: darkest (text on light bg)

CONTRAST CHECK (WCAG AA mandatory):
  □ Text on background: ≥4.5:1 (normal), ≥3:1 (large)
  □ UI elements: ≥3:1
  □ Generate contrast table: color pairs + ratios

DARK MODE MAPPING:
  □ Light bg → Dark bg (swap 50↔900, 100↔800, etc.)
  □ Ensure all contrast ratios maintained in dark mode

OUTPUT: CSS custom properties + contrast table + dark mode vars
```

---

## /craft [task]
> Build UI components theo Atomic Design, đạt WCAG 2.2 AA

```
PHASE 1 — DESIGN SYSTEM CHECK
  □ Đọc design tokens hiện có (colors, spacing, typography, radius)
  □ Nếu chưa có tokens → /design hoặc /tokens trước, không hardcode
  □ Identify component level: Atom / Molecule / Organism / Template?
  □ Check: component tương tự đã tồn tại chưa? (DRY)
  □ Design Inspiration: reference site/component nào giống?

PHASE 2 — COMPONENT SPEC
  □ Props interface (TypeScript): required vs optional
  □ Variants: size (sm/md/lg), state (default/hover/active/disabled/error)
  □ Responsive behavior: mobile-first breakpoints
  □ Animation/transition: prefers-reduced-motion check
  □ Dark mode: nếu project hỗ trợ
  □ Interactive states: hover effects, focus rings, loading states

PHASE 3 — IMPLEMENT
  □ Semantic HTML (đúng element cho đúng role)
  □ Design tokens ONLY (không hardcode)
  □ Keyboard navigation: Tab order, focus visible, Enter/Space/Arrow
  □ ARIA attributes: role, aria-label, aria-describedby, aria-live
  □ Error states + Loading states (skeleton / spinner với aria-busy)
  □ Micro-animations: hover lift, transitions, feedback (→ /animate)

PHASE 4 — WCAG CHECKLIST (bắt buộc)
  □ Color contrast ≥4.5:1 (text), ≥3:1 (large text/UI)
  □ Focus indicator rõ ràng (2px+ outline, high contrast)
  □ Touch target ≥44×44px (mobile)
  □ Alt text, heading hierarchy, form labels
  □ Screen reader testing (aria-live regions)

PHASE 5 — PERFORMANCE CHECK
  □ Images: WebP/AVIF, lazy loading, srcset, aspect-ratio
  □ Animation: GPU-accelerated (transform, opacity only)
  □ Bundle impact: import cụ thể, tree-shaking
  □ Font: display=swap, preload critical fonts

PHASE 6 — BROWSER AGENT VERIFY
  □ /responsive multi-breakpoint test
  □ Dark mode screenshot nếu applicable
  □ Keyboard navigation test + hover/focus states
  □ Form validation visual feedback
  □ Compare before/after nếu có changes
```

---

## /audit [scope]
> Multi-dimensional quality audit cho UI

```
5 DIMENSIONS:
  Visual Consistency 🎨 | Accessibility ♿ | Performance ⚡ | Responsive 📱 | Animation 🎬

SCORING (mỗi dimension /20, tổng /100):
  18-20: Excellent  |  14-17: Good  |  10-13: Needs Work  |  <10: Critical

OUTPUT: Scored report với CRITICAL / WARNING / INFO per dimension
→ Chi tiết audit checklist: references/patterns.md
```

---

## /tokens [scope]
> Tạo hoặc mở rộng design token system

```
TOKEN CATEGORIES:
  Colors:     --color-primary-50 → 900 + semantic tokens
  Spacing:    --space-1 (4px) → --space-16 (64px)
  Typography: --font-size-xs → 4xl, --font-weight-*, --line-height-*
  Effects:    --radius-*, --shadow-*, --duration-*, --ease-*
  Breakpoints: --bp-mobile, --bp-tablet, --bp-laptop, --bp-desktop

DARK MODE: @media (prefers-color-scheme: dark) hoặc [data-theme="dark"]
→ Chi tiết token structure: references/patterns.md
```

---

## /e2e [scope]
> Browser Agent visual testing — screenshots + keyboard + responsive + performance

```
WORKFLOW:
  □ Navigate to target URL / component / page
  □ /responsive multi-breakpoint screenshots
  □ Dark mode screenshot nếu project hỗ trợ
  □ Keyboard navigation test (Tab, Enter, Space, Arrow, Escape)
  □ Hover/focus states verification
  □ Form validation visual feedback
  □ Lighthouse quick check (Performance, Accessibility, SEO scores)
  □ Compare before/after nếu có changes (visual diff)
  □ Interaction test (modals, dropdowns, animations)

OUTPUT: Screenshot evidence + pass/fail report per dimension + Lighthouse scores
→ Chi tiết checklist: references/patterns.md
```
