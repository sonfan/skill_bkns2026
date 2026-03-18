# LESSONS_ARCHIVE — Skill Repository

> **Mục đích**: Entries importance < 0.8, archived từ LESSONS.md.
> Tất cả đều được embed vào Qdrant (nếu available).

---

### 🟡 #WARN-001 — Upgrade skills phải update cross-references (2026-03-05)

- **Importance:** 0.6 | 🟡 Warning
- **Entities:** [skill-upgrade, cross-reference, SKILL.md]
- **Topics:** #upgrade, #consistency, #cross-reference
- **Archived:** 2026-03-14 (moved from LESSONS.md during v4.1 /save)
- **Triệu chứng:** Sau upgrade 4 core skills v4.1→v5.0, `/start` vẫn scan `.agent/commands/` thay vì `changes/`. Version refs cũ còn lại.
- **Nguyên nhân gốc:** Chỉ focus upgrade files target mà không audit cross-references.
- **Quy tắc rút ra:** Mỗi khi upgrade N skills → BẮT BUỘC grep toàn bộ repo tìm refs cũ.
- **Connected:** #LEARN-001 (confirmed pattern in v4.0→v4.1 upgrade)
