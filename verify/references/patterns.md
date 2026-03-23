# Verify References — Patterns & Checklists (v7.0)

---

## Chain-of-Verification Deep Dive

> Based on: [Chain-of-Verification](https://arxiv.org/abs/2309.11495) — Reduces hallucination by verifying each generated claim

### Protocol
```
1. GENERATE: AI generates code/content as normal
2. LIST CLAIMS: Extract every factual claim from output
3. PLAN VERIFICATION: For each claim, plan how to verify
4. VERIFY INDEPENDENTLY: Check each claim separately
5. REVISE: Update output based on verification results
```

### Common Claims in Code
| Claim Type | How to Verify |
|---|---|
| Package exists | `npm info [package]` or `pip show [package]` |
| API endpoint | Check official API docs |
| Function signature | Check library source/docs |
| CSS property | MDN Web Docs reference |
| SQL syntax | Database-specific docs |
| File path | `ls` or `find` command |
| Config key | Framework documentation |
| Browser support | caniuse.com |

---

## LLM-as-Judge Rubric

### Code Quality Dimensions
```
CORRECTNESS (weight: 30%)
  10: Handles all edge cases, robust error handling
  7:  Works for common cases, some edge cases missed
  4:  Basic functionality works but fragile
  1:  Logic errors, won't work as intended

COMPLETENESS (weight: 20%)
  10: All requirements implemented, tests included
  7:  Core requirements done, minor features missing
  4:  Partially implemented
  1:  Major features missing

SECURITY (weight: 20%)
  10: Input validation, auth checks, no injection risks
  7:  Basic security present, minor issues
  4:  Some security gaps (no input validation)
  1:  Major vulnerabilities (SQL injection, XSS, etc.)

PERFORMANCE (weight: 15%)
  10: Optimized, efficient algorithms, proper caching
  7:  Acceptable performance, no obvious bottlenecks
  4:  Some N+1 queries, unnecessary re-renders
  1:  Will cause timeouts or crashes under load

READABILITY (weight: 15%)
  10: Clear naming, good structure, documented
  7:  Mostly readable, some complex parts
  4:  Hard to follow, inconsistent style
  1:  Unreadable, no documentation, magic numbers
```

### Scoring Formula
```
Overall = (Correctness × 0.3) + (Completeness × 0.2) + 
          (Security × 0.2) + (Performance × 0.15) + 
          (Readability × 0.15)

Threshold: ≥7.0 = Ready  |  5.0-6.9 = Needs Work  |  <5.0 = Major Issues
```

---

## Web Testing Checklists by Page Type

### Landing Page
```
□ Hero loads fast (LCP target)
□ CTA button visible above fold
□ Images optimized (WebP, lazy load)
□ Social proof visible
□ Mobile layout tested
□ Form submission works
□ Analytics tracking fires
```

### Blog/Article Page
```
□ Article schema present
□ Reading time estimate
□ Table of contents (long articles)
□ Social share buttons work
□ Related articles section
□ Comments section (if applicable)
□ Author bio with E-E-A-T signals
```

### E-Commerce Page
```
□ Product schema present
□ Price displays correctly
□ Add to cart works
□ Image gallery functional
□ Reviews section loads
□ Mobile checkout tested
□ Payment forms secure (HTTPS)
```

### Dashboard
```
□ Data loads within 2s
□ Charts render correctly
□ Filters/search work
□ Table pagination works
□ Export functionality
□ Permission checks
□ Real-time updates (if applicable)
```

---

## Anti-Hallucination Patterns

### Red Flags in AI-Generated Code
```
🚩 Package name you haven't heard of → verify with npm/pip
🚩 API endpoint with clean path → verify in official docs
🚩 "This is available since v4.0" → verify version compatibility
🚩 Complex regex without explanation → test with sample data
🚩 Config option that seems too convenient → verify in framework docs
🚩 "Simply add this to..." → verify the syntax is correct
🚩 Import path with many levels → verify file structure
```

### Verification Shortcuts
```bash
# Verify npm package exists
npm info package-name 2>/dev/null && echo "✅ EXISTS" || echo "❌ NOT FOUND"

# Verify API endpoint responds
curl -sI https://api.example.com/endpoint | head -1

# Verify file exists
test -f path/to/file && echo "✅" || echo "❌"

# Verify port is listening
ss -tlnp | grep :PORT

# Check website is accessible
curl -sI https://domain.com -o /dev/null -w '%{http_code}'
```
