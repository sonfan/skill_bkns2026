# BKNS Modules

> Tổ chức code theo từng module chức năng của hệ thống BKNS

## Danh sách Modules

| # | Module | Mô tả |
|---|--------|-------|
| 1 | **Domain** | Đăng ký, gia hạn, quản lý tên miền |
| 2 | **Fraud** | Phát hiện và phòng chống gian lận |
| 3 | **Hosting** | Quản lý dịch vụ hosting |
| 4 | **Notification** | Gửi thông báo (email, SMS, webhook) |
| 5 | **Other** | Các hàm utility / helper chung |
| 6 | **Payment** | Thanh toán, hóa đơn, hoàn tiền |
| 7 | **Site** | Quản lý website, giao diện, settings |

## Quy tắc đặt code

- Mỗi module có thư mục riêng
- File `functions.php` — chứa các hàm chính của module
- File `hooks.php` — chứa các hook handlers
- File `helpers.php` — chứa utility functions
- Đặt tên hàm theo pattern: `bkns_{module}_{action}()`
  - Ví dụ: `bkns_domain_register()`, `bkns_payment_create_invoice()`
