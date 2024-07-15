# Advanced SQL Functions (Các Hàm Nâng Cao)

## 1. Window Functions

### 1.1 ROW_NUMBER()

Mô tả: Trả về số thứ tự của mỗi hàng trong một tập hợp kết quả.

```sql
SELECT column_name, ROW_NUMBER() OVER (ORDER BY column_name) AS row_num
FROM table_name;
```

### 1.2 RANK()

Mô tả: Gán một thứ hạng cho mỗi hàng trong một tập hợp kết quả với các hàng có giá trị giống nhau sẽ có cùng thứ hạng.

```sql
SELECT column_name,
       RANK() OVER (ORDER BY column_name) AS rank
FROM table_name;
```

### 1.3 DENSE_RANK()

Mô tả: Giống như RANK() nhưng không bỏ qua thứ hạng nếu có giá trị trùng lặp.

```sql
SELECT column_name,
       DENSE_RANK() OVER (ORDER BY column_name) AS dense_rank
FROM table_name;
```

### 1.4 NTILE()

Mô tả: Phân chia dữ liệu thành n phần bằng nhau và gán một số thứ tự cho mỗi phần.

```sql
SELECT column_name,
       NTILE(number_of_groups) OVER (ORDER BY column_name) AS tile
FROM table_name;
```

### 1.5 LAG() and LEAD()

Mô tả: `LAG()` trả về giá trị của hàng trước đó và `LEAD()` trả về giá trị của hàng tiếp theo trong tập hợp kết quả.

```sql
SELECT column_name,
       LAG(column_name, offset, default_value) OVER (ORDER BY column_name) AS lag_value,
       LEAD(column_name, offset, default_value) OVER (ORDER BY column_name) AS lead_value
FROM table_name;
```

### 1.6 FIRST_VALUE() and LAST_VALUE():

Mô tả:
- `FIRST_VALUE()` trả về giá trị của cột được chỉ định trong hàng đầu tiên của cửa sổ,
- `LAST_VALUE()` trả về giá trị của cột được chỉ định trong hàng cuối cùng của cửa sổ.

```sql
SELECT order_date, revenue, FIRST_VALUE(revenue) OVER (ORDER BY order_date) AS first_month_revenue
FROM monthly_sales;
```

## 2. Aggregate Functions

### 2.1 SUM()

Mô tả: Tính tổng giá trị của một cột.

```sql
SELECT SUM(column_name)
FROM table_name
WHERE condition;
```

### 2.2 COUNT()

Mô tả: Đếm số hàng trong một bảng hoặc tập hợp kết quả.

```sql
SELECT COUNT(*)
FROM table_name
WHERE condition;
```

### 2.3 AVG()

Mô tả: Tính giá trị trung bình của một cột.

```sql
SELECT AVG(column_name)
FROM table_name
WHERE condition;
```

### 2.4 MAX()

Mô tả: Tìm giá trị lớn nhất của một cột.

```sql
SELECT MAX(column_name)
FROM table_name
WHERE condition;
```

### 2.5 MIN()

Mô tả: Tìm giá trị nhỏ nhất của một cột.

```sql
SELECT MIN(column_name)
FROM table_name
WHERE condition;
```

## 3. Numeric Functions

### 3.1 ABS()

Mô tả: Trả về giá trị tuyệt đối của một số.

```sql
SELECT ABS(column_name)
FROM table_name;
```

### 3.2 CEILING()

Mô tả: Trả về giá trị nhỏ nhất của số nguyên lớn hơn hoặc bằng giá trị được cung cấp.

```sql
SELECT CEILING(column_name)
FROM table_name;
```

### 3.3 FLOOR()

Mô tả: Trả về giá trị lớn nhất của số nguyên nhỏ hơn hoặc bằng giá trị được cung cấp.

```sql
SELECT FLOOR(column_name)
FROM table_name;
```

## 4. Analytic Functions

### 4.1 CUME_DIST()

Mô tả: Tính phân vị tích lũy của mỗi hàng trong tập hợp kết quả.

```sql
SELECT column_name,
       CUME_DIST() OVER (ORDER BY column_name) AS cum_dist
FROM table_name;
```

### 4.2 PERCENT_RANK()

Mô tả: Tính phần trăm thứ hạng của một giá trị trong tập hợp kết quả.

```sql
SELECT column_name,
       PERCENT_RANK() OVER (ORDER BY column_name) AS percent_rank
FROM table_name;
```

## 5. Stored Procedures

Mô tả: Một tập hợp các câu lệnh SQL được lưu trữ và có thể được thực thi.

```sql
CREATE PROCEDURE procedure_name
AS
BEGIN
    SQL_statements
END;
```

