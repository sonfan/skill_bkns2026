# GEMINI — Skill Repository v4.1 (Hybrid Memory + Production Code Framework)

> **GitHub**: https://github.com/tampd/skill
> **Local path**: /root/skill
> **Cập nhật**: 2026-03-04 — **v4.1 HYBRID MEMORY**

---

## 🔑 THÔNG TIN QUAN TRỌNG

### Skill System v4.1 — Hybrid Memory
Phiên bản 4.1 nâng cấp từ v4.0 (14 skills) lên **15 skills**, tập trung:
- 🆕 **memory**: 5-Layer Memory Management (/checkpoint, /recall, /memory)
- ⬆ **start**: Thêm **Beads Ready** (Layer 5) + **Qdrant Recall** (Layer 4)
- ⬆ **build**: Thêm **Qdrant recall** + **Beads claim/close** + **Qdrant store**
- ⬆ **save**: Thêm **Beads close/compact** + **Qdrant store knowledge**
- ⬆ **fix**: Thêm **Qdrant recall** trước debug + **Qdrant store** + **Beads close** sau fix
- ⬆ **plan**: Thêm **Beads epic/task creation** + **Qdrant recall**
- Giữ nguyên: docs, seo, design, n8n-pro, guard, integrate, brainstorm, web-security, review-website

### Triết lý v4.1: "Never Forget"
```
❌ KHÔNG AI được quên context giữa các phiên
✅ 5-Layer Memory: Working → Semantic → Episodic → Vector → Task Graph
✅ Beads (Dolt SQL) cho task tracking với dependency graph
✅ Qdrant (Vector DB) cho semantic search cross-project
✅ Graceful fallback: Layer 4-5 không available → bỏ qua im lặng
```

### GitHub Repository
```
URL:    https://github.com/tampd/skill
Remote: origin → git@github.com:tampd/skill.git (SSH)
Branch: main
SSH Key: SHA256:nTSlO07MbIplXX/j2FAHlyuSb+MJxPO1yboDHJJidFs
```

> **RULE**: Mọi dự án đều push qua SSH (`git@github.com:`), KHÔNG dùng HTTPS.
> Nếu remote đang là HTTPS → chạy `git remote set-url origin git@github.com:{user}/{repo}.git`

---

## ⚠️ GLOBAL RULES

### Rule 1: AI PHẢI HỎI KHI CHƯA RÕ
> Nếu yêu cầu chưa rõ nghĩa, thiếu thông tin, hoặc mâu thuẫn:
> 🛑 AI PHẢI HỎI user TRƯỚC KHI lập kế hoạch, viết code, ghi docs.
> ❌ KHÔNG giả định và code khi chưa xác nhận.

### Rule 2: ĐỌC LESSONS TRƯỚC KHI CODE
> Mỗi task PHẢI bắt đầu bằng việc đọc LESSONS.md + grep tags liên quan.
> Không có ngoại lệ. Đây là cách AI "nhớ" để không lặp sai lầm.

### Rule 3: EVIDENCE-BASED VERIFICATION
> Không chấp nhận "nó chạy rồi". Phải có bằng chứng cụ thể:
> curl output, test results, screenshot, hoặc log.

### Rule 4: ARCHITECTURE SPEC TRƯỚC KHI CODE
> Project mới hoặc module mới ≥ 3 files → BẮT BUỘC tạo `.spec.md` trước.
> Spec gồm: Site Map, Component Tree, Data Flow, File Structure, Design Tokens.
> Xem chi tiết: `/build` Step 0.5.

### Rule 5: BEADS CHO TASK TRACKING, NEXT-TODO LÀM FALLBACK (MỚI v4.1)
> Nếu dự án có `.beads/` → dùng `bd` CLI cho task management.
> Nếu Beads chưa init hoặc không available → dùng NEXT-TODO.md như bình thường.
> Layer 4-5 (Qdrant/Beads) KHÔNG bao giờ gây lỗi nếu không available.

---

## 📁 CẤU TRÚC SKILL REPOSITORY v4.1

```
/root/skill/
├── GEMINI.md                ← File này — brain & rules
├── README.md                ← Hướng dẫn cài đặt
│
│── ─── 8 CORE SKILLS (từ v2, nâng cấp v4.1) ───
├── start/SKILL.md           ← /start [task]          ⬆ Beads Ready + Qdrant Recall
├── build/SKILL.md           ← /build [task] ⭐       ⬆ 5-Layer Memory hooks
├── fix/SKILL.md             ← /fix [bug]             ⬆ Qdrant recall + store
├── save/SKILL.md            ← /save                  ⬆ Beads close + Qdrant store
├── plan/SKILL.md            ← /plan [feature]        ⬆ Beads epic creation
├── design/SKILL.md          ← /design [task]          ⬆ Token System + Component API
├── guard/SKILL.md           ← /guard [scope]
├── integrate/SKILL.md       ← /integrate [svc]
│
│── ─── 4 SKILLS (v3) ───
├── n8n-pro/SKILL.md         ← /n8n [task]             ⬆ MCP Server + Sub-workflows
├── brainstorm/SKILL.md      ← /brainstorm [idea]
├── web-security/SKILL.md    ← /security [target]
├── review-website/SKILL.md  ← /review-web [url]
│
│── ─── 2 SKILLS (v4) ───
├── docs/SKILL.md            ← /docs [scope]           Documentation + ADR
├── seo/SKILL.md             ← /seo [topic]            SEO + GEO Writer
│
│── ─── 1 SKILL (v4.1) ───
├── memory/SKILL.md          ← /memory /checkpoint /recall  🆕 5-Layer Management
│
│── ─── INFRASTRUCTURE ───
├── qdrant-memory/SKILL.md   ← Qdrant Layer 4 setup guide
└── archive/                 ← Skills cũ v1+v2 (preserved)
```

