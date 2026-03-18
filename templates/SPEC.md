# QUY CHUẨN VIẾT SPEC — BKNS Unified Standard v6.2.1

> **Nguyên tắc**: Không có SPEC = Không được code. Mọi SPEC dùng CÙNG cấu trúc section.
> **Template**: BKNS Dev Operating System Pack v2 — Chuẩn hóa 2026-03-06

---

## HỆ THỐNG SPEC 3 TẦNG

| Tầng | Khi nào dùng | Sections | Vị trí file |
|---|---|---|---|
| **FULL SPEC** | Dự án mới / Module lớn | 19 sections (tất cả ⭐) | `SPEC.md` ở root repo |
| **FEATURE SPEC** | Feature ≥ 3 files | 10 sections bắt buộc + optional | `changes/<feature>/SPEC.md` |
| **MINI-SPEC** | Task nhỏ ≤ 2 files | Bảng 10 dòng | Inline trong task hoặc NEXT-TODO |

### Quy tắc chọn tầng:
```
Task chỉ sửa 1-2 files, không thay đổi logic?     → MINI-SPEC
Feature mới 3+ files hoặc thay đổi logic lớn?      → FEATURE SPEC
Dự án mới hoàn toàn hoặc module core?               → FULL SPEC
```

### Tính kế thừa:
```
MINI-SPEC ⊂ FEATURE SPEC ⊂ FULL SPEC
     ↓              ↓              ↓
  10 rows      same sections   all 19 sections
              (subset of 19)   
```
> Feature SPEC dùng CÙNG số section với Full SPEC → merge trực tiếp khi archive.

---

# ═══════════════════════════════════════════════════
# TẦNG 1 — FULL SPEC (19 sections)
# Dùng cho: Dự án mới / Module lớn / SPEC.md root
# ═══════════════════════════════════════════════════

