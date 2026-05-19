# 📡 API Documentation

## Cuộc thi Đổi mới Sáng tạo THCS Thủ Đức

> Tài liệu API cho chức năng đăng ký tham gia cuộc thi.

---

## Mục lục

- [Tổng quan](#tổng-quan)
- [Authentication](#authentication)
- [Endpoints](#endpoints)
  - [POST /api/register](#post-apiregister)
  - [GET /api/registrations](#get-apiregistrations)
  - [GET /api/registration/:id](#get-apiregistrationid)
- [Error Codes](#error-codes)
- [Rate Limiting](#rate-limiting)
- [Examples](#examples)

---

## Tổng quan

API được thiết kế theo chuẩn RESTful, trả về dữ liệu dạng JSON.

| Thông tin | Giá trị |
|-----------|---------|
| Base URL | `https://taminhle.github.io/cuoc-thi-doi-moi-sang-tao-thcs-thu-duc/api` |
| Format | JSON |
| Encoding | UTF-8 |
| Version | v1 |

---

## Authentication

Form submission endpoint không yêu cầu authentication (public endpoint).

Admin endpoints yêu cầu API key trong header:

```
Authorization: Bearer <API_KEY>
```

---

## Endpoints

### POST /api/register

Đăng ký tham gia cuộc thi.

**URL:** `POST /api/register`

**Headers:**
```
Content-Type: application/json
```

**Request Body:**

| Field | Type | Required | Mô tả |
|-------|------|----------|-------|
| `ho_ten` | string | ✅ | Họ và tên thí sinh (2-100 ký tự) |
| `truong` | string | ✅ | Tên trường THCS (2-200 ký tự) |
| `lop` | string | ✅ | Lớp học (ví dụ: 8A1, 9B2) |
| `email` | string | ✅* | Email liên hệ (phải hợp lệ) |
| `so_dien_thoai` | string | ✅* | Số điện thoại (10 số, bắt đầu 0) |
| `y_tuong` | string | ✅ | Mô tả ý tưởng sáng tạo (10-2000 ký tự) |
| `dong_y_dieu_khoan` | boolean | ✅ | Đồng ý điều khoản tham gia |

> *Bắt buộc cung cấp ít nhất một trong hai: email hoặc số điện thoại.

**Request Example:**

```json
{
  "ho_ten": "Nguyễn Thị Bích Ngọc",
  "truong": "THCS Linh Trung",
  "lop": "8A1",
  "email": "bichngoc@example.com",
  "so_dien_thoai": "0901234567",
  "y_tuong": "Ứng dụng AI giúp học sinh ôn tập bài tập về nhà thông qua gamification và phần thưởng ảo.",
  "dong_y_dieu_khoan": true
}
```

**Response (200 - Success):**

```json
{
  "success": true,
  "message": "Đăng ký thành công! Chúng tôi sẽ liên hệ với bạn sớm.",
  "data": {
    "registration_id": "REG-2024-001234",
    "ho_ten": "Nguyễn Thị Bích Ngọc",
    "truong": "THCS Linh Trung",
    "submitted_at": "2024-11-15T08:30:00Z",
    "status": "pending_review"
  }
}
```

**Response (400 - Validation Error):**

```json
{
  "success": false,
  "error": "VALIDATION_ERROR",
  "message": "Dữ liệu không hợp lệ",
  "details": [
    {
      "field": "email",
      "message": "Email không đúng định dạng"
    },
    {
      "field": "y_tuong",
      "message": "Ý tưởng phải có ít nhất 10 ký tự"
    }
  ]
}
```

**Response (409 - Duplicate):**

```json
{
  "success": false,
  "error": "DUPLICATE_REGISTRATION",
  "message": "Email hoặc số điện thoại này đã được đăng ký trước đó."
}
```

**Response (429 - Rate Limited):**

```json
{
  "success": false,
  "error": "RATE_LIMIT_EXCEEDED",
  "message": "Quá nhiều yêu cầu. Vui lòng thử lại sau 60 giây.",
  "retry_after": 60
}
```

---

### GET /api/registrations

Lấy danh sách đăng ký (Admin only).

**URL:** `GET /api/registrations`

**Headers:**
```
Authorization: Bearer <API_KEY>
```

**Query Parameters:**

| Parameter | Type | Default | Mô tả |
|-----------|------|---------|-------|
| `page` | integer | 1 | Trang hiện tại |
| `limit` | integer | 20 | Số bản ghi mỗi trang (max: 100) |
| `status` | string | all | Lọc theo trạng thái: `pending_review`, `approved`, `rejected` |
| `truong` | string | - | Lọc theo tên trường |
| `search` | string | - | Tìm kiếm theo tên thí sinh |

**Response (200):**

```json
{
  "success": true,
  "data": {
    "registrations": [
      {
        "registration_id": "REG-2024-001234",
        "ho_ten": "Nguyễn Thị Bích Ngọc",
        "truong": "THCS Linh Trung",
        "lop": "8A1",
        "email": "bichngoc@example.com",
        "so_dien_thoai": "0901234567",
        "y_tuong": "Ứng dụng AI giúp học sinh...",
        "status": "pending_review",
        "submitted_at": "2024-11-15T08:30:00Z"
      }
    ],
    "pagination": {
      "current_page": 1,
      "total_pages": 5,
      "total_records": 98,
      "per_page": 20
    }
  }
}
```

---

### GET /api/registration/:id

Lấy thông tin một đăng ký cụ thể.

**URL:** `GET /api/registration/{registration_id}`

**Headers:**
```
Authorization: Bearer <API_KEY>
```

**Response (200):**

```json
{
  "success": true,
  "data": {
    "registration_id": "REG-2024-001234",
    "ho_ten": "Nguyễn Thị Bích Ngọc",
    "truong": "THCS Linh Trung",
    "lop": "8A1",
    "email": "bichngoc@example.com",
    "so_dien_thoai": "0901234567",
    "y_tuong": "Ứng dụng AI giúp học sinh ôn tập bài tập về nhà thông qua gamification và phần thưởng ảo.",
    "dong_y_dieu_khoan": true,
    "status": "pending_review",
    "submitted_at": "2024-11-15T08:30:00Z",
    "updated_at": "2024-11-15T08:30:00Z"
  }
}
```

**Response (404):**

```json
{
  "success": false,
  "error": "NOT_FOUND",
  "message": "Không tìm thấy đăng ký với ID này."
}
```

---

## Error Codes

| Code | HTTP Status | Mô tả |
|------|-------------|-------|
| `VALIDATION_ERROR` | 400 | Dữ liệu đầu vào không hợp lệ |
| `UNAUTHORIZED` | 401 | Thiếu hoặc sai API key |
| `FORBIDDEN` | 403 | Không có quyền truy cập |
| `NOT_FOUND` | 404 | Không tìm thấy tài nguyên |
| `DUPLICATE_REGISTRATION` | 409 | Đã đăng ký trước đó |
| `RATE_LIMIT_EXCEEDED` | 429 | Vượt quá giới hạn request |
| `INTERNAL_ERROR` | 500 | Lỗi server nội bộ |

---

## Rate Limiting

| Endpoint | Giới hạn |
|----------|---------|
| POST /api/register | 5 requests / phút / IP |
| GET /api/registrations | 60 requests / phút / API key |
| GET /api/registration/:id | 120 requests / phút / API key |

---

## Examples

### JavaScript (Fetch API)

```javascript
// Đăng ký tham gia cuộc thi
async function dangKyThamGia(formData) {
  try {
    const response = await fetch('/api/register', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        ho_ten: formData.hoTen,
        truong: formData.truong,
        lop: formData.lop,
        email: formData.email,
        so_dien_thoai: formData.soDienThoai,
        y_tuong: formData.yTuong,
        dong_y_dieu_khoan: formData.dongYDieuKhoan
      })
    });

    const result = await response.json();

    if (result.success) {
      console.log('Đăng ký thành công:', result.data.registration_id);
      return result;
    } else {
      throw new Error(result.message);
    }
  } catch (error) {
    console.error('Lỗi đăng ký:', error.message);
    throw error;
  }
}
```

### Form HTML Integration

```html
<form id="registration-form" onsubmit="handleSubmit(event)">
  <input type="text" name="ho_ten" placeholder="Họ và tên" required>
  <input type="text" name="truong" placeholder="Tên trường" required>
  <input type="text" name="lop" placeholder="Lớp" required>
  <input type="email" name="email" placeholder="Email">
  <input type="tel" name="so_dien_thoai" placeholder="Số điện thoại">
  <textarea name="y_tuong" placeholder="Mô tả ý tưởng của bạn..." required></textarea>
  <label>
    <input type="checkbox" name="dong_y_dieu_khoan" required>
    Tôi đồng ý với điều khoản tham gia
  </label>
  <button type="submit">Đăng ký ngay</button>
</form>

<script>
async function handleSubmit(event) {
  event.preventDefault();
  const formData = new FormData(event.target);
  const data = Object.fromEntries(formData.entries());
  data.dong_y_dieu_khoan = !!data.dong_y_dieu_khoan;

  try {
    const result = await dangKyThamGia(data);
    alert(`Đăng ký thành công! Mã đăng ký: ${result.data.registration_id}`);
  } catch (error) {
    alert(`Lỗi: ${error.message}`);
  }
}
</script>
```

---

*Tài liệu được tạo tự động bởi Documentation Writer Agent - 2026-05-19*
