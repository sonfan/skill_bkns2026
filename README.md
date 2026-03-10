# AG-SKILL — APEX Skill System v2.0

> 🧠 **AI không bao giờ quên.** Mỗi phiên đều học hỏi và kết nối với quá khứ.

**APEX**: Adaptive Pattern EXtraction — hệ thống skill tối ưu cho AI coding assistant.

## ✨ What's New (APEX v2.0)

- **6-Layer Memory Architecture** — +Ingest Layer (auto-tagging) + Consolidation Layer (cross-memory insights)
- **35 commands** across 9 skills (lên từ 32)
- **New commands**: `/consolidate` (sleep-brain pass), `/cross-link` (manual connections), `/recall` (quick resume)
- **Importance Scoring** — 0.0–1.0 cho mọi LESSONS entry
- **INSIGHTS.md** — compound insights từ memory consolidation
- **Auto-Ingest** — tự động tag Entity/Topic/Importance khi learn
- **Combo Skills** — workflow templates cho common scenarios
- Synthesized from: AG-SKILL v2.0 + Google ADK memory-agent + 12 top GitHub repos

## 📦 9 Skills — 35 Commands

| # | Skill | Commands | Purpose |
|---|---|---|---|
| 1 | **session** | `/start` `/save` `/checkpoint` `/review` `/recall` | 6-Layer Bootstrap + Consolidation Save |
| 2 | **build** ⭐ | `/build` `/plan` `/search` | Search-First + TDD + Memory-Enhanced |
| 3 | **fix** | `/fix` | 4-Phase Debug + Insight Match + Auto-Ingest |
| 4 | **craft** | `/craft` `/audit` `/tokens` `/e2e` | UI + Design Tokens + WCAG + Browser |
| 5 | **secure** | `/security` `/harden` `/ship` | OWASP + Hardening + Production |
| 6 | **automate** | `/n8n` `/integrate` `/mcp` | N8N + API + MCP Tool Design |
| 7 | **content** | `/seo` `/article` `/brief` `/audit-content` | SEO Pipeline + Content Engine |
| 8 | **spec** ⭐ | `/spec` `/handoff` `/adr` `/runbook` `/apidoc` `/componentdoc` | Architecture + Docs |
| 9 | **learn** ⭐ | `/learn` `/instinct` `/evolve` `/review-instincts` `/consolidate` `/cross-link` | Ingest + Consolidation + Evolution |

## 🚀 Install

```bash
# Clone
git clone git@github.com:tampd/skill.git /root/skill

# Symlink vào Antigravity skills directory
for skill in session build fix craft secure automate content spec learn; do
  ln -sfn /root/skill/$skill /root/.gemini/antigravity/skills/$skill
done

# Verify
ls /root/.gemini/antigravity/skills/
```

## 📋 Cheat Sheet

```
Bắt đầu phiên?           → /start [task]
Resume phiên cũ?          → /recall
Viết code?                → /build [task]           🔥 TDD + Search-First
Gặp bug?                  → /fix [bug]              🐛 4-Phase + Auto-Ingest
Design UI?                → /craft [task]           🎨 Tokens + WCAG
Chuẩn bị deploy?          → /ship [env]             🔒 Production Readiness
Ghi bài học?              → /learn [observation]     🧠 Ingest + Tag
Tổng hợp insights?       → /consolidate             🧠 Sleep-Brain Pass
Kết thúc phiên?           → /save                    (auto /consolidate)
```

## 🧠 Memory Architecture (6 Layers)

```
LAYER 0 — INGEST        Auto-tag: Entity + Topic + Importance
LAYER 1 — WORKING       ACTIVE_CONTEXT.md (session temp)
LAYER 2 — SEMANTIC      GEMINI.md + STATE.md (project brain)
LAYER 3 — EPISODIC      LESSONS.md + CHANGELOG.md (append-only)
LAYER 4 — INSTINCT      INSTINCTS.md (patterns + confidence)
LAYER 5 — CONSOLIDATION INSIGHTS.md (cross-memory connections)
```

## 📜 20 Global Rules

| # | Category | Rule |
|---|---|---|
| 1 | Core | Ask when unclear |
| 2 | Core | Read memory first (LESSONS + INSTINCTS + INSIGHTS) |
| 3 | Core | Evidence-based decisions |
| 4 | Core | Self-Reasoning Gate (3-question check) |
| 5 | Core | Search-first |
| 6 | Arch | Spec before code |
| 7 | Arch | Plan-first with task list |
| 8 | Arch | Brainstorm hard gate (≥2 approaches) |
| 9 | Arch | ADR for big decisions |
| 10 | Arch | Wave execution |
| 11 | Code | TDD Iron Law |
| 12 | Code | Quality gate before commit |
| 13 | Code | Cleanup pass |
| 14 | Code | Atomic commits |
| 15 | Verify | Root cause first |
| 16 | Verify | Verification loop |
| 17 | Verify | Instinct validation |
| 18 | Design | WCAG AA |
| 19 | Design | Design tokens mandatory |
| 20 | Design | Performance budget |

## 📝 Sources

- Google ADK `always-on-memory-agent` (Ingest → Consolidate → Cross-Link → Query)
- AG-SKILL v2.0 (9 Skills, 32 Commands, 20 Rules)
- Research: awesome-claude-code, awesome-agent-skills + 10 more GitHub repos
- ECC (Extreme Claude Code) methodology

## 📄 License

MIT
