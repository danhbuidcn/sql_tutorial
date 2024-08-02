# Trigger là gì?

Trigger là một cơ chế cho phép thực hiện một đoạn mã (SQL) tự động khi có một sự kiện xảy ra trong cơ sở dữ liệu.

Các sự kiện này có thể là INSERT, UPDATE, hoặc DELETE.

## 1. Trigger trong SQL

Ví dụ: Giả sử bạn có một bảng orders và bạn muốn tự động cập nhật trường updated_at của bảng customers mỗi khi một đơn hàng mới được thêm vào bảng orders.

```SQL
DELIMITER //

CREATE TRIGGER update_customer_timestamp
AFTER INSERT ON orders
FOR EACH ROW
BEGIN
  UPDATE customers
  SET updated_at = NOW()
  WHERE customers.id = NEW.customer_id;
END//

DELIMITER ;
```

Giải thích:

- AFTER INSERT: Trigger này sẽ kích hoạt sau khi một bản ghi mới được chèn vào bảng orders.
- FOR EACH ROW: Trigger sẽ chạy cho mỗi bản ghi mới được chèn.
- UPDATE customers: Trigger sẽ cập nhật trường updated_at của bảng customers dựa trên customer_id của đơn hàng mới (NEW.customer_id).

## 2. Callback trong Rails

Ví dụ: Bây giờ, hãy thực hiện tương tự trong Rails bằng cách sử dụng callback.

Mô hình Rails
Giả sử bạn có hai model Order và Customer.

```ruby
class Order < ApplicationRecord
  belongs_to :customer
  after_create :update_customer_timestamp

  private

  def update_customer_timestamp
    customer.touch(:updated_at)
  end
end

class Customer < ApplicationRecord
  has_many :orders
end
```

Giải thích:

- after_create: Đây là callback của Rails, nó sẽ được gọi sau khi một bản ghi Order mới được tạo.
- customer.touch(): Phương thức touch của ActiveRecord sẽ cập nhật trường updated_at của Customer tương ứng.
- touch() sử dụng thời gian của hệ thống, cụ thể là thời gian đã được thiết lập theo múi giờ của ứng dụng Rails (time_zone)

## 3.So sánh Trigger SQL và Callback Rails

Trigger SQL: 
- Được thực thi ở cấp độ cơ sở dữ liệu, độc lập với ứng dụng. 
- Trigger hoạt động ngay cả khi bạn thực hiện thao tác trên cơ sở dữ liệu mà không thông qua ứng dụng Rails. Điều này rất hữu ích trong các hệ thống lớn, nơi logic này cần được đảm bảo ngay cả khi có nhiều ứng dụng hoặc hệ thống truy cập cơ sở dữ liệu.

Callback Rails: 
- Được thực hiện trong tầng ứng dụng, giúp dễ dàng bảo trì và quản lý. 
- Tuy nhiên, callback chỉ hoạt động khi bạn thực hiện thao tác thông qua ứng dụng Rails. Nếu có các thao tác trực tiếp trên cơ sở dữ liệu ngoài ứng dụng, callback sẽ không được gọi.

## 4.Khi nào sử dụng Trigger và Callback

Trigger SQL: 
- Khi bạn cần logic được thực thi bất kể nguồn gốc của thao tác (dù từ ứng dụng hay trực tiếp từ cơ sở dữ liệu).

Callback Rails: 
- Khi bạn muốn logic xử lý gắn liền với vòng đời của model và đảm bảo rằng nó dễ hiểu và bảo trì trong ứng dụng Rails.
