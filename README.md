# Skill System v6.1 — Memory-First + Self-Reasoning Gate

> 14 Skills Production Code Framework + 5-Layer Memory + AI Self-Check
> Cập nhật: 2026-03-06

## Cài đặt

### Global (áp dụng tất cả projects):
```bash
# Clone repo
git clone git@github.com:tampd/skill.git ~/skill

# Symlink tất cả skills vào Antigravity global
for skill in start build fix save plan memory \
  craft quality ship \
  integrate n8n-pro web-security docs seo; do
  rm -rf ~/.gemini/antigravity/skills/$skill
  ln -s ~/skill/$skill ~/.gemini/antigravity/skills/$skill
done
```

## Có gì mới?

### v6.1 — Self-Reasoning Gate 🆕

AI tự hỏi **3 câu** trước MỌI quyết định thực thi (Rule 13):
- **Q1**: "Phương án tốt nhất chưa?" → ≥2 alternatives
- **Q2**: "Risk/side-effect đang bỏ qua?" → breaking, regression, perf, security
- **Q3**: "User cần approve?" → ≤2 files → tự làm; ≥3 files/risky → hỏi

Embedded trong: `/build` (Step 1.5), `/fix` (Phase 3), `/craft` (Step 2.5), `/plan` (Q2)

### v6.0 — Memory-First Architecture

- 🆕 **craft**: Gộp design + frontend → UI lifecycle (setup/component/css/a11y)
- 🆕 **quality**: Gộp guard + perf + review-website → quality gate (test/a11y/perf/all)
- 🆕 **ship**: Pre-launch checklist + CI/CD + Monitoring + Rollback
- ⬆ **plan**: Gộp brainstorm → Ideation Step 0 + Spec-driven
- ⬆ **memory**: Context Compression Protocol + 3-Tier Load Order
- **Giảm 18→14 skills**: Zero overlap, tiết kiệm context window
- **13 Global Rules**: +WCAG AA, Security Headers, Design Tokens, Perf Budget, Self-Reasoning

### v5.0 — TDD + Spec-Driven

- **build** ⭐: TDD Iron Law (RED→GREEN→REFACTOR) + Spec Compliance Check
- **fix**: 4-Phase Systematic Debug + Root Cause Iron Law
- **plan**: Change Folder (proposal+specs+design+tasks+delta-specs) + Hard Gate
- **save**: 2-Stage Review (Spec + Quality 7 tiêu chí) + Change Archive

### 🧠 5-Layer Memory:

| Layer | Engine | Mục đích |
|---|---|---|
| 1 — Working | `ACTIVE_CONTEXT.md` | Working memory (xóa sau /save) |
| 2 — Semantic | `GEMINI.md`, `STATE.md` | Não bộ dự án |
| 3 — Episodic | `LESSONS.md`, `CHANGE_LOG.md` | Bộ nhớ dài hạn (append-only) |
| 4 — Vector | Qdrant (MCP) | Semantic search cross-session |
| 5 — Task Graph | Beads (CLI) | Dependency-aware task tracking |

## Quick Reference — 14 Skills

```
── Session ──
/start [task]        → Khởi động phiên (14-skill auto-select + Qdrant recall)
/save                → 2-Stage Review + Change Archive + Push        🔥

── Build ──
/build [task]        → TDD: RED→GREEN→REFACTOR + Self-Reasoning      🔥
/fix [bug]           → 4-Phase Systematic Debug + Root Cause          🔥
/plan [feature]      → Change Folder + Brainstorming Hard Gate        🔥

── Web (v6.0 merged) ──
/craft [task]        → UI/UX + Atomic Design + Tokens + WCAG          🆕
/quality [scope]     → Test + A11y + Perf + Lighthouse                🆕
/ship [scope]        → Pre-launch + CI/CD + Monitor                   🆕

── Integration ──
/integrate [svc]     → API + webhook + 3rd-party
/n8n [task]          → N8N + MCP Server + Sub-workflows

── Specialist ──
/security [target]   → OWASP deep audit + CVE + hardening
/docs [scope]        → Documentation + ADR + handoff
/seo [topic]         → SEO + GEO content writer

── Memory ──
/memory              → 5-Layer Memory management
```

## Version History

| Version | Date | Skills | Highlights |
|---|---|---|---|
| **v6.1** 🆕 | 2026-03-06 | 14 skills | **Self-Reasoning Gate** — 3-Question Self-Check before every decision |
| **v6.0** 🔥 | 2026-03-05 | 14 skills | Memory-First, 18→14 skills, craft/quality/ship merged, 13 Global Rules |
| v5.0 | 2026-03-05 | 15 skills | TDD Iron Law, 4-Phase Debug, Change Folder, 2-Stage Review |
| v4.1 | 2026-03-04 | 15 skills | +/memory, Qdrant Layer 4, Beads Layer 5 |
| v4.0 | 2026-03-04 | 14 skills | +/docs, +/seo, Architecture Spec Phase |
| v3.0 | 2026-03-04 | 12 skills | +brainstorm, +n8n-pro, +web-security, +review-website |
| v2.0 | 2026-02-28 | 8 skills | Gộp 26 → 8 unified skills |
| v1.x | 2026-02-27 | 26 skills | Original (archived) |
