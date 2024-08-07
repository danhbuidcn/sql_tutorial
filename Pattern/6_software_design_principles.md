# Software Design Principles (Nguyên tắc thiết kế phần mềm)

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

## 5. Định luật Demeter (Nguyên tắc hiểu biết ít nhất)

- Nguyên tắc: Phân chia các phạm vi trách nhiệm giữa các lớp và đóng gói logic trong một lớp hoặc phương thức. Các thực thể phần mềm nên độc lập với các thành phần khác.
- Lợi ích: Giảm sự phụ thuộc giữa các lớp, giúp ứng dụng dễ hiểu, dễ bảo trì và mở rộng hơn.

```ruby
# BAD
class Customer
  def address
    @address
  end
end

class Order
  def initialize(customer)
    @customer = customer
  end

  def print_shipping_label
    label = @customer.address.street + ' ' + @customer.address.city
    puts label
  end
end

# GOOD
class Address
  attr_reader :street, :city

  def initialize(street, city)
    @street = street
    @city = city
  end
end

class Customer
  def initialize(address)
    @address = address
  end

  def shipping_label
    @address.street + ' ' + @address.city
  end
end

class Order
  def initialize(customer)
    @customer = customer
  end

  def print_shipping_label
    puts @customer.shipping_label
  end
end
```
## 6. Tránh tối ưu hóa quá sớm

- Nguyên tắc: Tối ưu hóa là cần thiết nhưng không nên thực hiện ở giai đoạn đầu của quá trình phát triển.
- Lợi ích: Giảm thiểu thời gian và công sức, tránh thiết kế mã quá phức tạp từ sớm

```ruby
# BAD: Tối ưu hóa quá sớm
def find_prime_numbers(limit)
  primes = []
  (2..limit).each do |num|
    primes << num if (2..Math.sqrt(num)).none? { |i| num % i == 0 }
  end
  primes
end

# GOOD: Đơn giản và dễ hiểu
def find_prime_numbers(limit)
  primes = []
  (2..limit).each do |num|
    is_prime = true
    (2..num-1).each do |i|
      if num % i == 0
        is_prime = false
        break
      end
    end
    primes << num if is_prime
  end
  primes
end
```

https://viblo.asia/p/cac-nguyen-tac-thiet-ke-phan-mem-4dbZNQakKYM
