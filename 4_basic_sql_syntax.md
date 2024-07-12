# Basic SQL Syntax

## 1. SELECT

Câu lệnh `SELECT` được sử dụng để truy vấn dữ liệu từ một bảng cơ sở dữ liệu.

```sql
SELECT column1, column2, ...
FROM table_name;
```

## 2. SELECT DISTINCT

Câu lệnh `SELECT DISTINCT` được sử dụng để trả về các giá trị khác nhau trong một cột.

```sql
SELECT DISTINCT column1, column2, ...
FROM table_name;
```

## 3. WHERE

Câu lệnh WHERE được sử dụng để lọc các bản ghi dựa trên các điều kiện cụ thể.

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

## 4. AND, OR, NOT

Các toán tử AND, OR, NOT được sử dụng để kết hợp các điều kiện trong mệnh đề WHERE.

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2;

SELECT column1, column2, ...
FROM table_name
WHERE condition1 OR condition2;

SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;
```

## 5. ORDER BY

Câu lệnh ORDER BY được sử dụng để sắp xếp kết quả truy vấn theo thứ tự tăng dần hoặc giảm dần.

```
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 [ASC|DESC];
```

## 6. INSERT INTO

Câu lệnh INSERT INTO được sử dụng để thêm một bản ghi mới vào bảng.

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

## 7. UPDATE

Câu lệnh UPDATE được sử dụng để cập nhật các bản ghi hiện có trong bảng.

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

## 8. DELETE

Câu lệnh DELETE được sử dụng để xóa các bản ghi hiện có trong bảng.

```
DELETE FROM table_name
WHERE condition;
```

## 9. CREATE TABLE

Câu lệnh CREATE TABLE được sử dụng để tạo một bảng mới.

```
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
);
```

## 10. ALTER TABLE

Câu lệnh ALTER TABLE được sử dụng để thêm, xóa hoặc sửa đổi các cột trong bảng.

```sql
ALTER TABLE table_name
ADD column_name datatype;

ALTER TABLE table_name
DROP COLUMN column_name;

ALTER TABLE table_name
MODIFY COLUMN column_name datatype;
```

## 11. DROP TABLE

Câu lệnh DROP TABLE được sử dụng để xóa một bảng hiện có.

```sql
DROP TABLE table_name;
```

## 12. JOINS

Các phép nối JOIN được sử dụng để kết hợp các hàng từ hai hoặc nhiều bảng dựa trên một cột chung giữa chúng.

### a.INNER JOIN

Trả về các hàng có giá trị phù hợp trong cả hai bảng.

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### b.LEFT JOIN (or LEFT OUTER JOIN)

Trả về tất cả các hàng từ bảng bên trái, và các hàng phù hợp từ bảng bên phải. Nếu không có sự phù hợp, kết quả là NULL từ bảng bên phải.

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```

### c.RIGHT JOIN (or RIGHT OUTER JOIN)

Trả về tất cả các hàng từ bảng bên phải, và các hàng phù hợp từ bảng bên trái. Nếu không có sự phù hợp, kết quả là NULL từ bảng bên trái.

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```

### d.FULL OUTER JOIN

Trả về các hàng khi có sự phù hợp trong một trong các bảng. Nếu không có sự phù hợp, kết quả là NULL từ bảng không có sự phù hợp.

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```
