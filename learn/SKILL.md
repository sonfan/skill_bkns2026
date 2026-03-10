---
name: learn
description: Continuous learning, instinct tracking, pattern extraction, and memory consolidation. Use for /learn (capture observation), /instinct (view/manage instincts), /evolve (cluster instincts into skills), /review-instincts (validate and prune), /consolidate (sleep-brain pass), /cross-link (manual connections). Triggers on "học hỏi", "pattern", "instinct", "lesson", "bài học", "ghi nhớ", "learn", "extract pattern", "consolidate", "cross-link", "insights".
---

# Learn Skill — Ingest + Consolidation + Instinct Evolution

## INSTINCTS.md Format
```yaml
# INSTINCTS.md
instincts:
  - id: INS-001
    pattern: "Khi dùng useEffect với async, luôn dùng cleanup function"
    context: "React, async data fetching"
    confidence: 0.85
    created: 2025-01-15
    last_applied: 2025-03-10
    apply_count: 12
    success_count: 11
    failure_count: 1
    counter_examples:
      - "Không áp dụng khi effect chỉ chạy một lần và không có cleanup cần thiết"
    source: "Bug INS-001-source: memory leak trong ProductList"
```

---

## /learn [observation]
> APEX Learn = Ingest Layer + Cross-Link + Store

```
BƯỚC 1 — INGEST TAG
  Extract từ observation:
  → Summary: [1-2 câu]
  → Entities: [tech, files, services liên quan]
  → Topics: [domain tags]
  → Importance: [0.0–1.0 + emoji]
     1.0 — Security vulnerability, data loss risk
     0.8 — 🔴 Critical: breaks production, major UX failure
     0.6 — 🟡 Warning: blocks feature, performance hit
     0.4 — 🟢 Info: best practice, optimization tip
     0.2 — 💡 Note: minor improvement, style

BƯỚC 2 — CLASSIFY
  Pattern (≥3 tình huống áp dụng) → INSTINCTS.md
  One-off (quá specific) → chỉ LESSONS.md

BƯỚC 3 — CROSS-LINK CHECK
  Tự động scan LESSONS.md tìm entries có overlapping entities/topics
  → "🔗 Tìm thấy connection với: #BUG-003 (same entities), #BUG-008"
  → Update Connected field cho các entries liên quan

BƯỚC 4 — STORE
  LESSONS.md: APEX format entry:
    ### #BUG-[SỐ] [Tiêu đề ngắn]
    - **Ngày:** YYYY-MM-DD
    - **Importance:** [score] | [emoji level]
    - **Entities:** [list]
    - **Topics:** #tag1, #tag2
    - **Triệu chứng:** Mô tả lỗi nhìn thấy
    - **Nguyên nhân gốc:** Tại sao lỗi xảy ra
    - **Cách fix:** Giải pháp với code example
    - **Quy tắc:** [rút ra]
    - **Connected:** #BUG-XXX, #INS-YYY
    - **File liên quan:** [paths]

  INSTINCTS.md: nếu là pattern (confidence: 0.5 mới)

BƯỚC 5 — CONSOLIDATE TRIGGER
  → Đếm lessons kể từ /consolidate cuối
  → Nếu ≥3: "💡 Nên chạy /consolidate để tìm compound insights"
```

---

## /consolidate
> Sleep-Brain Consolidation Pass — kết nối memories, tìm compound insights