```markdown
# SPEC — [Tên dự án]

> **Mục đích**: Tài liệu yêu cầu nghiệp vụ. Không có SPEC = Không được code.
> **Version**: v1.0 | **Updated**: YYYY-MM-DD

---

## 1. Thông tin chung

| Trường | Giá trị |
|---|---|
| Tên dự án / tính năng | [tên] |
| Mã dự án / mã task | [PROJ-XXX / TASK-XXX] |
| Người yêu cầu | [tên + vai trò] |
| Người phụ trách | [tên dev] |
| Backup owner | [tên dev backup] |
| Ngày tạo | YYYY-MM-DD |
| Phiên bản SPEC | v1.0 |
| Mức ưu tiên | `P0 Critical` / `P1 High` / `P2 Medium` / `P3 Low` |
| Trạng thái | `Draft` → `Reviewing` → `Approved` → `In Progress` → `Done` |
| Link Jira | [URL] |

## 2. Bối cảnh và vấn đề

Trả lời RÕ RÀNG 4 câu hỏi:

1. **Hiện tại đang có vấn đề gì?**
   [Mô tả tình trạng hiện tại — cụ thể, không chung chung]

2. **Vấn đề ảnh hưởng tới ai?**
   [End user / Internal team / Hệ thống nào?]

3. **Mức độ nghiêm trọng ra sao?**
   [Tần suất xảy ra × Mức ảnh hưởng = Priority]

4. **Nếu KHÔNG làm thì hậu quả là gì?**
   [Business impact cụ thể: mất doanh thu? mất khách? rủi ro pháp lý?]

## 3. Mục tiêu

- **Mục tiêu chính**: [1 câu duy nhất — measurable]
- **Mục tiêu phụ**: [nếu có]
- **Kết quả mong muốn sau khi hoàn thành**: [trạng thái cuối cùng]

## 4. Phạm vi triển khai

### 4.1. In scope — SẼ LÀM
- [Liệt kê cụ thể từng đầu mục]

### 4.2. Out of scope — KHÔNG LÀM (giai đoạn này)
- [Liệt kê rõ ràng để tránh scope creep]

## 5. Người dùng / Đối tượng sử dụng

| Vai trò | Ai | Hành động chính |
|---|---|---|
| Người dùng chính | [tên/nhóm] | [hành động] |
| Người vận hành | [tên/nhóm] | [hành động] |
| Người phê duyệt | [tên/nhóm] | [hành động] |
| Người bị ảnh hưởng | [tên/nhóm] | [ảnh hưởng gì] |

## 6. Mô tả nghiệp vụ / Business Flow

> Mô tả luồng nghiệp vụ theo từng bước. Dùng numbered list hoặc Mermaid diagram.

1. Người dùng thực hiện [hành động] trên [màn hình/API]
2. Hệ thống nhận [dữ liệu đầu vào]
3. Hệ thống xử lý [logic nghiệp vụ]
4. Kết quả trả về [output cho user]
5. Hệ thống ghi log / notify / lưu DB [cách ghi nhận]

## 7. Yêu cầu chức năng

| Mã | Mô tả | Ưu tiên |
|---|---|---|
| FR-01 | [Hệ thống PHẢI ...] | Must |
| FR-02 | [Hệ thống PHẢI ...] | Must |
| FR-03 | [Hệ thống NÊN ...] | Should |

> Format: "Hệ thống PHẢI/NÊN [hành động] KHI [điều kiện] ĐỂ [mục đích]"

## 8. Yêu cầu phi chức năng

| Mã | Loại | Mô tả | Tiêu chí đo |
|---|---|---|---|
| NFR-01 | Hiệu năng | [Yêu cầu] | [response < Xms] |
| NFR-02 | Bảo mật | [Yêu cầu] | [mã hóa AES-256] |
| NFR-03 | Logging | [Yêu cầu] | [format + retention] |
| NFR-04 | Khả năng mở rộng | [Yêu cầu] | [N concurrent users] |

## 9. Dữ liệu đầu vào / đầu ra

### 9.1. Input

| Trường | Kiểu | Bắt buộc | Validation | Ví dụ |
|---|---|---|---|---|
| [field] | string/int/date | Yes/No | [min/max/regex] | [example] |

### 9.2. Output

| Trường | Kiểu | Mô tả |
|---|---|---|
| [field] | [type] | [description] |

### 9.3. Error codes

| Code | HTTP | Mô tả | Khi nào xảy ra |
|---|---|---|---|
| [ERR_001] | 400 | [message] | [condition] |

## 10. Thiết kế dữ liệu

### Bảng mới
| Bảng | Mô tả | Cột chính |
|---|---|---|
| [table_name] | [purpose] | id, [columns...] |

### Bảng sửa đổi
| Bảng | Thay đổi | Migration |
|---|---|---|
| [table_name] | ADD column [name] | [migration file] |

### Quan hệ
- [table_a] → [table_b]: [relationship + FK]

### Index
- [table]([columns]) — [lý do: query pattern]

## 11. Thiết kế API / Integration

| Method | Endpoint | Auth | Request Body | Response | Error |
|---|---|---|---|---|---|
| POST | `/api/v1/[resource]` | Bearer | `{field: type}` | `{field: type}` | 400/401/500 |

### Timeout / Retry
- Timeout: [X]ms
- Retry: [N] lần, backoff [strategy]
- Circuit breaker: [threshold]

### Service phụ thuộc
| Service | Mục đích | SLA |
|---|---|---|
| [service] | [purpose] | [uptime %] |

## 12. UI / Màn hình

| Màn hình | Thay đổi | Mock/Wireframe |
|---|---|---|
| [screen name] | Thêm [element] | [link nếu có] |

### Trạng thái hiển thị
| Trạng thái | Hiển thị | Điều kiện |
|---|---|---|
| Loading | Skeleton/Spinner | Đang fetch data |
| Empty | Empty state message | Không có data |
| Error | Error message + retry | API fail |
| Success | Toast notification | Action thành công |

## 13. Logging / Audit / Monitoring

| Loại | Ghi gì | Ở đâu | Ai xem | Retention |
|---|---|---|---|---|
| Audit log | [actions] | [storage] | [role] | [days] |
| Error log | [errors] | [storage] | [role] | [days] |

### Alerts / Cảnh báo
| Trigger | Kênh | Người nhận |
|---|---|---|
| [condition] | Email/Slack | [role] |

## 14. Bảo mật và phân quyền

### Phân quyền
| Action | Roles cho phép | Điều kiện thêm |
|---|---|---|
| [action] | [admin/user/...] | [additional check] |

### Dữ liệu nhạy cảm
| Dữ liệu | Cách bảo vệ |
|---|---|
| [data type] | [encryption/masking/access control] |

### Rủi ro bảo mật
- [Risk 1]: [mitigation]
- [Risk 2]: [mitigation]

## 15. Rủi ro và điểm cần lưu ý

| # | Rủi ro | Xác suất | Ảnh hưởng | Mitigation |
|---|---|---|---|---|
| R-01 | [risk] | Low/Med/High | Low/Med/High | [plan] |
| R-02 | Ảnh hưởng hệ thống cũ | [prob] | [impact] | [plan] |
| R-03 | Phụ thuộc service ngoài | [prob] | [impact] | [plan] |

## 16. Tiêu chí nghiệm thu

| Mã | Tiêu chí | Cách verify |
|---|---|---|
| AC-01 | [Khi X thì Y phải xảy ra] | [test/curl/screenshot] |
| AC-02 | [Khi A thì B không được xảy ra] | [test/curl/screenshot] |
| AC-03 | [Performance: Z < Nms] | [benchmark/lighthouse] |

> ⚠️ DONE chỉ khi TẤT CẢ AC đều PASS với evidence.

## 17. Kế hoạch triển khai

| Giai đoạn | Môi trường | Thời gian | Điều kiện |
|---|---|---|---|
| Test | Dev/Staging | [date] | AC pass trên dev |
| Deploy | Production | [date] | AC pass trên staging |

### Rollback plan
- Trigger rollback khi: [conditions]
- Cách rollback: [steps]
- Downtime dự kiến: [duration]

## 18. Task breakdown

| # | Task | Owner | Size | Deps | Status |
|---|---|---|---|---|---|
| TASK-01 | [mô tả] | [dev] | S/M/L | — | ⬜ |
| TASK-02 | [mô tả] | [dev] | S/M/L | TASK-01 | ⬜ |
| TASK-03 | [mô tả] | [dev] | S/M/L | — | ⬜ |

> Tasks phải TDD bite-sized (2-5 phút). Xem chi tiết trong `tasks.md`.

## 19. Phụ lục

- Repo: [git URL]
- Jira board: [URL]
- Diagram: [link/inline mermaid]
- Tài liệu tham khảo: [links]
- SPEC version history:
  | Version | Date | Author | Changes |
  |---|---|---|---|
  | v1.0 | YYYY-MM-DD | [name] | Initial draft |
```

