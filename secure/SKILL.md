---
name: secure
description: Security audit and production deployment. Use for /security (OWASP audit), /ship (pre-deploy checklist), /harden (security hardening). Triggers on "security", "bảo mật", "deploy", "production", "OWASP", "ship", "hardening", "vulnerability", "lỗ hổng".
---

# Secure Skill — OWASP + Runtime Monitoring + Production Readiness (v7.0)

## /security [target]
> OWASP Top 10 audit + security hardening

```
OWASP TOP 10 CHECKLIST:

A01 — BROKEN ACCESS CONTROL
  □ Authentication required cho mọi protected route
  □ Authorization check: user chỉ access data của mình
  □ Admin endpoints protected (không chỉ hide ở UI)
  □ IDOR prevention: không expose sequential IDs trực tiếp
  □ JWT/session validation đúng

A02 — CRYPTOGRAPHIC FAILURES
  □ Passwords hashed với bcrypt/argon2 (min cost 12)
  □ Sensitive data encrypted at rest (PII, tokens)
  □ HTTPS enforced (no HTTP fallback)
  □ TLS 1.2+ only
  □ Secrets trong env vars (không trong code)

A03 — INJECTION
  □ SQL: parameterized queries / ORM only (không string concat)
  □ NoSQL: input validation trước khi query
  □ XSS: output encoding, Content-Security-Policy header
  □ Command injection: không exec() với user input
  □ LDAP/XML injection check nếu applicable

A04 — INSECURE DESIGN
  □ Rate limiting: login, API, webhook endpoints
  □ Account lockout sau N failed attempts
  □ Security design review cho new features

A05 — SECURITY MISCONFIGURATION
  □ Debug mode OFF trong production
  □ Default credentials đã đổi
  □ Unnecessary features/ports disabled
  □ Error messages không expose stack traces
  □ Directory listing disabled

A06 — VULNERABLE COMPONENTS
  □ npm audit / pip-audit: không có critical CVEs
  □ Dependencies update strategy (Dependabot?)
  □ Docker base images: không dùng :latest

A07 — AUTH & SESSION FAILURES
  □ Session invalidated sau logout
  □ Session timeout reasonable (idle + absolute)
  □ MFA available cho admin accounts
  □ Password reset flow secure (token expires)
  □ Cookie flags: HttpOnly, Secure, SameSite=Strict

A08 — INTEGRITY FAILURES
  □ Subresource Integrity (SRI) cho CDN assets
  □ Package lock file committed
  □ CI/CD pipeline không nhận untrusted input

A09 — LOGGING FAILURES
  □ Auth events logged (login, logout, failed attempts)
  □ Access control failures logged
  □ Logs không chứa PII / sensitive data
  □ Log integrity (append-only, offsite backup)

A10 — SSRF
  □ Outbound requests: validate URL destination
  □ Whitelist external domains nếu có thể
  □ Internal network inaccessible từ user input
```

---

## /harden [service/app]
> Security headers + hardening configuration

```
HTTP SECURITY HEADERS (bắt buộc):
  Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline'...
  Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
  X-Frame-Options: DENY
  X-Content-Type-Options: nosniff
  Referrer-Policy: strict-origin-when-cross-origin
  Permissions-Policy: camera=(), microphone=(), geolocation=()

CORS CONFIGURATION:
  □ Whitelist specific origins (không dùng *)
  □ Credentials: only nếu thực sự cần
  □ Methods: chỉ những gì dùng

NGINX / REVERSE PROXY:
  □ Hide server version (server_tokens off)
  □ Rate limiting (limit_req_zone)
  □ Max body size phù hợp
  □ Request timeout reasonable

DOCKER / CONTAINER:
  □ Non-root user trong container
  □ Read-only filesystem nếu có thể
  □ No --privileged flag
  □ Secrets qua Docker secrets / env, không COPY vào image
```

---

