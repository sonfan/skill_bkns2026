# APEX SKILL SYSTEM v7.0 — Global Rules
> Applied to ALL sessions in this project. Read before every task.
> Triết lý: AI không bao giờ quên. Mỗi phiên đều học hỏi và kết nối với quá khứ. Fresh context = High quality.

## MEMORY FILES (read at session start)
- `LESSONS.md` — **critical-only** bài học (≤10 entries, importance ≥0.8). Luôn đọc.
- `LESSONS_ARCHIVE.md` — archived lessons (importance <0.8 hoặc entries cũ). Chỉ đọc khi cần.
- `INSTINCTS.md` — patterns đã học + confidence score (0.0–1.0)
- `STATE.md` — project state hiện tại (phase, wave, blockers)
- `ACTIVE_CONTEXT.md` — working memory phiên này (xóa sau /save)
- `INSIGHTS.md` — compound insights từ /consolidate (auto-generated)
- `.ai/memory/MEMORY.md` — **auto-memory**: AI tự ghi notes giữa phiên (≤200 dòng index)

---

## 26 GLOBAL RULES

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

### Fresh Context & Deep Thinking (v4.0)
21. **ULTRATHINK GATE** — Architecture decisions, complex bugs, refactoring >5 files → prefix "ultrathink:" → full analysis plan (≥500 words) TRƯỜC khi code. List ≥3 alternatives.
22. **CONTEXT HEALTH MONITOR v2.1** — Track context health: 🟢 Fresh (0-30%) | 🟡 Loaded (30-50%) | 🟠 Attention (50-70%) | 🔴 Heavy (70-85%) | 💀 Critical (>85%). Research-backed: 70%→precision loss, 85%→hallucinations (ACM 2025). Khi Heavy/Critical → commit, /save, fresh session.
23. **GSD CYCLE** — Features lớn dùng /gsd: Discuss → Plan → Execute → Verify. Mỗi phase có checkpoint context. KHÔNG skip Phase V (Verify).

### Subagent & Verification (v4.1)
24. **VERIFICATION GATE** — NO completion claims without FRESH verification evidence. "Should pass" ≠ evidence. Run command → read output → THEN claim. Anti-rationalization: "confident" ≠ evidence, "partial check" ≠ verification.
25. **SUBAGENT ORCHESTRATION** — Fresh subagent per task + 2-stage review (spec compliance → code quality). Model selection: mechanical → cheap, integration → standard, architecture → capable. Status protocol: DONE/CONCERNS/CONTEXT/BLOCKED.

### Memory Intelligence (v4.2 — Hindsight-inspired)
26. **BIOMIMETIC MEMORY** — Mỗi memory entry PHẢI có `type`: `world` (facts về tech/framework/tool, tĩnh), `experience` (trải nghiệm debug/build/deploy cụ thể), `mental_model` (pattern/insight tổng hợp từ nhiều experiences). Giúp recall chính xác: bug → search experience trước, design → search world + mental_model.

### Project Scaffold & Safety (v6.0 — BKNS-inspired)
27. **RISK CLASSIFICATION** — Trước khi thực thi, phân loại risk:

| Action | Risk | Auto-execute? | Require Approval? |
|---|---|---|---|
| Read files, search | 🟢 None | ✅ Yes | No |
| Edit ≤2 files, no breaking | 🟡 Low | ✅ Yes | No |
| Edit ≥3 files | 🟠 Medium | ❌ No | Yes — show plan |
| Delete files | 🔴 High | ❌ No | Yes — explicit |
| Run npm install/update | 🔴 High | ❌ No | Yes — show changes |
| Deploy/push production | 🔴 Critical | ❌ No | Yes — full checklist |
| Write .env / secrets | 🔴 Critical | ❌ No | Yes + verify |

28. **SECURITY-SPEC MANDATORY** — Nếu project có `docs/SECURITY-SPEC.md`, PHẢI đọc trước khi viết code. Không có exception. Pattern từ BKNS: security rules = frozen SSOT.
29. **PERSISTENT PROGRESS** — Dùng `PROGRESS.md` thay `ACTIVE_CONTEXT.md`. KHÔNG XÓA sau `/save`. Session memory phải persistent qua sessions.

---

## ANTIGRAVITY NATIVE FEATURES — Sử dụng tích cực