---

## 🎯 15 SKILLS — QUICK REFERENCE

| # | Skill | Lệnh | Mục đích | Từ v |
|---|---|---|---|---|
| 1 | **start** | `/start [task]` | Khởi động phiên + Beads ready + Qdrant recall | v2 ⬆ |
| 2 | **build** ⭐ | `/build [task]` | Code + 5-Layer Memory hooks | v2 ⬆ |
| 3 | **fix** | `/fix [bug]` | Debug + Qdrant recall/store + Beads close | v2 ⬆ |
| 4 | **save** | `/save` | Review + Beads close/compact + Qdrant store | v2 ⬆ |
| 5 | **plan** | `/plan [feature]` | Blueprint + Beads epic creation | v2 ⬆ |
| 6 | **design** | `/design [task]` | UI/UX + Design Tokens + Component API | v2 ⬆ |
| 7 | **guard** | `/guard [scope]` | Test + security + performance | v2 ⬆ |
| 8 | **integrate** | `/integrate [svc]` | API + 3rd-party + webhook | v2 |
| 9 | **n8n-pro** | `/n8n [task]` | N8N + MCP Server + Sub-workflows | v3 ⬆ |
| 10 | **brainstorm** | `/brainstorm [idea]` | Ideation → Spec → Prototype | v3 |
| 11 | **web-security** | `/security [target]` | OWASP audit + CVE + hardening | v3 |
| 12 | **review-website** | `/review-web [url]` | Website review toàn diện 7 chiều | v3 |
| 13 | **docs** | `/docs [scope]` | Documentation + ADR + handoff | v4 |
| 14 | **seo** | `/seo [topic]` | SEO + GEO content writer | v4 |
| 15 | **memory** 🆕 | `/memory` `/checkpoint` `/recall` | 5-Layer Memory management | v4.1 |

---

## 🔄 SESSION LIFECYCLE v4.1

```
/start [task]  →  [auto-select skill]  →  /save
   │                    │                    │
   ├─ Load context      ├─ /build ⭐        ├─ 7-criteria review
   ├─ Check LESSONS     ├─ /fix             ├─ Write LESSONS
   ├─ Beads ready 🆕    ├─ /design          ├─ Beads close + compact 🆕
   ├─ Qdrant recall 🆕  ├─ /n8n             ├─ Qdrant store 🆕
   ├─ Scan blueprints   ├─ /guard           ├─ Update docs
   └─ Auto-select       ├─ /integrate       ├─ Atomic commit
      15 skills         ├─ /plan            └─ Push
                        ├─ /brainstorm
                        ├─ /security
                        ├─ /review-web
                        ├─ /docs
                        ├─ /seo
                        └─ /memory 🆕
```

---

## 🧠 MEMORY ARCHITECTURE (5 Tầng — Hybrid v4.1)

| Tầng | Engine/File | Mục đích | Skill tương tác |
|---|---|---|---|
| **1 — Working** | `ACTIVE_CONTEXT.md` | Working memory (xóa sau /save) | /checkpoint, /recall |
| **2 — Semantic** | `GEMINI.md`, `STATE.md`, `NEXT-TODO.md` | Não bộ dự án | /start, /save |
| **3 — Episodic** | `LESSONS.md`, `CHANGE_LOG.md` | Bộ nhớ dài hạn (append-only) | /fix, /save |
| **4 — Vector** 🆕 | **Qdrant** (MCP: qdrant_find/store) | Semantic search cross-session | /start, /build, /fix, /save |
| **5 — Task Graph** 🆕 | **Beads/Dolt** (CLI: bd ready/create/close) | Dependency-aware task tracking | /start, /build, /save, /plan |

---

## 📚 DOCUMENTATION STANDARDS

### Nguyên tắc viết docs

