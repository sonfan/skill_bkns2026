---
name: verify
description: "Code verification, anti-hallucination, web testing, and regression detection. Use for /verify (multi-stage verification), /fact-check (verify API/library usage), /regression (regression check), /test-web (comprehensive web testing). Triggers on: verify, kiểm tra, fact-check, regression, test web, anti-hallucination, quality check, xác minh."
---

# Verify Skill — Anti-Hallucination + Chain-of-Verification + Web Testing (v7.0)

> 📂 Chi tiết bổ sung: `verify/references/patterns.md`

---

## /verify [scope]
> Multi-stage verification — evidence-based quality assurance

```
STAGE 1 — CHAIN-OF-VERIFICATION (CoV):
  Paper: arxiv 2309.11495

  □ List ALL claims/assumptions in the code:
      - "API endpoint exists at /api/v1/..."
      - "Library function X accepts parameters Y"
      - "This regex matches pattern Z"
      - "Database column has type T"

  □ Verify EACH claim independently:
      - Check official documentation
      - Run test calls if possible
      - Verify import paths exist
      - Confirm function signatures match

  □ Flag unverified claims:
      🔴 Cannot verify → MUST check before deploy
      🟡 Likely correct but unverified → should verify
      🟢 Verified with evidence → safe

STAGE 2 — LLM-AS-JUDGE SELF-EVALUATION:
  Paper: arxiv 2306.05685

  □ Re-read generated code as a SKEPTICAL REVIEWER:
      - "Does this actually solve the stated problem?"
      - "Are there edge cases not handled?"
      - "Would a senior developer approve this?"
      - "Is error handling complete?"
      - "Are there security implications?"

  □ Rate code quality (1-10):
      | Dimension    | Score | Evidence |
      |-------------|-------|----------|
      | Correctness  | ?/10  | [why]    |
      | Completeness | ?/10  | [why]    |
      | Security     | ?/10  | [why]    |
      | Performance  | ?/10  | [why]    |
      | Readability  | ?/10  | [why]    |

  □ If average < 7 → identify specific improvements needed

STAGE 3 — EVIDENCE COLLECTION:
  □ Run ALL verification commands (no shortcuts):
      lint → type-check → test → security audit
  □ Read FULL output (not just exit code)
  □ Screenshot evidence if UI changes
  □ Log evidence in VERIFICATION REPORT

  VERIFICATION REPORT:
  ┌─────────────────────────────────────────┐
  │ VERIFICATION REPORT — /verify           │
  │ CoV Claims:   [X verified / Y total]    │
  │ Judge Score:  [X/10 average]            │
  │ Build:        [PASS/FAIL]               │
  │ Types:        [PASS/FAIL]               │
  │ Lint:         [PASS/FAIL]               │
  │ Tests:        [PASS/FAIL] (X/Y, Z%)     │
  │ Security:     [PASS/FAIL]               │
  │ Overall:      [READY / NOT READY]       │
  │ Unverified:   [list claims to check]    │
  └─────────────────────────────────────────┘
```

---

## /fact-check [code or file]
> Verify AI-generated code assumptions and API usage

```
FACT-CHECK PROTOCOL:

  IMPORT VERIFICATION:
    □ Do all imported packages exist? (npm search / pip search)
    □ Are package versions compatible?
    □ Are import paths correct? (named vs default export)
    □ Any deprecated packages being used?

  API VERIFICATION:
    □ Do endpoint URLs match official docs?
    □ Are request/response schemas correct?
    □ Are HTTP methods correct (GET vs POST)?
    □ Are auth headers formatted correctly?
    □ Are rate limits respected?

  FUNCTION SIGNATURE CHECK:
    □ Do function names match documentation?
    □ Are parameter types correct?
    □ Are return types correct?
    □ Any deprecated methods being called?

  CONFIGURATION CHECK:
    □ Are config keys spelled correctly?
    □ Are default values sensible?
    □ Are required env vars documented?
    □ Are file paths correct for the OS?

  COMMON HALLUCINATION PATTERNS:
    ❌ Invented API endpoints that don't exist
    ❌ Wrong function parameter order
    ❌ Mixing up similar library APIs (e.g., Express vs Fastify)
    ❌ Using features from newer version than installed
    ❌ Incorrect CSS property names or values
    ❌ Wrong SQL syntax for specific database (MySQL vs Postgres)
    ❌ Inventing npm packages that don't exist

OUTPUT: Fact-check report listing each claim + verified/unverified + evidence
```

