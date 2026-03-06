---
name: Plan — Ideation + Spec-Driven Task Planner (v6.0)
description: "Brainstorm → Spec-driven planning: Ideation pipeline → Qdrant recall → Research → Proposal → Specs → Design → Tasks → Beads epic. v6.0 gộp brainstorm + plan. Change Folder Structure + Delta Specs. Kích hoạt bằng /plan [feature name] hoặc /brainstorm [idea]."
---

# /plan [feature name] — cũng nhận `/brainstorm [idea]`

> **v6.0 IDEATION + SPEC-DRIVEN** — Gộp brainstorm + plan
> Mục tiêu: Từ ý tưởng mơ hồ → spec actionable → TDD tasks
> Mỗi change = 1 folder với proposal + specs + design + tasks.

---

## KHI NÀO DÙNG /plan?

| Tình huống | Dùng /plan? |
|---|---|
| Fix bug nhỏ / sửa UI | ❌ Không — `/fix` hoặc `/build` trực tiếp |
| Feature mới 1-2 files | ❌ Không — `/build` trực tiếp |
| Feature phức tạp (3+ files) | ✅ `/plan` trước, `/build` sau |
| Feature cần design decision | ✅ `/plan` + `/craft` |
| Ý tưởng mơ hồ, cần phân tích | ✅ `/plan` (= brainstorm + spec) |
| So sánh nhiều approaches | ✅ `/plan` |
| Dự án mới toàn bộ | ✅ `/plan` cho từng phase |

---

## QUY TRÌNH 6 BƯỚC

### Step 0 — IDEATION (Brainstorm — cho ý tưởng mơ hồ) 🆕 v6.0

> Bước này CHỈ chạy khi user có ý tưởng chưa rõ hoặc gọi `/brainstorm`.
> Nếu feature đã rõ ràng → nhảy sang Step 1.

```
1. CAPTURE raw idea:
   - Ghi lại CHÍNH XÁC lời user (không interpret sai)
   - Hỏi 3 câu hỏi mở:
     • "Vấn đề gốc mà bạn muốn giải quyết là gì?"
     • "Ai là người dùng chính?"
     • "Kết quả lý tưởng nhất trông như thế nào?"

2. EXPAND — Brainstorm ≥ 3 approaches:
   | # | Approach | Ưu điểm | Nhược điểm | Effort |
   |---|---|---|---|---|
   | A | [approach 1] | [pros] | [cons] | S/M/L |
   | B | [approach 2] | [pros] | [cons] | S/M/L |
   | C | [approach 3] | [pros] | [cons] | S/M/L |

3. ANALYZE approach được chọn:
   - User Stories: "Là [role], tôi muốn [action], để [benefit]"
   - Technical Feasibility: stack hiện tại support?
   - Risk Assessment: xác suất × impact
   - Dependencies: API, data, approval cần?

4. Output → Feature Spec sẵn sàng cho Step 1-5
```

### Step 1 — RESEARCH ⭐ (Brainstorming hard gate)

```
1. EXPLORE context trước khi plan:
   - Đọc GEMINI.md → tech stack, Architecture Rules
   - Đọc docs/ → patterns hiện có
   - Đọc LESSONS.md → warnings liên quan
   - Scan code hiện tại → identify files cần tạo/sửa
   - Đọc existing specs (changes/*/specs/) → context từ changes trước

2. HỎI CLARIFYING QUESTIONS:
   🛑 HARD GATE: KHÔNG tạo spec khi chưa hiểu rõ
   - Hỏi user TỪ 1 CÂU MỘT THỜI ĐIỂM
   - Multiple choice preferred, open-ended khi cần
   - Hiểu rõ: purpose, constraints, success criteria

3. PROPOSE 2-3 APPROACHES:
   - Trình bày trade-offs mỗi approach
   - Dẫn đầu bằng recommended option + lý do
   - Hỏi user chọn trước khi tạo spec

4. ⭐ QDRANT RECALL (Layer 4):
   → qdrant_find("plan: [feature name]") → patterns tương tự
5. ⭐ BEADS CONTEXT (Layer 5):
   → bd ready --json → tasks liên quan đã có
```

> 🛑 **HARD GATE** (từ Superpowers): Phải present approach VÀ được user approve TRƯỚC KHI tạo change folder.

> ⭐ **SELF-REASONING ENHANCEMENT (v6.1)**:
> Sau khi chọn approach, BẮT BUỘC thêm:
> Q2: "Risk/side-effect của approach được chọn?"
> → Liệt kê ≥ 1 risk + mitigation cho mỗi risk
> → Nếu risk HIGH → cảnh báo user rõ ràng trước khi tạo spec

---

### Step 2 — CREATE CHANGE FOLDER ⭐ (v6.2.1 BKNS-Unified)

> **v6.2.1**: Gộp `proposal.md` + `specs/spec.md` + `design.md` → 1 file `SPEC.md` chuẩn BKNS.

#### Cấu trúc change folder:

```
changes/<feature-name>/
├── SPEC.md          ← BKNS Feature SPEC (gộp WHY + WHAT + HOW, 10 sections chuẩn)
├── tasks.md         ← Implementation tasks (TDD bite-sized)
└── delta-specs.md   ← Spec changes to merge vào docs/ khi done
```

