# Lab 02: Unprotected Admin Functionality with Unpredictable URL

## Mục tiêu
Tìm đường dẫn admin bị ẩn và xóa user `carlos`.

## Đề bài
<img src="images/02_unprotected-admin-unpredictable-url-2026-04-20-07-50-48.png" width="760" />
<br><br>

## Bước 1: Khảo sát bề mặt ứng dụng
Kiểm tra nhanh các endpoint phổ biến như trang chủ và `robots.txt`, nhưng không thấy đường dẫn admin rõ ràng.

<img src="images/02_unprotected-admin-unpredictable-url-2026-04-20-23-46-13.png" width="760" />
<br><br>

## Bước 2: Xem source để tìm endpoint ẩn
Mở source trang (Ctrl + U) và phát hiện đoạn code bị ẩn, trong đó lộ URL admin:

```txt
/admin-u55qlh
```

<img src="images/02_unprotected-admin-unpredictable-url-2026-04-20-23-47-14.png" width="760" />
<br><br>

## Bước 3: Truy cập trang admin
Mở trực tiếp endpoint vừa tìm được:

```http
GET /admin-u55qlh
```

<img src="images/02_unprotected-admin-unpredictable-url-2026-04-20-23-51-00.png" width="760" />
<br><br>

## Bước 4: Xóa user carlos
Trong admin panel, nhấn `Delete` tại user `carlos`.

<img src="images/02_unprotected-admin-unpredictable-url-2026-04-20-23-51-33.png" width="760" />
<br><br>

## Kết quả
Lab được giải bằng cách đọc source để tìm URL admin khó đoán (`/admin-u55qlh`) và truy cập trực tiếp để xóa `carlos`.
