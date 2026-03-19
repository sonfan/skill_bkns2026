# TASK-BREAKDOWN.md — {PROJECT_NAME}

> Checklist từng task cho dự án. Tạo từ SPEC hoặc `/plan`.
> Template: APEX v6.0 — adapted từ BKNS PR-BREAKDOWN pattern

---

## Task Overview

| Total | ⬜ TODO | 🔄 In Progress | ✅ Done | ❌ Blocked |
|---|---|---|---|---|
| {N} | {N} | {N} | {N} | {N} |

---

## T-01 · {Task Title}

**Scope:** {module/component} · **Effort:** {S/M/L} · **Depends:** {T-XX hoặc none}
**Branch:** `feature/{short-desc}`

- [ ] {checklist item 1}
- [ ] {checklist item 2}
- [ ] {checklist item 3}
- [ ] Build + tests pass
- [ ] Security check (nếu applicable)

---

## T-02 · {Task Title}

**Scope:** {module/component} · **Effort:** {S/M/L} · **Depends:** {T-XX hoặc none}
**Branch:** `feature/{short-desc}`

- [ ] {checklist item 1}
- [ ] {checklist item 2}
- [ ] Build + tests pass

---

## Effort Guide

| Size | Thời gian | Ví dụ |
|---|---|---|
| **S** | < 1 giờ | Config, deploy files, stub, docs update |
| **M** | 1-4 giờ | Feature với tests, refactor module |
| **L** | 4-8 giờ | Complex feature, nhiều integrations, migration |

---

## Dependencies Graph

```
T-01 ──→ T-02 ──→ T-04
              ↗
T-03 ─────┘
```

> Chỉ bắt đầu task khi tất cả dependencies đã ✅ DONE.
