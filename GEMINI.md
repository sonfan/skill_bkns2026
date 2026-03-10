# APEX SKILL SYSTEM v2.0 — Global Rules
> Applied to ALL sessions in this project. Read before every task.
> Triết lý: AI không bao giờ quên. Mỗi phiên đều học hỏi và kết nối với quá khứ.

## MEMORY FILES (read at session start)
- `LESSONS.md` — bài học từ quá khứ (append-only, APEX format)
- `INSTINCTS.md` — patterns đã học + confidence score (0.0–1.0)
- `STATE.md` — project state hiện tại (phase, wave, blockers)
- `ACTIVE_CONTEXT.md` — working memory phiên này (xóa sau /save)
- `INSIGHTS.md` — compound insights từ /consolidate (auto-generated)

---

## 20 GLOBAL RULES

### Core Behavior
1. **ASK WHEN UNCLEAR** — Nếu yêu cầu mơ hồ hoặc có ≥2 cách hiểu → hỏi trước, đừng đoán
2. **READ MEMORY FIRST** — Đọc `LESSONS.md` + `INSTINCTS.md` + `INSIGHTS.md` trước bất kỳ task nào
3. **EVIDENCE-BASED** — Mọi quyết định kỹ thuật phải có lý do cụ thể, không phán đoán
4. **SELF-REASONING GATE** — Tự hỏi 3 câu trước khi implement: (a) Đây có phải cách tốt nhất? (≥2 alternatives) (b) Có risk/side-effect nào đang bỏ qua? (c) User có cần approve không?
5. **SEARCH-FIRST** — Tìm code/solution có sẵn trước khi tự viết. Ưu tiên: official > popular > custom

### Architecture & Planning
6. **SPEC BEFORE CODE** — Task ≥3 files hoặc ≥2h effort → viết `/spec` trước, không code ngay
7. **PLAN-FIRST** — Generate task list có checkpoint TRƯỚC khi bắt đầu code
8. **BRAINSTORM HARD GATE** — Feature phức tạp → `/plan` bắt buộc, đề xuất ≥2 approaches
9. **ADR FOR DECISIONS** — Mọi architectural decision quan trọng → ghi `/adr` ngay lúc quyết định
10. **WAVE EXECUTION** — Foundation → Integration → Polish

### Code Quality
11. **TDD IRON LAW** — Test TRƯỚC code (feature phức tạp). Coverage ≥80%
12. **QUALITY GATE** — Trước mỗi commit: `lint → format → type-check → test → audit`. Tất cả PASS mới commit
13. **CLEANUP PASS** — Sau implement + verify → review pass: dead code, TODO cũ, console.log, magic numbers
14. **ATOMIC COMMITS** — 1 task = 1 commit. Conventional format: `feat|fix|chore|perf|test|sec(scope): mô tả`

### Verification
15. **ROOT CAUSE FIRST** — Bug: tìm nguyên nhân gốc trước khi fix. Không patch symptom
16. **VERIFICATION LOOP** — Sau mỗi implementation: verify → regression check. Chỉ báo "done" khi tất cả pass
17. **INSTINCT VALIDATION** — Khi apply instinct → log kết quả. Đúng: +0.1. Sai: −0.2. Dưới 0.3 sau 5 lần → xem xét xóa

### Design & UX
18. **WCAG AA** — Mọi UI component phải đạt WCAG 2.2 AA. Color contrast, keyboard nav, aria-label
19. **DESIGN TOKEN MANDATORY** — Không dùng hardcoded color/spacing/font. Luôn dùng design tokens
20. **PERFORMANCE BUDGET** — LCP ≤2.5s, CLS ≤0.1, FID ≤100ms

---

## ANTIGRAVITY NATIVE FEATURES — Sử dụng tích cực

```
Browser Sub-Agent    → /craft, /fix UI bugs, /e2e verification
Multi-Agent Parallel → /build large features (split thành sub-tasks)
Mission Control      → Monitor parallel agents, assign /spec + /build + /secure cùng lúc
Artifact Output      → /spec, /handoff, /runbook output dạng structured Artifact
Planning Mode        → Luôn gen task-list có checkpoint trước khi code
Stitch MCP           → /craft setup → generate screens → edit screens → export code
```

