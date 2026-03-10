---
name: session
description: Session lifecycle management. Use for /start (begin session), /save (end session), /checkpoint (save mid-session), /review (multi-perspective code review), /recall (quick resume). Triggers on "bắt đầu phiên", "kết thúc phiên", "lưu context", "review code", "start session", "save session", "recall", "resume".
---

# Session Skill — 6-Layer Bootstrap + Consolidation Save + Quality Gate

## /start [task]
> Khởi động phiên làm việc, load 6-Layer memory, set context

```
APEX Bootstrap Protocol:

LAYER 1 — Check ACTIVE_CONTEXT.md:
  → Có: hiển thị "📍 Đang làm: [task] | Files: [X] | Tiếp theo: [Y]"
         → /recall ngay, không cần đọc thêm
  → Không: tiếp tục bình thường

LAYER 2 — Load Semantic:
  □ Đọc GEMINI.md: tech stack, rules hiện tại
  □ Đọc STATE.md: phase, wave, blockers

LAYER 3 — Scan Episodic:
  □ LESSONS.md: top-5 entries by importance score liên quan đến task
  □ CHANGELOG.md: 3 thay đổi gần nhất

LAYER 4 — Load Instincts:
  □ INSTINCTS.md: top-3 instincts liên quan (confidence ≥ 0.7)

LAYER 5 — Check Insights:
  □ INSIGHTS.md: có compound insight nào liên quan task không?
  □ Nếu có: alert ngay "💡 INSIGHT liên quan: [tóm tắt]"

SET TASK:
  □ Parse [task] input
  □ Áp dụng SELF-REASONING GATE:
      (a) Đây có phải cách tốt nhất? (≥2 alternatives)
      (b) Có risk/side-effect nào đang bỏ qua?
      (c) User có cần approve không?
  □ Tạo ACTIVE_CONTEXT.md với: task, approach, risks, checklist

ANTIGRAVITY PLAN:
  □ Generate task-list có numbered checkpoints
  □ Nếu task lớn → đề xuất spawn parallel sub-agents
  □ Output: plan rõ ràng trước khi bắt đầu code

OUTPUT FORMAT:
═══════════════════════════════════════
🚀 APEX SESSION START
═══════════════════════════════════════
📍 Task: [task nếu có]
🏗️ Phase: [X] | Wave: [Y]
⚠️ Lessons cần nhớ:
  - #BUG-007 [0.8] — [tóm tắt 1 dòng]
🧠 Instincts active:
  - INS-003 [0.85] — [pattern]
💡 Insights: [tóm tắt nếu có]
🎯 Ready. Gõ lệnh tiếp theo.
═══════════════════════════════════════
```

**Output:** `ACTIVE_CONTEXT.md` + task plan với checkpoints

---

## /recall
> Quick resume từ ACTIVE_CONTEXT.md — không cần load lại toàn bộ

```
□ Đọc ACTIVE_CONTEXT.md
□ Hiển thị: snapshot hiện tại + NEXT IMMEDIATE ACTION
□ Tiếp tục từ đúng vị trí đã checkpoint
```

---

## /checkpoint
> Save mid-session state, không kết thúc phiên

```
□ Update ACTIVE_CONTEXT.md (theo template chuẩn):
    - Task snapshot: đang làm gì, đã xong gì
    - Files: path đầy đủ + đang làm gì với file đó
    - Decisions: quyết định quan trọng đã ra phiên này
    - Blockers: nếu có
    - Lessons applied: #BUG-XXX đang cẩn thận tránh
    - NEXT IMMEDIATE ACTION: đủ cụ thể để AI tiếp tục ngay
□ Chạy VERIFICATION LOOP nhanh:
    lint → type-check → test (nếu applicable)
□ Ghi timestamp
□ Output: "✅ Checkpoint #N lưu thành công lúc HH:MM"
```

---

## /save
> Kết thúc phiên, consolidate memory, push code

```
STEP 1 — MEMORY AUDIT
  □ Đọc ACTIVE_CONTEXT.md → liệt kê task xong/còn dở
  □ Task dở → cảnh báo: "⚠️ [N] task chưa xong. Tiếp tục hay lưu tạm?"

STEP 2 — VERIFICATION LOOP (bắt buộc)
  □ Run: lint → format → type-check → test
  □ Nếu FAIL → FIX trước, không save với broken state
  □ Run CLEANUP PASS: tìm console.log, TODO, hardcoded values
  □ Commit nếu có changes (conventional commit format)

STEP 3 — EXTRACT LEARNINGS + INGEST
  □ Trong phiên này, gặp vấn đề gì?
  □ Giải pháp nào hiệu quả? Cái nào không?
  □ Append vào LESSONS.md (APEX format: Importance + Entities + Topics + Connected)
  □ Never overwrite existing entries

STEP 4 — CONSOLIDATION CHECK
  □ Đếm LESSONS entries kể từ /consolidate cuối
  □ Nếu ≥3: tự động chạy /consolidate trước khi save
  □ INSIGHTS.md được update

STEP 5 — UPDATE INSTINCTS
  □ Pattern nào được confirm? → confidence += 0.1
  □ Pattern nào sai? → confidence -= 0.2 + thêm counter-example
  □ Pattern mới nào xuất hiện? → thêm vào INSTINCTS.md (confidence: 0.5)

STEP 6 — UPDATE STATE
  □ Merge ACTIVE_CONTEXT quan trọng → STATE.md
  □ Cập nhật CHANGELOG.md: những gì đã thay đổi

STEP 7 — CLEANUP & PUSH
  □ Archive ACTIVE_CONTEXT.md (timestamp) → Xóa ACTIVE_CONTEXT.md
  □ README sync check (có cần update không?)
  □ git push (MANDATORY — không xong = không "done")
```

---

## /review [scope]
> Multi-perspective code review — 3 góc nhìn độc lập

```
INPUT: [scope] = file path, PR, hoặc "last changes"

PERSPECTIVE 1 — SECURITY 🔴
  □ Injection vulnerabilities (SQL, XSS, SSRF)
  □ Authentication / authorization gaps
  □ Sensitive data exposure (logs, errors, responses)
  □ Dependency vulnerabilities (outdated packages)
  □ Security headers present?
  □ Secrets hardcoded?

PERSPECTIVE 2 — PERFORMANCE 🔵
  □ Unnecessary re-renders (React) / N+1 queries
  □ Missing indexes, unoptimized queries
  □ Bundle size impact (new imports?)
  □ Memory leaks (event listeners, subscriptions)
  □ Core Web Vitals impact (LCP, CLS, FID)
  □ Caching opportunities missed?

PERSPECTIVE 3 — MAINTAINABILITY 🟢
  □ Functions >30 lines → đề xuất split
  □ Duplicated logic (DRY violations)
  □ Missing/outdated comments trên complex logic
  □ Type safety (any, unknown không có guard)
  □ Error handling đầy đủ không?
  □ Test coverage adequate?

OUTPUT FORMAT:
  🔴 SECURITY ISSUES (phải fix trước khi merge):
  🔵 PERFORMANCE ISSUES (nên fix):
  🟢 MAINTAINABILITY (có thể fix sau):
  ✅ APPROVED nếu không có critical issues
```

---

## VERIFICATION LOOP (dùng trong tất cả workflows)
```bash
# Thứ tự bắt buộc — dừng ngay khi có lỗi
1. lint (eslint/biome/ruff)
2. format check (prettier/black)
3. type-check (tsc/mypy)
4. test (jest/pytest/vitest) — coverage check
5. security audit (npm audit/pip-audit)

# Chỉ sau khi tất cả PASS mới tiếp tục
```
