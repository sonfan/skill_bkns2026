# Agent Instructions

This project uses **bd** (beads) for issue tracking. Run `bd onboard` to get started.

## Quick Reference

```bash
bd ready              # Find available work
bd show <id>          # View issue details
bd update <id> --claim  # Claim work atomically
bd close <id>         # Complete work
bd sync               # Sync with git
```

## Non-Interactive Shell Commands

**ALWAYS use non-interactive flags** with file operations to avoid hanging on confirmation prompts.

```bash
cp -f source dest           # NOT: cp source dest
mv -f source dest           # NOT: mv source dest
rm -f file                  # NOT: rm file
rm -rf directory            # NOT: rm -r directory
```

## APEX Skill System v2.0 Core Rules

**MANDATORY** for all AI agents working on this project:

1. **Self-Reasoning Gate (Rule 4)**: 3-Question Self-Check before EVERY execution — best approach? hidden risks? user approval needed?
2. **TDD Iron Law (Rule 11)**: Write tests BEFORE code. RED → GREEN → REFACTOR → COMMIT.
3. **Brainstorming Hard Gate (Rule 8)**: `/plan` MUST propose ≥2 approaches BEFORE creating specs.
4. **Root Cause First (Rule 15)**: `/fix` MUST complete Phase 1 (Root Cause) BEFORE fixing.
5. **Atomic Commits (Rule 14)**: 1 task = 1 commit. Conventional format: `feat|fix|chore(scope): mô tả`
6. **WCAG AA (Rule 18)**: All user-facing pages MUST meet WCAG 2.2 AA.
7. **Design Tokens (Rule 19)**: No hardcoded colors/fonts/spacing — use semantic tokens.
8. **Performance Budget (Rule 20)**: LCP ≤2.5s, CLS ≤0.1, FID ≤100ms.

### 9 Skills — 35 Commands (APEX v2.0)

| Category | Skills |
|---|---|
| **Core** | session (`/start` `/save` `/checkpoint` `/review` `/recall`), build ⭐ (`/build` `/plan` `/search`), fix (`/fix`) |
| **Design** | craft (`/craft` `/audit` `/tokens` `/e2e`) |
| **Ops** | secure (`/security` `/harden` `/ship`), automate (`/n8n` `/integrate` `/mcp`) |
| **Content** | content (`/seo` `/article` `/brief` `/audit-content`), spec ⭐ (`/spec` `/handoff` `/adr` `/runbook` `/apidoc` `/componentdoc`) |
| **Learning** | learn ⭐ (`/learn` `/instinct` `/evolve` `/review-instincts` `/consolidate` `/cross-link`) |

See `GEMINI.md` for full rules and individual `*/SKILL.md` for workflows.

<!-- BEGIN BEADS INTEGRATION -->
## Issue Tracking with bd (beads)

- ✅ Use bd for ALL task tracking
- ✅ Use `--json` flag for programmatic use
- ✅ Link discovered work with `discovered-from` dependencies
- ❌ Do NOT create markdown TODO lists
- ❌ Do NOT duplicate tracking systems

## Landing the Plane (Session Completion)

**MANDATORY WORKFLOW:**
1. File issues for remaining work
2. Run quality gates (if code changed)
3. Update issue status
4. **PUSH TO REMOTE** — MANDATORY: `git push`
5. Verify — all changes committed AND pushed

**CRITICAL**: Work is NOT complete until `git push` succeeds.
<!-- END BEADS INTEGRATION -->