## 6. String Functions

### 6.1 CONCAT()

Mô tả: Nối hai hoặc nhiều chuỗi lại với nhau.

```sql
SELECT CONCAT(string1, string2)
FROM table_name;
```

### 6.2 SUBSTRING()

Mô tả: Trả về một phần của chuỗi.

```sql
SELECT SUBSTRING(column_name, start_position, length)
FROM table_name;
```

### 6.3 REPLACE()

Mô tả: Thay thế một phần của chuỗi bằng một chuỗi khác.

```sql
SELECT REPLACE(column_name, 'old_string', 'new_string')
FROM table_name;
```

### 6.4 TRIM()

Mô tả: loại bỏ các khoảng trắng không cần thiết từ đầu và cuối của chuỗi.

```sql
SELECT TRIM('   hello   ') AS trimmed_text;
```

### 6.5 LENGTH()

Mô tả: trả về độ dài của một chuỗi (số ký tự).

```sql
SELECT product_name, LENGTH(product_name) AS name_length
FROM products;
```

### UPPER() and LOWER():

Mô tả:
- `UPPER()` chuyển đổi toàn bộ chuỗi thành chữ in hoa
- `LOWER()` chuyển đổi toàn bộ chuỗi thành chữ thường.

```sql
SELECT UPPER(city) AS capitalized_city
FROM customers;
```

## 7. Date Functions

### 7.1 GETDATE()

Mô tả: Trả về ngày giờ hiện tại.

```sql
SELECT GETDATE();
```

### 7.2 DATEADD()

Mô tả: Thêm một khoảng thời gian vào một ngày.

```sql
SELECT DATEADD(day, number, date_column)
FROM table_name;
```

### 7.3 DATEDIFF()

Mô tả: Trả về sự khác biệt giữa hai ngày.

```sql
SELECT DATEDIFF(day, start_date, end_date)
FROM table_name;
```

### 7.4 CONVERT()

Mô tả: sử dụng để chuyển đổi giá trị ngày tháng từ một định dạng sang một định dạng khác.

```sql
SELECT CONVERT(VARCHAR, order_date, 101) AS formatted_date
FROM orders;
```

### 7.5 DAY(), MONTH(), YEAR()

Mô tả: DAY(), MONTH(), và YEAR() trích xuất ngày, tháng và năm từ một giá trị ngày tháng.

```sql
SELECT order_date, DAY(order_date) AS order_day, MONTH(order_date) AS order_month, YEAR(order_date) AS order_year
FROM orders;
```

### 7.6 DATEPART():

Mô tả: trích xuất một phần cụ thể của ngày tháng, chẳng hạn như ngày, tháng hoặc năm, từ một giá trị ngày tháng.

```sql
SELECT order_date, DATEPART(day, order_date) AS order_day, DATEPART(month, order_date) AS order_month
FROM orders;
```

### 7.7 EOMONTH()

Mô tả: trả về ngày cuối cùng của tháng dựa trên một ngày cụ thể.

```sql
SELECT invoice_date, EOMONTH(invoice_date) AS end_of_month
FROM invoices;
```

### 7.8 FORMAT():

Mô tả: cho phép bạn định dạng ngày tháng dưới dạng chuỗi với định dạng tùy chỉnh.

```sql
SELECT FORMAT(order_date, 'dd/MM/yyyy') AS formatted_date
FROM orders;
```

## 8. Conditional Functions

### 8.1 CASE WHEN

Mô tả: Thực hiện các điều kiện logic để trả về giá trị.

```sql
SELECT column_name,
       CASE
           WHEN condition THEN result
           ELSE result
       END
FROM table_name;
```

### 8.2 COALESCE()

Mô tả: Trả về giá trị đầu tiên không phải là NULL trong danh sách các biểu thức.

```sql
SELECT COALESCE(column1, column2, column3)
FROM table_name;
```

### 8.3 NULLIF()

Mô tả: so sánh hai giá trị. Nếu hai giá trị bằng nhau, nó trả về NULL; nếu không, nó trả về giá trị đầu tiên.

```sql
-- Tìm ra các sinh viên có điểm số bằng 90 hoặc có số điểm là NULL.
SELECT students.*
FROM students
WHERE
    NULLIF(score, 90) IS NULL;
```

### 8.4 IIF()

Mô tả: hoạt động giống như câu lệnh IF trong lập trình. Nó kiểm tra một điều kiện và trả về một giá trị nếu điều kiện đúng và một giá trị khác nếu điều kiện sai.

```sql
SELECT name, age, IIF(age >= 18, 'Adult', 'Child') AS age_group
FROM students;
```