```
Khi nào chạy:
  - Tự động: cuối mỗi /save (nếu ≥3 lessons mới)
  - Thủ công: sau khi thêm ≥3 LESSONS entries mới
  - Định kỳ: sau 5+ phiên làm việc

PROCESS:

  BƯỚC 1 — SCAN
    Đọc toàn bộ LESSONS.md + INSTINCTS.md
    Đếm entries chưa được consolidate

  BƯỚC 2 — CLUSTER
    Nhóm entries theo:
    - Overlapping entities
    - Same topic domain
    - Sequential timeline (bugs trong cùng 1 tuần)
    - Causal relationships (bug A dẫn đến bug B)

  BƯỚC 3 — CONNECT
    Với mỗi cluster, tìm pattern chung:
    Example:
      #BUG-001 [Next.js, SSR, hydration, importance: 0.8]
      #BUG-003 [Next.js, Date, hydration, importance: 0.8]
      → Connection: "Mọi hydration bugs có cùng root: client-only APIs trong SSR"

  BƯỚC 4 — GENERATE INSIGHT
    Ghi vào INSIGHTS.md:
    ---
    ## 💡 INSIGHT-[N] [date] | Importance: [max of cluster]
    **Cluster:** [tên pattern]
    **Connected Memories:** [#BUG-XXX, ...]
    **Pattern Discovered:** [mô tả connection]
    **Compound Solution:** [giải pháp tổng quát]
    **Impact:** [nếu áp dụng → kết quả gì]
    ---

  BƯỚC 5 — BACKLINK
    Update Connected field trong mỗi entry đã cluster

  BƯỚC 6 — PROMOTE TO INSTINCT (nếu đủ điều kiện)
    Cluster ≥3 entries + cùng solution → propose instinct mới
    confidence: 0.6 (có evidence từ nhiều instances)

OUTPUT: "✅ /consolidate xong: [N] clusters, [M] insights, [K] instinct candidates"
```

---

## /cross-link
> Manual cross-linking giữa memories

```
□ Chỉ định 2+ entries cần link
□ Mô tả relationship
□ Update Connected field cho tất cả entries liên quan
□ Nếu tạo cluster mới ≥3 entries → suggest /consolidate
```

---

## /instinct [action]
> Xem và quản lý instinct library

```
/instinct → list all (sorted by confidence desc)
/instinct apply [INS-ID] → apply và log result
/instinct validate [INS-ID] [correct|wrong|partial] → update confidence
/instinct show [INS-ID] → full detail + history
/instinct prune → list candidates for removal (confidence <0.3, ≥5 lần apply)
/instinct export → export sang JSON/YAML
/instinct import [file] → import instincts từ external source
```

**Display format:**
```
INS-001 [0.85] ████████░ "useEffect async cleanup"         React     Applied: 12x
INS-007 [0.72] ███████░░ "Hydration: no client-API in SSR" Next.js   Applied: 8x
INS-012 [0.45] ████░░░░░ "CSS Grid cho complex layouts"    Frontend  Applied: 4x
INS-004 [0.28] ██░░░░░░░ [CANDIDATE FOR REMOVAL]           N8N       Applied: 3x

Confidence rules:
  correct → +0.10 (max 1.0)
  partial → +0.02
  wrong   → -0.20 (min 0.0)
  < 0.30 sau ≥5 lần → flag for review
  = 0.00 → auto-archive (không xóa)
```

---

## INSTINCT VALIDATION CYCLE (tự động trong /save)
```
SAU MỖI TASK — khi /save chạy:

  1. RECALL: instinct nào đã được apply trong session?
  2. EVALUATE từng applied instinct:
     → Kết quả: correct / wrong / partial?
  3. UPDATE CONFIDENCE: theo rules ở trên
  4. PRUNE CANDIDATES: confidence < 0.30 sau ≥5 lần → flag
  5. SURFACE NEW PATTERNS: gì lặp lại ≥2 lần chưa có instinct?
     → Propose new instinct (user confirm trước khi add)
```

---

## /evolve
> Cluster related instincts thành formal skill section

```
PROCESS:
  1. GROUP: identify instincts có cùng domain/context
  2. THRESHOLD: nhóm ≥3 instincts liên quan → candidate for evolution
  3. DRAFT: viết skill section từ instinct cluster
  4. INTEGRATE: merge vào skill phù hợp (build/fix/craft/...)
  5. RETIRE: instincts đã evolved → đánh dấu "promoted to skill"
```

---

## /review-instincts
> Periodic review — prune noise, promote high-confidence

```
REVIEW CHECKLIST (chạy monthly):

HIGH CONFIDENCE (≥0.85):
  □ Promote candidates: đưa thành rule hoặc /evolve thành skill section
  □ Document with examples

MEDIUM CONFIDENCE (0.50-0.84):
  □ Đang learn: tiếp tục apply và validate

LOW CONFIDENCE (0.30-0.49):
  □ Còn 5 lần apply nữa → quyết định keep/drop

PRUNE CANDIDATES (<0.30, ≥5 lần apply):
  □ Xem lại counter-examples
  □ Archive hoặc rewrite
  □ Không xóa — chỉ deactivate (history preserved)
```
