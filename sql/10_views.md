# Views trong Cơ Sở Dữ Liệu

## 1. Khái niệm

Views là các bảng ảo được tạo ra bằng cách thực hiện một truy vấn SQL trên một hoặc nhiều bảng thực trong cơ sở dữ liệu.

View không lưu trữ dữ liệu thật, mà chỉ lưu trữ định nghĩa của truy vấn và kết quả truy vấn sẽ được tính toán lại mỗi khi view được gọi.

## 2. Lợi ích của Views

Đơn giản hóa Truy Vấn: Views giúp đơn giản hóa các truy vấn phức tạp bằng cách ẩn đi sự phức tạp của bảng cơ sở dữ liệu.

Bảo Mật: Views có thể được sử dụng để bảo vệ dữ liệu nhạy cảm bằng cách hạn chế quyền truy cập chỉ vào những phần dữ liệu cần thiết.

Tái Sử Dụng Truy Vấn: Views có thể được tái sử dụng trong các truy vấn khác mà không cần viết lại các truy vấn phức tạp.

Dữ Liệu Ảo: Views cung cấp một cách để xử lý dữ liệu mà không làm thay đổi dữ liệu gốc trong các bảng cơ sở dữ liệu.

## 3. Tạo và Sử Dụng Views

Tạo View
```sql
-- Tạo view đơn giản
CREATE VIEW view_employee_details AS
SELECT employee_id, employee_name, department_name
FROM employees
JOIN departments ON employees.department_id = departments.department_id;
```

Sử Dụng View
```sql
-- Sử dụng view để lấy dữ liệu
SELECT * FROM view_employee_details;
```

Cập Nhật Dữ Liệu Thông Qua View
```sql
-- Cập nhật dữ liệu thông qua view
UPDATE view_employee_details
SET employee_name = 'John Doe'
WHERE employee_id = 1;
```

Xóa View
```sql
-- Xóa view
DROP VIEW view_employee_details;
```

## 4. Giới Hạn của Views

Không Thể Lưu Trữ Dữ Liệu: Views không lưu trữ dữ liệu thực tế mà chỉ lưu trữ định nghĩa của truy vấn.

Giới Hạn Trong Cập Nhật: Một số view không thể cập nhật trực tiếp nếu chúng chứa các phép tính phức tạp, các hàm tổng hợp hoặc kết hợp nhiều bảng.

Hiệu Suất: Việc sử dụng view phức tạp có thể ảnh hưởng đến hiệu suất truy vấn do phải tính toán lại kết quả mỗi khi view được gọi.

## 5. Các Loại Views

### Simple Views

Views đơn giản chỉ bao gồm một truy vấn SELECT từ một bảng duy nhất và không chứa các phép tính phức tạp.

### Complex Views

Views phức tạp có thể kết hợp nhiều bảng, chứa các phép tính tổng hợp, các hàm và các điều kiện phức tạp.

### Indexed Views (Materialized Views)

Indexed views, hay còn gọi là materialized views, lưu trữ kết quả của truy vấn để cải thiện hiệu suất.

Tuy nhiên, loại view này không phổ biến trong tất cả các hệ quản trị cơ sở dữ liệu

```sql
-- Tạo một indexed view trong SQL Server
CREATE VIEW view_employee_summary WITH SCHEMABINDING AS
SELECT department_id, COUNT(*) AS employee_count
FROM employees
GROUP BY department_id;

-- Tạo index trên view
CREATE UNIQUE CLUSTERED INDEX idx_employee_summary ON view_employee_summary(department_id);
```

`
Views là một công cụ mạnh mẽ trong cơ sở dữ liệu để đơn giản hóa truy vấn, bảo mật dữ liệu và tái sử dụng truy vấn.
Tuy nhiên, cần phải hiểu rõ các giới hạn và sử dụng chúng một cách hiệu quả để tối ưu hóa hiệu suất và tính toàn vẹn của cơ sở dữ liệu.
`
