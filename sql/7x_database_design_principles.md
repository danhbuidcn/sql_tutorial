# Database Design Principles

## 1. Normalization

- Nguyên tắc: Chia nhỏ các bảng dữ liệu để loại bỏ dữ liệu dư thừa và đảm bảo tính toàn vẹn dữ liệu.
- Lợi ích: Giảm thiểu sự trùng lặp dữ liệu và tăng cường tính toàn vẹn của dữ liệu.

```sql
-- BAD: Denormalized table
CREATE TABLE employees (
    employee_id INT,
    employee_name VARCHAR(100),
    department_id INT,
    department_name VARCHAR(100)
);

-- GOOD: Normalized tables
CREATE TABLE employees (
    employee_id INT,
    employee_name VARCHAR(100),
    department_id INT
);

CREATE TABLE departments (
    department_id INT,
    department_name VARCHAR(100)
);
```

## 2. Denormalization

- Nguyên tắc: Kết hợp các bảng dữ liệu để cải thiện hiệu suất truy vấn.
- Lợi ích: Tăng tốc độ truy vấn, đặc biệt là trong các hệ thống đọc nhiều hơn ghi.

```sql
-- Denormalized table for faster read operations
CREATE TABLE employee_details (
    employee_id INT,
    employee_name VARCHAR(100),
    department_name VARCHAR(100)
);
```

## 3. Use Appropriate Data Types

- Nguyên tắc: Sử dụng các kiểu dữ liệu thích hợp cho các cột trong bảng.
- Lợi ích: Tăng hiệu suất, giảm dung lượng lưu trữ và đảm bảo tính toàn vẹn của dữ liệu.

```sql
-- BAD: Using inappropriate data types
CREATE TABLE users (
    user_id VARCHAR(255),
    age VARCHAR(255)
);

-- GOOD: Using appropriate data types
CREATE TABLE users (
    user_id INT,
    age TINYINT
);
```

## 4. Indexing

- Nguyên tắc: Tạo chỉ mục (index) trên các cột được sử dụng thường xuyên trong các câu truy vấn.
- Lợi ích: Tăng tốc độ truy vấn dữ liệu.

```sql
-- Creating an index on the 'email' column
CREATE INDEX idx_email ON users(email);
```

## 5. Avoid NULLable Columns

- Nguyên tắc: Tránh sử dụng các cột có giá trị NULL nếu có thể.
- Lợi ích: Giảm phức tạp trong truy vấn và xử lý dữ liệu, cải thiện hiệu suất.

```sql
-- BAD: Using nullable columns
CREATE TABLE orders (
    order_id INT,
    customer_id INT,
    delivery_date DATE NULL
);

-- GOOD: Avoiding nullable columns
CREATE TABLE orders (
    order_id INT,
    customer_id INT,
    delivery_date DATE NOT NULL
);
```

## 6. Foreign Keys and Constraints

- Nguyên tắc: Sử dụng khóa ngoại (foreign key) và các ràng buộc (constraints) để đảm bảo tính toàn vẹn của dữ liệu.
- Lợi ích: Đảm bảo các mối quan hệ giữa các bảng và dữ liệu chính xác.

```sql
-- Using foreign keys and constraints
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    CONSTRAINT fk_customer
      FOREIGN KEY (customer_id)
      REFERENCES customers(customer_id)
);
```

## 7. Backup and Recovery

- Nguyên tắc: Thực hiện sao lưu và phục hồi cơ sở dữ liệu định kỳ.
- Lợi ích: Đảm bảo dữ liệu không bị mất mát và có thể phục hồi trong trường hợp xảy ra sự cố.

```sql
-- Example command to backup a MySQL database
mysqldump -u username -p database_name > backup_file.sql
```

## 8. Scalability

- Nguyên tắc: Thiết kế cơ sở dữ liệu để có thể mở rộng dễ dàng khi cần.
- Lợi ích: Đảm bảo cơ sở dữ liệu có thể xử lý được lưu lượng tăng lên mà không ảnh hưởng đến hiệu suất.

```sql
-- Using partitioning for scalability
CREATE TABLE orders (
    order_id INT,
    order_date DATE,
    customer_id INT
)
PARTITION BY RANGE (YEAR(order_date)) (
    PARTITION p0 VALUES LESS THAN (1991),
    PARTITION p1 VALUES LESS THAN (1992),
    PARTITION p2 VALUES LESS THAN (1993)
);
```