```
Browser Sub-Agent    → /craft, /fix UI bugs, /e2e verification
Multi-Agent Parallel → /build large features (split thành sub-tasks)
Mission Control      → Monitor parallel agents, assign /spec + /build + /secure cùng lúc
Artifact Output      → /spec, /handoff, /runbook output dạng structured Artifact
Planning Mode        → Luôn gen task-list có checkpoint trước khi code
Stitch MCP           → /craft setup → generate screens → edit screens → export code
Ultrathink           → Deep reasoning cho architecture/complex bugs (v4.0)
Context Health       → Monitor context window, auto-suggest fresh session (v4.0)
```

---

## 🎯 10 SKILLS — 59 COMMANDS

| # | Skill | Commands | Purpose |
|---|---|---|---|
| 1 | **session** | `/start` `/save` `/checkpoint` `/review` `/recall` `/init` `/status` | 🔄 4-Layer Bootstrap + Scaffold + Compaction |
| 2 | **build** ⭐ | `/build` `/plan` `/search` `/gsd` | 🔥 Search-First + TDD + Web Patterns + Ultrathink |
| 3 | **fix** | `/fix` | 🐛 4-Phase Debug + Kaizen + Browser/N8N Debug |
| 4 | **craft** ⭐ | `/craft` `/design` `/animate` `/responsive` `/palette` `/audit` `/tokens` `/e2e` | 🎨 Premium UI + Design System + WCAG + Visual Testing |
| 5 | **secure** | `/security` `/harden` `/ship` `/monitor` `/ssl` `/firewall` | 🔒 OWASP + Runtime Monitoring + VPS Security |
| 6 | **automate** ⭐ | `/n8n` `/n8n-ai` `/openclaw` `/pipeline` `/monitor-flow` `/integrate` `/mcp` | ⚡ N8N AI + OpenClaw + Pipeline + API |
| 7 | **content** ⭐ | `/seo` `/article` `/brief` `/cluster` `/competitor` `/refresh` `/internal-link` `/schema` `/audit-content` | 📝 SEO Engine v2 + Topic Clusters + Schema |
| 8 | **spec** | `/spec` `/spec refine` `/spec verify` `/handoff` `/adr` `/runbook` `/apidoc` `/componentdoc` | 📋 SDD + Architecture + Handoff |
| 9 | **learn** | `/learn` `/instinct` `/evolve` `/review-instincts` `/consolidate` `/cross-link` `/skill-audit` | 🧠 Ingest + Consolidation + Instinct Evolution |
| 10 | **verify** 🆕 | `/verify` `/fact-check` `/regression` `/test-web` | ✅ Anti-Hallucination + CoV + Web Testing |

---

## 🧠 MEMORY ARCHITECTURE v4.2 — Biomimetic + 3-Strategy Recall

> 📂 Chi tiết: `session/references/memory-architecture.md` (diagrams, importance scores, combo skills)

**4 Layers:** A (Rules: GEMINI.md) → B (Critical Lessons: LESSONS.md ≤10) → C (Semantic: Qdrant) → D (Auto: .ai/memory/)
**3 Memory Types:** `world` (facts) | `experience` (debug/build cụ thể) | `mental_model` (patterns tổng hợp)
**3-Strategy Recall:** semantic + keyword + temporal → merge top-5, ưu tiên match ≥2 strategies

---

## SKILL MAP

| Trigger | Skill |
|---------|-------|
| Bắt đầu / kết thúc phiên | `session` |
| Viết code mới, feature | `build` |
| Debug, lỗi, crash | `fix` |
| UI, design, component | `craft` |
| Security, deploy, production | `secure` |
| N8N, API, automation, MCP, OpenClaw | `automate` |
| Bài viết, SEO, content, cluster | `content` |
| Architecture, docs, handoff | `spec` |
| Học hỏi, patterns, instincts | `learn` |
| Kiểm tra, verify, fact-check, test web | `verify` |

---

## 📋 CHEAT SHEET

