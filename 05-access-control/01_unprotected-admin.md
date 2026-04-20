# Lab 01: Unprotected Admin Functionality

## Mục tiêu
Truy cập trang quản trị không được bảo vệ và xóa user `carlos`.

## Đề bài
<img src="images/01_unprotected-admin-2026-04-20-07-26-15.png" width="760" />
<br><br>

## Bước 1: Kiểm tra robots.txt
Mở file:

```http
GET /robots.txt
```

<img src="images/01_unprotected-admin-2026-04-20-07-39-59.png" width="760" />
<br><br>

Trong nội dung `robots.txt` có:

```txt
Disallow: /administrator-panel
```

<img src="images/01_unprotected-admin-2026-04-20-07-41-04.png" width="760" />
<br><br>

Giải thích ngắn: `robots.txt` chỉ là hướng dẫn cho crawler, không phải cơ chế kiểm soát truy cập. Nếu endpoint admin không có auth, người dùng thường vẫn vào được trực tiếp.

## Bước 2: Truy cập trang admin
Mở trực tiếp:

```http
GET /administrator-panel
```

<img src="images/01_unprotected-admin-2026-04-20-07-42-45.png" width="760" />
<br><br>

## Bước 3: Xóa user carlos
Tại trang admin, bấm `Delete` ở user `carlos`.

<img src="images/01_unprotected-admin-2026-04-20-07-43-44.png" width="760" />
<br><br>

## Kết quả
Đã giải quyết lab bằng cách truy cập trực tiếp `/administrator-panel` lộ từ `robots.txt` và xóa user `carlos`.
