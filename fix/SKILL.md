---
name: fix
description: "Bug fixing and debugging. Use for /fix (debug any error), error traces, crashes, unexpected behavior, failing tests. Triggers on: lỗi, bug, crash, không chạy được, error, exception, fix, debug, sửa lỗi."
---

# Fix Skill — 4-Phase Debug + Kaizen + Browser Debug + N8N Debug (v7.0)

> 📂 Chi tiết bổ sung: `fix/references/patterns.md` (bug classification, common patterns, browser agent)

---

## /fix [bug description or error]
> Tìm root cause trước khi fix — không patch symptoms

```
PHASE 0 — MEMORY MATCH (v4.2 Biomimetic Retrieval)
  □ Check INSTINCTS.md: đã gặp error pattern này chưa?
  □ Nếu có instinct match (confidence ≥0.7) → apply và log
  □ 3-Strategy Recall (Rule 26 — experience-first):
     1. Experience-first: tìm entries type=experience match error pattern
     2. Mental models: tìm entries type=mental_model về domain lỗi
     3. Temporal: bugs fix trong 14 ngày gần nhất (recent patterns)
  □ Qdrant: qdrant_find("error: [mô tả]", filter: {memory_type: "experience"})
     → "🧠 Qdrant found: đã fix lỗi tương tự ở [project]!"
  □ Check INSIGHTS.md: compound insight nào liên quan?
  □ Nếu không match → tiếp tục 4-phase debug

PHASE 1 — REPRODUCE (không fix mù)
  □ Reproduce bug một cách nhất quán
  □ Xác định: LUÔN hay ĐÔI KHI? Trigger conditions?
  □ Expected vs actual behavior
  □ Screenshot / error trace / log đầy đủ

PHASE 2 — DIAGNOSE (root cause)
  □ Đọc TOÀN BỘ error message (không chỉ dòng đầu)
  □ Trace call stack từ dưới lên
  □ Check: input data, state, network/async timing, env differences
  □ Form hypothesis: "Nguyên nhân có thể là ___"
  □ Verify hypothesis bằng evidence (log, test, reproduce)
  □ Nếu hypothesis sai → form hypothesis mới, KHÔNG patch
  □ 5-WHY technique → "Root cause is: ___"

  🛑 STOP: Không được bắt đầu PHASE 3 khi chưa xác nhận root cause.

  ULTRATHINK: Nếu bug không reproduce được sau 15 phút
    → Prefix "ultrathink:" → full reasoning plan TRƯỚC khi fix

PHASE 3 — FIX (targeted, minimal)
  □ SELF-REASONING GATE:
      (a) Đây có phải cách fix tốt nhất? (≥2 alternatives)
      (b) Có risk/side-effect nào đang bỏ qua?
      (c) User có cần approve không?

  RATIONALIZATION PREVENTION:
  | Excuse                            | Reality                                    |
  |-----------------------------------|--------------------------------------------|
  | "Issue is simple, skip process"   | Simple bugs have root causes too           |
  | "Emergency, no time"              | Systematic is FASTER than thrashing        |
  | "Just try this first"             | First fix sets the pattern. Do it right.   |
  | "I see the problem, let me fix"   | Seeing symptoms ≠ understanding root cause |
  | "One more fix attempt" (after 2+) | 3+ failures = architectural problem        |
  | "Multiple fixes at once"          | Can't isolate what worked. Causes new bugs |

  RED FLAGS — nếu đang nghĩ bất kỳ câu nào ở trên → STOP, return to PHASE 1

  □ Fix chỉ root cause — không "cải thiện" thêm trong cùng PR
  □ Thêm test case reproduce exact bug (regression guard)
  □ Đảm bảo fix không break existing tests

PHASE 4 — VERIFY + LEARN (APEX Enhanced)
  □ Confirm bug không còn reproduce được
  □ Run full test suite: không có new failures
  □ UI bug → Browser Agent visual verify
  □ Run VERIFICATION LOOP: lint → type-check → test → audit

  AUTO-INGEST:
  □ Ingest tagging: Summary, Entities, Topics, Importance
  □ ≥0.8 → LESSONS.md | <0.8 → LESSONS_ARCHIVE.md
  □ Qdrant store + auto-memory update
  □ "🔗 Connection với #BUG-XXX?" + "/consolidate?"

  REFLEXION (self-review sau fix):
  □ Tự hỏi:
    - "Fix này solve đúng ROOT CAUSE chứ không phải symptom?"
    - "Có side-effect nào từ fix này tôi chưa kiểm tra?"
    - "Bug tương tự có thể xảy ra ở chỗ khác không?"
  □ Nếu phát hiện vấn đề → quay lại Phase 3
  □ Nếu OK → close bug

→ Bug classification & common patterns: references/patterns.md
→ Browser Agent workflow: references/patterns.md
```

