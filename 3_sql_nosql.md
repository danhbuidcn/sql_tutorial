# So sánh SQL và NoSQL

## Cấu trúc dữ liệu

### SQL

- **Cấu trúc cố định**: SQL sử dụng các bảng (tables) với cấu trúc hàng (rows) và cột (columns). Mỗi hàng đại diện cho một bản ghi và mỗi cột đại diện cho một thuộc tính của bản ghi.

- **Schemas rõ ràng**: Dữ liệu trong SQL có schemas xác định rõ ràng, nghĩa là bạn phải xác định trước cấu trúc dữ liệu (các bảng, các cột, các loại dữ liệu của cột) trước khi thêm dữ liệu vào.

- **Quan hệ**: SQL quản lý các mối quan hệ giữa các bảng thông qua các khóa ngoại (foreign keys) và hỗ trợ các phép nối (joins) phức tạp để truy vấn dữ liệu liên quan.

### NoSQL

- **Cấu trúc linh hoạt**: NoSQL hỗ trợ nhiều mô hình dữ liệu khác nhau như tài liệu (document), cột rộng (wide-column), đồ thị (graph), và giá trị khóa (key-value).

- **Schemas linh hoạt**: NoSQL không yêu cầu schemas cố định. Dữ liệu có thể được thêm vào mà không cần xác định trước cấu trúc, cho phép thay đổi cấu trúc dữ liệu dễ dàng.

- **Không quan hệ hoặc quan hệ nhẹ nhàng**: NoSQL thường không hỗ trợ các phép nối phức tạp. Các mối quan hệ giữa dữ liệu được quản lý ở cấp ứng dụng hoặc thông qua các cơ chế khác.

## Ngôn ngữ truy vấn

### SQL

- **Structured Query Language (SQL)**: SQL là ngôn ngữ truy vấn tiêu chuẩn được sử dụng để truy vấn và thao tác dữ liệu trong các cơ sở dữ liệu quan hệ. SQL có cú pháp mạnh mẽ cho việc tìm kiếm, lọc và xử lý dữ liệu.

- **Tối ưu hóa truy vấn**: Các hệ quản trị cơ sở dữ liệu SQL có các công cụ tối ưu hóa truy vấn để cải thiện hiệu suất.

### NoSQL

- **Ngôn ngữ truy vấn khác nhau**: NoSQL không có một ngôn ngữ truy vấn tiêu chuẩn như SQL. Mỗi loại cơ sở dữ liệu NoSQL có thể sử dụng một ngôn ngữ truy vấn riêng hoặc các API riêng để truy vấn dữ liệu.

- **Đơn giản hơn**: Truy vấn trong NoSQL thường đơn giản hơn và ít phức tạp hơn so với SQL, nhưng có thể không hỗ trợ các truy vấn phức tạp.

## Khả năng mở rộng

### SQL

- **Mở rộng theo chiều dọc (Vertical Scaling)**: SQL thường mở rộng bằng cách nâng cấp phần cứng máy chủ (CPU, RAM, ổ cứng).

- **Khó mở rộng theo chiều ngang (Horizontal Scaling)**: Mở rộng theo chiều ngang (thêm nhiều máy chủ) trong SQL khó hơn và phức tạp hơn, mặc dù có các giải pháp như phân mảnh (sharding) hoặc sử dụng các cơ sở dữ liệu phân tán.

### NoSQL

- **Mở rộng theo chiều ngang (Horizontal Scaling)**: NoSQL được thiết kế để dễ dàng mở rộng theo chiều ngang, cho phép thêm nhiều máy chủ để chia sẻ tải công việc và tăng khả năng xử lý.

- **Khả năng chịu lỗi cao**: NoSQL thường có khả năng chịu lỗi cao hơn với các cơ chế sao chép và phục hồi tự động.

## Tính nhất quán và độ tin cậy

### SQL

- **ACID Transactions**: SQL hỗ trợ các giao dịch ACID (Atomicity, Consistency, Isolation, Durability) để đảm bảo tính nhất quán và độ tin cậy của dữ liệu.

- **Tính nhất quán mạnh mẽ**: SQL cung cấp tính nhất quán mạnh mẽ, đảm bảo rằng tất cả các thay đổi dữ liệu đều được thực hiện hoặc không thực hiện gì cả.

### NoSQL

- **BASE Transactions**: NoSQL thường theo nguyên tắc BASE (Basically Available, Soft state, Eventual consistency), có nghĩa là dữ liệu có thể không nhất quán tức thời nhưng sẽ đạt được sự nhất quán cuối cùng.

- **Tính nhất quán linh hoạt**: NoSQL cho phép các cấu hình linh hoạt về tính nhất quán, cho phép tối ưu hóa hiệu suất và khả năng mở rộng.

## Sử dụng

### SQL

- **Các ứng dụng doanh nghiệp**: SQL thích hợp cho các ứng dụng doanh nghiệp, nơi dữ liệu có cấu trúc và yêu cầu tính nhất quán cao.

- **Hệ thống quản lý dữ liệu phức tạp**: SQL phù hợp cho các hệ thống quản lý dữ liệu phức tạp với nhiều mối quan hệ giữa các bảng.

### NoSQL

- **Dữ liệu phi cấu trúc hoặc bán cấu trúc**: NoSQL thích hợp cho việc lưu trữ dữ liệu phi cấu trúc hoặc bán cấu trúc như JSON, XML, dữ liệu đa phương tiện.

- **Ứng dụng web và di động hiện đại**: NoSQL phù hợp cho các ứng dụng web và di động hiện đại, nơi yêu cầu khả năng mở rộng và tính linh hoạt cao.

## Tổng kết

| Tiêu chí            | SQL                                               | NoSQL                                            |
|---------------------|---------------------------------------------------|--------------------------------------------------|
| **Cấu trúc dữ liệu**| Cấu trúc cố định (bảng, hàng, cột)                | Cấu trúc linh hoạt (document, key-value, column, graph) |
| **Schemas**         | Rõ ràng, xác định trước                           | Linh hoạt, không yêu cầu xác định trước          |
| **Ngôn ngữ truy vấn**| SQL (Structured Query Language)                 | Ngôn ngữ truy vấn hoặc API riêng                  |
| **Khả năng mở rộng**| Mở rộng theo chiều dọc, khó mở rộng ngang         | Mở rộng theo chiều ngang, dễ dàng                 |
| **Tính nhất quán**  | ACID Transactions, tính nhất quán mạnh mẽ         | BASE Transactions, tính nhất quán linh hoạt      |
| **Ứng dụng**        | Ứng dụng doanh nghiệp, quản lý dữ liệu phức tạp   | Ứng dụng web và di động hiện đại, dữ liệu phi cấu trúc |
