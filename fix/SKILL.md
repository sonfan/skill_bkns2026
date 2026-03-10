---
name: fix
description: Bug fixing and debugging. Use for /fix (debug any error), error traces, crashes, unexpected behavior, failing tests. Triggers on "lỗi", "bug", "crash", "không chạy được", "error", "exception", "fix", "debug", "sửa lỗi".
---

# Fix Skill — 4-Phase Debug + Insight Match + Auto-Ingest

## /fix [bug description or error]
> Tìm root cause trước khi fix — không patch symptoms

```
PHASE 0 — MEMORY MATCH (10 giây)
  □ Check INSTINCTS.md: đã gặp error pattern này chưa?
  □ Nếu có instinct match (confidence ≥0.7) → apply và log
  □ Check LESSONS.md: search entities/topics liên quan
  □ Check INSIGHTS.md: có compound insight nào liên quan?
     → Nếu có: "💡 INSIGHT liên quan: [tóm tắt]"
  □ Nếu không match → tiếp tục 4-phase debug

PHASE 1 — REPRODUCE (không fix mù)
  □ Reproduce bug một cách nhất quán
  □ Xác định: bug xảy ra LUÔN hay ĐÔI KHI?
  □ Xác định: trigger conditions là gì?
  □ Xác định: expected vs actual behavior
  □ Screenshot / error trace / log đầy đủ

PHASE 2 — DIAGNOSE (root cause)
  □ Đọc toàn bộ error message (không chỉ dòng đầu)
  □ Trace call stack từ dưới lên
  □ Check: input data có hợp lệ không?
  □ Check: state tại thời điểm lỗi
  □ Check: network/async timing issues?
  □ Check: environment differences (dev vs prod)?
  □ 5-WHY technique: hỏi "tại sao" 5 lần để tìm root cause thật sự
  □ Ghi: "Root cause is: ___" trước khi viết bất kỳ fix nào

  🛑 STOP: Không được bắt đầu PHASE 3 khi chưa xác nhận root cause.

PHASE 3 — FIX (targeted, minimal)
  □ SELF-REASONING GATE:
      (a) Đây có phải cách fix tốt nhất? (≥2 alternatives)
      (b) Có risk/side-effect nào đang bỏ qua?
      (c) User có cần approve không?
  □ Fix chỉ root cause — không "cải thiện" thêm trong cùng PR
  □ Nếu fix ảnh hưởng nhiều file → comment rõ lý do từng change
  □ Thêm test case reproduce exact bug (regression guard)
  □ Đảm bảo fix không break existing tests

PHASE 4 — VERIFY + LEARN (APEX Enhanced)
  □ Bug đã được reproduce trước fix → confirm không còn reproduce được
  □ Run full test suite: không có new failures
  □ Nếu là UI bug → dùng Antigravity Browser Agent để visual verify
  □ Run VERIFICATION LOOP: lint → type-check → test → audit
  □ Log instinct result: fix này đúng hay sai? Update confidence

  AUTO-INGEST:
  □ Tự động chạy Ingest tagging:
     Summary, Entities, Topics, Importance score
  □ "📝 Ghi bài học này vào LESSONS.md không?"
  □ Nếu có: format APEX entry + check connections
  □ "🔗 Tìm thấy connection với #BUG-XXX, #BUG-YYY"
  □ "/consolidate khi nào? Đã có [N] lessons mới."
```

---

## BUG CLASSIFICATION

```
CRITICAL (fix ngay, không commit khác):
  □ Data loss / corruption
  □ Security vulnerability
  □ Production down / service unavailable
  □ Authentication bypass

HIGH (fix trong sprint này):
  □ Feature không hoạt động đúng spec
  □ Performance degradation >20%
  □ UI broken trên major browser/device

MEDIUM (backlog):
  □ Edge case không handle
  □ Error message không rõ ràng
  □ Minor UX issue

LOW (nice-to-have):
  □ Typo trong UI
  □ Console warning không critical
```

---

## COMMON PATTERNS & QUICK DIAGNOSIS

```
React / Next.js:
  "Cannot read properties of undefined" → async data chưa load, check loading state
  "Hydration error" → server/client render khác nhau, check conditional rendering
  "Maximum update depth exceeded" → dependency array trong useEffect sai
  "Module not found" → import path sai, check tsconfig paths

Node.js / API:
  "CORS error" → missing/wrong CORS headers, check origin whitelist
  "JWT expired" → token refresh logic, check expiry handling
  "Cannot connect to DB" → connection pool exhausted, check max connections
  "Request timeout" → slow query / external API, check indexes + timeouts

N8N / Automation:
  "Execution failed" → check node input/output mapping
  "Rate limit exceeded" → add delay node, check retry logic
  "Webhook not received" → check URL, authentication, firewall

WordPress / REST API:
  "401 Unauthorized" → check nonce, check user capabilities
  "Cannot modify header information" → output buffer issue, early exit
```

---

## ANTIGRAVITY BROWSER AGENT — UI Bug Fixing

```
Dùng cho: visual bugs, layout issues, UI state bugs

WORKFLOW:
  1. Mô tả bug cho Browser Agent
  2. Browser Agent: navigate → screenshot → identify issue
  3. Fix code
  4. Browser Agent: verify fix (before/after screenshots)
  5. Check: responsive (mobile, tablet, desktop)
  6. Check: dark mode nếu có
  7. Confirm với visual diff

Đặc biệt hữu ích cho:
  - CSS specificity issues
  - Z-index layering bugs
  - Animation/transition glitches
  - Form validation visual feedback
```
