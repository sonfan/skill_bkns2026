# ADR — Architecture Decision Records

> Mỗi quyết định kiến trúc quan trọng PHẢI được ghi lại ở đây.
> "6 tháng sau, ADR giải thích tại sao code trông như vậy."
> Template: APEX v6.0 — adapted từ BKNS ADR pattern

---

## Index

| # | Date | Decision | Status |
|---|---|---|---|
| 001 | YYYY-MM-DD | {tên} | Accepted |

> Khi tạo ADR mới: append row vào Index + tạo section mới bên dưới.

---

## Khi nào tạo ADR?

- Thay đổi tech stack (framework, ORM, queue, ...)
- Quyết định architectural pattern quan trọng
- Quyết định ảnh hưởng nhiều tasks
- Lý do từ chối một approach phổ biến
- Trade-off có thể bị quên sau thời gian

---

## ADR-001: {Tiêu đề}

**Date:** YYYY-MM-DD | **Status:** Accepted | **Decider:** {tên}

### Context
{Vấn đề gì? Tại sao cần quyết định?}

### Decision
{Quyết định cụ thể — "Dùng X thay vì Y vì..."}

### Consequences

**Positive:**
- {lợi ích 1}
- {lợi ích 2}

**Negative:**
- {hạn chế 1}
- {hạn chế 2}

### Alternatives Considered

| Option | Pros | Cons | Rejected vì |
|---|---|---|---|
| {option A} | {pros} | {cons} | {lý do} |
| {option B} | {pros} | {cons} | {lý do} |
