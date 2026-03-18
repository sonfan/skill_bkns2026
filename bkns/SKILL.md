---
name: bkns
description: "BKNS infrastructure & platform knowledge. Use for /bkns-infra (infrastructure patterns), /bkns-deploy (deployment), /bkns-standards (coding standards). Triggers on: bkns, infrastructure, deploy, standards, server, vps, domain."
---

# BKNS Skill — Infrastructure & Platform Knowledge (2026)

> Kiến thức chung về hạ tầng, quy trình, chuẩn code của BKNS.
> 📂 Ném thêm tài liệu vào: `bkns/references/`

---

## /bkns-infra [topic]
> Tra cứu kiến thức hạ tầng BKNS

```
Dùng khi cần biết:
  □ Server architecture & topology
  □ API endpoints nội bộ
  □ Service connections (OpenClaw, S3, Proxy, Backup...)
  □ Database schemas & relationships
  □ Network & DNS architecture

→ Tài liệu chi tiết đặt tại: bkns/references/
```

---

## /bkns-deploy [service]
> Quy trình deploy service BKNS

```
CHECKLIST DEPLOY:
  □ Code review passed
  □ Test on staging
  □ Backup current version
  □ Deploy to production
  □ Verify service health
  □ Monitor logs 15 phút
  □ Rollback plan ready
```

---

## /bkns-standards [scope]
> Chuẩn coding & naming conventions BKNS

```
QUY ƯỚC:
  □ PHP: PSR-12
  □ Naming: snake_case cho files, camelCase cho methods
  □ Git: conventional commits (feat|fix|chore)
  □ Template: Smarty (.tpl)
  □ CSS: BEM methodology + namespace .bkns-*
```

---

## 📂 REFERENCES — Ném tài liệu vào đây

```
bkns/references/
├── (đặt tài liệu hạ tầng tại đây)
├── (API docs, server configs, etc.)
└── (AI sẽ tự đọc khi cần)
```

> **Tip**: Mỗi file .md trong `references/` sẽ được AI tự động tìm và đọc khi liên quan.
