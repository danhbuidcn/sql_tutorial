# Indexes trong Cơ Sở Dữ Liệu

## 1. Khái niệm

Index (Chỉ mục) trong cơ sở dữ liệu là một cấu trúc dữ liệu đặc biệt giúp tăng tốc độ truy vấn dữ liệu trong bảng.

Index tương tự như một cuốn sách, giúp bạn nhanh chóng tìm kiếm thông tin mà không cần phải duyệt qua toàn bộ cuốn sách.

## 2. Lợi ích của Indexes

Tăng Tốc Độ Truy Vấn: Index giúp tăng tốc độ truy vấn SELECT, đặc biệt là khi tìm kiếm theo cột được lập chỉ mục.

Hiệu Quả Trong Truy Vấn JOIN: Index giúp tăng hiệu suất của các truy vấn JOIN giữa các bảng.

Tăng Hiệu Quả Truy Vấn Sắp Xếp: Index cải thiện hiệu suất của các truy vấn sử dụng ORDER BY hoặc GROUP BY.

## 3. Các Loại Indexes

### 1. B-Tree Index

Khái niệm: Đây là loại index phổ biến nhất, lưu trữ dữ liệu theo cấu trúc cây cân bằng.

Lợi ích: Hiệu quả trong các truy vấn tìm kiếm, truy vấn phạm vi và sắp xếp.

```sql
-- Tạo một B-Tree index
CREATE INDEX idx_employee_name ON employees(employee_name);
```

### 2. Hash Index

Khái niệm: Lưu trữ dữ liệu bằng cách sử dụng hàm băm.

Lợi ích: Hiệu quả trong các truy vấn bằng cách sử dụng phép so sánh bằng (equality searches).

Giới hạn: Không hiệu quả trong các truy vấn phạm vi hoặc sắp xếp.

```sql
-- Tạo một Hash index (hỗ trợ bởi một số hệ quản trị cơ sở dữ liệu như PostgreSQL)
CREATE INDEX idx_employee_id ON employees USING HASH (employee_id);
```

### 3. Bitmap Index

Khái niệm: Lưu trữ dữ liệu dưới dạng bitmaps.

Lợi ích: Hiệu quả trong các bảng lớn có ít giá trị khác nhau trong cột.

Giới hạn: Không hiệu quả cho các cột có nhiều giá trị khác nhau.


```sql
-- Tạo một Bitmap index (hỗ trợ bởi Oracle)
CREATE BITMAP INDEX idx_gender ON employees(gender);
```

### 4. Unique Index

Khái niệm: Đảm bảo rằng tất cả các giá trị trong cột được lập chỉ mục là duy nhất.

Lợi ích: Đảm bảo tính duy nhất của dữ liệu trong cột.

```sql
-- Tạo một Unique index
CREATE UNIQUE INDEX idx_unique_employee_id ON employees(employee_id);
```

### 5. Composite Index

Khái niệm: Lập chỉ mục trên nhiều cột.

Lợi ích: Hiệu quả trong các truy vấn sử dụng nhiều cột trong mệnh đề WHERE.

```sql
-- Tạo một Composite index
CREATE INDEX idx_composite ON employees(department_id, employee_name);
```

### 6. Full-Text Index

Khái niệm: Dùng cho việc tìm kiếm toàn văn (full-text search).

Lợi ích: Hiệu quả trong các truy vấn tìm kiếm văn bản.

```sql
-- Tạo một Full-Text index (hỗ trợ bởi MySQL)
CREATE FULLTEXT INDEX idx_fulltext ON documents(content);
```

### 4. Quản Lý Indexes

Tạo Index

```sql
-- Tạo một index đơn giản
CREATE INDEX idx_employee_name ON employees(employee_name);
```

Xóa Index

```sql
-- Xóa một index
DROP INDEX idx_employee_name ON employees;
```

Kiểm Tra Indexes

```sql
-- Kiểm tra các indexes trên một bảng (MySQL)
SHOW INDEX FROM employees;
```

### 5. Các Vấn Đề Liên Quan Đến Indexes

Tốn Dung Lượng Lưu Trữ: Indexes yêu cầu thêm không gian lưu trữ.

Ảnh Hưởng Đến Hiệu Suất Ghi: Cập nhật, chèn và xóa dữ liệu có thể chậm hơn do cần cập nhật các indexes liên quan.

Quản Lý Indexes: Cần phải tối ưu hóa và quản lý indexes để đảm bảo hiệu suất tốt nhất.

`Indexes là một công cụ mạnh mẽ trong cơ sở dữ liệu, giúp tăng tốc độ truy vấn và cải thiện hiệu suất.

Tuy nhiên, cần sử dụng indexes một cách hợp lý và cân nhắc đến các vấn đề liên quan đến dung lượng lưu trữ và hiệu suất ghi dữ liệu.`

https://viblo.asia/p/nhung-kien-thuc-co-ban-ve-sql-9-zOQJwAgqVMP
