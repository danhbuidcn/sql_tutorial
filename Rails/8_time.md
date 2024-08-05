# Time & Time zone

```ruby
Time.now.utc # trả về thời gian hiện tại theo múi giờ UTC, không bị ảnh hưởng bởi múi giờ của ứng dụng.

Time.now # trả về thời gian hiện tại theo múi giờ của hệ thống máy chủ (không phụ thuộc vào config.time_zone của Rails).

Time.current # trả về thời gian hiện tại theo múi giờ đã thiết lập trong ứng dụng Rails(config.time_zone).

Date.today # trả về ngày hiện tại theo múi giờ của hệ thống máy chủ.

Date.current # trả về ngày hiện tại theo múi giờ đã thiết lập trong ứng dụng Rails(config.time_zone).
```

# Phân biệt DateTime.now và DateTime.current

## `DateTime.now` 

Trả về một đối tượng DateTime với thời gian hiện tại, dựa trên múi giờ của hệ thống máy chủ, không phụ thuộc vào cấu hình múi giờ của ứng dụng Rails.

## `DateTime.current` 

Trả về một đối tượng DateTime với thời gian hiện tại theo múi giờ đã cấu hình trong ứng dụng Rails (config.time_zone).

`DateTime.current` là một alias cho `Time.zone.now`

## Nên sử dụng loại nào?

Sử dụng `DateTime.current` (hoặc `Time.current`):
  - Khi làm việc trong ứng dụng Rails: Đây là lựa chọn ưu tiên khi bạn cần đồng bộ hóa với múi giờ của ứng dụng Rails. Đảm bảo rằng các đối tượng thời gian của bạn được xử lý nhất quán với múi giờ của ứng dụng.

  - Khi bạn cần xử lý thời gian dựa trên múi giờ của ứng dụng: Ví dụ, khi hiển thị thời gian cho người dùng hoặc thực hiện các phép toán thời gian mà cần đồng bộ hóa với múi giờ của ứng dụng.

Sử dụng `DateTime.now`:
  - Khi làm việc ngoài Rails: Nếu bạn đang làm việc trong một môi trường Ruby không sử dụng Rails hoặc không quan tâm đến cấu hình múi giờ của ứng dụng, `DateTime.now` có thể là một lựa chọn.

  - Khi bạn muốn thời gian theo múi giờ của hệ thống máy chủ: Nếu ứng dụng của bạn không yêu cầu điều chỉnh múi giờ hoặc khi làm việc với hệ thống không hỗ trợ các tính năng múi giờ của Rails.

## Kết luận

Trong Rails: Nên sử dụng DateTime.current hoặc Time.current để đảm bảo rằng thời gian được xử lý theo cấu hình múi giờ của ứng dụng.

Ngoài Rails: DateTime.now có thể là lựa chọn nếu bạn không quan tâm đến múi giờ của ứng dụng hoặc đang làm việc trong môi trường không có cấu hình múi giờ.
