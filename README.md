# APEX Skill System v5.2

> 🧠 **AI không bao giờ quên.** Mỗi phiên đều học hỏi và kết nối với quá khứ.

**APEX**: Adaptive Pattern EXtraction — hệ thống skill cho AI coding assistant (Antigravity / Gemini CLI).

## ✨ What's New (v5.2 — Selective Upgrade)

- **Verification Report** — Output chuẩn PASS/FAIL sau mỗi `/build` verify. Structured table: Build / Types / Lint / Tests / Security / Diff / Overall
- **Context Health Monitor v2.1** — 5-level scale (thêm 🟠 Attention 50-70%). Research-backed: 70%→precision loss, 85%→hallucinations (ACM 2025 + Florian Guide)
- **Compaction Decision Guide** — Bảng quyết định khi nào nên `/checkpoint` vs tiếp tục (từ ECC strategic-compact)
- **Hypothesis-Driven Debugging** — Phase 2 `/fix` thêm form→verify→iterate hypothesis trước 5-WHY
- **`/skill-audit` command** — 4-phase kiểm tra sức khỏe skill system (Inventory→Quality→Summary→Recommendations)
- **Token Optimization** — GEMINI.md giảm 24.5% (16,599→12,536 bytes). Verbose sections → `references/`

### Previous Versions
- **v5.0**: Reflexion Loop, Context Health v2 (3 chiều) — [NeoLabHQ/context-engineering-kit](https://github.com/NeoLabHQ/context-engineering-kit)
- **v4.2**: Biomimetic Memory (world/experience/mental_model), 3-Strategy Recall — [vectorize-io/hindsight](https://github.com/vectorize-io/hindsight)
- **v4.1**: Verification Gate, Subagent Orchestration — [obra/superpowers](https://github.com/obra/superpowers)
- **v4.0**: Progressive Disclosure, /gsd, Ultrathink — [GSD2](https://github.com/jlowin/gsd2)

## 📦 9 Skills — 36 Commands

| # | Skill | Commands | Purpose |
|---|---|---|---|
| 1 | **session** | `/start` `/save` `/checkpoint` `/review` `/recall` | 4-Layer Bootstrap + Compaction Guide |
| 2 | **build** ⭐ | `/build` `/plan` `/search` `/gsd` | TDD + Search-First + Verification Report |
| 3 | **fix** | `/fix` | 4-Phase Debug + Hypothesis-Driven |
| 4 | **craft** | `/craft` `/audit` `/tokens` `/e2e` | UI + Design Tokens + WCAG + Browser |
| 5 | **secure** | `/security` `/harden` `/ship` | OWASP + Hardening + Production |
| 6 | **automate** | `/n8n` `/integrate` `/mcp` | N8N + API + MCP Tool Design |
| 7 | **content** | `/seo` `/article` `/brief` `/audit-content` | SEO Pipeline + Content Engine |
| 8 | **spec** ⭐ | `/spec` `/handoff` `/adr` `/runbook` `/apidoc` `/componentdoc` | Architecture + Docs |
| 9 | **learn** ⭐ | `/learn` `/instinct` `/evolve` `/review-instincts` `/consolidate` `/cross-link` `/skill-audit` | Ingest + Evolution + Skill Health |

## 🚀 Install

```bash
# Clone repo
git clone https://github.com/sonfan/skill_bkns2026.git /home/hostbilldev/public_html/skill_bkns2026

# Tạo thư mục skills (nếu chưa có)
mkdir -p ~/.gemini/antigravity/skills

# Symlink toàn bộ skills vào Antigravity global
for skill in session build fix craft secure automate content spec learn; do
  ln -sfn /home/hostbilldev/public_html/skill_bkns2026/$skill ~/.gemini/antigravity/skills/$skill
done

# Copy GEMINI.md vào global config
cp /home/hostbilldev/public_html/skill_bkns2026/GEMINI.md ~/.gemini/GEMINI.md

# Verify
ls -la ~/.gemini/antigravity/skills/
```

### Update

```bash
cd /home/hostbilldev/public_html/skill_bkns2026 && git pull
# Xong! Symlinks tự cập nhật — không cần chạy lại lệnh link.
```

## 📋 26 Global Rules

### Core Behavior (1-5)
1. **ASK WHEN UNCLEAR** — ≥2 cách hiểu → hỏi trước
2. **READ MEMORY FIRST** — LESSONS + INSTINCTS + INSIGHTS
3. **EVIDENCE-BASED** — Mọi quyết định phải có lý do
4. **SELF-REASONING GATE** — 3 câu trước khi implement: best approach? risks? need approval?
5. **SEARCH-FIRST** — Tìm solution có sẵn trước khi tự viết

### Architecture (6-10)
6. **SPEC BEFORE CODE** — ≥3 files → viết spec trước
7. **PLAN-FIRST** — Task list có checkpoints
8. **BRAINSTORM HARD GATE** — ≥2 approaches bắt buộc
9. **ADR FOR DECISIONS** — Ghi lại quyết định lớn
10. **WAVE EXECUTION** — Foundation → Integration → Polish

### Code Quality (11-14)
11. **TDD IRON LAW** — Test trước code. RED → GREEN → REFACTOR
12. **QUALITY GATE** — lint → format → type-check → test → audit
13. **CLEANUP PASS** — Dead code, TODO, console.log
14. **ATOMIC COMMITS** — `feat|fix|chore(scope): desc`

### Verification (15-17)
15. **ROOT CAUSE FIRST** — Không patch symptoms
16. **VERIFICATION LOOP** — Verify → regression check → Verification Report
17. **INSTINCT VALIDATION** — Correct: +0.1 | Wrong: -0.2

### Design (18-20)
18. **WCAG AA** — Color contrast, keyboard nav, ARIA
19. **DESIGN TOKENS** — Không hardcode colors/fonts/spacing
20. **PERFORMANCE BUDGET** — LCP ≤2.5s, CLS ≤0.1, FID ≤100ms

### Fresh Context (21-23)
21. **ULTRATHINK GATE** — Complex tasks → full analysis ≥500 words
22. **CONTEXT HEALTH v2.1** — 🟢 Fresh (0-30%) | 🟡 Loaded (30-50%) | 🟠 Attention (50-70%) | 🔴 Heavy (70-85%) | 💀 Critical (>85%)
23. **GSD CYCLE** — Discuss → Plan → Execute → Verify

### Subagent & Memory (24-26)
24. **VERIFICATION GATE** — Evidence before claims. Anti-rationalization
25. **SUBAGENT ORCHESTRATION** — 2-stage review + model selection
26. **BIOMIMETIC MEMORY** — world | experience | mental_model

## 🧠 Memory Architecture (4-Layer)

```
┌───────────────────────────────────────────────┐
│  A — RULES         GEMINI.md + STATE.md       │
├───────────────────────────────────────────────┤
│  B — CRITICAL      LESSONS.md (≤10, ≥0.8)    │
├───────────────────────────────────────────────┤
│  C — SEMANTIC      Qdrant + 3-Strategy Recall │
├───────────────────────────────────────────────┤
│  D — AUTO-MEMORY   .ai/memory/MEMORY.md       │
└───────────────────────────────────────────────┘

3 Memory Types: world (facts) | experience (debug/build) | mental_model (patterns)
3-Strategy Recall: semantic + keyword + temporal → merge top-5
```

> 📂 Chi tiết: `session/references/memory-architecture.md`

## 📋 Cheat Sheet

```
Bắt đầu phiên?           → /start [task]
Feature lớn?              → /gsd [feature]       (Discuss→Plan→Execute→Verify)
Viết code?                → /build [task]        🔥 TDD + Verification Report
Gặp bug?                  → /fix [bug]           🐛 Hypothesis-Driven Debug
Design UI?                → /craft [task]        🎨 Tokens + WCAG + /e2e
Chuẩn bị deploy?          → /ship [env]          🔒 Production Readiness
Ghi bài học?              → /learn [observation]  🧠 Ingest + Tag
Audit skill health?       → /skill-audit         📋 4-Phase Stocktake
Tổng hợp insights?       → /consolidate          🧠 Sleep-Brain Pass
Kết thúc phiên?           → /save                 (Verification Gate + /consolidate)
```

## 📂 Directory Structure

```
skill/
├── GEMINI.md              # 26 Global Rules (v5.2, token-optimized)
├── AGENTS.md              # Agent instructions
├── LESSONS.md             # Critical lessons (≤10, ≥0.8)
├── CHANGE_LOG.md          # Timeline changes
├── README.md              # This file
├── session/               # /start /save /checkpoint /review /recall
│   ├── SKILL.md           # v5.2 — Compaction Decision Guide
│   └── references/        # context-management, quality-gates, memory-architecture
├── build/                 # /build /plan /search /gsd
│   ├── SKILL.md           # v5.2 — 8-Step + Verification Report + Context Health v2.1
│   └── references/        # patterns, tdd, parallel-guide, subagent-prompts
├── fix/                   # /fix
│   ├── SKILL.md           # v5.2 — 4-Phase + Hypothesis-Driven Debug
│   └── references/        # patterns, lessons-template
├── craft/                 # /craft /audit /tokens /e2e
│   ├── SKILL.md
│   └── references/        # patterns, design-tokens, wcag, perf-targets
├── secure/                # /security /harden /ship
│   ├── SKILL.md
│   └── references/        # owasp, security-headers, ci-templates
├── automate/              # /n8n /integrate /mcp
│   ├── SKILL.md
│   └── references/        # api-design, n8n-patterns
├── content/               # /seo /article /brief /audit-content
│   ├── SKILL.md
│   └── references/        # seo-checklist, content-engine
├── spec/                  # /spec /handoff /adr /runbook /apidoc /componentdoc
│   ├── SKILL.md
│   └── references/        # templates (adr, api, architecture, handoff...)
├── learn/                 # /learn /instinct /evolve /consolidate /skill-audit
│   ├── SKILL.md           # v5.2 — /skill-audit command
│   └── references/        # instinct-format, review-perspectives
└── templates/             # File templates (ACTIVE_CONTEXT, INSIGHTS...)
```

## 📝 Research Sources

| Version | Source | Contribution |
|---|---|---|
| v5.2 | [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) (78k⭐) | Verification Report, skill-stocktake, strategic-compact |
| v5.2 | [FlorianBruniaux/claude-code-ultimate-guide](https://github.com/FlorianBruniaux/claude-code-ultimate-guide) | Context pressure thresholds (ACM 2025), Golden Rules |
| v5.2 | [shanraisshan/claude-code-best-practice](https://github.com/shanraisshan/claude-code-best-practice) | RPI workflow, development patterns |
| v5.0 | [NeoLabHQ/context-engineering-kit](https://github.com/NeoLabHQ/context-engineering-kit) | Reflexion loops, context degradation |
| v4.2 | [vectorize-io/hindsight](https://github.com/vectorize-io/hindsight) | Biomimetic memory (world/experience/mental_model) |
| v4.1 | [obra/superpowers](https://github.com/obra/superpowers) | Verification gate, anti-rationalization |
| v4.0 | [GSD2](https://github.com/jlowin/gsd2) (23k⭐) | Get Shit Done cycle, Ultrathink |
| v1.0 | ECC methodology | Foundation patterns |

## 📄 License

MIT