---

## BROWSER DEBUG PROTOCOL (v7.0) 🌐
> CSS issues, layout broken, JavaScript errors — Browser Agent workflow

```
STEP 1 — VISUAL IDENTIFICATION:
  □ Open Browser Agent → navigate to problem URL
  □ Screenshot: what does the bug look like?
  □ Compare with expected design (mockup/reference)
  □ Check multiple breakpoints (mobile/tablet/desktop)
  □ Check dark mode nếu applicable

STEP 2 — CONSOLE & NETWORK:
  □ Browser console errors? (JavaScript exceptions)
  □ Network tab: failed requests? (404, 500, CORS)
  □ CSS computed values: are styles being applied?
  □ Specificity conflicts: inspector shows overridden styles?

STEP 3 — COMMON WEB BUGS:
  | Symptom | Likely Cause | Quick Fix |
  |---|---|---|
  | Layout broken | Missing CSS, wrong selector | Check class names, inspect |
  | Text overflow | No overflow handling | overflow-wrap, truncate |
  | Image missing | Wrong path, not deployed | Check src, network tab |
  | Button no response | JS error, wrong event | Console errors, handler |
  | Mobile broken | No responsive styles | Media queries, viewport |
  | Flash of content | Font/CSS loading order | Preload, display=swap |
  | Scroll jank | Heavy paint, no GPU accel | transform instead of top |

STEP 4 — FIX & VERIFY:
  □ Fix targeted CSS/JS
  □ Screenshot AFTER fix (compare with before)
  □ Test all breakpoints again
  □ Check no regressions on other components
```

---

## KAIZEN ROOT CAUSE ANALYSIS (v7.0) 🎯

```
5 WHYS TEMPLATE:
  Bug: [describe the bug]
  Why 1: Tại sao bug xảy ra? → [answer]
  Why 2: Tại sao [answer 1]? → [answer]
  Why 3: Tại sao [answer 2]? → [answer]
  Why 4: Tại sao [answer 3]? → [answer]
  Why 5: Tại sao [answer 4]? → [ROOT CAUSE]

  Root cause: [1 câu rõ ràng]
  Fix: [giải pháp targeted]
  Prevention: [làm gì để không tái diễn]

PREVENTION PLAN:
  □ Có thể thêm automated check không? (lint rule, test)
  □ Có cần update CONVENTIONS.md không?
  □ Bug pattern này có xảy ra ở chỗ khác? (→ grep codebase)
  □ Cần thêm vào INSTINCTS.md? (/instinct)
```

---

## N8N WORKFLOW DEBUG (v7.0) ⚡

```
STEP 1 — EXECUTION ANALYSIS:
  □ Open execution history trong N8N
  □ Check: node nào failed? Error message gì?
  □ Input data của failed node: correct format?
  □ Check: execution timeout? Memory limit?

STEP 2 — COMMON N8N ISSUES:
  | Error | Cause | Fix |
  |---|---|---|
  | 401 Unauthorized | Expired token/wrong key | Refresh credentials |
  | 429 Too Many Req | Rate limit hit | Add Wait node, reduce freq |
  | Timeout | Slow API/large data | Increase timeout, paginate |
  | Empty output | Wrong JSON path | Check expression, test data |
  | Webhook not firing | URL wrong, N8N down | Verify URL, check N8N status |

STEP 3 — FIX & VERIFY:
  □ Fix node configuration
  □ Test with "Execute Workflow" (manual trigger)
  □ Verify output data correct
  □ Test error path (force error scenario)
  □ Check: other workflows affected?
```
