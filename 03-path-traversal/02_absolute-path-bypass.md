# Lab 02: Absolute Path Bypass

## Mục tiêu
Khai thác lỗi Path Traversal để đọc file `/etc/passwd` khi ứng dụng chặn chuỗi `../` nhưng vẫn cho dùng đường dẫn tuyệt đối.

## Đề bài
![02_absolute-path-bypass-2026-04-16-00-34-40.png](images/02_absolute-path-bypass-2026-04-16-00-34-40.png)
<br><br>

## Bước 1: Lấy request ảnh
Mở ảnh sản phẩm để thấy endpoint:

```http
GET /image?filename=21.jpg
```

![02_absolute-path-bypass-2026-04-16-00-35-41.png](images/02_absolute-path-bypass-2026-04-16-00-35-41.png)
<br><br>

## Bước 2: Bypass bằng absolute path
Trong Burp, sửa tham số `filename` thành đường dẫn tuyệt đối đến file hệ thống:

```http
GET /image?filename=%2fetc%2fpasswd HTTP/2
```

Vì server xử lý giá trị này theo filesystem path, nên dù chặn traversal sequence, nó vẫn đọc được `/etc/passwd`.

![02_absolute-path-bypass-2026-04-16-00-38-16.png](images/02_absolute-path-bypass-2026-04-16-00-38-16.png)
<br><br>

## Kết quả
Response trả về nội dung `/etc/passwd` và lab được solve.
