---
name: bkns
description: BKNS code reference — thư viện hàm theo từng module. Khi code bất kỳ task nào, AI PHẢI kiểm tra module tương ứng trong bkns/includes/modules/ để xem các hàm đã có, tránh viết trùng, và tuân theo pattern hiện tại. Triggers on "domain", "hosting", "payment", "fraud", "notification", "site", "bkns", "đăng ký", "thanh toán", "tên miền", "gian lận", "thông báo".
---

# BKNS Code Reference — Module Functions Library

> 📚 **Thư viện hàm BKNS** — Tổ chức theo module. AI PHẢI đọc trước khi code.

## 🔑 QUY TẮC BẮT BUỘC

**Trước khi viết code cho bất kỳ task nào:**

1. **XÁC ĐỊNH MODULE** — Task thuộc module nào? (Domain / Fraud / Hosting / Notification / Other / Payment / Site)
2. **ĐỌC MODULE** — Mở `bkns/includes/modules/{Module}/` → đọc các file hàm đã có
3. **KIỂM TRA TRÙNG** — Hàm cần viết đã tồn tại chưa? Có hàm tương tự có thể reuse không?
4. **TUÂN THEO PATTERN** — Code theo đúng pattern, naming convention của module đó
5. **CẬP NHẬT MODULE** — Sau khi code xong, ghi lại hàm mới vào module tương ứng

## 📂 Cấu trúc

```
bkns/includes/modules/
├── Domain/          # Tên miền: đăng ký, gia hạn, DNS, WHOIS
├── Fraud/           # Gian lận: phát hiện, blacklist, scoring
├── Hosting/         # Hosting: tạo/quản lý account, backup
├── Notification/    # Thông báo: email, SMS, webhook
├── Other/           # Hàm chung, utilities
├── Payment/         # Thanh toán: invoice, refund, gateway
└── Site/            # Website: template, settings, users
```

## 🏷️ Naming Convention

```php
// Tên hàm: bkns_{module}_{action}()
bkns_domain_register()
bkns_payment_create_invoice()
bkns_hosting_create_account()
bkns_fraud_check_ip()
bkns_notification_send_email()
bkns_site_update_settings()
```

## 🔄 Workflow khi code

```
1. User giao task → AI xác định module liên quan
2. AI đọc bkns/includes/modules/{Module}/ → biết hàm đã có
3. AI code → reuse hàm có sẵn, bổ sung hàm mới nếu cần
4. AI cập nhật module → ghi lại hàm mới vào đúng module
```

## 📋 Module Mapping

| Keyword trong task | Module |
|---|---|
| domain, tên miền, DNS, WHOIS, đăng ký miền, gia hạn miền | Domain |
| fraud, gian lận, blacklist, chống giả mạo | Fraud |
| hosting, cpanel, directadmin, server, backup | Hosting |
| email, SMS, thông báo, notify, webhook, alert | Notification |
| utility, helper, chung, misc | Other |
| thanh toán, payment, invoice, hóa đơn, refund, VNPay, MoMo | Payment |
| site, website, template, giao diện, settings, user | Site |
