---
name: build
description: Feature implementation and code writing. Use for /build (implement feature with TDD), /plan (plan before code), /search (research packages/solutions). Triggers on "viết code", "implement", "tạo feature", "build", "tdd", "xây dựng".
---

# Build Skill — Search-First + TDD + Memory-Enhanced Build

## /plan [idea or feature]
> Brainstorm và lập kế hoạch TRƯỚC khi viết bất kỳ dòng code nào

```
STEP 1 — UNDERSTAND
  □ Parse requirement: what exactly needs to be built?
  □ Clarifying questions (hỏi nếu mơ hồ, không đoán)
  □ Define success criteria rõ ràng

STEP 2 — BRAINSTORM GATE (Bắt buộc)
  □ Đề xuất ≥2 approaches KHÁC NHAU:
      "Approach A: [mô tả] — Pros/Cons"
      "Approach B: [mô tả] — Pros/Cons"
  □ Hỏi user chọn TRƯỚC KHI tiếp tục
  □ Check INSIGHTS.md: có compound insight liên quan?

STEP 3 — SPEC (GSD Methodology)
  WHY:  [vấn đề đang giải quyết]
  WHAT: [2-3 bullet tính năng cụ thể]
  HOW:  [pattern/library nào]
  DONE: [acceptance criteria]
  FILES: [list file cần tạo/sửa]

STEP 4 — WAVE PLAN
  Wave 1: Foundation (data, schema, base structure)
  Wave 2: Integration (logic, API, connections)
  Wave 3: Polish (UI, UX, edge cases, tests)

STEP 5 — ANTIGRAVITY TASK LIST
  □ Break down thành numbered tasks có checkpoint
  □ Identify tasks có thể parallel (spawn sub-agents?)
  □ Estimate: small (<1h) / medium (1-3h) / large (>3h)
  □ Nếu large → đề xuất /spec trước

OUTPUT: Structured plan, task list, file list — TRƯỚC khi bất kỳ code nào được viết
```

---

## /search [need]
> Research packages, solutions, và existing patterns

```
SEARCH PROTOCOL — 4 Steps:

  1. INTERNAL SEARCH (codebase + memory):
     □ grep -r "[keyword]" --include="*.ts" .
     □ Check LESSONS.md: đã giải quyết vấn đề tương tự?
     □ Check INSTINCTS.md: có pattern liên quan?
     □ Check INSIGHTS.md: compound insight nào relevant?

  2. EXTERNAL SEARCH (packages/docs):
     □ npm/pip/github + official docs
     □ Evaluate top 3 candidates:
        - Weekly downloads / stars (popularity = maturity)
        - Last commit (maintenance active?)
        - Bundle size / performance overhead
        - Security: known CVEs?
        - TypeScript support?

  3. DECISION MATRIX:
     official lib exists → dùng official
     no official + >1M weekly downloads → dùng popular
     niche need + small + well-maintained → dùng specialized
     nothing good → build minimal custom (document why)

  4. OUTPUT:
     "🔍 Found: [kết quả] → Sẽ dùng pattern [X]"
     "🔍 Not found: → Sẽ implement từ đầu theo pattern [Y]"
```

---

## /build [task]
> Implement feature với APEX 7-Step Build Protocol

```
BƯỚC 0 — MEMORY LOAD (KHÔNG SKIP)
  □ Đọc ACTIVE_CONTEXT.md → snapshot hiện tại
  □ Check INSTINCTS: có instinct confidence ≥0.7 liên quan không?
     → Nếu có: "🧠 Applying INS-XXX: [pattern]"
  □ Scan LESSONS.md: từ khóa liên quan task
     → Nếu có: "⚠️ Bài học liên quan: #BUG-XXX [importance]"
  □ Check INSIGHTS.md: compound insight nào relevant?
  🛑 STOP: Nếu chưa hoàn thành Bước 0, KHÔNG code.

BƯỚC 1 — SEARCH FIRST
  □ /search đã chạy chưa? (nếu chưa → chạy trước)
  □ Task ≥3 files? → /spec hoặc /plan bắt buộc trước

BƯỚC 2 — SPEC (30 giây)
  WHY:  Tại sao cần task này?
  WHAT: Thay đổi/tạo file nào?
  HOW:  Pattern/library nào?
  DONE: Khi nào biết là xong?

BƯỚC 3 — CODE (Clean + Typed)
  □ Viết TypeScript interfaces / type definitions TRƯỚC
  □ Viết function signatures (không có implementation)
  □ Implement code

BƯỚC 4 — TDD (Red → Green → Refactor)
  □ Viết test TRƯỚC code nếu feature phức tạp
  □ RED: test fail (expected)
  □ GREEN: code vừa đủ để pass
  □ REFACTOR: clean up, không break tests
  □ Coverage ≥80%

BƯỚC 5 — VERIFY (Prove it, don't trust it)
  □ lint → format → type-check → test → audit
  □ Diff review: list từng file đã thay đổi + lý do
  □ Regression check: những gì có thể bị ảnh hưởng?

BƯỚC 6 — CLEANUP PASS (separate review pass)
  □ Scan: console.log, debugger, TODO cũ
  □ Scan: magic numbers → extract vào constants
  □ Scan: dead code, unused imports
  □ Đây là PASS RIÊNG — không làm cùng lúc với implementation

BƯỚC 7 — ATOMIC COMMIT + MINI CHECKPOINT
  □ git add <file1> <file2>  # Chỉ file của task này
  □ git commit -m "feat(module): mô tả ngắn gọn"
  □ Update ACTIVE_CONTEXT.md:
     - Mark task vừa commit là [x]
     - Set NEXT IMMEDIATE ACTION = task tiếp theo
     - Record decision nếu có
     - Ghi evidence verify

CHECKLIST TRƯỚC COMMIT:
  [ ] Đã search trước khi code
  [ ] Không có debug statements
  [ ] Null-safe operators đầy đủ
  [ ] DB transactions nếu multi-step
  [ ] Evidence verify đã có
  [ ] Commit message theo conventional commits
  [ ] INSTINCT đã apply: log kết quả
```

### TDD HARD GATE — Không được bypass
```
❌ KHÔNG được viết implementation trước test
❌ KHÔNG được commit khi coverage <80%
❌ KHÔNG được skip verification loop
❌ KHÔNG được bỏ qua cleanup pass
✅ Exceptions phải được ghi rõ lý do vào LESSONS.md
```

### ANTIGRAVITY PARALLEL BUILD
```
Khi feature lớn (>3h), xem xét split cho parallel agents:
  Agent A: Backend / API layer
  Agent B: Frontend / UI components
  Agent C: Tests / documentation
  
Sync point: Trước khi merge, chạy /review trên combined output
```
