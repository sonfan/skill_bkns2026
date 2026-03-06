# Cấu trúc thư mục repo chuẩn BKNS

> **Mọi repo BKNS phải tuân thủ cấu trúc này.**
> Files đánh dấu ⭐ là BẮT BUỘC cho mọi dự án.

```
repo/
├── README.md            ⭐ Overview + Quick Start + Owner
├── SPEC.md              ⭐ Yêu cầu nghiệp vụ
├── CHANGELOG.md         ⭐ Timeline thay đổi (Keep a Changelog)
├── DEPLOYMENT.md        ⭐ Cách deploy, rollback, env vars
├── PROJECT-META.md      ⭐ Owner, backup, status, URLs
├── .env.example         ⭐ Biến môi trường mẫu (KHÔNG chứa secret)
├── .gitignore           ⭐ Git ignore rules
│
├── GEMINI.md            ← AI brain (nếu dùng Skill System)
├── LESSONS.md           ← Bug journal (nếu dùng Skill System)
├── NEXT-TODO.md         ← Task backlog (nếu dùng Skill System)
│
├── docs/                ← Tài liệu chi tiết
│   ├── architecture.md  ← Kiến trúc tổng quan, data flow
│   ├── api.md           ← API endpoints, request/response
│   ├── deployment.md    ← Chi tiết deploy (mở rộng DEPLOYMENT.md)
│   ├── test-cases.md    ← Các case test quan trọng
│   └── decisions.md     ← Quyết định kỹ thuật (ADR)
│
├── src/                 ← Mã nguồn chính
├── tests/               ← Unit, integration, e2e tests
├── scripts/             ← Migration, backup, helper scripts
├── docker/              ← Dockerfile, compose, config
├── config/              ← Config files tham chiếu
├── ci/                  ← CI/CD workflows
│
├── changes/             ← Spec-driven development (Skill System)
│   └── <feature>/
│       ├── proposal.md
│       ├── specs/spec.md
│       ├── design.md
│       ├── tasks.md
│       └── delta-specs.md
│
└── archive/             ← Completed changes (Skill System)
```

## Quy ước đặt tên repo BKNS

| Pattern | Dùng khi | Ví dụ |
|---|---|---|
| `bkns-<tên>` | Dự án chung | `bkns-payroll` |
| `bkns-internal-<tên>` | Tool nội bộ | `bkns-internal-abuse-tracker` |
| `bkns-hostbill-<tên>` | Module HostBill | `bkns-hostbill-ipv6-ipam` |
| `bkns-api-<tên>` | API service | `bkns-api-provisioning` |

## Checklist khởi tạo repo mới

- [ ] Tạo repo theo naming chuẩn (`bkns-*`)
- [ ] Tạo `README.md` từ template
- [ ] Tạo `SPEC.md` hoặc import từ template
- [ ] Tạo `DEPLOYMENT.md`
- [ ] Tạo `PROJECT-META.md`
- [ ] Tạo `.env.example`
- [ ] Tạo `.gitignore`
- [ ] Tạo `CHANGELOG.md`
- [ ] Tạo board task trên Jira
- [ ] Gán owner và backup owner
- [ ] Setup branch strategy (main/develop/feature/hotfix)
