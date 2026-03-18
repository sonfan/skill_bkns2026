# DEPLOYMENT — [Tên dự án]

> **Mục đích**: Hướng dẫn deploy, update, rollback. Ai đọc cũng có thể triển khai.
> **Bắt buộc**: Mọi repo BKNS production PHẢI có file này.

---

## 1. Mục tiêu triển khai

- Mô tả ngắn gọn dự án cần deploy ở đâu, phục vụ gì.

## 2. Yêu cầu hệ thống

| Thành phần | Yêu cầu tối thiểu |
|---|---|
| OS | Ubuntu 22.04+ |
| Runtime | Node 20+ / PHP 8.2+ / Python 3.11+ |
| Database | MySQL 8.0+ / PostgreSQL 15+ |
| RAM | Xmin GB |
| Disk | Xmin GB |

## 3. Biến môi trường

> ⚠️ Copy `.env.example` và điền giá trị thật. KHÔNG commit `.env`.

| Biến | Mô tả | Ví dụ | Bắt buộc |
|---|---|---|---|
| `APP_ENV` | Môi trường | `production` | ✅ |
| `DB_HOST` | Database host | `localhost` | ✅ |
| `DB_PASSWORD` | Database password | `***` | ✅ |

## 4. Service phụ thuộc

| Service | Mục đích | URL/Port |
|---|---|---|
| MySQL | Database chính | `3306` |
| Redis | Cache/Queue | `6379` |
| Nginx | Reverse proxy | `80/443` |

## 5. Cách build

```bash
# Clone repo
git clone git@github.com:bkns/[repo-name].git
cd [repo-name]

# Install dependencies
[npm install / composer install / pip install -r requirements.txt]

# Build
[npm run build / ...]
```

## 6. Cách chạy

```bash
# Development
[npm run dev / php artisan serve]

# Production
[pm2 start / systemctl start / docker compose up -d]
```

## 7. Cách migrate dữ liệu

```bash
# Chạy migrations
[php artisan migrate / npx prisma migrate deploy]

# Seed data (nếu cần)
[php artisan db:seed / ...]
```

## 8. Cách kiểm tra sau deploy

```bash
# Health check
curl -s https://[domain]/api/health | jq

# Verify version
curl -s https://[domain]/api/version

# Check logs
[tail -f /var/log/app.log / pm2 logs / docker logs]
```

## 9. Cách rollback

```bash
# Rollback code
git checkout [previous-tag]

# Rollback database
[php artisan migrate:rollback / npx prisma migrate reset]

# Restart service
[pm2 restart / systemctl restart / docker compose restart]
```

## 10. Lỗi thường gặp

| Lỗi | Nguyên nhân | Fix |
|---|---|---|
| `Connection refused` | Service chưa start | `systemctl start [service]` |
| `Permission denied` | Sai quyền file | `chown -R www-data:www-data` |
| `Out of memory` | Thiếu RAM | Tăng RAM hoặc swap |

## 11. Người phụ trách deploy

| Vai trò | Tên | Liên hệ |
|---|---|---|
| Deploy owner | | |
| Backup deployer | | |
| Approve release | | |
