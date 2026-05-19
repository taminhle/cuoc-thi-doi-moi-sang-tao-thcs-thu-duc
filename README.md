# 🚀 Cuộc thi Tìm hiểu về Đổi mới Sáng tạo THCS Thủ Đức

> Website chính thức cho Cuộc thi Tìm hiểu về Đổi mới Sáng tạo dành cho học sinh THCS tại Thủ Đức.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen.svg)]()
[![Responsive](https://img.shields.io/badge/Responsive-Mobile%20First-orange.svg)]()

---

## 📋 Mục lục

- [Giới thiệu](#-giới-thiệu)
- [Tính năng](#-tính-năng)
- [Design System](#-design-system)
- [Cấu trúc dự án](#-cấu-trúc-dự-án)
- [Cài đặt & Chạy](#-cài-đặt--chạy)
- [API Documentation](#-api-documentation)
- [Deployment Guide](#-deployment-guide)
- [Content Management](#-content-management)
- [Đội ngũ AI](#-đội-ngũ-ai)
- [Liên hệ](#-liên-hệ)

---

## 🎯 Giới thiệu

Website landing page cho **Cuộc thi Tìm hiểu về Đổi mới Sáng tạo** nhằm:

- 🎓 Thu hút học sinh THCS tại Thủ Đức tham gia cuộc thi
- 💡 Truyền cảm hứng sáng tạo – công nghệ – đổi mới
- 📝 Cho phép đăng ký tham gia trực tuyến
- 📅 Cung cấp thông tin thể lệ, timeline, giải thưởng

---

## ✨ Tính năng

| Tính năng | Mô tả |
|-----------|-------|
| 🏠 Hero Section | Banner chính với CTA "Đăng ký ngay" |
| 📋 Thể lệ | Accordion layout hiển thị quy định cuộc thi |
| 📅 Timeline | Step timeline từ đăng ký đến trao giải |
| 🏆 Giải thưởng | Pricing-card style hiển thị các giải |
| 📝 Form đăng ký | Form thu thập thông tin thí sinh |
| 📱 Responsive | Tương thích hoàn toàn trên mobile |
| ✨ Animation | Fade up, hover glow, floating effects |

---

## 🎨 Design System

### Color Palette

| Tên | Hex | Sử dụng |
|-----|-----|---------|
| Primary Blue | `#2563EB` | Buttons, links, headings |
| Cyan Glow | `#22D3EE` | Accents, highlights, glow effects |
| White | `#FFFFFF` | Background, text on dark |
| Purple Gradient | `#7C3AED` → `#2563EB` | Hero gradient, cards |
| Dark BG | `#0F172A` | Dark sections background |

### Typography

| Role | Font | Weight |
|------|------|--------|
| Heading | Poppins | 700 (Bold) |
| Body | Inter | 400, 500 |
| Caption | Inter | 300 |

### Design Style
- **Glassmorphism**: `backdrop-filter: blur(10px)`, semi-transparent backgrounds
- **Flat Design**: Clean icons, minimal shadows
- **Vibe**: Trẻ trung, Công nghệ, Truyền cảm hứng

---

## 📁 Cấu trúc dự án

```
cuoc-thi-doi-moi-sang-tao-thcs-thu-duc/
├── index.html              # Trang chính
├── assets/
│   ├── css/
│   │   ├── main.css        # Styles chính
│   │   ├── animations.css  # Animation definitions
│   │   └── responsive.css  # Mobile responsive
│   ├── js/
│   │   ├── main.js         # Logic chính
│   │   ├── form.js         # Form submission handler
│   │   └── animations.js   # Scroll animations
│   └── images/
│       ├── hero-bg.jpg     # Hero background
│       └── icons/          # SVG icons
├── docs/
│   ├── API.md              # API documentation
│   ├── DEPLOYMENT.md       # Deployment guide
│   └── CONTENT_MANAGEMENT.md # Content management guide
└── README.md               # File này
```

---

## 🛠️ Cài đặt & Chạy

### Yêu cầu hệ thống

- Trình duyệt hiện đại (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)
- Web server (Apache, Nginx, hoặc bất kỳ static file server nào)
- Node.js 16+ (nếu dùng build tools)

### Chạy local

```bash
# Clone repository
git clone https://github.com/taminhle/cuoc-thi-doi-moi-sang-tao-thcs-thu-duc.git
cd cuoc-thi-doi-moi-sang-tao-thcs-thu-duc

# Chạy với Python (đơn giản nhất)
python3 -m http.server 8080

# Hoặc dùng Node.js live-server
npx live-server --port=8080

# Mở trình duyệt tại
# http://localhost:8080
```

### Build cho production

```bash
# Minify CSS
npx clean-css-cli assets/css/main.css -o assets/css/main.min.css

# Minify JS
npx terser assets/js/main.js -o assets/js/main.min.js

# Optimize images
npx imagemin assets/images/* --out-dir=assets/images/optimized
```

---

## 📡 API Documentation

Xem chi tiết tại [docs/API.md](docs/API.md).

### Form Submission Endpoint

```
POST /api/register
Content-Type: application/json
```

**Request Body:**

```json
{
  "ho_ten": "Nguyễn Văn A",
  "truong": "THCS Linh Trung",
  "lop": "8A1",
  "email": "nguyenvana@example.com",
  "so_dien_thoai": "0901234567",
  "y_tuong": "Ý tưởng sáng tạo của tôi là..."
}
```

**Response (Success):**

```json
{
  "success": true,
  "message": "Đăng ký thành công! Chúng tôi sẽ liên hệ với bạn sớm.",
  "registration_id": "REG-2024-001234"
}
```

---

## 🚀 Deployment Guide

Xem chi tiết tại [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md).

### Triển khai nhanh với GitHub Pages

```bash
# Bật GitHub Pages trong Settings > Pages
# Source: Deploy from branch > main > / (root)
# URL: https://taminhle.github.io/cuoc-thi-doi-moi-sang-tao-thcs-thu-duc/
```

### Triển khai với Netlify

```bash
# Kéo thả thư mục dự án vào netlify.com/drop
# Hoặc kết nối GitHub repo để auto-deploy
```

---

## 📝 Content Management

Xem chi tiết tại [docs/CONTENT_MANAGEMENT.md](docs/CONTENT_MANAGEMENT.md).

### Cập nhật nhanh các nội dung chính

| Nội dung | File | Vị trí |
|----------|------|--------|
| Thể lệ cuộc thi | `index.html` | Section `#the-le` |
| Timeline | `index.html` | Section `#timeline` |
| Giải thưởng | `index.html` | Section `#giai-thuong` |
| Thông tin liên hệ | `index.html` | Section `#footer` |

---

## 🤖 Đội ngũ AI

Dự án được hỗ trợ bởi hệ thống AI đa tác nhân:

| Tác nhân | Vai trò |
|----------|---------|
| 📊 Project Manager | Quản lý tiến độ, phân công tasks |
| 🔍 Code Reviewer | Review code, đảm bảo chất lượng |
| ⚙️ DevOps Engineer | CI/CD, deployment, infrastructure |
| 🧪 QA Tester | Kiểm thử chức năng, UI/UX |
| 🔒 Security Auditor | Kiểm tra bảo mật |
| 🛡️ Penetration Tester | Kiểm tra lỗ hổng bảo mật |
| 📜 Compliance Monitor | Tuân thủ quy định |
| 📝 Documentation Writer | Viết và cập nhật tài liệu |
| 💬 Client Communication | Giao tiếp với khách hàng |

---

## 📞 Liên hệ

**Ban tổ chức Cuộc thi Đổi mới Sáng tạo THCS Thủ Đức**

- 📍 Địa chỉ: Thủ Đức, TP. Hồ Chí Minh
- 📧 Email: contact@dmst-thcsthuduc.edu.vn
- 🌐 Website: https://taminhle.github.io/cuoc-thi-doi-moi-sang-tao-thcs-thu-duc/

---

## 📄 License

MIT License © 2024 Cuộc thi ĐMST THCS Thủ Đức

---

*Tài liệu được tạo tự động bởi Documentation Writer Agent - 2026-05-19*
