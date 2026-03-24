# Domain Hooks — HostBill Reference

> 📚 Source: https://hooks.hostbillapp.com/
> 📋 Tổng: **17 hooks** (12 After + 5 Before)

---

## 📊 Tổng quan

| # | Hook | Loại | Mô tả |
|---|------|------|--------|
| 1 | `after_domain_cancellationrequest` | After | Client/admin yêu cầu hủy domain |
| 2 | `after_domaincontactchange` | After | Domain contacts đã được cập nhật |
| 3 | `after_domaindelete` | After | Xóa domain từ registry thành công |
| 4 | `after_domaindelete_failed` | After | Xóa domain từ registry thất bại |
| 5 | `after_domainexpire` | After | Domain đã hết hạn |
| 6 | `after_domainregister` | After | Đăng ký domain thành công |
| 7 | `after_domainregister_failed` | After | Đăng ký domain thất bại |
| 8 | `after_domainrenew` | After | Gia hạn domain thành công |
| 9 | `after_domainrenew_failed` | After | Gia hạn domain thất bại |
| 10 | `after_domainsave` | After | Domain details đã thay đổi |
| 11 | `after_domaintransfer` | After | Transfer domain thành công |
| 12 | `after_domaintransfer_failed` | After | Transfer domain thất bại |
| 13 | `before_domain_contactset` | Before ⚡modifier | Trước khi hiển thị/lưu contact details |
| 14 | `before_domainlookup` | Before | Trước khi check domain availability |
| 15 | `before_domainregister` | Before | Trước khi đăng ký domain |
| 16 | `before_domainrenew` | Before | Trước khi gia hạn domain |
| 17 | `before_domaintransfer` | Before | Trước khi transfer domain |

---

## 🔵 AFTER Hooks

### 1. `after_domain_cancellationrequest`
> Client/admin requested domain cancelation

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `reason` | string | Lý do hủy |
| `type` | string | `End of billing period` hoặc `Immediate` |
| `domain_id` | int | ID domain |

**URL:** https://hooks.hostbillapp.com/domains/after_domain_cancellationrequest.html

---

### 2. `after_domaincontactchange`
> Domain contacts have been updated

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `contacts_before` | array | Contact trước khi đổi |
| `contacts_after` | array | Contact sau khi đổi |

**Nested — `contacts_before` / `contacts_after`:**
| Key | Type |
|-----|------|
| `registrant` | array |
| `tech` | array |
| `admin` | array |
| `billing` | array |

**Nested — mỗi contact type (registrant/tech/admin/billing):**
| Key | Type |
|-----|------|
| `firstname` | string |
| `lastname` | string |
| `companyname` | string |
| `address1` | string |
| `address2` | string |
| `city` | string |
| `state` | string |
| `country` | string |
| `postcode` | string |
| `email` | string |
| `phonenumber` | string |

**URL:** https://hooks.hostbillapp.com/domains/after_domaincontactchange.html

---

### 3. `after_domaindelete`
> HostBill successfully deleted domain from registry

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `name` | string | Tên domain |

**URL:** https://hooks.hostbillapp.com/domains/after_domaindelete.html

---

### 4. `after_domaindelete_failed`
> HostBill failed to delete domain from registry

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `name` | string | Tên domain |

**URL:** https://hooks.hostbillapp.com/domains/after_domaindelete_failed.html

---

### 5. `after_domainexpire`
> HostBill expired domain

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `name` | string | Tên domain |
| `status` | string | Trạng thái domain |

**URL:** https://hooks.hostbillapp.com/domains/after_domainexpire.html

---

### 6. `after_domainregister`
> HostBill successfully registered domain

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `name` | string | Tên domain |

**URL:** https://hooks.hostbillapp.com/domains/after_domainregister.html

---

### 7. `after_domainregister_failed`
> HostBill failed to register domain

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `name` | string | Tên domain |

**URL:** https://hooks.hostbillapp.com/domains/after_domainregister_failed.html

---

### 8. `after_domainrenew`
> HostBill successfully renewed domain

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `name` | string | Tên domain |

**URL:** https://hooks.hostbillapp.com/domains/after_domainrenew.html

---

### 9. `after_domainrenew_failed`
> HostBill failed to renew domain

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `name` | string | Tên domain |

**URL:** https://hooks.hostbillapp.com/domains/after_domainrenew_failed.html

---

### 10. `after_domainsave`
> Domain details have been changed

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `name` | string | Tên domain |
| `period` | int | Thời hạn (năm) |
| `expires` | string | Ngày hết hạn |
| `date_created` | string | Ngày tạo |
| `reg_module` | int | Module đăng ký |
| `firstpayment` | float | Thanh toán lần đầu |
| `status` | string | Trạng thái |
| `recurring_amount` | float | Số tiền gia hạn |
| `nameservers` | array | Danh sách nameservers |
| `epp_code` | string | EPP/Auth code |
| `autorenew` | int | Tự động gia hạn (0/1) |
| `notes` | string | Ghi chú |

**URL:** https://hooks.hostbillapp.com/domains/after_domainsave.html

---

### 11. `after_domaintransfer`
> HostBill successfully transferred domain

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `name` | string | Tên domain |

**URL:** https://hooks.hostbillapp.com/domains/after_domaintransfer.html

---

### 12. `after_domaintransfer_failed`
> HostBill failed to transfer domain

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `name` | string | Tên domain |

**URL:** https://hooks.hostbillapp.com/domains/after_domaintransfer_failed.html

---

