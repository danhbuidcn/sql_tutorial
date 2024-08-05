# Phân biêt include và extends

```
module Greeting
  def say_hello
    puts "Hello!"
  end

  def self.say_hi
    puts "Hi!"
  end
end

class MyClass
  include Greeting
end

class AnotherClass
  extend Greeting
end


MyClass.new.say_hello # in ra Hello!
MyClass.new.say_hi # undefined
MyClass.say_hello # undefined
MyClass.say_hi # undefined


AnotherClass.new.say_hello # undefined
AnotherClass.new.say_hi # undefined
AnotherClass.say_hello # in ra Hello!
AnotherClass.say_hi # undefined
```

- Khi sử dụng include, các phương thức của module trở thành phương thức instance của class 
- Khi sử dụng extend, các phương thức của module trở thành phương thức class của class
