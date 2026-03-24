# Domain Module

> Các hàm xử lý liên quan đến tên miền (Domain) trong HostBill

## 📚 Reference Files

| File | Nội dung |
|------|----------|
| [hooks.md](hooks.md) | 17 Domain hooks (12 After + 5 Before) — full parameters |

## Chức năng
- Đăng ký tên miền (Register)
- Gia hạn tên miền (Renew)
- Chuyển đổi tên miền (Transfer)
- Xóa tên miền (Delete)
- Quản lý DNS / Nameservers
- Cập nhật thông tin WHOIS / Contacts
- Domain availability lookup
- Xử lý hủy domain (Cancellation)

## 17 Hooks Available

### After Hooks (12)
| Hook | Trigger |
|------|---------|
| `after_domain_cancellationrequest` | Yêu cầu hủy domain |
| `after_domaincontactchange` | Contacts đã cập nhật |
| `after_domaindelete` | Xóa domain thành công |
| `after_domaindelete_failed` | Xóa domain thất bại |
| `after_domainexpire` | Domain hết hạn |
| `after_domainregister` | Đăng ký thành công |
| `after_domainregister_failed` | Đăng ký thất bại |
| `after_domainrenew` | Gia hạn thành công |
| `after_domainrenew_failed` | Gia hạn thất bại |
| `after_domainsave` | Domain details thay đổi |
| `after_domaintransfer` | Transfer thành công |
| `after_domaintransfer_failed` | Transfer thất bại |

### Before Hooks (5)
| Hook | Trigger |
|------|---------|
| `before_domain_contactset` ⚡ | Trước khi hiển thị/lưu contacts (modifier) |
| `before_domainlookup` | Trước khi check availability |
| `before_domainregister` | Trước khi đăng ký |
| `before_domainrenew` | Trước khi gia hạn |
| `before_domaintransfer` | Trước khi transfer |

> 📖 Chi tiết parameters → xem [hooks.md](hooks.md)
