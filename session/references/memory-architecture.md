# Memory Architecture v4.2 — Biomimetic + 3-Strategy Recall

> Triết lý: Không đọc hết, chỉ đọc đúng. Memory có type + thời gian + nghĩa.
> Inspired by: vectorize-io/hindsight (biomimetic memory — world/experiences/mental models)

```
┌─────────────────────────────────────────────────────────────┐
│  LAYER A — RULES (tĩnh, user kiểm soát, luôn đọc)          │
│  Files: GEMINI.md, STATE.md                                  │
│  Nội dung: Tech stack, conventions, rules, project state     │
│  Đặc điểm: Git-tracked, human-editable                       │
├─────────────────────────────────────────────────────────────┤
│  LAYER B — CRITICAL LESSONS (biomimetic, ≤10 entries)        │
│  File: LESSONS.md (importance ≥ 0.8)                         │
│  Archive: LESSONS_ARCHIVE.md (importance <0.8 hoặc cũ)      │
│  Memory Types: world | experience | mental_model (Rule 26)   │
│  Đặc điểm: Luôn đọc mỗi /start, ngắn gọn, git-tracked      │
├─────────────────────────────────────────────────────────────┤
│  LAYER C — SEMANTIC MEMORY (Qdrant, 3-strategy recall)      │
│  Engine: Qdrant Vector DB (MCP: qdrant_find / qdrant_store)  │
│  Recall: semantic + keyword + temporal (3 chiều)             │
│  Metadata: memory_type, timestamp, entities, importance      │
│  Đặc điểm: Cross-project, scale vô hạn, multi-strategy      │
├─────────────────────────────────────────────────────────────┤
│  LAYER D — AUTO-MEMORY (AI tự viết, local)                  │
│  File: .ai/memory/MEMORY.md (≤200 dòng) + topic files        │
│  Nội dung: Debugging insights, gotchas, project-specific      │
│  Đặc điểm: AI tự ghi, machine-local, không git               │
│  200-line rule: quá dài → tách thành topic files              │
└─────────────────────────────────────────────────────────────┘
```

## Memory Types (Biomimetic — Rule 26)
```
world        = Facts về tech/framework/tool (tĩnh, ít thay đổi)
               VD: "Laravel route specific trước wildcard"
experience   = Trải nghiệm debug/build/deploy cụ thể
               VD: "Fix bug N+1 bằng whereIn trong PayrollController"
mental_model = Pattern tổng hợp từ nhiều experiences (reflect output)
               VD: "70% lỗi deploy liên quan .env → checklist pre-deploy"

Recall priority theo task type:
  /fix  → experience first, then mental_model
  /build → world + mental_model first
  /craft → world (tokens) + mental_model (UX patterns)
```

## /start Smart Load Flow (v4.2)
```
1. RULES:    Đọc GEMINI.md + STATE.md                    ← Layer A
2. CRITICAL: Đọc LESSONS.md (≤10 entries, ≥0.8)          ← Layer B
3. 3-STRATEGY RECALL:                                    ← Layer C
   a. Semantic: qdrant_find(task context) → top 5
   b. Keyword:  grep LESSONS + ARCHIVE (tags, entities)
   c. Temporal: entries từ 7 ngày gần nhất
   → Merge top-5 (deduplicate, ưu tiên match ≥2 strategies)
4. AUTO:     Đọc .ai/memory/MEMORY.md (≤200 dòng)        ← Layer D
5. INSTINCT: INSTINCTS.md (top-3, confidence ≥0.7)       
6. INSIGHT:  INSIGHTS.md (nếu có liên quan)
→ Tổng: ~15-20 entries MAX thay vì ALL entries
```

## Importance Score

```
≥0.8 — Giữ trong LESSONS.md (critical, luôn đọc)
<0.8 — Archive sang LESSONS_ARCHIVE.md (Qdrant search khi cần)

1.0 — Security vulnerability, data loss risk
0.8 — 🔴 Critical: breaks production, major UX failure
0.6 — 🟡 Warning: blocks feature, performance hit
0.4 — 🟢 Info: best practice, optimization tip
0.2 — 💡 Note: minor improvement, style
```

## Combo Skills

| Tình huống | Combo |
|---|---|
| Feature code mới | `/start` → check INSIGHTS → `/build` → `/save` |
| Feature lớn (GSD) | `/start` → `/gsd` (D→P→E→V) → `/save` |
| Fix bug | `/fix` (4-phase) → `/learn` (ingest) → `/consolidate` (nếu ≥3 lessons) |
| API endpoint mới | `/search` → `/build` → `/security` → `/review` |
| UI/Component mới | `/craft` → `/tokens` → `/audit` → `/e2e` |
| Dự án mới | `/plan` (GSD) → `/spec` → `/build` (wave-by-wave) |
| Deploy/Release | `/audit` → `/security` → `/harden` → `/ship` |
| Sau nhiều phiên | `/consolidate` → check INSIGHTS → `/evolve` |
