# 📝 Content Management Guide

## Cuộc thi Đổi mới Sáng tạo THCS Thủ Đức

> Hướng dẫn cập nhật nội dung website: thể lệ, timeline, giải thưởng và các thông tin khác.

---

## Mục lục

- [Tổng quan](#tổng-quan)
- [Cập nhật Thể lệ](#cập-nhật-thể-lệ)
- [Cập nhật Timeline](#cập-nhật-timeline)
- [Cập nhật Giải thưởng](#cập-nhật-giải-thưởng)
- [Cập nhật Thông tin liên hệ](#cập-nhật-thông-tin-liên-hệ)
- [Cập nhật Hero Section](#cập-nhật-hero-section)
- [Quản lý hình ảnh](#quản-lý-hình-ảnh)
- [Quy trình cập nhật](#quy-trình-cập-nhật)

---

## Tổng quan

Website được xây dựng dưới dạng **static HTML**. Tất cả nội dung được lưu trực tiếp trong file `index.html`. Để cập nhật nội dung, bạn chỉ cần chỉnh sửa file này và push lên GitHub.

### Cấu trúc sections trong index.html

```
index.html
├── <header>          → Navigation bar
├── <section#hero>    → Hero banner
├── <section#benefits>→ Lợi ích tham gia
├── <section#timeline>→ Lịch trình cuộc thi
├── <section#the-le>  → Thể lệ cuộc thi
├── <section#giai-thuong> → Giải thưởng
├── <section#dang-ky> → Form đăng ký
└── <footer>          → Footer
```

---

## Cập nhật Thể lệ

### Vị trí trong file

Tìm section có id `the-le`:

```html
<section id="the-le" class="section-the-le">
  <div class="container">
    <h2>📋 Thể lệ cuộc thi</h2>
    <div class="accordion">
      <!-- Các mục thể lệ ở đây -->
    </div>
  </div>
</section>
```

### Thêm/sửa mục thể lệ

Mỗi mục thể lệ có cấu trúc:

```html
<div class="accordion-item">
  <button class="accordion-header">
    <span class="accordion-icon">📌</span>
    <span class="accordion-title">Tiêu đề mục thể lệ</span>
    <span class="accordion-arrow">▼</span>
  </button>
  <div class="accordion-content">
    <p>Nội dung chi tiết của mục thể lệ này...</p>
    <ul>
      <li>Điều kiện 1</li>
      <li>Điều kiện 2</li>
    </ul>
  </div>
</div>
```

### Ví dụ cập nhật điều kiện tham gia

```html
<div class="accordion-item">
  <button class="accordion-header">
    <span class="accordion-icon">👤</span>
    <span class="accordion-title">Điều kiện tham gia</span>
    <span class="accordion-arrow">▼</span>
  </button>
  <div class="accordion-content">
    <ul>
      <li>Học sinh đang học tại các trường THCS trên địa bàn Thủ Đức</li>
      <li>Độ tuổi: 11-15 tuổi (lớp 6-9)</li>
      <li>Mỗi học sinh chỉ được đăng ký 1 ý tưởng</li>
      <li>Có thể tham gia theo nhóm (tối đa 3 thành viên)</li>
    </ul>
  </div>
</div>
```

---

## Cập nhật Timeline

### Vị trí trong file

```html
<section id="timeline" class="section-timeline">
  <div class="container">
    <h2>📅 Lịch trình cuộc thi</h2>
    <div class="timeline">
      <!-- Các bước timeline ở đây -->
    </div>
  </div>
</section>
```

### Cấu trúc một bước timeline

```html
<div class="timeline-item">
  <div class="timeline-dot">
    <span class="timeline-icon">📝</span>
  </div>
  <div class="timeline-content">
    <div class="timeline-date">01/11/2024 - 30/11/2024</div>
    <h3 class="timeline-title">Đăng ký tham gia</h3>
    <p class="timeline-desc">Học sinh điền form đăng ký trực tuyến trên website</p>
  </div>
</div>
```

### Timeline đầy đủ (ví dụ)

```html
<div class="timeline">
  <!-- Bước 1: Đăng ký -->
  <div class="timeline-item">
    <div class="timeline-dot active">
      <span class="timeline-icon">📝</span>
    </div>
    <div class="timeline-content">
      <div class="timeline-date">01/11/2024 - 30/11/2024</div>
      <h3 class="timeline-title">Đăng ký tham gia</h3>
      <p class="timeline-desc">Điền form đăng ký trực tuyến</p>
    </div>
  </div>

  <!-- Bước 2: Nộp ý tưởng -->
  <div class="timeline-item">
    <div class="timeline-dot">
      <span class="timeline-icon">💡</span>
    </div>
    <div class="timeline-content">
      <div class="timeline-date">01/12/2024 - 31/12/2024</div>
      <h3 class="timeline-title">Nộp ý tưởng</h3>
      <p class="timeline-desc">Nộp bài thuyết trình ý tưởng sáng tạo</p>
    </div>
  </div>

  <!-- Bước 3: Sơ khảo -->
  <div class="timeline-item">
    <div class="timeline-dot">
      <span class="timeline-icon">🔍</span>
    </div>
    <div class="timeline-content">
      <div class="timeline-date">15/01/2025</div>
      <h3 class="timeline-title">Vòng sơ khảo</h3>
      <p class="timeline-desc">Ban giám khảo chấm điểm và chọn 20 ý tưởng xuất sắc</p>
    </div>
  </div>

  <!-- Bước 4: Chung kết -->
  <div class="timeline-item">
    <div class="timeline-dot">
      <span class="timeline-icon">🏆</span>
    </div>
    <div class="timeline-content">
      <div class="timeline-date">01/02/2025</div>
      <h3 class="timeline-title">Vòng chung kết</h3>
      <p class="timeline-desc">Top 20 thí sinh thuyết trình trực tiếp trước ban giám khảo</p>
    </div>
  </div>

  <!-- Bước 5: Trao giải -->
  <div class="timeline-item">
    <div class="timeline-dot">
      <span class="timeline-icon">🎉</span>
    </div>
    <div class="timeline-content">
      <div class="timeline-date">15/02/2025</div>
      <h3 class="timeline-title">Lễ trao giải</h3>
      <p class="timeline-desc">Công bố kết quả và trao giải thưởng</p>
    </div>
  </div>
</div>
```

---

## Cập nhật Giải thưởng

### Vị trí trong file

```html
<section id="giai-thuong" class="section-giai-thuong">
  <div class="container">
    <h2>🏆 Giải thưởng</h2>
    <div class="prizes-grid">
      <!-- Các card giải thưởng ở đây -->
    </div>
  </div>
</section>
```

### Cấu trúc card giải thưởng

```html
<div class="prize-card prize-first">
  <div class="prize-badge">🥇</div>
  <h3 class="prize-title">Giải Nhất</h3>
  <div class="prize-value">5.000.000 VNĐ</div>
  <ul class="prize-perks">
    <li>Học bổng 5 triệu đồng</li>
    <li>Bằng khen của UBND Thủ Đức</li>
    <li>Cơ hội tham gia chương trình mentorship</li>
    <li>Giấy chứng nhận thành tích</li>
  </ul>
  <div class="prize-cta">
    <span class="prize-tag">Top 1</span>
  </div>
</div>
```

### Các class CSS cho từng giải

| Giải | Class CSS |
|------|-----------|
| Giải Nhất | `prize-first` |
| Giải Nhì | `prize-second` |
| Giải Ba | `prize-third` |
| Giải Sáng tạo | `prize-creative` |
| Giải Khuyến khích | `prize-encourage` |

### Ví dụ cập nhật giá trị giải thưởng

```html
<!-- Thay đổi giá trị giải thưởng -->
<div class="prize-value">10.000.000 VNĐ</div>

<!-- Thêm phần thưởng mới -->
<ul class="prize-perks">
  <li>Học bổng 10 triệu đồng</li>
  <li>Laptop học tập</li>
  <li>Bằng khen của UBND TP. Thủ Đức</li>
  <li>Cơ hội tham gia chương trình STEM quốc tế</li>
</ul>
```

---

## Cập nhật Thông tin liên hệ

### Vị trí trong file

```html
<footer id="footer" class="footer">
  <div class="container">
    <div class="footer-info">
      <!-- Thông tin liên hệ ở đây -->
    </div>
  </div>
</footer>
```

### Cập nhật địa chỉ và liên hệ

```html
<div class="footer-contact">
  <h4>📞 Liên hệ Ban tổ chức</h4>
  <ul>
    <li>
      <span class="icon">📍</span>
      <span>123 Đường Võ Văn Ngân, Phường Linh Chiểu, TP. Thủ Đức</span>
    </li>
    <li>
      <span class="icon">📧</span>
      <a href="mailto:contact@dmst-thcsthuduc.edu.vn">contact@dmst-thcsthuduc.edu.vn</a>
    </li>
    <li>
      <span class="icon">📱</span>
      <a href="tel:+84901234567">0901 234 567</a>
    </li>
    <li>
      <span class="icon">🕐</span>
      <span>Thứ 2 - Thứ 6: 8:00 - 17:00</span>
    </li>
  </ul>
</div>
```

---

## Cập nhật Hero Section

### Thay đổi tiêu đề và slogan

```html
<section id="hero" class="hero-section">
  <div class="hero-content">
    <!-- Thay đổi tiêu đề chính -->
    <h1 class="hero-title">
      Khơi nguồn Sáng tạo<br>
      <span class="highlight">Kiến tạo Tương lai</span>
    </h1>

    <!-- Thay đổi mô tả -->
    <p class="hero-subtitle">
      Cuộc thi Tìm hiểu về Đổi mới Sáng tạo dành cho học sinh THCS tại Thủ Đức.
      Hãy chia sẻ ý tưởng của bạn và cùng nhau xây dựng tương lai!
    </p>

    <!-- Thay đổi deadline -->
    <div class="hero-deadline">
      <span class="deadline-label">⏰ Hạn đăng ký:</span>
      <span class="deadline-date">30/11/2024</span>
    </div>

    <!-- CTA Button -->
    <a href="#dang-ky" class="btn-primary btn-glow">
      🚀 Đăng ký ngay
    </a>
  </div>
</section>
```

---

## Quản lý hình ảnh

### Thay đổi ảnh nền Hero

```html
<!-- Trong CSS hoặc inline style -->
<section id="hero" style="background-image: url('assets/images/hero-bg-new.jpg')">
```

Hoặc trong file CSS:

```css
.hero-section {
  background-image: url('../images/hero-bg.jpg');
  background-size: cover;
  background-position: center;
}
```

### Yêu cầu kỹ thuật cho hình ảnh

| Loại ảnh | Kích thước | Format | Dung lượng tối đa |
|----------|-----------|--------|-------------------|
| Hero background | 1920x1080px | JPG/WebP | 500KB |
| Card images | 800x600px | JPG/WebP | 200KB |
| Icons | 64x64px | SVG/PNG | 10KB |
| Logo | 200x60px | SVG/PNG | 50KB |

### Tối ưu hình ảnh trước khi upload

```bash
# Sử dụng imagemin
npx imagemin assets/images/hero-bg.jpg --out-dir=assets/images/

# Hoặc convert sang WebP
cwebp -q 80 hero-bg.jpg -o hero-bg.webp
```

---

## Quy trình cập nhật

### Quy trình chuẩn

```bash
# 1. Clone hoặc pull code mới nhất
git pull origin main

# 2. Tạo branch mới cho thay đổi
git checkout -b update/cap-nhat-the-le-thang-11

# 3. Chỉnh sửa nội dung trong index.html
# (sử dụng text editor hoặc IDE)

# 4. Kiểm tra local
python3 -m http.server 8080
# Mở http://localhost:8080 để xem trước

# 5. Commit thay đổi
git add index.html
git commit -m "Update: cập nhật thể lệ và timeline tháng 11/2024"

# 6. Push và tạo Pull Request
git push origin update/cap-nhat-the-le-thang-11

# 7. Merge vào main sau khi review
# GitHub Pages sẽ tự động deploy
```

### Checklist trước khi cập nhật

- [ ] Kiểm tra chính tả và ngữ pháp
- [ ] Xác nhận ngày tháng chính xác
- [ ] Test trên mobile (Chrome DevTools)
- [ ] Kiểm tra links hoạt động
- [ ] Xem trước trên local trước khi push

### Lưu ý quan trọng

> ⚠️ **Không xóa** các class CSS quan trọng như `glassmorphism`, `glow-effect`, `fade-up` vì chúng liên quan đến animations.

> ⚠️ **Backup** file `index.html` trước khi thực hiện thay đổi lớn.

> ✅ **Luôn test** trên mobile sau khi cập nhật nội dung.

---

## Hỗ trợ

Nếu gặp vấn đề khi cập nhật nội dung, liên hệ:

- 📧 Email: contact@dmst-thcsthuduc.edu.vn
- 💬 GitHub Issues: [Tạo issue mới](https://github.com/taminhle/cuoc-thi-doi-moi-sang-tao-thcs-thu-duc/issues)

---

*Tài liệu được tạo tự động bởi Documentation Writer Agent - 2026-05-19*
