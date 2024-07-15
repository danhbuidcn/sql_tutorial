# Data Constraints (Ràng Buộc Dữ Liệu)

Ràng buộc dữ liệu (Constraints) trong SQL :
  - Được sử dụng để quy định các quy tắc trên dữ liệu trong bảng
  - Đảm bảo tính toàn vẹn của dữ liệu
  - Đảm bảo tính chính xác của dữ liệu
  - Đảm bảo tính nhất quán của dữ liệu
  - Bảo vệ dữ liệu khỏi những lỗi hoặc sự bất thường

Dưới đây là một số ràng buộc dữ liệu phổ biến trong SQL:

## 1. PRIMARY KEY

Đảm bảo mỗi hàng trong bảng có một giá trị duy nhất, khác null.

```sql
CREATE TABLE nhanvien (
    id INT PRIMARY KEY,
    ten VARCHAR(100),
    luong DECIMAL(10, 2)
);
```

## 2. FOREIGN KEY

Đảm bảo giá trị trong cột này phải khớp với giá trị (khóa chính) trong cột của bảng khác, thiết lập mối quan hệ giữa các bảng.

```sql
CREATE TABLE phongban (
    id INT PRIMARY KEY,
    tenphongban VARCHAR(100)
);

CREATE TABLE nhanvien (
    id INT PRIMARY KEY,
    ten VARCHAR(100),
    phongban_id INT,
    FOREIGN KEY (phongban_id) REFERENCES phongban(id)
);
```

## 3. UNIQUE

Đảm bảo tất cả các giá trị trong cột là duy nhất.

```sql
CREATE TABLE nhanvien (
    id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

## 4. NOT NULL

Đảm bảo cột không được chứa giá trị NULL.

```sql
CREATE TABLE nhanvien (
    id INT PRIMARY KEY,
    ten VARCHAR(100) NOT NULL,
    luong DECIMAL(10, 2) NOT NULL
);
```

## 5. CHECK

Đảm bảo giá trị trong cột thỏa mãn một điều kiện cụ thể.

```sql
CREATE TABLE nhanvien (
    id INT PRIMARY KEY,
    ten VARCHAR(100),
    luong DECIMAL(10, 2),
    CHECK (luong > 0)
);
```

## 6. DEFAULT

Đặt giá trị mặc định cho cột nếu không có giá trị nào được chỉ định.

```sql
CREATE TABLE nhanvien (
    id INT PRIMARY KEY,
    ten VARCHAR(100),
    luong DECIMAL(10, 2) DEFAULT 5000.00
);
```

## 7. Composite Key

Sử dụng kết hợp hai hoặc nhiều cột để tạo thành khóa chính.

```sql
CREATE TABLE nhanvien_du_an (
    nhanvien_id INT,
    du_an_id INT,
    PRIMARY KEY (nhanvien_id, du_an_id)
);
```

## 8. Data Type Constraint

Ràng buộc kiểu dữ liệu xác định loại dữ liệu mà một cột có thể chứa

```sql
CREATE TABLE Employees (
    EmployeeID INT,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    BirthDate DATE,
    Salary DECIMAL(10, 2)
);
```

# Sử Dụng Các Ràng Buộc Dữ Liệu

Các ràng buộc dữ liệu được xác định tại thời điểm tạo bảng hoặc có thể được thêm vào bảng hiện có bằng cách sử dụng câu lệnh `ALTER TABLE`.

```sql
-- Thêm ràng buộc NOT NULL
ALTER TABLE nhanvien
MODIFY COLUMN ten VARCHAR(100) NOT NULL;

-- Thêm ràng buộc UNIQUE
ALTER TABLE nhanvien
ADD CONSTRAINT unq_email UNIQUE (email);

-- Thêm ràng buộc CHECK
ALTER TABLE nhanvien
ADD CONSTRAINT chk_luong CHECK (luong > 0);

-- Thêm khóa ngoại (FOREIGN KEY)
ALTER TABLE nhanvien
ADD CONSTRAINT fk_phongban FOREIGN KEY (phongban_id) REFERENCES phongban(phongban_id);
```