```
Bắt đầu phiên?           → /start [task]
Resume phiên cũ?          → /recall
Ý tưởng mơ hồ?           → /plan [idea]
Feature phức tạp?         → /plan [feature]
Feature lớn (GSD)?       → /gsd [feature]          🆕 v4.0
Research trước code?      → /search [need]
Viết code?                → /build [task]           🔥 TDD + Search-First
Deep thinking?            → ultrathink: [task]      🆕 v4.0
Gặp bug?                  → /fix [bug]              🐛 4-Phase Debug
Design UI?                → /craft [task]           🎨 Tokens + WCAG
Design system?            → /design [style]         🆕 v7.0
Animations?               → /animate [scope]        🆕 v7.0
Color palette?            → /palette [theme]        🆕 v7.0
Responsive test?          → /responsive [url]       🆕 v7.0
Design tokens?            → /tokens [scope]
Browser test?             → /e2e [scope]
Audit chất lượng?         → /audit [scope]
Audit bảo mật?            → /security [target]      🔒 OWASP
Hardening?                → /harden [service]
Server monitoring?        → /monitor [server]       🆕 v7.0
SSL certificate?          → /ssl [domain]           🆕 v7.0
Firewall audit?           → /firewall [server]      🆕 v7.0
Chuẩn bị deploy?          → /ship [env]
API / webhook?            → /integrate [service]     ⚡
N8N workflow?             → /n8n [task]              ⚡
N8N AI workflow?          → /n8n-ai [task]          🆕 v7.0
OpenClaw automation?      → /openclaw [task]        🆕 v7.0
Automation pipeline?      → /pipeline [flow]        🆕 v7.0
Monitor workflow?         → /monitor-flow [id]      🆕 v7.0
Thiết kế MCP tool?        → /mcp [tool-name]
Topic cluster?            → /cluster [topic]        🆕 v7.0
Competitor analysis?      → /competitor [url]       🆕 v7.0
Refresh bài cũ?           → /refresh [url]          🆕 v7.0
Internal linking?         → /internal-link [site]   🆕 v7.0
Schema markup?            → /schema [type]          🆕 v7.0
Content brief?            → /brief [topic]           📝
Viết bài SEO?             → /seo [topic]
Viết article?             → /article [topic]
Audit content?            → /audit-content [URL]
Verify code quality?      → /verify [scope]         🆕 v7.0
Fact-check AI code?       → /fact-check [code]      🆕 v7.0
Regression check?         → /regression [scope]     🆕 v7.0
Test website?             → /test-web [url]         🆕 v7.0
Spec refine?              → /spec refine [file]     🆕 v7.0
Spec verify?              → /spec verify [scope]    🆕 v7.0
Architecture docs?        → /spec [scope]            📋
Bàn giao dự án?           → /handoff [project]
API documentation?        → /apidoc [endpoint]
Component docs?           → /componentdoc [scope]
Ghi ADR?                  → /adr [decision]
Tạo runbook?              → /runbook [service]
Ghi bài học?              → /learn [observation]     🧠 Ingest + Tag
Xem instincts?            → /instinct
Evolve instincts?         → /evolve
Audit skill health?       → /skill-audit              📋
Review instincts?         → /review-instincts
Tổng hợp insights?       → /consolidate             🧠 Sleep-Brain Pass
Cross-link memories?      → /cross-link
Review code?              → /review [scope]
Lưu context?              → /checkpoint
Kết thúc phiên?           → /save                    (auto /consolidate)
```
```

---

## 📊 COMBO SKILLS

> 📂 Chi tiết: `session/references/memory-architecture.md`

| Tình huống | Combo |
|---|---|
| Feature mới | `/start` → `/build` → `/save` |
| Feature lớn | `/gsd` (D→P→E→V) |
| Fix bug | `/fix` → `/learn` → `/consolidate` |
| Deploy | `/audit` → `/security` → `/ship` |
| Build website | `/design` → `/craft` → `/build` → `/test-web` → `/ship` |
| SEO article | `/brief` → `/article` → `/schema` → `/seo` |
| Topic cluster | `/cluster` → `/brief` (each) → `/article` (each) → `/internal-link` |
| N8N AI workflow | `/n8n-ai` → `/integrate` → `/monitor-flow` |
| Server security | `/monitor` → `/ssl` → `/firewall` → `/security` |

---

## DOCUMENTATION — ZERO OVERLAP

| File | Layer | Viết gì | KHÔNG viết gì |
|---|---|---|---|
| `GEMINI.md` | A — Rules | Tech stack, Rules, Skill map | Tasks, logs, state |
| `STATE.md` | A — Rules | Phase, wave, blockers, next milestones | History |
| `LESSONS.md` | B — Critical | **Chỉ** lessons importance ≥0.8, ≤10 entries | Low-priority lessons |
| `LESSONS_ARCHIVE.md` | B → C | Lessons importance <0.8 hoặc cũ (Qdrant searchable) | Critical lessons |
| `CHANGELOG.md` | A — Rules | Timeline thay đổi theo ngày | Tasks, lessons |
| `INSTINCTS.md` | A — Rules | Learned patterns + confidence 0.0–1.0 | Bug reports |
| `INSIGHTS.md` | C — Semantic | Cross-memory connections, compound insights | Raw data |
| `PROGRESS.md` | D — Session | Session memory **persistent** (KHÔNG xóa) | Một-lần info |
| `ACTIVE_CONTEXT.md` | D — Legacy | Working memory (deprecated → migrate PROGRESS) | Persistent info |
| `CONVENTIONS.md` | A — Rules | Project-specific coding standards | Global rules |
| `SECURITY-SPEC.md` | A — Rules | Security rules (frozen SSOT) | Code |

---

## CHANGELOG

| Date | Change |
|---|---|
| **2026-03-23** | **APEX v7.0**: Targeted Upgrade for Website/UI/N8N/SEO — New `verify` skill (Anti-Hallucination + CoV + LLM-as-Judge + Web Testing). `craft` v7.0: +4 commands (`/design`, `/animate`, `/responsive`, `/palette`) + design-patterns reference. `content` v7.0: +5 commands (`/cluster`, `/competitor`, `/refresh`, `/internal-link`, `/schema`) + seo-advanced reference. `automate` v7.0: +4 commands (`/n8n-ai`, `/openclaw`, `/pipeline`, `/monitor-flow`) + n8n-ai-patterns reference. `secure` v7.0: +3 commands (`/monitor`, `/ssl`, `/firewall`) + WordPress/N8N security. `build` v7.0: LLM-as-Judge reflexion + web-patterns reference. `spec` v7.0: +2 commands (`/spec refine`, `/spec verify`) + SDD. `fix` v7.0: Browser Debug + Kaizen 5 Whys + N8N Debug. 10 skills, 59 commands, 29 rules. Research: 10+ GitHub repos (240k⭐), 13 papers, NeoLabHQ/context-engineering-kit, sickn33/antigravity-awesome-skills (1306+), affaan-m/everything-claude-code (78k⭐). |
| **2026-03-19** | **APEX v6.0**: BKNS Scaffold Integration — `/init` command (project scaffold generator), `/status` command (quick overview), PROGRESS.md persistent (thay ACTIVE_CONTEXT), SECURITY-SPEC mandatory (đọc trước khi code), Risk Classification Table (Rule 27-29). 6 new templates: GEMINI-PROJECT, CONVENTIONS, PROGRESS, SECURITY-SPEC, TASK-BREAKDOWN, ADR. Research-based: BKNS Project Scaffold Guide + claudefa.st + 8 open-source frameworks. |
| **2026-03-14** | **APEX v4.2**: Biomimetic Memory Upgrade — Rule 26 (BIOMIMETIC MEMORY: world/experience/mental_model types), 3-Strategy Recall (semantic + keyword + temporal), Reflect Auto-Trigger in /consolidate, type-aware retrieval in /build + /fix. Research-based: vectorize-io/hindsight (SOTA agent memory). |
| 2026-03-14 | **APEX v4.1**: Superpowers Integration — Verification Gate (Rule 24), Subagent Orchestration (Rule 25), anti-rationalization tables, model selection strategy, subagent prompt templates. Research-based: obra/superpowers (6.9k⭐). |
| 2026-03-14 | **APEX v4.0**: Progressive Disclosure (references/ folders), /gsd command (GSD workflow), Ultrathink Mode, Context Health Monitor. 3 rules mới (21-23). Skills: build/fix/craft được refactor với references/. Research-based: GSD2 (23k⭐), Anthropic SKILL.md patterns, Claude Code docs, sub-agent patterns, context rot research. |
| 2026-03-10 | **APEX v3.0 Memory**: 4-Layer Smart Retrieval. LESSONS.md critical-only (≤10, ≥0.8). LESSONS_ARCHIVE.md. Auto-Memory. Qdrant search. |
| 2026-03-10 | **APEX v2.0**: 6-Layer Memory, 35 commands, Importance scoring, INSIGHTS.md, consolidation. |
| 2026-03-10 | v2.0: 20 rules, 9 skills, 32 commands. Research-based: ECC + 12 GitHub repos. |
| 2026-03-09 | v1.0 LAUNCH: 9 skills, 17 rules, ECC-inspired. |
