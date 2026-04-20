# Lab 03: User Role Controlled by Request Parameter

## Mục tiêu
Nâng quyền từ user thường lên admin bằng cách sửa tham số role trong cookie, rồi xóa user `carlos`.

## Đề bài
<img src="images/03_role-controlled-by-param-2026-04-20-23-58-27.png" width="760" />
<br><br>

## Bước 1: Đăng nhập bằng tài khoản được cấp
Sử dụng tài khoản:

```txt
wiener:peter
```

<img src="images/03_role-controlled-by-param-2026-04-21-00-04-33.png" width="760" />
<br><br>

## Bước 2: Sửa cookie phân quyền
Mở DevTools, vào phần cookie và sửa:

```txt
Admin=false  ->  Admin=true
```

Reload trang sau khi sửa cookie.

<img src="images/03_role-controlled-by-param-2026-04-21-00-06-43.png" width="760" />
<br><br>

Giải thích ngắn: ứng dụng tin giá trị role từ phía client (cookie có thể forge). Khi đổi `Admin=true`, server cấp quyền admin và hiện `Admin panel`.

## Bước 3: Truy cập admin và xóa carlos
Mở `/admin`, sau đó bấm `Delete` ở user `carlos`.

<img src="images/03_role-controlled-by-param-2026-04-21-00-07-15.png" width="760" />
<br><br>

## Kết quả
Đã giải quyết lab bằng cách giả mạo cookie `Admin=true` để truy cập admin panel và xóa `carlos`.
