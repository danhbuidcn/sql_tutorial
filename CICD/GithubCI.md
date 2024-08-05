- Github CI flow

```
Run RSpec:
  - Đây là một job trong quy trình CI chạy test RSpec của ứng dụng Rails của bạn.

Setup Job:
  - Bước này chuẩn bị môi trường chạy job bằng cách cấu hình các thông số cần thiết như hệ điều hành, image Docker, hoặc các biến môi trường.

Initialize Container:
  - Tạo và khởi chạy container Docker để chạy các bước trong job.
  
Checkout Code:
  - Lấy mã nguồn của ứng dụng từ kho lưu trữ Git.

Setup System Package:
  - Cài đặt các gói phần mềm hệ thống cần thiết để chạy ứng dụng của bạn. Điều này có thể bao gồm cài đặt các gói phụ thuộc, công cụ cần thiết, hoặc các thiết lập môi trường.

Setup Database:
  - Cấu hình và chuẩn bị cơ sở dữ liệu cho việc chạy test. Trong trường hợp của bạn, đây là bước cấu hình kết nối đến máy chủ MySQL.

Run RSpec:
  - Chạy các bài kiểm tra RSpec của ứng dụng.

Post Setup System Package:
  - Hoàn tất việc cài đặt các gói phần mềm hệ thống và thiết lập môi trường sau khi test đã hoàn thành.

Post Checkout Code:
  - Hoàn tất việc lấy mã nguồn của ứng dụng từ kho lưu trữ Git.

Stop Container:
  - Dừng và xóa container Docker đã sử dụng trong quy trình CI.

Complete Job:
  - Kết thúc job và báo cáo kết quả.
```