| File | Viết gì | KHÔNG viết gì |
|---|---|---|
| `GEMINI.md` | Tech stack, Architecture Rules (✅❌ code), Version, Links | Task TODO, logs phiên |
| `LESSONS.md` | Bug #WARN-XXX + ✅❌ code examples + quy tắc rút ra | Feature code, changelog |
| `CHANGE_LOG.md` | Timeline thay đổi: Added/Fixed/Changed/Removed | Task future |
| `NEXT-TODO.md` | Task backlog (bảng tracking: #, Size, Status, Deps) | Task đã xong (xóa ngay) |
| `docs/architecture.md` | System diagrams, module tree, data flow | Task backlog |
| `docs/business-rules.md` | Logic nghiệp vụ thuần (KHÔNG code) | UI details |
| `docs/api-endpoints.md` | REST API: method + URL + auth + request/response | Business logic |
| `docs/setup.md` | Cài đặt môi trường dev/prod | Business rules |
| `docs/security-audit.md` | Audit results, CVEs, remediation plan | Code patches |

### Cách viết Architecture Rules (bắt buộc)

```markdown
### Rule N: [Tên rule] (VI PHẠM = BUG)
[Giải thích 1 dòng tại sao rule này tồn tại]

// ✅ Đúng — [giải thích]
[code example đúng]

// ❌ Sai — [giải thích]
[code example sai]
```

### Cách viết LESSONS.md entries (bắt buộc)

```markdown
### 🟡 #WARN-NNN — Tiêu đề (YYYY-MM-DD)
- **Mức độ:** 🟡 Warning
- **Thẻ:** #tag1, #tag2
- **Triệu chứng:** [mô tả quan sát]
- **Nguyên nhân gốc:** [WHY]
- **Cách fix:**
  // ✅ Đúng
  [code]
  // ❌ Sai
  [code]
- **Quy tắc rút ra:** [Rule áp dụng mãi]
- **File liên quan:** `path/to/file`
```

### Cách viết Task Blueprint (.agent/commands/task-NNN.md)

Tạo bởi `/plan`, follow bởi `/build`:

```markdown
> **Complexity: [S|M|L]**

# Task-NNN: [Feature Name]

## Step 1 — Read Rules & Docs
- `GEMINI.md` (Rules: [chỉ rõ rule nào])
- `LESSONS.md` (grep: [keywords])
- `docs/[doc].md` (Section: [chỉ rõ])

## Step 2 — Implementation
[File tree + logic flow + error handling table]

## Step 3 — Tests
[Liệt kê từng test case cụ thể]

## Step 4 — Documentation
[Chỉ rõ files nào cần update]
```

### Cách viết NEXT-TODO.md (bảng tracking)

```markdown
| # | Task | Size | Status | Deps | Notes |
|---|------|------|--------|------|-------|
| T-001 | [name] | M | ⬜ | - | |
| T-002 | [name] | L | 🔄 | T-001 | Đang làm |
| T-003 | [name] | S | ✅ | - | Done 28/02 |
```

Status: ⬜ Not started | 🔄 In progress | ✅ Done | ⏸️ Blocked

---

## 📋 CHEAT SHEET v4.1

```
Bắt đầu phiên?           → /start [task]
Viết code?                → /build [task]         ⭐ 5-Layer Memory hooks
Gặp bug?                  → /fix [bug]            ⬆ Qdrant recall
Feature phức tạp?         → /plan [feature] → /build
Design / UI?              → /design [task]         ⬆ Token System
Test / audit code?        → /guard [scope]
API / webhook?            → /integrate [service]
N8N workflow?             → /n8n [task]            ⬆ MCP Server
Cần ý tưởng / spec?      → /brainstorm [idea]
Audit bảo mật sâu?       → /security [target]
Review website?           → /review-web [url]
Viết docs / handoff?      → /docs [scope]
Viết bài SEO / content?   → /seo [topic]
Lưu context giữa phiên?  → /checkpoint            🆕
Khôi phục context?        → /recall                🆕
Xem trạng thái memory?    → /memory                🆕
Kết thúc phiên?           → /save
```

---

## 📝 CHANGE LOG

| Date | Change |
|---|---|
| **2026-03-04** | **v4.1 HYBRID MEMORY**: +1 skill mới (/memory, /checkpoint, /recall). Thêm Layer 5 Beads (task graph) + nâng cấp Layer 4 Qdrant. Nâng cấp /start (Beads ready + Qdrant recall), /build (5-Layer hooks), /save (Beads close/compact + Qdrant store), /fix (Qdrant recall/store + Beads close), /plan (Beads epic). Thêm Rule 5. 14 → 15 skills. |
| 2026-03-04 | v4.0 STRUCTURED VIBE: +2 skills mới (/docs, /seo). Nâng cấp /build (Architecture Spec Phase), /design (Token System + Component API), /n8n (MCP Server + Sub-workflows + Scaling), /start (14-rule auto-select). Thêm Rule 4 (Architecture Spec). |
| 2026-03-04 | v3.0 EXTENDED: +4 skills mới (brainstorm, n8n-pro, web-security, review-website). Nâng cấp start + guard. |
| 2026-02-28 | v2.0: Gộp 26 skills → 8 unified skills. Thêm /plan, /guard. Archive 27 skills cũ. |
| 2026-02-27 | v1.x: 26 skills, memory-optimizer, qdrant integration |
