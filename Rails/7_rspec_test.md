# Viết unit test với RSpec trong Rails

Viết unit test với RSpec trong Rails là một phần quan trọng trong quá trình phát triển phần mềm để đảm bảo rằng mã của bạn hoạt động như mong đợi và duy trì tính ổn định của hệ thống. Đây là một hướng dẫn cơ bản về cách viết unit test với RSpec trong môi trường Rails:

## Cách viết unit test

### 1. Cấu trúc của một test file

Mỗi model, controller, service, hoặc các đơn vị logic khác thường có một test file tương ứng. Ví dụ:

- `Models`: spec/models/model_name_spec.rb

- `Controllers`: spec/controllers/controller_name_spec.rb

- `Services`: spec/services/service_name_spec.rb

- `Libraries`: spec/lib/library_name_spec.rb

### 2. Cấu trúc cơ bản của một spec file

Một spec file bao gồm các khối sau:

- Setup: Chuẩn bị dữ liệu và điều kiện cần thiết trước khi chạy các test case.

- Test cases: Các test cases đánh giá các hành vi và kết quả của phần mềm.

Ví dụ đơn giản cho một model User:
```ruby
# spec/models/user_spec.rb
require 'rails_helper'

RSpec.describe User, type: :model do
  describe 'validations' do
    it 'is valid with valid attributes' do
      user = User.new(email: 'test@example.com', password: 'password')
      expect(user).to be_valid
    end

    it 'is not valid without an email' do
      user = User.new(password: 'password')
      expect(user).not_to be_valid
    end
  end

  describe 'associations' do
    it 'has many posts' do
      association = described_class.reflect_on_association(:posts)
      expect(association.macro).to eq :has_many
    end
  end

  describe 'custom methods' do
    it 'returns the full name' do
      user = User.new(first_name: 'John', last_name: 'Doe')
      expect(user.full_name).to eq 'John Doe'
    end
  end
end
```

### 3. Lưu ý khi viết unit test

- `RSpec DSL`: Sử dụng các DSL (Domain Specific Language) của RSpec như `describe`, `context`, `it`, `expect`, `before`, `let`, `subject` để tổ chức và viết test case.

- `Mocks và Stubs`: Sử dụng `allow` và `expect` để stub các phương thức và kiểm tra các gọi hàm (method calls) mong đợi.

- `Fixture và Factory`: Sử dụng FactoryBot để tạo dữ liệu giả lập cho các model.

- `Rails Helper`: Sử dụng `rails_helper` trong các spec file để tải toàn bộ cấu hình của Rails và RSpec.

- `Database Cleaner`: Sử dụng gem `database_cleaner` để làm sạch database giữa các test case.

- `Expectations`: Viết các expectations dễ đọc và mô tả chính xác các kết quả mong đợi từ hành vi của mã.

### 4. Chạy và theo dõi kết quả

- Sử dụng lệnh rspec hoặc bundle exec rspec để chạy tất cả các test case trong dự án.

- Đảm bảo rằng tất cả các test case đều pass và các kết quả mong đợi là như dự kiến.

# Test Double

- Test Double là các đối tượng giả lập được sử dụng trong kiểm thử phần mềm để thay thế các đối tượng thật trong một môi trường kiểm thử, giúp kiểm soát được các phản hồi và hành vi của các đối tượng này một cách dễ dàng.

- Có năm loại Test Double phổ biến:

## 1.Dummy

Thường được sử dụng để lấp đầy tham số của một hàm trong những case mà tham số đấy không được sử dụng nhằm tăng tốc test case.

```ruby
class Dummy
  define method1 excute_method2, very_complex_object
    if excute_method2
      method2 very_complex_object
    end
 end

 define method2 very_complex_object
   # excute some logic
 end
end

# Rspec
# Trong case excute_method2 = false very_complex_object không được sử dụng,
# method chỉ đơn giản return nil nên việc tạo ra 1 object phức tạp như
# thực tế là không cần thiết
...
describe ".method1" do
  it "should return nil" do
    dummy = double("dummy")
    expect(Dummy.new.method1(false, dummy)).to be_nil
  end
end
...
```

## 2.Stub

Được sử dụng để thay thế phương thức hoặc thuộc tính của một đối tượng để kiểm soát kết quả trả về.

```ruby
class Stub
  define method1
    if method2
      return "ok"
    end
 end

 define method2
   if condition
     # excute some logic
     return true
   else
     # excute some logic
     return false
   end
 end
end

# Rspec
# Ở đây mình stub method2 trả về true
...
describe ".method1" do
  it "should return ok" do
    stub = Stub.new
    allow(stub).to receive(:method2).and_return(true)
    expect(stub.method1).to eq "ok"
  end
end
...
```
## 3.Spy

Được sử dụng để theo dõi và ghi lại thông tin về cách mà một phương thức hoặc đối tượng được gọi trong quá trình kiểm thử.
Spy cho phép kiểm tra xem một phương thức đã được gọi bao nhiêu lần và với các đối số nào.

```ruby
class SomeCommand
  def call(arg:, other:)
    if arg <= 0
      logger.warn("args should be positive")
    else
      logger.debug("all fine")
    end
    # some logic
  end

  def logger
    Rails.logger
  end
end

describe SomeCommand
  let(:logger) { spy('Logger') }

  # stub method logger trả về spy logger
  before { allow(subject).to receive(:logger) { logger } }

  context 'with negative value' do
    it 'warns' do
      subject.call(arg: -1, other: 6)
      # verify việc ghi log
      expect(logger).to have_received(:warn).with("args should be positive")
      expect(logger).not_to have_received(:debug)
    end
  end

  context 'with positive value' do
    it 'logs as debug' do
      subject.call(arg: 1, other: 6)
      # verify việc ghi log
      expect(logger).not_to have_received(:warn)
      expect(logger).to have_received(:debug).with("all fine")
    end
  end
end

```

## 4.Mock

Tương tự như Spy, nhưng Mock còn bao gồm kiểm tra điều kiện xem một phương thức đã được gọi đúng cách với các đối số đúng.
Mock cung cấp các kỳ vọng cụ thể về việc gọi phương thức và đầu vào của nó.

```ruby
class Mock
  define test_key key
    if is_valid_key
      open_door key
    end
 end

 define open_door
   # some logic
   return "door is opened"
 end

 define valid_key? key
   # some logic
 end
end

# Rspec
...
describe ".test_key" do
  it "should return door is opened" do
    mock = Mock.new
    # Ở đây mình đang test case key valid nên sẽ mock method valid_key? trả về true
    expect(mock).to receive(:valid_key?).with("key") {true}
    expect(mock).to receive(:open_door).with("key") {"door is opened"}
    mock.test_key("key")
    expect(mock.test_key("key")).to eq "door is opened"
  end
end
...
```

## 5.Fake

các đối tượng thực sự có triển khai hoạt động, nhưng không được lưu trữ như trong thực tế (InMemoryTestDatabase là một ví dụ điển hình).

```ruby
# Fake object để thay thế một thành phần thực với một phiên bản đơn giản hóa
RSpec.describe InMemoryDatabase, type: :model do
  it "lưu các bản ghi trong bộ nhớ" do
    database = InMemoryDatabase.new
    record = build(:record)

    database.save(record)

    expect(database.all_records).to include(record)
  end
end
```
