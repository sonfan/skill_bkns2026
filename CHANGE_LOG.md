# CHANGE LOG — Skill Repository

## 2026-03-06

### Added
- **v6.2.1 UNIFIED SPEC STANDARD** — Chuẩn hóa quy trình viết SPEC theo BKNS
  - Hệ thống SPEC 3 tầng thống nhất:
    - **Full SPEC** (19 sections) → Dự án mới / Module lớn → `SPEC.md` ở root
    - **Feature SPEC** (10 sections) → Feature ≥ 3 files → `changes/<name>/SPEC.md`
    - **Mini-SPEC** (bảng 10 dòng) → Task ≤ 2 files → inline
  - Section numbers đồng nhất 1-19 giữa các tầng cho tính kế thừa
  - **Files thay đổi chi tiết** (cho rollback):

  | Action | File | Mô tả |
  |---|---|---|
  | REWRITE | `templates/SPEC.md` | Thêm 3-tier system header, enriched Full SPEC, thêm Feature SPEC template, cập nhật Mini-Spec |
  | REWRITE | `plan/SKILL.md` Step 2 | Change folder: gộp `proposal.md` + `specs/spec.md` + `design.md` → 1 file `SPEC.md` (Feature SPEC) |
  | MODIFY | `build/SKILL.md` Step 0.5 | `.spec.md` (6 sections frontend) → BKNS SPEC reference (3 tầng) |
  | MODIFY | `save/SKILL.md` Step 4 | Archive verify: thêm check SPEC.md trạng thái Done |
  | MODIFY | `GEMINI.md` docs table | `changes/` description: "proposal + specs + design + tasks" → "SPEC.md + tasks + delta-specs" |
  | MODIFY | `CHANGE_LOG.md` | Thêm entry v6.2.1 chi tiết cho rollback |

  - **Files REMOVED từ change folder template**: `proposal.md`, `specs/spec.md`, `design.md`
  - **Files GIỮA NGUYÊN trong change folder**: `tasks.md`, `delta-specs.md`
  - **Rollback**: Revert commit chứa "feat(spec): unified SPEC standard v6.2.1"

### Added
- **v6.2 BKNS-ALIGNED** — Chuẩn hóa theo BKNS Dev Operating System Pack v2
  - Rule 14: BKNS Repo Standard — 6 files bắt buộc + naming convention
  - +8 templates: SPEC (19 sections + Mini-Spec), DEPLOYMENT (11 sections), PROJECT-META, README-BKNS, CHANGELOG (Keep a Changelog), WEEKLY-REPORT, PROJECT-AUDIT, REPO-STRUCTURE
  - `/docs init bkns` — khởi tạo repo BKNS chuẩn từ templates
  - `/start` — thêm BKNS compliance check (6 mandatory files)
  - `/plan` — thêm BKNS SPEC template cho dự án mới
  - `/save` — thêm DEPLOYMENT.md, PROJECT-META.md, SPEC.md vào docs update
  - `/ship check` — thêm BKNS release checklist (10 items)
  - Updated docs table (Skill System Files + BKNS Repo Standard Files)

### Added
- **v6.1 SELF-REASONING GATE** — Global Rule 13
  - 3-Question Self-Check trước MỌI quyết định thực thi
  - Q1: "Đây đã là phương án tốt nhất chưa?" (≥2 alternatives)
  - Q2: "Có risk/side-effect nào đang bỏ qua?" (breaking, regression, perf, security)
  - Q3: "User có cần approve không?" (scope-based auto-decide)
  - Embedded: `/build` Step 1.5, `/fix` Phase 3, `/craft` Step 2.5, `/plan` Q2 enhancement
  - Updated: GEMINI.md (13 Rules), AGENTS.md

## 2026-03-05

### Changed
- **v6.0 MEMORY-FIRST ARCHITECTURE** — Gộp thông minh 18→14 skills
  - 🆕 `/craft`: Gộp design + frontend → UI lifecycle (setup/component/css/a11y)
  - 🆕 `/quality`: Gộp guard + perf + review-website → quality gate (test/a11y/perf/all)
  - 🆕 `/ship`: Pre-launch checklist + CI/CD + Monitoring + Rollback
  - ⬆ `/plan`: Gộp brainstorm → Ideation Step 0
  - ⬆ `/memory`: Context Compression Protocol + 3-Tier Load Order
  - +4 Global Rules (9-12): A11y WCAG AA, Security Headers, Design Tokens, Perf Budget
  - Website Development Workflow
  - Zero-overlap documentation model
  - Archived: design→craft, guard→quality, brainstorm→plan, review-website→quality

### Added
- `LESSONS.md` — Bài học đầu tiên: #WARN-001 cross-reference consistency
- `CHANGE_LOG.md` — File theo dõi thay đổi theo timeline

### Changed
- **v5.0 HYBRID UPGRADE** — 4 core skills nâng cấp (build, plan, fix, save)
  - `/build`: TDD Iron Law (RED→GREEN→REFACTOR) + Spec Compliance Check
  - `/plan`: Change Folder + Brainstorming Hard Gate
  - `/fix`: 4-Phase Systematic Debugging + Root Cause Iron Law
  - `/save`: 2-Stage Review + Change Archive + Delta Merge
- **Self-audit fixes** — 9 bugs + 6 improvements
  - `/start`: scan `changes/`, keyword table v5.0, version fix
  - `/memory`: version v4.1 → v5.0
  - `/guard`: TDD Rule 6 note
  - `/brainstorm`: v5.0 change folder output
  - `/design`: TDD exception note
  - `/integrate`: change folder reference
  - `AGENTS.md`: v5.0 Core Rules section
  - `GEMINI.md`: v5.0 header, Rules 6-8, workflow, cheat sheet

## 2026-03-04

### Changed
- v4.1 HYBRID MEMORY: +1 skill (/memory). Layer 5 Beads + Layer 4 Qdrant.
- v4.0 STRUCTURED VIBE: +2 skills (/docs, /seo). Architecture Spec Phase.
- v3.0 EXTENDED: +4 skills (brainstorm, n8n-pro, web-security, review-website).

## 2026-02-28

### Changed
- v2.0: Gộp 26 skills → 8 unified skills. Thêm /plan, /guard.
