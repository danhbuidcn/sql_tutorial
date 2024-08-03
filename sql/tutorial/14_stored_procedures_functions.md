# Stored Procedures and Functions trong SQL

Stored procedures và functions trong SQL là hai cơ chế quan trọng được sử dụng để thực thi các tác vụ tự động, tăng cường tính modular và giảm thiểu sự lặp lại trong các câu lệnh SQL. Dưới đây là mô tả chi tiết và sự khác biệt giữa chúng:

## 1.Stored Procedures (Thủ tục lưu trữ)

### Định nghĩa:

Stored procedure là một nhóm các câu lệnh SQL được biên dịch và lưu trữ trong cơ sở dữ liệu.

Chúng có thể thực thi các thao tác phức tạp, bao gồm việc gọi các thủ tục khác, thực hiện các câu lệnh điều kiện và lặp lại.

Stored Procedure được tạo ra một lần và sau đó có thể được gọi nhiều lần mà không cần viết lại mã.

### Đặc điểm:

`Khả năng tái sử dụng`: Một stored procedure có thể được gọi nhiều lần bởi các ứng dụng khác nhau.

`Cải thiện hiệu suất`: Stored procedures được biên dịch một lần và lưu trữ trong cơ sở dữ liệu, do đó giảm thiểu thời gian thực thi.

`Bảo mật`: Quyền truy cập có thể được cấp chỉ để thực thi stored procedures, thay vì truy cập trực tiếp vào các bảng dữ liệu.

```sql
CREATE PROCEDURE UpdateEmployeeSalary
    @EmployeeID INT,
    @NewSalary DECIMAL(10, 2)
AS
BEGIN
    UPDATE Employees
    SET Salary = @NewSalary
    WHERE EmployeeID = @EmployeeID;

    IF @@ROWCOUNT = 0
    BEGIN
        PRINT 'No employee found with the given ID';
    END
    ELSE
    BEGIN
        PRINT 'Employee salary updated successfully';
    END
END
```

## 2.Functions (Hàm)

### Định nghĩa:

Function là một khối mã SQL có thể được gọi từ trong câu truy vấn hoặc từ trong Stored Procedure.

Nó trả về một giá trị duy nhất.

Functions thường được sử dụng để tính toán và trả về một giá trị cụ thể.

### Đặc điểm:

`Trả về giá trị`: Functions luôn trả về một giá trị duy nhất.

`Khả năng tái sử dụng`: Functions có thể được gọi ở nhiều nơi trong các câu lệnh SQL.

`Dễ bảo trì`: Giúp mã nguồn dễ đọc và bảo trì hơn bằng cách tách các chức năng logic thành các phần riêng biệt.

`Hạn chế`: Functions không thể thực hiện các thao tác như cập nhật, xóa hoặc chèn dữ liệu vào bảng.

```sql
CREATE FUNCTION CalculateEmployeeBonus
    (@EmployeeID INT)
RETURNS DECIMAL(10, 2)
AS
BEGIN
    DECLARE @Bonus DECIMAL(10, 2);
    SELECT @Bonus = Salary * 0.10
    FROM Employees
    WHERE EmployeeID = @EmployeeID;

    RETURN @Bonus;
END
```

## 3.Sự khác biệt chính giữa Stored Procedures và Functions:

### Trả về giá trị:

Stored procedures có thể trả về nhiều giá trị (bằng cách sử dụng các tham số đầu ra hoặc result sets).

Functions chỉ trả về một giá trị duy nhất.

### Gọi trong câu lệnh SQL:

Functions có thể được gọi trong các câu lệnh SQL như SELECT, WHERE, hoặc bất kỳ nơi nào mà một biểu thức có thể được sử dụng.

Stored procedures phải được gọi bằng cách sử dụng lệnh EXEC hoặc EXECUTE.

### Thao tác dữ liệu:

Stored procedures có thể thực hiện các thao tác DML (INSERT, UPDATE, DELETE) và DDL (CREATE, ALTER, DROP).

Functions thường không được phép thực hiện các thao tác DML trực tiếp trên các bảng dữ liệu.

### Quản lý lỗi:

Stored procedures có khả năng quản lý lỗi tốt hơn và có thể sử dụng TRY...CATCH để bắt và xử lý lỗi.

Functions có khả năng quản lý lỗi hạn chế hơn.

### Kết luận

Cả stored procedures và functions đều là các công cụ mạnh mẽ trong SQL để tự động hóa và tối ưu hóa các tác vụ. Việc sử dụng chúng đúng cách sẽ giúp cải thiện hiệu suất và khả năng quản lý của cơ sở dữ liệu.