---

# ═══════════════════════════════════════════════════
# TẦNG 2 — FEATURE SPEC (10 sections bắt buộc)
# Dùng cho: Feature ≥ 3 files / changes/<feature>/SPEC.md
# ═══════════════════════════════════════════════════

> **Dùng CÙNG số section** với Full SPEC để kế thừa khi archive.
> Sections không liên quan → ghi "N/A" hoặc bỏ qua.

```markdown
# SPEC — [Feature Name]

> **Type**: Feature SPEC | **Parent**: [Project SPEC nếu có]
> **Version**: v1.0 | **Updated**: YYYY-MM-DD
> **Trạng thái**: `Draft` → `Reviewing` → `Approved` → `In Progress` → `Done`

## 1. Thông tin chung

| Trường | Giá trị |
|---|---|
| Tên tính năng | [feature name] |
| Mã task | [TASK-XXX] |
| Người yêu cầu | [ai yêu cầu] |
| Người phụ trách | [dev] |
| Ngày tạo | YYYY-MM-DD |
| Mức ưu tiên | P0/P1/P2/P3 |
| Size | S (1-2 files) / M (3-5 files) / L (6+ files) |
| Breaking changes | Yes / No — [nếu yes, mô tả] |

## 2. Bối cảnh và vấn đề
[Vấn đề gì? Ảnh hưởng ai? Hậu quả nếu không làm?]

## 3. Mục tiêu
- **Mục tiêu**: [1 câu — measurable]
- **Kết quả mong muốn**: [trạng thái cuối]

## 4. Phạm vi
- **In scope**: [liệt kê]
- **Out of scope**: [liệt kê]

## 6. Business Flow
[Numbered steps hoặc mermaid diagram]

## 7. Yêu cầu chức năng
| Mã | Mô tả |
|---|---|
| FR-01 | [requirement] |

## 10. Thiết kế dữ liệu (nếu có DB changes)
[Tables, columns, relations, migrations]

## 11. Thiết kế API (nếu có API changes)
| Method | Endpoint | Request | Response |
|---|---|---|---|

## 15. Rủi ro
| Rủi ro | Mitigation |
|---|---|
| [risk] | [plan] |

## 16. Tiêu chí nghiệm thu
| Mã | Tiêu chí | Verify |
|---|---|---|
| AC-01 | [criteria] | [how] |

## 18. Task breakdown
| # | Task | Size | Status |
|---|---|---|---|
| T-01 | [task] | S/M | ⬜ |

---
### Sections tùy chọn (thêm nếu cần):
- §5 Người dùng — nếu feature ảnh hưởng nhiều roles
- §8 NFR — nếu có yêu cầu performance/security đặc biệt
- §9 Input/Output — nếu có data format phức tạp
- §12 UI — nếu có thay đổi giao diện
- §13 Logging — nếu cần audit trail
- §14 Bảo mật — nếu ảnh hưởng phân quyền
- §17 Triển khai — nếu deploy phức tạp
```