## /ship [environment]
> Pre-deployment production readiness checklist

```
CODE QUALITY
  □ All tests passing (CI green)
  □ No TODO/FIXME critical
  □ No debug code (console.log, breakpoints)
  □ Dependencies: no unresolved peer deps
  □ Bundle size within budget

ENVIRONMENT & CONFIG
  □ Environment variables documented (.env.example updated)
  □ Production config khác với dev (debug off, strict mode on)
  □ Database: migrations ready + rollback tested
  □ Feature flags: correct state for prod

PERFORMANCE
  □ Lighthouse score ≥90 (Performance, Accessibility, Best Practices)
  □ Core Web Vitals trong budget (LCP, CLS, FID)
  □ Images optimized
  □ CDN configured cho static assets

MONITORING & OBSERVABILITY
  □ Error tracking configured (Sentry / similar)
  □ Uptime monitoring active
  □ Key metrics dashboarded (response time, error rate)
  □ Alerts set up cho critical thresholds
  □ Log aggregation working

SECURITY (quick final check)
  □ npm audit / pip-audit: no criticals
  □ Security headers present
  □ No secrets in code / git history
  □ API keys rotated nếu cần

ROLLBACK PLAN
  □ Previous version tagged in git
  □ Database rollback migration ready
  □ Rollback procedure documented + tested
  □ Who to notify if rollback triggered?

DEPLOYMENT
  □ Deploy to staging first → smoke test
  □ Zero-downtime deploy? (blue-green / canary)
  □ Health check endpoint responds
  □ Post-deploy smoke test list ready

POST-DEPLOY SMOKE TEST (bắt buộc sau MỌI deploy — LESSONS #BUG-001):
  🛑 KHÔNG claim "deploy thành công" cho đến khi TẤT CẢ checks PASS
  # 1. Build artifacts tồn tại
  test -f .next/BUILD_ID && echo "✅" || echo "❌ NO BUILD_ID — build FAILED"
  # Hoặc: test -d dist/ , test -f build/index.html (tùy framework)
  # 2. Process healthy (không crash loop)
  pm2 list | grep -E "online|errored"
  # Hoặc: systemctl status <service> | grep "active (running)"
  # 3. Local HTTP 200
  HTTP=$(curl -sI http://localhost:PORT -o /dev/null -w '%{http_code}')
  [ "$HTTP" = "200" ] && echo "✅ Local OK" || echo "❌ Local HTTP: $HTTP"
  # 4. External HTTP 200
  EXT=$(curl -sI https://DOMAIN -o /dev/null -w '%{http_code}')
  [ "$EXT" = "200" ] && echo "✅ External OK" || echo "❌ External HTTP: $EXT"
  # 5. Response body không empty (chống false positive)
  BODY=$(curl -s https://DOMAIN | wc -c)
  [ "$BODY" -gt 100 ] && echo "✅ Body: ${BODY}B" || echo "❌ EMPTY RESPONSE"

SIGN-OFF: Code ✓  Security ✓  Performance ✓  Monitoring ✓  Rollback ✓  Smoke ✓
```

---

## /monitor [server]
> Runtime security monitoring — logs, processes, ports, intrusion detection

