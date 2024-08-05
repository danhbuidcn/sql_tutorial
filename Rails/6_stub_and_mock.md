# Stub and Mock

Trong RSpec, stub và mock đều là các phương thức được sử dụng để thiết lập và kiểm soát hành vi của các đối tượng trong quá trình test automation.

Tuy nhiên, chúng có một số điểm khác nhau cơ bản:

```ruby
class Calculator
  def add(a, b)
    a + b
  end

  def multiply(a, b)
    a * b
  end
end
```

## Stub

Chức năng: Stub được sử dụng để thay thế hoặc giả lập một phương thức hoặc giá trị trả về từ một đối tượng.

Sử dụng: Thường được sử dụng khi bạn muốn kiểm soát giá trị trả về từ một phương thức mà không cần quan tâm đến việc phương thức đó được gọi hay không.

```ruby
# Trong ví dụ này, chúng ta sẽ sử dụng stub để thay thế hoặc giả lập giá trị trả về từ phương thức add của đối tượng Calculator mà không quan tâm đến việc phương thức này được gọi hay không.
require 'rspec'

RSpec.describe Calculator do
  let(:calculator) { Calculator.new }

  it 'adds two numbers' do
    # Stub phương thức add để trả về giá trị cố định
    allow(calculator).to receive(:add).and_return(5)

    result = calculator.add(2, 3)

    expect(result).to eq(5)
  end
end
```

## Mock

Chức năng: Mock được sử dụng để thiết lập và kiểm tra các expectation về hành vi của đối tượng trong quá trình chạy test.

Sử dụng: Thường được sử dụng khi bạn muốn kiểm tra xem một phương thức cụ thể đã được gọi và với các đối số nhất định.

```ruby
# Trong ví dụ này, chúng ta sẽ sử dụng mock để kiểm tra xem phương thức multiply của đối tượng Calculator đã được gọi với các đối số cụ thể hay không.
require 'rspec'

RSpec.describe Calculator do
  let(:calculator) { Calculator.new }

  it 'multiplies two numbers' do
    # Mock phương thức multiply và kiểm tra xem nó đã được gọi với các đối số cụ thể
    expect(calculator).to receive(:multiply).with(2, 3).and_return(6)

    result = calculator.multiply(2, 3)

    expect(result).to eq(6)
  end
end

```

## Tóm tắt

- Stub: Được sử dụng để thay thế giá trị trả về từ một phương thức hoặc đối tượng mà không quan tâm đến hành vi gọi.

- Mock: Được sử dụng để thiết lập và kiểm tra các expectation về hành vi gọi của một phương thức cụ thể.

- Sử dụng chủ yếu: Stub để giả lập giá trị trả về, mock để kiểm tra hành vi và đảm bảo logic trong test cases.

Khi viết unit test trong RSpec, bạn sẽ thường xuyên sử dụng cả hai kỹ thuật này để đảm bảo rằng các đơn vị code của bạn hoạt động như mong đợi và không bị ảnh hưởng bởi các thành phần bên ngoài (như database, network, ...).
