# Coding Principles

## 1. DRY (Don't Repeat Yourself)

- **Nguyên tắc**: Tránh lặp lại mã, thay vào đó hãy tái sử dụng mã thông qua hàm, lớp hoặc module.
- **Lợi ích**: Giảm thiểu lỗi, dễ bảo trì và nâng cấp.

```ruby
# BAD
def calculate_area_of_rectangle(width, height)
  width * height
end

def calculate_area_of_square(side)
  side * side
end

# GOOD
def calculate_area(shape, dimensions)
  case shape
  when :rectangle
    dimensions[:width] * dimensions[:height]
  when :square
    dimensions[:side] * dimensions[:side]
  end
end
```

## 2. KISS (Keep It Simple, Stupid)

- Nguyên tắc: Giữ cho mã nguồn đơn giản và dễ hiểu. Tránh các cấu trúc phức tạp không cần thiết.
- Lợi ích: Dễ hiểu, dễ bảo trì, giảm thiểu lỗi.

```ruby
# BAD
def calculate(a, b, operator)
  if operator == '+'
    a + b
  elsif operator == '-'
    a - b
  elsif operator == '*'
    a * b
  elsif operator == '/'
    a / b
  end
end

# GOOD
def calculate(a, b, operator)
  a.send(operator, b)
end
```

## 3. YAGNI (You Aren't Gonna Need It)

- Nguyên tắc: Chỉ phát triển những tính năng cần thiết cho hiện tại, tránh phát triển những tính năng chưa chắc sẽ dùng.
- Lợi ích: Giảm thiểu công sức và tài nguyên, tăng hiệu quả.

```ruby
# BAD
def future_feature
  # code for a feature that might be needed in the future
end

# GOOD
def current_feature
  # code for the feature that is needed now
end
```

## 4. SOLID

### S - Single Responsibility Principle

- Nguyên tắc: Một lớp chỉ nên có một lý do để thay đổi, tức là chỉ chịu trách nhiệm về một phần chức năng của chương trình.
- Lợi ích: Dễ bảo trì, dễ hiểu, giảm thiểu rủi ro khi thay đổi mã.
ruby

```ruby
# BAD
class User
  def initialize(name, email)
    @name = name
    @mail = email
  end

  def send_welcome_email
    # code to send email
  end
end

# GOOD
class User
  def initialize(name, email)
    @name = name
    @mail = email
  end
end

class UserMailer
  def send_welcome_email(user)
    # code to send email
  end
end
```

### O - Open/Closed Principle

- Nguyên tắc: Các thực thể (lớp, module, hàm, ...) nên mở để mở rộng nhưng đóng để sửa đổi.
- Lợi ích: Dễ dàng thêm tính năng mới mà không ảnh hưởng đến mã hiện có.

```ruby
# BAD
class Shape
  def area(shape)
    if shape.type == 'circle'
      # calculate circle area
    elsif shape.type == 'rectangle'
      # calculate rectangle area
    end
  end
end

# GOOD
class Shape
  def area
    raise NotImplementedError
  end
end

class Circle < Shape
  def area
    # calculate circle area
  end
end

class Rectangle < Shape
  def area
    # calculate rectangle area
  end
end
```

### L - Liskov Substitution Principle

- Nguyên tắc: Các lớp con phải có thể thay thế cho các lớp cha mà không làm thay đổi tính đúng đắn của chương trình.
- Lợi ích: Tăng tính khả dụng và tái sử dụng mã.

```ruby
# BAD
class Bird
  def fly
    # fly
  end
end

class Ostrich < Bird
  def fly
    raise "Can't fly"
  end
end

# GOOD
class Bird
  def move
    # move
  end
end

class Ostrich < Bird
  def move
    # run
  end
end
```

### I - Interface Segregation Principle

- Nguyên tắc: Nhiều giao diện cụ thể tốt hơn là một giao diện tổng quát.
- Lợi ích: Tránh việc các lớp phải implement những phương thức không cần thiết.

```ruby
# BAD
class Worker
  def work
    # work
  end

  def eat
    # eat
  end
end

class Robot < Worker
  def eat
    raise "Robot can't eat"
  end
end

# GOOD
class Worker
  def work
    # work
  end
end

class HumanWorker < Worker
  def eat
    # eat
  end
end
```

### D - Dependency Inversion Principle

- Nguyên tắc: Các module cấp cao không nên phụ thuộc vào các module cấp thấp. Cả hai nên phụ thuộc vào các abstraction.
- Lợi ích: Tăng tính linh hoạt và khả năng tái sử dụng.

```ruby
# BAD
class Backend
  def fetch_data
    # fetch data from backend
  end
end

class Frontend
  def initialize
    @backend = Backend.new
  end

  def display
    data = @backend.fetch_data
    # display data
  end
end

# GOOD
class Backend
  def fetch_data
    # fetch data
  end
end

class Frontend
  def initialize(backend)
    @backend = backend
  end

  def display
    data = @backend.fetch_data
    # display data
  end
end
```

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
