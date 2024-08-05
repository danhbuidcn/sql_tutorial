# Các tính chất của lập trình hướng đối tượng thông qua OOP

- Trong Ruby mọi thứ đều là đối tượng, mọi đối tượng đều có các thuộc tính (variable) và hành vi (method)
- Tất cả mọi thứ đều là đối tượng vì nó là thể hiện của lớp.

VD:
- 5 là một đối tượng của lớp Integer
- Lớp Integer không có các thuộc tính được định nghĩa trước nhưng có các phương thức được thể hiện qua các instance của lớp

[reference link](https://www.geeksforgeeks.org/object-oriented-programming-in-ruby-set-1/?ref=lbp)

## Tính kế thừa (Inheritance)

- Lớp con kế thừa các thuộc tính và phương thức của lớp cha, giúp tái sử dụng mã và tổ chức mã một cách có hiệu quả.
- Lớp con có thể mở rộng hoặc ghi đè các thuộc tính của lớp cha hoặc thêm các thuộc tính và phương thức mới.
- Ruby không hỗ trợ đa kế thừa, nhưng có thể sử dùng include hoặc extend để thay thế.

```
class Animal
  def speak
    puts "Animal speaks"
  end
end

class Dog < Animal
  def speak
    puts "Dog barks"
  end

  def run
    # do something
  end
end

animal = Animal.new
animal.speak  # Output: "Animal speaks"

dog = Dog.new
dog.speak     # Output: "Dog barks"
```

## Tính đa hình (Polymorphism)

- Các đối tượng của các lớp khác nhau có thể phản ứng khác nhau với cùng một phương thức tùy theo lớp của nó.
- Định nghĩa lại hành vi hoặc phương thức của lớp cha để thay đổi hoặc mở rộng hành vi của nó.
- Giúp mã trở trở nên linh hoạt và dễ mở rộng.
- Đa hình được thông qua kĩ thuật ghi đè :
  - Khi gọi một phương thức trên một đối tượng, ruby sẽ tìm phương thức tương ứng trong lớp của đối tượng đó
  - Nếu không tìm thấy, nó sẽ tìm đến lớp cơ sở.

```
class Animal
  def speak
    raise NotImplementedError, "Subclasses must override this method"
  end
end

class Dog < Animal
  def speak
    puts "Dog barks"
  end
end

class Cat < Animal
  def speak
    puts "Cat meows"
  end
end

dog = Dog.new
cat = Cat.new

dog.speak  # Output: "Dog barks"
cat.speak  # Output: "Cat meows"
```

## Tính đóng gói (Encapsulation)

- Gói dữ liệu dưới 1 đơn vị duy nhất.
- Mục đích nhằm bảo vệ dữ liệu của đối tượng khỏi các truy cập trái phép.
- Tính đóng gói được thể hiện qua mức độ truy cập của đối tượng :
  - attr_reader: Tạo phương thức đọc (getter) cho một biến instance.
  - attr_writer: Tạo phương thức ghi (setter) cho một biến instance.
  - attr_accessor: Tạo cả phương thức đọc và phương thức ghi cho một biến instance.

```
class Demoencapsulation
  attr_reader :id, :name, :addr

  def initialize(id, name, addr)     
    # Instance Variables       
    @cust_id = id  
    @cust_name = name  
    @cust_addr = addr  
  end

  # displaying result  
  def display_details()
    information
  end

  private

  def information
    puts "Customer id: #{id}"
    puts "Customer name: #{cust_name}"
    puts "Customer address: #{cust_addr}"
  end
end
    
# Create Objects
cust1 = Demoencapsulation .new("1", "Mike", "Wisdom Apartments, Ludhiya")
cust2 = Demoencapsulation .new("2", "Jackey", "New Empire road, Khandala")  
    
# Call Methods  
cust1.display_details()  
cust2.display_details() 
```

## Tính trừu tượng (Abstraction)

- Biểu diễn các chi tiết quan trọng và che giấu các chi tiết chức năng được gọi là trừu tượng hóa dữ liệu.
- Trừu tượng hóa dữ liệu bằng cách sử dụng Kiểm soát truy cập private, protected, public.

```
class Geeks  
  # defining publicMethod
  def publicMethod  
    puts "In Public!"
    # calling privateMethod inside publicMethod  
    privateMethod 
  end

  # defining privateMethod
  private  

  def privateMethod  
    puts "In Private!"
  end
end
  
  
# creating an object of class Geeks  
obj = Geeks.new
  
# calling the public method of class Geeks  
obj.publicMethod 
```
