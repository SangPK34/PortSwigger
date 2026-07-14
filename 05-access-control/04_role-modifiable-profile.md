# Lab 04: User Role Can Be Modified in User Profile

## Mục tiêu
Nâng quyền từ user thường lên admin bằng cách chỉnh sửa tham số `roleid` trong request cập nhật profile, sau đó xóa user `carlos`.

## Đề bài
<img src="images/04_role-modifiable-profile-2026-04-21-00-12-13.png" width="760" />
<br><br>

## Bước 1: Đăng nhập và gửi request thay đổi email
Đăng nhập bằng tài khoản được cấp:
```txt
wiener:peter
```
Truy cập **My account**, thay đổi email và bấm **Update email**:
<img src="images/04_role-modifiable-profile-2026-07-14-08-09-14.png" width="760" />
<br><br>

## Bước 2: Phân tích request và response qua Burp Suite
Bắt request `POST /my-account/change-email` trong Burp Suite:
<img src="images/04_role-modifiable-profile-2026-07-14-08-10-20.png" width="760" />
<br><br>

Response trả về dữ liệu người dùng dạng JSON, chứa trường `"roleid": 1`:
<img src="images/04_role-modifiable-profile-2026-07-14-08-12-13.png" width="760" />
<br><br>

## Bước 3: Thêm tham số roleid để nâng quyền admin
Gửi request sang **Repeater**, thêm cặp key-value `"roleid": 2` vào JSON body và gửi đi:
<img src="images/04_role-modifiable-profile-2026-07-14-08-13-42.png" width="760" />
<br><br>

Response trả về `"roleid": 2` cho thấy tài khoản đã được nâng quyền thành công.

## Bước 4: Truy cập Admin panel và xóa carlos
Quay lại trình duyệt, tải lại trang sẽ thấy xuất hiện nút **Admin panel**. Truy cập vào trang admin:
<img src="images/04_role-modifiable-profile-2026-07-14-08-14-44.png" width="760" />
<br><br>

Bấm **Delete** để xóa user `carlos` và hoàn thành lab:
<img src="images/04_role-modifiable-profile-2026-07-14-08-15-22.png" width="760" />
<br><br>

## Kết quả
Đã giải quyết lab bằng cách chèn thêm tham số `"roleid": 2` vào JSON body của request cập nhật profile để nâng quyền admin và thực hiện xóa user `carlos`.