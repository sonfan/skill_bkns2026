# GEMINI.md — {PROJECT_NAME}

> Đọc file này trước mọi task. Đây là "bộ nhớ dự án" cho Antigravity.
> Template: APEX v6.0 — adapted từ BKNS Scaffold Guide

---

## 1. Project

**{project-name}** — {1-2 câu mô tả, URL nếu có, vai trò trong hệ thống}.

## 2. Tech stack & phiên bản

| Component | Version | EOL |
|---|---|---|
| Node.js | 24 LTS | Apr 2028 |
| {Framework} | {version} | {EOL} |
| TypeScript | ~5.8.0 | Rolling |
| {Database} | {version} | {EOL} |
| {Cache/Queue} | {version} | {EOL} |
| Docker base | node:24-alpine | Apr 2028 |
| OS (prod) | Ubuntu 24.04 LTS | Apr 2029 |

## 3. Skills & Commands thường dùng

| Khi cần... | Dùng |
|---|---|
| Viết code mới | `/build [task]` |
| Fix bug | `/fix [bug]` |
| Design UI | `/craft [task]` |
| Xem tiến độ | `/status` |
| Deploy | `/ship [env]` |
| Security audit | `/security [target]` |

## 4. File Lookup — Khi X → đọc Y

| Khi cần... | Đọc file |
|---|---|
| Kiến trúc, tech stack | `GEMINI.md` (file này) |
| Coding conventions | `CONVENTIONS.md` |
| Security rules | `docs/SECURITY-SPEC.md` |
| Tiến độ hiện tại | `PROGRESS.md` |
| Bài học, bugs cũ | `LESSONS.md` |
| Lịch sử thay đổi | `CHANGELOG.md` |
| API endpoints | `docs/API-CONTRACT.md` |
| Database schema | `docs/DATABASE-SCHEMA.md` |
| Deploy, rollback | `DEPLOYMENT.md` |
| Quyết định kiến trúc | `docs/adr/000-index.md` |

## 5. Cấu trúc thư mục

```
{project-name}/
├── src/
│   └── {fill in}
├── tests/
├── scripts/
├── docs/
│   ├── SECURITY-SPEC.md       ← MANDATORY — đọc trước khi code
│   ├── API-CONTRACT.md        ← Endpoints, request/response
│   ├── DATABASE-SCHEMA.md     ← Schema, migrations
│   └── adr/                   ← Architecture Decision Records
│       └── 000-index.md
├── GEMINI.md                  ← File này — AI brain
├── CONVENTIONS.md             ← Coding standards
├── PROGRESS.md                ← Tiến độ + session memory
├── LESSONS.md                 ← Bug journal
├── CHANGELOG.md               ← Timeline thay đổi
├── DEPLOYMENT.md              ← Deploy, rollback, env vars
├── README.md                  ← Overview + Quick Start
├── .env.example               ← Env vars mẫu (KHÔNG chứa secret)
└── .gitignore
```

## 6. Conventions — PHẢI TUÂN THỦ

> Chi tiết: xem `CONVENTIONS.md`. Dưới đây là tóm tắt.

1. **Conventional Commits.** `feat({scope}):`, `fix({scope}):`, `chore({scope}):`
2. **Branch naming.** `feature/{desc}`, `fix/{desc}`, `hotfix/{desc}`
3. **Không commit secret/credential.** Dùng `.env` + `.env.example`.
4. **TDD khi feature phức tạp.** RED → GREEN → REFACTOR.
5. {thêm quy tắc đặc thù của project}

## 7. Dev setup

```bash
# Cài dependencies
npm install

# Chạy dev server
npm run dev

# Chạy tests
npm test

# Build production
npm run build
```

## 8. Secrets — KHÔNG BAO GIỜ COMMIT

```
{DATABASE_URL}
{JWT_SECRET}
{API_KEY_XXX}
{thêm env vars nhạy cảm...}
```

> Mọi secret lưu trong `.env`. File `.env.example` chỉ chứa key names, KHÔNG có values.

## 9. Memory files

| File | Mục đích | Khi nào đọc |
|---|---|---|
| `PROGRESS.md` | Session memory — tiến độ, blockers | Đầu + cuối mỗi session |
| `LESSONS.md` | Bug journal — bài học critical | Đầu session |
| `CHANGELOG.md` | Timeline thay đổi | Khi cần lịch sử |
| `.ai/memory/MEMORY.md` | AI auto-notes | AI tự quyết |
