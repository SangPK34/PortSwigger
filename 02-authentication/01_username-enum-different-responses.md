# Authentication Lab 01: Username Enumeration via Different Responses

## Mục tiêu
Dùng khác biệt phản hồi của endpoint đăng nhập để tìm username hợp lệ và brute-force mật khẩu tương ứng.

## Đề bài
<img src="images/01_username-enum-different-responses-2026-04-15-16-49-36.png" alt="Lab overview" width="760" />
<br><br>

## Bước 1: Bắt request đăng nhập và đưa vào Intruder
Từ form login, gửi request `POST /login` vào Burp Intruder và đánh dấu 2 vị trí payload:
- `username=§...§`
- `password=§...§`

<img src="images/01_username-enum-different-responses-2026-04-15-16-55-18.png" alt="Intruder vị trí username" width="760" />
<br><br>
<img src="images/01_username-enum-different-responses-2026-04-15-16-55-47.png" alt="Intruder vị trí password" width="760" />
<br><br>

## Bước 2: Cấu hình Cluster bomb với wordlist đề bài
- Payload 1: danh sách `Candidate usernames`
- Payload 2: danh sách `Candidate passwords`

Chạy `Cluster bomb attack`, sau đó sort theo `Status code` và `Length` để tìm response bất thường.

<img src="images/01_username-enum-different-responses-2026-04-15-17-04-38.png" alt="Kết quả Intruder" width="760" />
<br><br>

Từ kết quả, dòng nổi bật có:
- `Status code = 302`
- `username = mysql`
- `password = qwertyuiop`

## Bước 3: Đăng nhập tài khoản tìm được
Đăng nhập bằng credential đã tìm:

```text
username: mysql
password: qwertyuiop
```

<img src="images/01_username-enum-different-responses-2026-04-15-17-05-18.png" alt="Lab solved" width="760" />
<br><br>

## Kết quả
Đăng nhập thành công tài khoản `mysql` và hoàn thành lab.
