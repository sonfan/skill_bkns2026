# Craft References — Design Patterns & Animation Cookbook (v7.0)

---

## 20+ Modern Web Design Patterns

### Hero Sections
```
HERO VARIANTS:
  Split:       Image left + text right (hoặc ngược lại)
  Full-screen: Background image/video + overlay text
  Gradient:    Gradient mesh background + centered text
  Animated:    Particle/wave/3D background + text
  Minimal:     Large typography + subtle animation
  Product:     Product screenshot + feature highlights
```

### Card Patterns
```
Standard:    Image + title + desc + CTA button
Hover-lift:  translateY(-8px) + shadow increase on hover
Glass:       backdrop-filter: blur(10px) + semi-transparent bg
Pricing:     Highlighted "popular" card with scale(1.05)
Testimonial: Avatar + quote + name + role
Stats:       Large number + label + icon
```

### Navigation
```
Sticky:      Fixed top, shrinks on scroll, blur background
Sidebar:     Collapsible, icon-only on mobile
Mega-menu:   Full-width dropdown with columns
Breadcrumb:  Path-based, SEO-friendly
Tab:         Underline indicator, smooth slide
Bottom-bar:  Mobile fixed bottom, 3-5 icons
```

### Dashboard Components
```
Metric card: Large number + trend arrow + sparkline
Data table:  Sortable, filterable, paginated, responsive
Chart:       Line/bar/pie with tooltips + legends
Activity:    Timeline with avatars + actions
KPI grid:    4-col grid, color-coded status
```

---

## Animation Cookbook

### CSS Keyframes Library
```css
/* Fade In Up (most common entrance) */
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* Scale In (modals, popovers) */
@keyframes scaleIn {
  from { opacity: 0; transform: scale(0.95); }
  to   { opacity: 1; transform: scale(1); }
}

/* Slide In Right (drawers, panels) */
@keyframes slideInRight {
  from { transform: translateX(100%); }
  to   { transform: translateX(0); }
}

/* Shimmer (skeleton loading) */
@keyframes shimmer {
  0%   { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}
.skeleton {
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}

/* Pulse (notification badge) */
@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50%      { transform: scale(1.05); }
}
```

### Hover Effect Recipes
```css
/* Card Lift */
.card { transition: transform 0.2s ease, box-shadow 0.2s ease; }
.card:hover { transform: translateY(-4px); box-shadow: 0 12px 24px rgba(0,0,0,0.1); }

/* Button Scale */
.btn { transition: transform 0.15s ease; }
.btn:hover { transform: scale(1.02); }
.btn:active { transform: scale(0.98); }

/* Image Zoom (within container) */
.img-container { overflow: hidden; }
.img-container img { transition: transform 0.3s ease; }
.img-container:hover img { transform: scale(1.05); }

/* Link Underline Slide */
.link { position: relative; }
.link::after {
  content: ''; position: absolute; bottom: 0; left: 0;
  width: 0; height: 2px; background: currentColor;
  transition: width 0.3s ease;
}
.link:hover::after { width: 100%; }
```

### Scroll Reveal (Intersection Observer)
```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('revealed');
      observer.unobserve(entry.target);
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('[data-reveal]').forEach(el => observer.observe(el));
```

```css
[data-reveal] { opacity: 0; transform: translateY(20px); transition: all 0.6s ease; }
[data-reveal].revealed { opacity: 1; transform: translateY(0); }
/* Stagger children */
[data-reveal].revealed > *:nth-child(1) { transition-delay: 0ms; }
[data-reveal].revealed > *:nth-child(2) { transition-delay: 100ms; }
[data-reveal].revealed > *:nth-child(3) { transition-delay: 200ms; }
```

---

## Color Palette Templates

### Warm Professional
```css
:root {
  --primary: hsl(24, 85%, 55%);    /* Warm orange */
  --secondary: hsl(340, 65%, 50%); /* Rose */
  --accent: hsl(45, 90%, 55%);     /* Gold */
  --neutral-50: hsl(30, 10%, 98%);
  --neutral-900: hsl(30, 15%, 12%);
}
```

### Cool Tech
```css
:root {
  --primary: hsl(220, 80%, 55%);   /* Royal blue */
  --secondary: hsl(180, 65%, 45%); /* Teal */
  --accent: hsl(260, 70%, 60%);    /* Purple */
  --neutral-50: hsl(220, 15%, 97%);
  --neutral-900: hsl(220, 25%, 10%);
}
```

### Dark Premium
```css
:root {
  --bg: hsl(220, 20%, 8%);
  --surface: hsl(220, 18%, 12%);
  --primary: hsl(45, 90%, 55%);    /* Gold accent */
  --text: hsl(0, 0%, 95%);
  --text-muted: hsl(0, 0%, 60%);
  --border: hsl(220, 15%, 20%);
}
```

---

## Typography Pairing Guide (Google Fonts)

| Style | Heading | Body | vibe |
|---|---|---|---|
| Modern | Inter | Inter | Clean, tech |
| Editorial | Playfair Display | Source Sans 3 | Elegant, content |
| Startup | Outfit | Outfit | Friendly, modern |
| Dashboard | DM Sans | DM Sans | Data-focused |
| Creative | Space Grotesk | Nunito | Playful, unique |
| Premium | Cormorant Garamond | Lato | Luxury, sophisticated |

---

## Glassmorphism Recipe
```css
.glass-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 16px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
}

/* Dark mode glass */
[data-theme="dark"] .glass-card {
  background: rgba(0, 0, 0, 0.2);
  border: 1px solid rgba(255, 255, 255, 0.08);
}
```

## Gradient Mesh Background
```css
.gradient-mesh {
  background-color: hsl(220, 80%, 55%);
  background-image:
    radial-gradient(at 20% 80%, hsl(260, 70%, 60%) 0px, transparent 50%),
    radial-gradient(at 80% 20%, hsl(180, 65%, 45%) 0px, transparent 50%),
    radial-gradient(at 50% 50%, hsl(340, 65%, 50%) 0px, transparent 50%);
}
```