> 💡 **Dự án MỚI** → `SPEC.md` ở root repo dùng Full SPEC (19 sections)
> 💡 **Feature** → `changes/<name>/SPEC.md` dùng Feature SPEC (10 sections)
> 💡 **Task nhỏ ≤ 2 files** → Mini-Spec inline, KHÔNG cần change folder
> 📋 Template: `templates/SPEC.md` (3 tầng đầy đủ)

#### SPEC.md (Feature SPEC — 10 sections bắt buộc)
```markdown
# SPEC — [Feature Name]

> **Type**: Feature SPEC | **Version**: v1.0 | **Updated**: YYYY-MM-DD
> **Trạng thái**: Draft → Reviewing → Approved → In Progress → Done

## 1. Thông tin chung
| Trường | Giá trị |
|---|---|
| Tên tính năng | [name] |
| Mã task | [TASK-XXX] |
| Người phụ trách | [dev] |
| Mức ưu tiên | P0/P1/P2/P3 |
| Size | S / M / L |
| Breaking changes | Yes / No |

## 2. Bối cảnh và vấn đề
[WHY — Vấn đề gì? Ảnh hưởng ai? Hậu quả?]

## 3. Mục tiêu
[Mục tiêu measurable + kết quả mong muốn]

## 4. Phạm vi
- **In scope**: [liệt kê]
- **Out of scope**: [liệt kê]

## 6. Business Flow
[Numbered steps hoặc mermaid]

## 7. Yêu cầu chức năng
| Mã | Mô tả |
|---|---|
| FR-01 | [requirement] |

## 10. Thiết kế dữ liệu (nếu có)
[Tables, columns, migrations]

## 11. Thiết kế API (nếu có)
| Method | Endpoint | Request | Response |
|---|---|---|---|

## 15. Rủi ro
| Rủi ro | Mitigation |
|---|---|

## 16. Tiêu chí nghiệm thu
| Mã | Tiêu chí | Verify bằng |
|---|---|---|
| AC-01 | [criteria] | [test/curl/screenshot] |
```

> **Mapping format cũ → mới**:
> `proposal.md` (WHY) → §1 + §2 + §3 + §4 + §15
> `specs/spec.md` (WHAT) → §6 + §7 + §16
> `design.md` (HOW) → §10 + §11 + optional sections

#### tasks.md (TDD bite-sized — giữ nguyên format v5.0)
```markdown
# [Feature Name] — Implementation Tasks

> **REQUIRED**: Use /build with TDD (RED→GREEN→REFACTOR) for each task.

### Task 1: [Component Name] (2-5 min)
**Files:** Create: `path/to/file` | Test: `tests/path/test_file`
**RED**: Write failing test → run → expect FAIL
**GREEN**: Write minimal code → run → expect PASS
**REFACTOR**: Clean up → run → still PASS
**COMMIT**: `git commit -m "feat: add [behavior] with test"`
```

#### delta-specs.md (giữ nguyên format v5.0)
```markdown
# [Feature Name] — Delta Specs
> These deltas will be merged into docs/ when this change is archived.

### docs/architecture.md
- ADD: [New component description]

### GEMINI.md
- ADD: [New rule if any]
```


---

### Step 3 — PROGRESS TRACKING

#### NEXT-TODO.md (bảng tracking)
```markdown
| # | Task | Size | Status | Deps | Notes |
|---|------|------|--------|------|-------|
| T-001 | [task] | M | ⬜ | - | |
| T-002 | [task] | L | ⬜ | T-001 | |
```

#### ⭐ BEADS TASK CREATION (Layer 5 — nếu available)
```bash
bd create "[Feature Name]" -t epic -p 1 --json
bd create "[Task 1]" --parent <epic-id> -p 1 --json
bd dep add <task-2-id> <task-1-id>
```

---

### Step 4 — PRESENT & CONFIRM

```
📋 CHANGE FOLDER đã tạo:
  changes/<feature-name>/
  ├── SPEC.md        (Feature SPEC — 10 sections BKNS)
  ├── tasks.md       (N tasks, TDD bite-sized)
  └── delta-specs.md (Merge vào docs/ khi done)

📊 SPEC:
  Size: [S|M|L] | Files: [N] | Tasks: [N] | Tests: [N cases]

🔜 TIẾP THEO:
  /build [feature name] → TDD từng task trong tasks.md
```

---

### Step 5 — ARCHIVE (Khi feature DONE — gọi từ /save)

```
1. Verify: tất cả tasks trong tasks.md đã ✅
2. Merge delta-specs.md vào docs/ tương ứng
3. Move folder: changes/<name>/ → archive/YYYY-MM-DD-<name>/
4. Specs giờ phản ánh trạng thái MỚI

→ Virtuous cycle: Specs → Change → Implement → Archive → Updated Specs
```

---

## QUY TẮC

- 🛑 HARD GATE: Phải hỏi + được approve TRƯỚC KHI tạo change folder
- Tasks phải TDD bite-sized (2-5 phút mỗi task)
- Mỗi task có exact file paths, code, test commands
- Delta specs PHẢI merge sau khi done
- NNN tăng dần (scan .agent/commands/ hoặc changes/)
- Beads/Qdrant không available → bỏ qua im lặng
