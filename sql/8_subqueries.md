# Subqueries

Subqueries (truy vấn con) là những truy vấn được lồng bên trong một truy vấn khác.

Subqueries thường được sử dụng để thực hiện các tác vụ phức tạp trong SQL và giúp chia nhỏ các vấn đề lớn thành các phần dễ quản lý hơn.

Subqueries có thể trả về một hoặc nhiều giá trị và có thể được sử dụng trong các phần của câu lệnh SQL khác nhau như `WHERE, FROM, SELECT, HAVING`.

Dưới đây là các loại subqueries và cách sử dụng chúng:

## Cách Subqueries Hoạt Động

Khi một truy vấn chính chạy, các subquery bên trong nó được thực hiện trước.

Kết quả của subquery được sử dụng trong truy vấn chính để hoàn thành câu lệnh.

Subqueries có thể trả về một giá trị duy nhất hoặc một tập hợp giá trị, tùy thuộc vào cách bạn xây dựng chúng.

## Cấu Trúc Của Một Subquery

### 1. Scalar Subquery (truy vấn con vô hướng)

- Định nghĩa: Trả về một giá trị duy nhất.

- Sử dụng: Thường được sử dụng để so sánh với một cột trong câu truy vấn chính hoặc để trích xuất một giá trị duy nhất từ một bảng.

```sql
SELECT name
FROM customers
WHERE id = (SELECT customer_id FROM orders WHERE order_number = '12345');

-- Lấy tên nhân viên và tổng số giờ làm việc của họ
SELECT
    nhanvien.ten,
    (SELECT SUM(gio_lam_viec)
     FROM lich_su_lam_viec
     WHERE lich_su_lam_viec.nhanvien_id = nhanvien.nhanvien_id) AS tong_gio_lam_viec
FROM nhanvien;

```

### 2. Row Subquery

- Định nghĩa: Trả về một hàng hoặc tập hợp các giá trị từ một hàng.

- Sử dụng: Thường được sử dụng để so sánh toàn bộ hàng dữ liệu hoặc để trích xuất một tập hợp các giá trị từ hàng dữ liệu.

```sql
SELECT *
FROM employees
WHERE (first_name, last_name) = (SELECT first_name, last_name FROM managers WHERE department = 'HR');
```

### 3. Column Subquery

- Định nghĩa: Trả về một cột hoặc tập hợp các giá trị từ một cột.

- Sử dụng: Thường được sử dụng để trích xuất tập hợp các giá trị từ một cột dựa trên điều kiện hoặc để tính toán một giá trị từ các cột dữ liệu.

```sql
SELECT department_name,
       (SELECT AVG(salary) FROM employees WHERE department = departments.department_name) AS avg_salary
FROM departments;
```

### 4. Table Subquery

- Định nghĩa: Trả về một bảng hoặc tập hợp các hàng từ một bảng.

- Sử dụng: Thường được sử dụng để trích xuất dữ liệu từ một bảng dựa trên điều kiện hoặc để thực hiện các phép biến đổi dữ liệu phức tạp.

```sql
SELECT *
FROM (SELECT * FROM orders WHERE order_date >= '2023-01-01') AS recent_orders
WHERE total_amount > 1000;
```

# Lợi ích của Subqueries

- Tích hợp và xử lý dữ liệu từ nhiều bảng hoặc nguồn dữ liệu khác nhau.

- Tạo các điều kiện phức tạp và tìm kiếm dữ liệu dựa trên kết quả của các truy vấn con.

- Tính toán và trả về giá trị dựa trên dữ liệu
