---
name: hostbill
description: "HostBill platform development. Use for /hb-module (create/edit hosting modules), /hb-widget (create/edit widgets), /hb-template (Smarty templates), /hb-hook (hooks & events), /hb-api (HostBill API). Triggers on: hostbill, module, widget, template, tpl, hook, hosting module."
---

# HostBill Skill — Platform Development (BKNS 2026)

> Chuyên biệt cho phát triển HostBill: modules, widgets, templates, hooks, API.
> 📂 References: `hostbill/references/`

---

## /hb-module [module-name]
> Tạo hoặc chỉnh sửa Hosting Module

```
BƯỚC 1 — RESEARCH
  □ Kiểm tra module đã tồn tại chưa:
    includes/modules/Hosting/[module-name]/
  □ Tìm module tương tự làm reference:
    grep -r "class.*extends HostingModule" includes/modules/Hosting/
  □ Check LESSONS.md: có lesson liên quan module này?

BƯỚC 2 — STRUCTURE
  Hosting module bắt buộc có:
  ├── class.[module-name].php    # Main class extends HostingModule
  ├── widgets/                   # Widget directory
  │   └── [widget-name]/
  │       └── default.tpl        # Smarty template
  └── assets/                    # CSS, JS, images (optional)

BƯỚC 3 — CLASS SKELETON
  □ Class PHẢI extend HostingModule hoặc parent phù hợp
  □ Implement required methods:
    - connect() — kết nối API bên thứ 3
    - testConnection() — verify kết nối
    - Create/Suspend/Unsuspend/Terminate
    - getDetails() — thông tin account
  □ Server config fields (getConfigOptions)
  □ Package config fields (getPackageOptions)

BƯỚC 4 — WIDGET INTEGRATION
  □ Nếu cần widget → chạy /hb-widget
  □ Register widget trong class chính
  □ Pass data từ module → widget qua Smarty assign

BƯỚC 5 — VERIFY
  □ Module load được trong Admin Panel?
  □ Connection test pass?
  □ Provisioning flow: Create → Suspend → Unsuspend → Terminate
  □ Widget render đúng?
```

---

## /hb-widget [widget-name]
> Tạo hoặc chỉnh sửa Widget cho module

```
BƯỚC 1 — LOCATE
  □ Widget nằm tại:
    includes/modules/Hosting/[module]/widgets/[widget-name]/default.tpl
  □ CSS chung tại:
    includes/modules/Hosting/[module]/assets/widgets.css
  □ Check widget hiện có: ls widgets/

BƯỚC 2 — TEMPLATE RULES (Smarty)
  □ Dùng Smarty syntax: {$variable}, {if}, {foreach}
  □ KHÔNG inline CSS → tách vào widgets.css
  □ KHÔNG inline JS quá 20 dòng → tách file .js riêng
  □ Biến Smarty từ module: {$data.*}, {$account.*}
  □ HostBill built-in: {$lng.*} (language), {$currency}

BƯỚC 3 — DESIGN STANDARDS
  □ Dùng HostBill CSS framework classes có sẵn:
    - .panel, .panel-heading, .panel-body
    - .table, .table-striped
    - .btn, .btn-primary, .btn-success
    - .label, .label-success, .label-danger
    - .row, .col-md-*, .col-sm-*
  □ Custom CSS phải namespace: .hb-[module]-[widget] { }
  □ Responsive: test xs, sm, md, lg
  □ Dark mode compatible (nếu theme hỗ trợ)

BƯỚC 4 — DATA PASSING
  □ Trong class PHP module:
    $this->assign('variable_name', $value);
  □ Trong template:
    {$variable_name}
  □ Array/Object:
    {foreach from=$items item=row}
      {$row.field}
    {/foreach}

BƯỚC 5 — VERIFY
  □ Widget hiển thị đúng vị trí (sidebar/content)?
  □ Data binding chính xác?
  □ CSS không conflict với theme?
  □ Responsive OK trên mobile?
```

---

## /hb-template [template-path]
> Chỉnh sửa Smarty template (.tpl files)