---

## /regression [scope]
> Automated regression detection before merge

```
REGRESSION CHECK PROTOCOL:

  STEP 1 — IMPACT ANALYSIS:
    □ List ALL files changed: git diff --stat
    □ For each changed file:
        - What functions were modified?
        - What other files import/use these functions?
        - What tests cover this code?

  STEP 2 — DEPENDENCY TRACE:
    □ Trace imports: who depends on changed code?
    □ Map affected components (upstream + downstream)
    □ Identify potentially broken features

  STEP 3 — TEST VERIFICATION:
    □ Run full test suite (not just changed files)
    □ Run tests for ALL dependent files identified
    □ Compare test results with main branch
    □ New tests added for new code? (coverage check)

  STEP 4 — VISUAL REGRESSION (if UI changes):
    □ Screenshot comparison: before vs after
    □ Check all breakpoints (mobile/tablet/desktop)
    □ Verify dark mode not broken
    □ Check all interactive states

  STEP 5 — BEHAVIORAL CHECK:
    □ Does the app still start without errors?
    □ Core user flows still work? (login, nav, main features)
    □ API endpoints still respond correctly?
    □ Database queries still return expected results?

OUTPUT: Regression report + impact map + test results
```

---

## /test-web [url]
> Comprehensive web testing — performance, links, forms, security

```
WEB TESTING MATRIX:

  PERFORMANCE (Lighthouse-based):
    □ Performance score ≥90
    □ LCP (Largest Contentful Paint) ≤2.5s
    □ CLS (Cumulative Layout Shift) ≤0.1
    □ FID (First Input Delay) ≤100ms
    □ TTFB (Time to First Byte) ≤800ms
    □ Total page weight ≤3MB
    □ Image optimization (WebP/AVIF, lazy loading)
    □ Font loading (display=swap, preload)

  LINKS & NAVIGATION:
    □ No broken internal links (404)
    □ No broken external links
    □ All navigation links work
    □ Breadcrumbs correct
    □ Mobile menu functional
    □ Footer links complete

  FORMS & INTERACTIONS:
    □ All forms submittable
    □ Validation messages display correctly
    □ Required fields enforced
    □ Success/error states clear
    □ No console JavaScript errors
    □ All interactive elements keyboard-accessible

  SEO:
    □ Title tag present and ≤60 chars
    □ Meta description present and ≤160 chars
    □ H1 exists and unique
    □ Canonical URL correct
    □ OG tags present (title, description, image)
    □ robots.txt accessible
    □ sitemap.xml accessible

  SECURITY HEADERS:
    □ Content-Security-Policy present
    □ Strict-Transport-Security present
    □ X-Frame-Options present
    □ X-Content-Type-Options: nosniff
    □ Referrer-Policy set
    □ Permissions-Policy set

  ACCESSIBILITY:
    □ Lighthouse Accessibility ≥90
    □ All images have alt text
    □ Color contrast WCAG AA
    □ Keyboard navigation works
    □ Focus indicators visible
    □ ARIA labels on interactive elements

  MOBILE:
    □ Mobile-friendly test pass
    □ Touch targets ≥44×44px
    □ No horizontal scroll
    □ Text readable without zoom
    □ Viewport meta tag correct

OUTPUT:
  ┌─────────────────────────────────────────┐
  │ WEB TEST REPORT — [URL]                 │
  │ Performance:   [score]/100              │
  │ SEO:           [score]/100              │
  │ Accessibility: [score]/100              │
  │ Links:         [X broken / Y total]     │
  │ Forms:         [X issues / Y forms]     │
  │ Security:      [X/6 headers present]    │
  │ Mobile:        [PASS/FAIL]              │
  │ Overall:       [READY / NOT READY]      │
  └─────────────────────────────────────────┘

→ Chi tiết checklists: references/patterns.md
```