---

## 🎯 9 SKILLS — 35 COMMANDS

| # | Skill | Commands | Purpose |
|---|---|---|---|
| 1 | **session** | `/start` `/save` `/checkpoint` `/review` `/recall` | 🔄 6-Layer Bootstrap + Consolidation Save + Quality Gate |
| 2 | **build** ⭐ | `/build` `/plan` `/search` | 🔥 Search-First + TDD + Memory-Enhanced Build |
| 3 | **fix** | `/fix` | 🐛 4-Phase Debug + Insight Match + Auto-Ingest |
| 4 | **craft** | `/craft` `/audit` `/tokens` `/e2e` | 🎨 UI + Design Tokens + WCAG + Browser Testing |
| 5 | **secure** | `/security` `/harden` `/ship` | 🔒 OWASP + Hardening + Production Readiness |
| 6 | **automate** | `/n8n` `/integrate` `/mcp` | ⚡ N8N + API Design + MCP Tool Design |
| 7 | **content** | `/seo` `/article` `/brief` `/audit-content` | 📝 SEO Pipeline + Content Engine |
| 8 | **spec** ⭐ | `/spec` `/handoff` `/adr` `/runbook` `/apidoc` `/componentdoc` | 📋 Architecture + Handoff + API/Component Docs |
| 9 | **learn** ⭐ | `/learn` `/instinct` `/evolve` `/review-instincts` `/consolidate` `/cross-link` | 🧠 Ingest + Consolidation + Instinct Evolution |

---

## 🧠 MEMORY ARCHITECTURE (6 Layers — APEX Enhanced)

```
┌─────────────────────────────────────────────────────────────┐
│  LAYER 0 — INGEST                                           │
│  Auto-tag mọi input: Entity + Topic + Importance (0.0–1.0)  │
├─────────────────────────────────────────────────────────────┤
│  LAYER 1 — WORKING       → ACTIVE_CONTEXT.md                │
│  Task hiện tại, files đang sửa, decisions phiên này         │
├─────────────────────────────────────────────────────────────┤
│  LAYER 2 — SEMANTIC      → GEMINI.md, STATE.md              │
│  Tech stack, rules, phase/wave, project brain                │
├─────────────────────────────────────────────────────────────┤
│  LAYER 3 — EPISODIC      → LESSONS.md, CHANGELOG.md         │
│  Bugs, bài học, timeline (append-only)                       │
├─────────────────────────────────────────────────────────────┤
│  LAYER 4 — INSTINCT      → INSTINCTS.md                     │
│  Learned patterns + confidence score (0.0–1.0)               │
├─────────────────────────────────────────────────────────────┤
│  LAYER 5 — CONSOLIDATION → INSIGHTS.md                       │
│  Cross-memory connections, compound insights                  │
│  Trigger: /save auto hoặc /consolidate manual                │
└─────────────────────────────────────────────────────────────┘
```

### Importance Score (áp dụng cho LESSONS entries)

```
1.0 — Security vulnerability, data loss risk
0.8 — 🔴 Critical: breaks production, major UX failure
0.6 — 🟡 Warning: blocks feature, performance hit
0.4 — 🟢 Info: best practice, optimization tip
0.2 — 💡 Note: minor improvement, style
```

---

## SKILL MAP

| Trigger | Skill |
|---------|-------|
| Bắt đầu / kết thúc phiên | `session` |
| Viết code mới, feature | `build` |
| Debug, lỗi, crash | `fix` |
| UI, design, component | `craft` |
| Security, deploy, production | `secure` |
| N8N, API, automation, MCP | `automate` |
| Bài viết, SEO, content | `content` |
| Architecture, docs, handoff | `spec` |
| Học hỏi, patterns, instincts, consolidate | `learn` |

---

## 📋 CHEAT SHEET

