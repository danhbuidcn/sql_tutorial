# Các Quy Tắc Chuẩn Hóa Cơ Sở Dữ Liệu (CSDL)

Chuẩn hóa cơ sở dữ liệu là một quá trình tổ chức dữ liệu trong cơ sở dữ liệu để giảm sự dư thừa và cải thiện tính toàn vẹn dữ liệu. Các quy tắc chuẩn hóa thường được gọi là các dạng chuẩn (Normal Forms). Dưới đây là các dạng chuẩn chính từ 1NF đến 5NF.

## 1. First Normal Form (1NF)

- Nguyên tắc:
  - Mỗi cột trong bảng phải là nguyên tử, tức là không được chứa các tập hợp hoặc mảng.
  - Mỗi hàng phải là duy nhất và không có hàng nào trùng lặp.


```sql
-- BAD: Dữ liệu không ở dạng 1NF
CREATE TABLE Students (
    StudentID INT,
    StudentName VARCHAR(100),
    Subjects VARCHAR(100) -- Chứa nhiều giá trị
);

-- GOOD: Dữ liệu ở dạng 1NF
CREATE TABLE Students (
    StudentID INT,
    StudentName VARCHAR(100)
);

CREATE TABLE StudentSubjects (
    StudentID INT,
    Subject VARCHAR(100)
);
```

## 2. Second Normal Form (2NF)

- Nguyên tắc:
  - Bảng phải đạt chuẩn 1NF.
  - Tất cả các cột không phải khóa chính phải phụ thuộc hoàn toàn vào khóa chính, không có sự phụ thuộc từng phần.

```sql
-- BAD: Dữ liệu không ở dạng 2NF
CREATE TABLE Orders (
    OrderID INT,
    ProductID INT,
    ProductName VARCHAR(100),
    Quantity INT
);

-- GOOD: Dữ liệu ở dạng 2NF
CREATE TABLE Orders (
    OrderID INT,
    ProductID INT,
    Quantity INT
);

CREATE TABLE Products (
    ProductID INT,
    ProductName VARCHAR(100)
);
```

## 3. Third Normal Form (3NF)

- Nguyên tắc:
  - Bảng phải đạt chuẩn 2NF.
  - Không có cột nào phụ thuộc vào cột không phải khóa chính khác, tức là không có sự phụ thuộc bắc cầu.

```sql
-- BAD: Dữ liệu không ở dạng 3NF
CREATE TABLE Employees (
    EmployeeID INT,
    DepartmentID INT,
    DepartmentName VARCHAR(100),
    EmployeeName VARCHAR(100)
);

-- GOOD: Dữ liệu ở dạng 3NF
CREATE TABLE Employees (
    EmployeeID INT,
    DepartmentID INT,
    EmployeeName VARCHAR(100)
);

CREATE TABLE Departments (
    DepartmentID INT,
    DepartmentName VARCHAR(100)
);
```

## 4. Boyce-Codd Normal Form (BCNF)

- Nguyên tắc:
  - Bảng phải đạt chuẩn 3NF.
  - Với mỗi phụ thuộc hàm (A → B), A phải là siêu khóa.

```sql
-- BAD: Dữ liệu không ở dạng BCNF
CREATE TABLE CourseInstructor (
    CourseID INT,
    InstructorID INT,
    CourseName VARCHAR(100),
    InstructorName VARCHAR(100)
);

-- GOOD: Dữ liệu ở dạng BCNF
CREATE TABLE CourseInstructor (
    CourseID INT,
    InstructorID INT
);

CREATE TABLE Courses (
    CourseID INT,
    CourseName VARCHAR(100)
);

CREATE TABLE Instructors (
    InstructorID INT,
    InstructorName VARCHAR(100)
);
```

## 5. Fourth Normal Form (4NF)

- Nguyên tắc:
  - Bảng phải đạt chuẩn BCNF.
  - Không có phụ thuộc đa trị phi tầm thường.

```sql
-- BAD: Dữ liệu không ở dạng 4NF
CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT,
    Hobby VARCHAR(100)
);

-- GOOD: Dữ liệu ở dạng 4NF
CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT
);

CREATE TABLE StudentHobbies (
    StudentID INT,
    Hobby VARCHAR(100)
);
```

## 6. Fifth Normal Form (5NF)

- Nguyên tắc:
  - Bảng phải đạt chuẩn 4NF.
  - Không có sự phụ thuộc kết hợp phi tầm thường.

```sql
-- BAD: Dữ liệu không ở dạng 5NF
CREATE TABLE ProjectAssignments (
    ProjectID INT,
    EmployeeID INT,
    RoleID INT
);

-- GOOD: Dữ liệu ở dạng 5NF
CREATE TABLE Projects (
    ProjectID INT,
    ProjectName VARCHAR(100)
);

CREATE TABLE Employees (
    EmployeeID INT,
    EmployeeName VARCHAR(100)
);

CREATE TABLE Roles (
    RoleID INT,
    RoleName VARCHAR(100)
);

CREATE TABLE ProjectAssignments (
    ProjectID INT,
    EmployeeID INT,
    RoleID INT
);
```