---

# ═══════════════════════════════════════════════════
# TẦNG 3 — MINI-SPEC (10 dòng)
# Dùng cho: Task nhỏ ≤ 2 files / inline
# ═══════════════════════════════════════════════════

```markdown
# MINI-SPEC — [Tên task]

| # | Mục | Nội dung |
|---|---|---|
| 1 | Tên task | [tên rõ ràng] |
| 2 | Vấn đề hiện tại | [mô tả ngắn gọn] |
| 3 | Mục tiêu cần đạt | [1 câu — measurable] |
| 4 | Phạm vi LÀM | [files/modules affected] |
| 5 | Phạm vi KHÔNG LÀM | [explicit exclusions] |
| 6 | Đầu ra cụ thể | [deliverable] |
| 7 | Tiêu chí done | [acceptance criteria] |
| 8 | Cách verify | [test command / curl / screenshot] |
| 9 | Rủi ro | [breaking? regression? performance?] |
| 10 | Ghi chú | [links, LESSONS refs, dependencies] |
```

> **Tương đương `/build` Step 1** (WHY/WHAT/HOW/DONE/TEST/DEPS) nhưng chuẩn hóa format.

---

# QUY TẮC

1. **1 SPEC = 1 scope**: Không trộn nhiều features vào 1 SPEC
2. **Section numbers KHÔNG ĐỔI**: Luôn giữ đúng thứ tự 1-19 để merge được
3. **Sections không dùng**: Ghi "N/A" hoặc bỏ qua (KHÔNG đánh số lại)
4. **SPEC version**: Cập nhật version + date ở header khi sửa nội dung
5. **Trạng thái lifecycle**: Draft → Reviewing → Approved → In Progress → Done
6. **Kế thừa**: Feature SPEC merge vào Full SPEC khi archive (qua delta-specs.md)
7. **Evidence**: AC trong §16 PHẢI có cách verify cụ thể (test/curl/screenshot)
