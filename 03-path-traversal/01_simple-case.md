# Path Traversal Lab 01: Simple Case

## Mục tiêu
Khai thác tham số `filename` của endpoint ảnh để đọc nội dung file hệ thống `/etc/passwd`.

## Đề bài
<img src="images/01_simple-case-2026-04-16-00-04-52.png" alt="Lab overview" width="760" />
<br><br>

## Bước 1: Xác định endpoint tải ảnh
Từ giao diện sản phẩm, kiểm tra phần tử ảnh để lấy URL nguồn.

<img src="images/01_simple-case-2026-04-16-00-08-13.png" alt="Trang sản phẩm" width="760" />
<br><br>
<img src="images/01_simple-case-2026-04-16-00-07-56.png" alt="Kiểm tra src ảnh" width="760" />
<br><br>

Mở ảnh ở tab mới để thấy request mẫu:

```http
GET /image?filename=9.jpg
```

<img src="images/01_simple-case-2026-04-16-00-09-20.png" alt="URL ảnh gốc" width="760" />
<br><br>

## Bước 2: Thử path traversal trên tham số filename
Gửi request qua Burp Repeater và thay `filename` bằng chuỗi traversal.

<img src="images/01_simple-case-2026-04-16-00-15-43.png" alt="Request ảnh trong Burp" width="760" />
<br><br>

Payload:

```text
../../../etc/passwd
```

Vì sao payload này hoạt động:
- `..` giúp lùi lên thư mục cha.
- Lặp lại nhiều lần để thoát khỏi thư mục hiện tại của ứng dụng.
- Sau đó trỏ tới file tuyệt đối cần đọc: `/etc/passwd`.

## Bước 3: Đọc file /etc/passwd thành công
Sửa tham số `filename` thành payload traversal và gửi lại request.

```http
GET /image?filename=../../../etc/passwd
```

Response trả về nội dung `/etc/passwd`, chứng minh khai thác thành công.

<img src="images/01_simple-case-2026-04-16-00-18-10.png" alt="Đọc được /etc/passwd" width="760" />
<br><br>

## Payload Solve

```text
../../../etc/passwd
```

## Kết quả
Truy xuất thành công nội dung file `/etc/passwd` và hoàn thành lab.