```
Bắt đầu phiên?           → /start [task]
Resume phiên cũ?          → /recall
Ý tưởng mơ hồ?           → /plan [idea]
Feature phức tạp?         → /plan [feature]
Research trước code?      → /search [need]
Viết code?                → /build [task]           🔥 TDD + Search-First
Gặp bug?                  → /fix [bug]              🐛 4-Phase Debug
Design UI?                → /craft [task]           🎨 Tokens + WCAG
Design tokens?            → /tokens [scope]
Browser test?             → /e2e [scope]
Audit chất lượng?         → /audit [scope]
Audit bảo mật?            → /security [target]      🔒 OWASP
Hardening?                → /harden [service]
Chuẩn bị deploy?          → /ship [env]
API / webhook?            → /integrate [service]     ⚡
N8N workflow?             → /n8n [task]              ⚡
Thiết kế MCP tool?        → /mcp [tool-name]
Content brief?            → /brief [topic]           📝
Viết bài SEO?             → /seo [topic]
Viết article?             → /article [topic]
Audit content?            → /audit-content [URL]
Architecture docs?        → /spec [scope]            📋
Bàn giao dự án?           → /handoff [project]
API documentation?        → /apidoc [endpoint]
Component docs?           → /componentdoc [scope]
Ghi ADR?                  → /adr [decision]
Tạo runbook?              → /runbook [service]
Ghi bài học?              → /learn [observation]     🧠 Ingest + Tag
Xem instincts?            → /instinct
Evolve instincts?         → /evolve
Review instincts?         → /review-instincts
Tổng hợp insights?       → /consolidate             🧠 Sleep-Brain Pass
Cross-link memories?      → /cross-link
Review code?              → /review [scope]
Lưu context?              → /checkpoint
Kết thúc phiên?           → /save                    (auto /consolidate)
```

---

## 📊 COMBO SKILLS

| Tình huống | Combo |
|---|---|
| Feature code mới | `/start` → check INSIGHTS → `/build` → `/save` |
| Fix bug | `/fix` (4-phase) → `/learn` (ingest) → `/consolidate` (nếu ≥3 lessons) |
| API endpoint mới | `/search` → `/build` → `/security` → `/review` |
| UI/Component mới | `/craft` → `/tokens` → `/audit` → `/e2e` |
| Dự án mới | `/plan` (GSD) → `/spec` → `/build` (wave-by-wave) |
| Deploy/Release | `/audit` → `/security` → `/harden` → `/ship` |
| Sau nhiều phiên | `/consolidate` → check INSIGHTS → `/evolve` |

---

## DOCUMENTATION — ZERO OVERLAP

| File | Layer | Viết gì | KHÔNG viết gì |
|---|---|---|---|
| `GEMINI.md` | Semantic (L2) | Tech stack, Rules, Skill map | Tasks, logs, state |
| `STATE.md` | Semantic (L2) | Phase, wave, blockers, next milestones | History |
| `LESSONS.md` | Episodic (L3) | Bug + bài học + Importance + Connected | Features, changelog |
| `CHANGELOG.md` | Episodic (L3) | Timeline thay đổi theo ngày | Tasks, lessons |
| `INSTINCTS.md` | Instinct (L4) | Learned patterns + confidence 0.0–1.0 | Bug reports |
| `INSIGHTS.md` | Consolidation (L5) | Cross-memory connections, compound insights | Raw data |
| `ACTIVE_CONTEXT.md` | Working (L1) | Working memory phiên hiện tại | Persistent info |

---

## CHANGELOG

| Date | Change |
|---|---|
| **2026-03-10** | **APEX v2.0**: 6-Layer Memory (+ Ingest L0 + Consolidation L5), 35 commands (+ /consolidate, /cross-link, /recall), Importance scoring, INSIGHTS.md, auto-Ingest tagging, sleep-brain consolidation, combo skills table. Synthesized from AG-SKILL v2.0 + Google ADK memory-agent + APEX v1.0 draft. |
| 2026-03-10 | v2.0: 20 rules, 9 skills, 32 commands. Research-based: ECC + 12 GitHub repos. |
| 2026-03-09 | v1.0 LAUNCH: 9 skills, 17 rules, ECC-inspired. |
