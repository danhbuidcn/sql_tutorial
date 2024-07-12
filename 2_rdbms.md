# Relational Databases

- Cơ sở dữ liệu quan hệ là một hệ thống lưu trữ dữ liệu có cấu trúc sử dụng bảng để tổ chức thông tin. Dưới đây là một số điểm chính:
  + Bảng: Dữ liệu được lưu trữ trong các bảng. Mỗi bảng tương ứng với một loại thông tin cụ thể, ví dụ: một bảng cho thông tin người dùng và một bảng khác cho sản phẩm.

  + Cột: Mỗi bảng có các cột để đại diện cho các thuộc tính riêng biệt. Ví dụ: bảng người dùng có thể có các cột như "tên," "địa chỉ email," và "tuổi."

  + Hàng: Mỗi hàng trong bảng đại diện cho một mục cụ thể hoặc bản ghi. Ví dụ: một hàng trong bảng người dùng có thể chứa thông tin về một người dùng cụ thể, như tên, địa chỉ email và tuổi.

  + Khóa chính: Mỗi bảng có một cột hoặc một nhóm cột được xác định là khóa chính, giúp xác định một cách duy nhất từng hàng trong bảng.

  + Quan hệ: Dữ liệu trong các bảng có thể liên kết với nhau thông qua các quan hệ. Ví dụ: thông tin về một người dùng có thể được liên kết với các bản ghi trong bảng đơn hàng thông qua một trường chung như ID người dùng.

  + Câu truy vấn: Để truy xuất dữ liệu, chúng ta sử dụng ngôn ngữ truy vấn SQL để định rõ yêu cầu. Ví dụ: "SELECT tên FROM người dùng WHERE tuổi > 30" truy vấn tên của các người dùng có tuổi trên 30.

  + Tính toàn vẹn dữ liệu: Cơ sở dữ liệu quan hệ thường có các quy tắc để đảm bảo tính toàn vẹn dữ liệu, bao gồm ràng buộc duy nhất, ràng buộc khóa ngoại và các quy tắc kiểm tra.

`
Cơ sở dữ liệu quan hệ thường được sử dụng rộng rãi trong các ứng dụng và hệ thống để lưu trữ và quản lý dữ liệu một cách có tổ chức, dễ dàng truy xuất và tương tác.
`

# Lợi ích và hạn chế của RDBMS

## Ưu điểm:

- Tính toàn vẹn dữ liệu:
  + RDBMS thường áp dụng các ràng buộc để đảm bảo tính toàn vẹn dữ liệu, bao gồm ràng buộc duy nhất (unique constraints), ràng buộc khóa ngoại (foreign key constraints), và các quy tắc kiểm tra (check constraints).
  + Điều này giúp đảm bảo dữ liệu luôn đúng và nhất quán.

- ACID Transactions:
  + RDBMS hỗ trợ ACID (Atomicity, Consistency, Isolation, Durability) transactions, làm cho nó phù hợp cho các ứng dụng đòi hỏi độ tin cậy cao và tính nhất quán trong giao dịch dữ liệu.
  + Điều này đảm bảo rằng các thao tác trên dữ liệu sẽ được thực hiện đầy đủ hoặc không thực hiện gì cả, giúp bảo vệ dữ liệu khỏi các lỗi hệ thống.

- Dữ liệu có cấu trúc:
  + RDBMS sử dụng cấu trúc bảng để lưu trữ dữ liệu, giúp tổ chức dữ liệu một cách rõ ràng và dễ dàng truy xuất.
  + Các bảng liên kết với nhau thông qua các khóa ngoại, cho phép xây dựng các mối quan hệ phức tạp giữa các tập dữ liệu.

- Truy vấn mạnh mẽ:
  + SQL (Structured Query Language) cung cấp một cách mạnh mẽ để truy vấn và thao tác dữ liệu trong RDBMS.
  + Ngôn ngữ này có cú pháp cụ thể và mạnh mẽ cho việc tìm kiếm, lọc và xử lý dữ liệu.


- Quản lý dữ liệu phức tạp:
  + RDBMS thích hợp cho việc quản lý dữ liệu có mối quan hệ phức tạp và cần tổ chức dữ liệu một cách có cấu trúc.
  + Nó cho phép xây dựng các báo cáo và phân tích dữ liệu dễ dàng hơn.

- Bảo mật dữ liệu:
  + RDBMS cung cấp các cơ chế bảo mật mạnh mẽ, bao gồm quản lý quyền truy cập, mã hóa dữ liệu và kiểm soát truy cập chi tiết, giúp bảo vệ dữ liệu nhạy cảm.

# Hạn chế:

- Khó mở rộng theo chiều ngang:
  + RDBMS thường khó mở rộng khi cần xử lý tải cao hoặc có nhu cầu mở rộng theo chiều ngang (horizontal scalability).
  + Điều này có nghĩa là việc thêm nhiều máy chủ để chia sẻ tải công việc không phải lúc nào cũng dễ dàng hoặc khả thi.

- Không phù hợp cho dữ liệu không cấu trúc:
  + RDBMS không hiệu quả cho việc lưu trữ và truy xuất dữ liệu không có cấu trúc như dữ liệu văn bản không cấu trúc hoặc dữ liệu đa phương tiện.
  + Các hệ thống NoSQL thường phù hợp hơn cho loại dữ liệu này.

- Yêu cầu kiến thức phức tạp:
  + Sử dụng RDBMS đòi hỏi kiến thức về cơ sở dữ liệu và SQL, điều này có thể là một ngưỡng đối với người mới vào lĩnh vực này.
  + Việc thiết kế cơ sở dữ liệu và tối ưu hóa truy vấn đòi hỏi kinh nghiệm và kiến thức chuyên sâu.

- Có thể gặp vấn đề về hiệu suất:
  + Trong một số trường hợp, RDBMS có thể gặp khó khăn trong việc xử lý tải cao và yêu cầu tối ưu hóa để đảm bảo hiệu suất.
  + Việc tối ưu hóa chỉ số, cấu trúc bảng và truy vấn có thể trở nên phức tạp.

- Chi phí cao:
  + Một số RDBMS thương thúc đẩy chi phí cao, bao gồm giấy phép phần mềm và quản trị hệ thống.
  + Việc duy trì và quản lý một hệ thống RDBMS đòi hỏi nguồn lực tài chính và nhân sự đáng kể.

`
RDBMS cung cấp nhiều lợi ích vượt trội về quản lý dữ liệu chặt chẽ, bảo mật, và khả năng truy vấn mạnh mẽ, nhưng cũng có những hạn chế về hiệu suất, chi phí, và tính linh hoạt khi xử lý các khối lượng dữ liệu lớn hoặc dữ liệu phi cấu trúc. Việc lựa chọn sử dụng RDBMS hay một hệ quản trị cơ sở dữ liệu khác (như NoSQL) phụ thuộc vào yêu cầu cụ thể của ứng dụng và hệ thống của bạn.
`

https://viblo.asia/p/nhung-kien-thuc-co-ban-ve-sql-1-Yym40ngEL91