## 🟢 BEFORE Hooks

### 13. `before_domain_contactset` ⚡ MODIFIER
> Trước khi hiển thị và lưu contact details cho domain
>
> 💡 **TIP:** `$details` được truyền bằng **reference** — có thể modify giá trị trong Advanced hook

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `domain_id` | int | Domain ID |
| `module_id` | int | Module ID |
| `name` | string | Tên domain |
| `registrant` | array | Thông tin registrant |
| `admin` | array | Thông tin admin contact |
| `billing` | array | Thông tin billing contact |
| `tech` | array | Thông tin tech contact |

**URL:** https://hooks.hostbillapp.com/domains/before_domain_contactset.html

---

### 14. `before_domainlookup`
> Hook triggered before domain will be checked for availability
>
> 💡 **TIP:** Throw exception để đánh dấu domain là unavailable

**Parameters:** Không có parameters cụ thể

**URL:** https://hooks.hostbillapp.com/domains/before_domainlookup.html

---

### 15. `before_domainregister`
> HostBill is about to take an attempt to register domain
>
> ⚠️ Nếu có custom registration fields → parameters có thể khác

**Parameters:**
| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `name` | string | Tên domain |

**URL:** https://hooks.hostbillapp.com/domains/before_domainregister.html

---

### 16. `before_domainrenew`
> Domain is about to be renewed in HostBill
>
> 💡 **TIP:** Throw exception trong hook để block gia hạn

**Parameters (full `hb_domains` table row):**
| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `client_id` | int | Client ID |
| `order_id` | int | Order ID |
| `tld_id` | int | TLD ID |
| `name` | string | Tên domain |
| `server_id` | int | Server ID |
| `reg_module` | int | Module đăng ký |
| `payment_module` | int | Module thanh toán |
| `date_created` | string | Ngày tạo |
| `firstpayment` | float | Thanh toán lần đầu |
| `recurring_amount` | float | Số tiền gia hạn |
| `period` | int | Thời hạn |
| `expires` | string | Ngày hết hạn |
| `type` | string | Loại domain |
| `status` | string | Trạng thái |
| `next_due` | string | Ngày thanh toán tiếp |
| `next_invoice` | string | Hóa đơn tiếp |
| `idprotection` | int | ID Protection (0/1) |
| `nameservers` | string | Nameservers |
| `autorenew` | int | Auto renew (0/1) |
| `reglock` | int | Registry lock (0/1) |
| `manual` | int | Manual (0/1) |
| `premium` | int | Premium domain (0/1) |
| `epp_code` | string | EPP/Auth code |
| `notes` | string | Ghi chú |
| `extended` | string | Extended data |
| `synch_date` | string | Ngày sync cuối |
| `nsips` | string | NS IPs |
| `failed_syncs` | int | Số lần sync thất bại |

**URL:** https://hooks.hostbillapp.com/domains/before_domainrenew.html

---

### 17. `before_domaintransfer`
> Domain is about to be transferred into HostBill
>
> 💡 **TIP:** Throw exception trong hook để block transfer

**Parameters (full `hb_domains` table row):**
*(Giống `before_domainrenew` — full row từ bảng `hb_domains`)*

| Key | Type | Mô tả |
|-----|------|--------|
| `id` | int | Domain ID |
| `client_id` | int | Client ID |
| `order_id` | int | Order ID |
| `tld_id` | int | TLD ID |
| `name` | string | Tên domain |
| `server_id` | int | Server ID |
| `reg_module` | int | Module đăng ký |
| `payment_module` | int | Module thanh toán |
| `date_created` | string | Ngày tạo |
| `firstpayment` | float | Thanh toán lần đầu |
| `recurring_amount` | float | Số tiền gia hạn |
| `period` | int | Thời hạn |
| `expires` | string | Ngày hết hạn |
| `type` | string | Loại domain |
| `status` | string | Trạng thái |
| `next_due` | string | Ngày thanh toán tiếp |
| `next_invoice` | string | Hóa đơn tiếp |
| `idprotection` | int | ID Protection (0/1) |
| `nameservers` | string | Nameservers |
| `autorenew` | int | Auto renew (0/1) |
| `reglock` | int | Registry lock (0/1) |
| `manual` | int | Manual (0/1) |
| `premium` | int | Premium domain (0/1) |
| `epp_code` | string | EPP/Auth code |
| `notes` | string | Ghi chú |
| `extended` | string | Extended data |
| `synch_date` | string | Ngày sync cuối |
| `nsips` | string | NS IPs |
| `failed_syncs` | int | Số lần sync thất bại |

**URL:** https://hooks.hostbillapp.com/domains/before_domaintransfer.html

---

## 🔄 Quick Reference — Hooks by Action

| Action | Before Hook | After (Success) | After (Failed) |
|--------|-------------|-----------------|----------------|
| **Register** | `before_domainregister` | `after_domainregister` | `after_domainregister_failed` |
| **Renew** | `before_domainrenew` | `after_domainrenew` | `after_domainrenew_failed` |
| **Transfer** | `before_domaintransfer` | `after_domaintransfer` | `after_domaintransfer_failed` |
| **Delete** | — | `after_domaindelete` | `after_domaindelete_failed` |
| **Expire** | — | `after_domainexpire` | — |
| **Save** | — | `after_domainsave` | — |
| **Cancel** | — | `after_domain_cancellationrequest` | — |
| **Contact** | `before_domain_contactset` | `after_domaincontactchange` | — |
| **Lookup** | `before_domainlookup` | — | — |
