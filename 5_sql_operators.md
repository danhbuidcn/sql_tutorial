# SQL Operators

Các toán tử trong SQL được sử dụng để thực hiện các phép toán như so sánh và tính toán số học. Chúng rất quan trọng trong việc tạo câu truy vấn. Toán tử SQL được chia thành các loại sau:

## 1. Toán tử Số học

Chúng được sử dụng để thực hiện các phép toán toán học. Dưới đây là danh sách các toán tử này:

- `+` : Phép cộng
- `-` : Phép trừ
- `*` : Phép nhân
- `/` : Phép chia
- `%` : Phép chia lấy dư

```sql
SELECT product, price, (price * 0.18) as tax
FROM products;
```

## 2. Toán tử So sánh

Chúng được sử dụng trong mệnh đề WHERE để so sánh một biểu thức với một biểu thức khác. Một số toán tử so sánh bao gồm:

- `=` : Bằng
- `!=` hoặc `<>` : Không bằng
- `>` : Lớn hơn
- `<` : Nhỏ hơn
- `>=` : Lớn hơn hoặc bằng
- `<=` : Nhỏ hơn hoặc bằng

```sql
SELECT name, age
FROM students
WHERE age > 18;
```

## 3. Toán tử Logic
Chúng được sử dụng để kết hợp kết quả của hai điều kiện khác nhau. Bao gồm:

- `AND` : Trả về true nếu cả hai điều kiện đều đúng.
- `OR` : Trả về true nếu ít nhất một trong hai điều kiện là đúng.
- `NOT` : Trả về giá trị boolean ngược lại của điều kiện.

```sql
SELECT *
FROM employees
WHERE salary > 50000 AND age < 30;
```

## 4. Toán tử Bitwise
Chúng thực hiện các phép toán trên mức bit trên dữ liệu đầu vào. Dưới đây là danh sách các toán tử này:

- `&` : Bitwise AND
- `|` : Bitwise OR
- `^` : Bitwise XOR

```sql
SELECT id, (flags & 1) as is_active
FROM users;
```