```
BƯỚC 1 — LOCATE TEMPLATE
  □ Client area: templates/2019/*.tpl
  □ Module widgets: includes/modules/Hosting/[module]/widgets/
  □ Cart: templates/2019/cart.tpl
  □ Admin: includes/modules/[type]/[module]/admin*.tpl

BƯỚC 2 — SMARTY CONVENTIONS
  □ Variables: {$var}
  □ Modifiers: {$var|escape:'html'}, {$var|date_format:"%Y-%m-%d"}
  □ Conditions: {if $var == 'value'}...{/if}
  □ Loops: {foreach from=$array item=row}{$row.field}{/foreach}
  □ Includes: {include file="partial.tpl"}
  □ Language: {$lng.key}
  □ URLs: {$PageURL}, {$baseURL}

BƯỚC 3 — QUALITY RULES
  □ KHÔNG mix logic phức tạp trong template → xử lý trong PHP
  □ Escape output: {$userInput|escape:'htmlall'}
  □ i18n: dùng {$lng.*} cho mọi text hiển thị
  □ IIFE cho JS nếu template dùng nhiều lần (tránh conflict)
  □ Unique IDs cho elements nếu template render multiple instances

BƯỚC 4 — VERIFY
  □ Render không lỗi Smarty syntax?
  □ Variables tất cả có data?
  □ HTML valid? (no unclosed tags)
  □ JS events hoạt động?
```

---

## /hb-hook [hook-name]
> Tạo hook / event listener cho HostBill

```
BƯỚC 1 — IDENTIFY EVENT
  □ HostBill events phổ biến:
    - ClientAdd, ClientEdit, ClientDelete
    - AccountCreate, AccountSuspend, AccountTerminate
    - InvoicePaid, InvoiceCreated
    - TicketOpen, TicketReply
  □ Hook file tại: includes/extend/[hook-name].php

BƯỚC 2 — IMPLEMENT
  □ Hook function signature:
    function hookName($params) { ... }
  □ Register trong: includes/extend/
  □ Return array kết quả

BƯỚC 3 — VERIFY
  □ Hook trigger đúng event?
  □ Không ảnh hưởng performance?
  □ Error handling đầy đủ?
  □ Log output để debug?
```

---

## /hb-api [endpoint]
> Phát triển hoặc sử dụng HostBill API

```
BƯỚC 1 — API STRUCTURE
  □ HostBill API base: /admin/api.php
  □ Auth: API ID + API Key
  □ Format: POST with action parameter

BƯỚC 2 — COMMON ACTIONS
  □ Accounts: getAccountDetails, getClientAccounts
  □ Clients: getClientDetails, addClient
  □ Orders: addOrder, getOrderDetails
  □ Invoices: getInvoiceDetails, addPayment
  □ Modules: module custom functions

BƯỚC 3 — TESTING
  □ Dùng Postman collection (nếu có):
    [module]/OpenClaw_Management_API.postman_collection.json
  □ curl test từ command line
  □ Verify response format
```

---

## HOSTBILL ARCHITECTURE QUICK REFERENCE

```
public_html/
├── includes/
│   ├── config.php                    # DB config
│   ├── hostbill.php                  # Core bootstrap
│   ├── modules/
│   │   ├── Hosting/                  # Hosting modules
│   │   │   ├── [module]/
│   │   │   │   ├── class.[module].php
│   │   │   │   ├── widgets/
│   │   │   │   └── assets/
│   │   ├── Domain/                   # Domain modules
│   │   ├── Other/                    # Other modules
│   │   └── Addon/                    # Addon modules
│   ├── extend/                       # Hooks & extensions
│   ├── libs/                         # Libraries
│   └── core/                         # Core classes
├── templates/
│   └── 2019/                         # Client area theme
│       ├── header.tpl
│       ├── footer.tpl
│       ├── clientarea.tpl
│       ├── cart.tpl
│       └── ...
└── admin/                            # Admin panel
```

---

## BKNS CUSTOM MODULES

| Module | Path | Mô tả |
|---|---|---|
| openclaw | `Hosting/openclaw/` | OpenClaw hosting management |
| bkns_backups | `Hosting/bkns_backups/` | BKNS Backup service |
| bkns_proxy | `Hosting/bkns_proxy/` | BKNS Proxy service |
| bkns_s3_storage | `Hosting/bkns_s3_storage/` | BKNS S3 Storage |
| web_nhanh | `Hosting/web_nhanh/` | Web Nhanh hosting |

---

## COMMON PATTERNS & GOTCHAS

```
⚠️ Widget sidebar position:
  - Dùng key 'content-cloud' cho right sidebar trong HostBill
  - KHÔNG dùng 'right' hay 'sidebar' — sẽ không render

⚠️ CSS conflicts:
  - Namespace tất cả custom CSS: .hb-[module]-[widget]
  - KHÔNG override .panel, .btn trực tiếp
  - Tách CSS vào widgets.css, KHÔNG inline trong .tpl

⚠️ Template multiple instances:
  - Dùng IIFE cho JavaScript
  - Unique IDs: sử dụng {$doms.name} hoặc {$id} suffix
  - Event delegation thay vì direct binding

⚠️ Module class naming:
  - File: class.[module].php
  - Class: [Module] extends HostingModule
  - PHẢI match với directory name
```