```
SERVER HEALTH CHECK:
  □ Uptime: uptime -p
  □ Load average: cat /proc/loadavg (alert if >CPU cores)
  □ Memory: free -h (alert if >85% used)
  □ Disk: df -h (alert if >80% used)
  □ Process count: ps aux | wc -l

SECURITY MONITORING:
  □ Failed SSH logins: grep "Failed password" /var/log/auth.log | tail -20
  □ fail2ban status: fail2ban-client status sshd
  □ Active connections: ss -tlnp (unexpected listeners?)
  □ Open ports: nmap localhost (compare with expected)
  □ Running services: systemctl list-units --type=service --state=running
  □ Cron jobs: crontab -l && ls /etc/cron.d/ (unexpected entries?)
  □ Recent logins: last -10
  □ Modified files (last 24h): find /etc -mtime -1 -type f

LOG ANALYSIS:
  □ nginx access: suspicious patterns (scanners, brute force)
  □ nginx error: 502/503 errors, upstream timeouts
  □ pm2 logs: crash loops, memory warnings
  □ N8N logs: workflow execution errors
  □ System: dmesg | tail (kernel errors, OOM kills)

AUTOMATED ALERTS (recommend setup):
  □ UptimeRobot/Uptime Kuma: HTTP check every 5min
  □ fail2ban: auto-ban after 5 failed SSH attempts
  □ Disk space: cron alert at 80%
  □ SSL expiry: 14 days before expiry

OUTPUT: Server health report + security issues + recommended actions
```

---

## /ssl [domain]
> SSL/TLS certificate check + auto-renewal guide

```
SSL CHECK:
  □ Certificate valid: openssl s_client -connect domain.com:443
  □ Expiry date: echo | openssl s_client -servername domain -connect domain:443 2>/dev/null | openssl x509 -noout -dates
  □ Certificate chain: complete? (no missing intermediates)
  □ TLS version: 1.2+ only (no SSLv3, TLSv1.0, TLSv1.1)
  □ Strong ciphers: no NULL, RC4, DES, MD5
  □ HSTS header: present with reasonable max-age?

AUTO-RENEWAL (Let's Encrypt + Certbot):
  □ Certbot installed: certbot --version
  □ Auto-renewal: systemctl status certbot.timer
  □ Test renewal: certbot renew --dry-run
  □ Post-hook: nginx reload after renewal
  □ Cron backup: 0 0 1 * * certbot renew --post-hook "nginx -s reload"

SSL HARDENING (nginx):
  ssl_protocols TLSv1.2 TLSv1.3;
  ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:...;
  ssl_prefer_server_ciphers on;
  ssl_session_cache shared:SSL:10m;
  ssl_session_timeout 1d;
  ssl_stapling on;
  ssl_stapling_verify on;

OUTPUT: SSL health report + expiry countdown + hardening suggestions
```

---

## /firewall [server]
> UFW/iptables audit + recommended rules

```
FIREWALL AUDIT:
  □ UFW status: ufw status verbose
  □ Default policy: incoming=deny, outgoing=allow?
  □ Allowed ports list:
      22/tcp   — SSH (consider changing port)
      80/tcp   — HTTP (redirect to HTTPS)
      443/tcp  — HTTPS
      [app ports] — only what's needed
  □ Rate limiting: ufw limit ssh/tcp
  □ No wildcard rules (0.0.0.0/0 on sensitive ports)

RECOMMENDED RULES:
  ufw default deny incoming
  ufw default allow outgoing
  ufw allow 22/tcp comment 'SSH'
  ufw allow 80/tcp comment 'HTTP'
  ufw allow 443/tcp comment 'HTTPS'
  ufw limit ssh/tcp comment 'Rate limit SSH'
  ufw enable

WORDPRESS SECURITY:
  □ wp-config.php: DISALLOW_FILE_EDIT = true
  □ wp-config.php: define('FORCE_SSL_ADMIN', true)
  □ Database prefix: not default 'wp_'
  □ Admin URL: changed from /wp-admin? (plugin)
  □ XML-RPC: disabled if not needed
  □ File permissions: 644 files, 755 dirs, 400 wp-config
  □ Plugin audit: remove unused, update all
  □ User audit: no default 'admin' username

N8N SECURITY:
  □ N8N_BASIC_AUTH_ACTIVE=true (basic auth enabled)
  □ N8N_ENCRYPTION_KEY set (credentials encrypted)
  □ Execution data: auto-prune old executions
  □ Webhook paths: not guessable
  □ N8N behind reverse proxy with HTTPS

OUTPUT: Firewall audit + rule recommendations + app-specific hardening
```
