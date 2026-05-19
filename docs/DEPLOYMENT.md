# 🚀 Deployment Guide

## Cuộc thi Đổi mới Sáng tạo THCS Thủ Đức

> Hướng dẫn triển khai website lên các môi trường khác nhau.

---

## Mục lục

- [Yêu cầu](#yêu-cầu)
- [GitHub Pages (Khuyến nghị)](#github-pages-khuyến-nghị)
- [Netlify](#netlify)
- [Vercel](#vercel)
- [VPS / Server riêng](#vps--server-riêng)
- [Environment Variables](#environment-variables)
- [CI/CD Pipeline](#cicd-pipeline)
- [Monitoring & Maintenance](#monitoring--maintenance)

---

## Yêu cầu

### Môi trường tối thiểu

| Yêu cầu | Phiên bản tối thiểu |
|---------|---------------------|
| Node.js | 16.x LTS |
| npm | 8.x |
| Git | 2.x |

### Trình duyệt hỗ trợ

| Trình duyệt | Phiên bản tối thiểu |
|-------------|---------------------|
| Chrome | 90+ |
| Firefox | 88+ |
| Safari | 14+ |
| Edge | 90+ |
| Mobile Chrome | 90+ |
| Mobile Safari | 14+ |

---

## GitHub Pages (Khuyến nghị)

Phương pháp đơn giản nhất, miễn phí, tích hợp sẵn với GitHub.

### Bước 1: Chuẩn bị repository

```bash
# Clone repository
git clone https://github.com/taminhle/cuoc-thi-doi-moi-sang-tao-thcs-thu-duc.git
cd cuoc-thi-doi-moi-sang-tao-thcs-thu-duc

# Đảm bảo code đã được push lên main branch
git status
git push origin main
```

### Bước 2: Bật GitHub Pages

1. Vào **Settings** của repository trên GitHub
2. Chọn **Pages** trong menu bên trái
3. Trong **Source**, chọn:
   - Branch: `main`
   - Folder: `/ (root)`
4. Nhấn **Save**

### Bước 3: Truy cập website

Sau 1-2 phút, website sẽ có tại:
```
https://taminhle.github.io/cuoc-thi-doi-moi-sang-tao-thcs-thu-duc/
```

### Cập nhật nội dung

```bash
# Chỉnh sửa file
# ...

# Commit và push
git add .
git commit -m "Update: cập nhật nội dung cuộc thi"
git push origin main

# GitHub Pages sẽ tự động deploy trong 1-2 phút
```

---

## Netlify

Hỗ trợ custom domain, HTTPS tự động, form handling.

### Deploy qua Drag & Drop

1. Truy cập [netlify.com/drop](https://app.netlify.com/drop)
2. Kéo thả thư mục dự án vào trang
3. Netlify sẽ tự động deploy và cung cấp URL

### Deploy qua GitHub (Auto-deploy)

1. Đăng nhập [netlify.com](https://netlify.com)
2. Nhấn **Add new site** → **Import an existing project**
3. Chọn **GitHub** và authorize
4. Chọn repository `cuoc-thi-doi-moi-sang-tao-thcs-thu-duc`
5. Cấu hình:
   - **Branch to deploy**: `main`
   - **Build command**: (để trống nếu là static HTML)
   - **Publish directory**: `.` (root)
6. Nhấn **Deploy site**

### Cấu hình `netlify.toml`

```toml
[build]
  publish = "."

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"
    Cache-Control = "public, max-age=3600"

[[headers]]
  for = "/assets/*"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"
```

---

## Vercel

Tốc độ cao, CDN toàn cầu, miễn phí cho dự án cá nhân.

### Deploy qua CLI

```bash
# Cài đặt Vercel CLI
npm install -g vercel

# Deploy
cd cuoc-thi-doi-moi-sang-tao-thcs-thu-duc
vercel

# Theo hướng dẫn:
# - Set up and deploy? Y
# - Which scope? (chọn account của bạn)
# - Link to existing project? N
# - Project name: cuoc-thi-dmst-thcs-thu-duc
# - Directory: ./
# - Override settings? N
```

### Deploy qua GitHub Integration

1. Truy cập [vercel.com](https://vercel.com)
2. Nhấn **New Project**
3. Import từ GitHub
4. Chọn repository và deploy

---

## VPS / Server riêng

Dành cho môi trường production với yêu cầu cao hơn.

### Cài đặt Nginx

```bash
# Cài đặt Nginx
sudo apt update
sudo apt install nginx -y

# Tạo thư mục web
sudo mkdir -p /var/www/dmst-thcs-thu-duc

# Clone code
sudo git clone https://github.com/taminhle/cuoc-thi-doi-moi-sang-tao-thcs-thu-duc.git \
  /var/www/dmst-thcs-thu-duc

# Cấu hình Nginx
sudo nano /etc/nginx/sites-available/dmst-thcs-thu-duc
```

**Nội dung file cấu hình Nginx:**

```nginx
server {
    listen 80;
    server_name dmst-thcs-thu-duc.edu.vn www.dmst-thcs-thu-duc.edu.vn;
    root /var/www/dmst-thcs-thu-duc;
    index index.html;

    # Gzip compression
    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml;

    # Cache static assets
    location /assets/ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    # Security headers
    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Content-Type-Options "nosniff";

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

```bash
# Kích hoạt site
sudo ln -s /etc/nginx/sites-available/dmst-thcs-thu-duc \
  /etc/nginx/sites-enabled/

# Kiểm tra cấu hình
sudo nginx -t

# Reload Nginx
sudo systemctl reload nginx
```

### Cài đặt SSL với Let's Encrypt

```bash
# Cài đặt Certbot
sudo apt install certbot python3-certbot-nginx -y

# Lấy SSL certificate
sudo certbot --nginx -d dmst-thcs-thu-duc.edu.vn -d www.dmst-thcs-thu-duc.edu.vn

# Auto-renew (đã được cài đặt tự động)
sudo systemctl status certbot.timer
```

---

## Environment Variables

Nếu dự án sử dụng backend/API, cần cấu hình các biến môi trường:

```bash
# .env.production
API_BASE_URL=https://api.dmst-thcs-thu-duc.edu.vn
FORM_ENDPOINT=https://api.dmst-thcs-thu-duc.edu.vn/api/register
GOOGLE_ANALYTICS_ID=G-XXXXXXXXXX
RECAPTCHA_SITE_KEY=your_recaptcha_key
```

> ⚠️ **Lưu ý**: Không commit file `.env` lên GitHub. Thêm vào `.gitignore`.

---

## CI/CD Pipeline

### GitHub Actions

Tạo file `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm ci

      - name: Build
        run: npm run build

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

---

## Monitoring & Maintenance

### Kiểm tra uptime

```bash
# Ping website
curl -I https://taminhle.github.io/cuoc-thi-doi-moi-sang-tao-thcs-thu-duc/

# Kiểm tra response time
curl -w "@curl-format.txt" -o /dev/null -s \
  https://taminhle.github.io/cuoc-thi-doi-moi-sang-tao-thcs-thu-duc/
```

### Cập nhật định kỳ

```bash
# Pull code mới nhất
cd /var/www/dmst-thcs-thu-duc
sudo git pull origin main

# Reload server (nếu cần)
sudo systemctl reload nginx
```

### Backup

```bash
# Backup toàn bộ website
tar -czf backup-$(date +%Y%m%d).tar.gz /var/www/dmst-thcs-thu-duc/

# Upload lên cloud storage
# aws s3 cp backup-*.tar.gz s3://your-backup-bucket/
```

---

## Checklist trước khi Deploy

- [ ] Kiểm tra tất cả links hoạt động
- [ ] Test form đăng ký
- [ ] Kiểm tra responsive trên mobile
- [ ] Kiểm tra tốc độ tải trang (Google PageSpeed)
- [ ] Kiểm tra SEO meta tags
- [ ] Kiểm tra favicon và Open Graph images
- [ ] Xác nhận SSL certificate hoạt động
- [ ] Test trên các trình duyệt khác nhau

---

*Tài liệu được tạo tự động bởi Documentation Writer Agent - 2026-05-19*
