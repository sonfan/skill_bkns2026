# DEV Project Audit — BKNS

> **Mục tiêu**: Trong 60 phút, nắm toàn bộ trạng thái kỹ thuật các dự án.
> **Người thực hiện**: CEO / Head of Engineering
> **Ngày audit**: YYYY-MM-DD

---

## 1. Project Inventory

| # | Project | Business Purpose | Repo URL | Owner | Backup | Status | Env | Docs | Deploy Guide | Last Update | Jira | Risk |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | | | | | | Active/Maint/Dep | Dev/Test/Prod | Full/Partial/None | Yes/No | | | Low/Med/High |
| 2 | | | | | | | | | | | | |
| 3 | | | | | | | | | | | | |

## 2. Quality Score

| # | Project | Repo OK | README | SPEC | Deploy Guide | Owner | Backup | Tests | Score | Risk |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | | ✅/❌ | ✅/❌ | ✅/❌ | ✅/❌ | ✅/❌ | ✅/❌ | ✅/❌ | /7 | |
| 2 | | | | | | | | | | |

> **Rule**: Thiếu ≥ 3 tiêu chí → **High Risk** 🔴

## 3. Risk Register

| Project | Rủi ro | Mức độ | Action Required |
|---|---|---|---|
| | Không có repo | 🔴 | Tạo repo ngay |
| | Chỉ 1 dev hiểu | 🔴 | Assign backup + viết docs |
| | Không có deploy guide | 🟡 | Viết DEPLOYMENT.md |
| | Không có changelog | 🟡 | Tạo CHANGELOG.md |
| | Không rõ prod ở đâu | 🔴 | Document infra |

## 4. Kết luận Audit

Sau audit phải trả lời được:

- [ ] BKNS có bao nhiêu project dev? **→ [N]**
- [ ] Project nào đang chạy production? **→ [list]**
- [ ] Project nào có nguy cơ mất kiểm soát? **→ [list]**
- [ ] Project nào cần chuẩn hóa docs ngay? **→ [list]**

## 5. Action Plan

| Priority | Action | Owner | Deadline |
|---|---|---|---|
| P0 | | | |
| P1 | | | |
| P2 | | | |
