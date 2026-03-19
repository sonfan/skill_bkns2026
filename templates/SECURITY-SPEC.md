# SECURITY-SPEC.md — {PROJECT_NAME}

> **Version:** 1.0 | **Date:** {YYYY-MM-DD}
> **Rule:** Mọi session PHẢI đọc file này trước khi viết bất kỳ dòng code nào.
> **Đây là file ĐÓNG BĂNG** — chỉ sửa trong planning session, không sửa trong feature branch.
> Template: APEX v6.0 — adapted từ BKNS SECURITY-SPEC pattern

---

## §1 Primary Security Concerns

{Mô tả các mối lo bảo mật chính của dự án}

- **{Concern 1}:** {mô tả + quy tắc}
- **{Concern 2}:** {mô tả + quy tắc}

### Examples

```{language}
// ❌ KHÔNG BAO GIỜ
{anti-pattern code}

// ✅ ĐÚNG CÁCH
{correct pattern code}
```

---

## §2 Startup Validation

App PHẢI crash ngay nếu:
- {condition 1 — e.g., missing critical env var}
- {condition 2 — e.g., DB connection failed}
- {condition 3 — e.g., invalid SSL certificate}

```{language}
// Startup check pattern
{code ví dụ}
```

---

## §3 Response Safety

- **KHÔNG BAO GIỜ** trả về stack trace trong production response
- **KHÔNG BAO GIỜ** trả về internal error messages cho client
- **LUÔN** trả về generic error message + error code
- **LUÔN** log full error vào server-side logging

```{language}
// Response safety pattern
{code ví dụ}
```

---

## §4 Authentication & Authorization

- **Auth method:** {e.g., JWT Bearer token / Session / API Key}
- **Token storage:** {e.g., httpOnly cookie / Authorization header}
- **Token expiry:** {e.g., access: 15min, refresh: 7 days}
- **Protected routes:** {e.g., tất cả /api/* trừ /api/auth/login}

### RBAC Matrix (nếu có)

| Endpoint | Admin | User | Guest |
|---|---|---|---|
| {endpoint} | ✅ | ✅ | ❌ |

---

## §5 Data Protection

| Dữ liệu | Cách bảo vệ |
|---|---|
| Passwords | bcrypt/argon2, NEVER plaintext |
| API keys | Hash (SHA-256) in DB, full value ONLY in .env |
| PII | {encryption/masking method} |
| Logs | NEVER log credentials, tokens, PII |

---

## §6 Project-Specific Security Rules

{Ghi các quy tắc bảo mật đặc thù của dự án}

1. {rule 1}
2. {rule 2}
3. {rule 3}

---

## §7 Pre-deploy Security Checklist

```bash
# 1. Check dependencies
npm audit --production
# 2. Check for hardcoded secrets
grep -rn "password\|secret\|api_key\|token" src/ --include="*.ts" --include="*.js"
# 3. Check .env.example has NO real values
cat .env.example
# 4. Verify CORS config
grep -rn "cors\|CORS" src/ --include="*.ts"
# 5. Verify rate limiting
grep -rn "rate\|throttle\|limit" src/ --include="*.ts"
# 6. Run security tests
npm run test:security  # nếu có
```

> ⚠️ KHÔNG deploy nếu bất kỳ bước nào FAIL.
