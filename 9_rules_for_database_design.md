# 31 Quy tắc trong thiết kế Cơ sở dữ liệu

## Quy tắc 1
Không thể có nhiều giá trị trong 1 cột trong 1 bản ghi. Ví dụ: Mr Vinh có 3 số điện thoại nhưng bản ghi của Mr Vinh không nên có 1 cột Telephone với 3 giá trị trong đó.

## Quy tắc 2
Càng ít bảng càng tốt.

## Quy tắc 3
Khóa không nên dài quá. Nếu bạn đang thử quyết định giữa xác định 1 khóa với 2 cột (ví dụ Mã SV và Email) và 1 khóa với 1 cột (ví dụ Mã SV), cả 2 đều xác định duy nhất 1 dòng trong bảng, hãy lựa chọn khóa ngắn hơn trong 2 khóa. Khi định nghĩa 1 khóa, bạn cần chắc chắn rằng tập hợp thông tin này là cần và đủ để xác định 1 hàng, không nên có thêm hoặc ít hơn thông tin.

## Quy tắc 4
Sử dụng tên được xác định rõ và phù hợp cho các bảng và cột (ví dụ như trong bảng student: student_id thay vì chỉ dùng id).

## Quy tắc 5
Sử dụng số ít cho tên bảng (ví dụ student thay thế cho students). Bảng thể hiện cho 1 tập các thực thể, không cần thiết phải sử dụng số nhiều.

## Quy tắc 6
Không dùng khoảng trắng cho tên bảng. Tên bảng viết thường, nếu có nhiều hơn 1 từ thì sử dụng dấu gạch dưới, ví dụ: user_group, order_detail,…

## Quy tắc 7
Không sử dụng tiền tố hoặc hậu tố không cần thiết cho tên bảng (ví dụ đặt là student thay cho tblstudent, studenttable…).

## Quy tắc 8
Giữ mật khẩu được mã hóa để đảm bảo tính bảo mật. Giải mã mật khẩu trong ứng dụng nếu cần thiết.

## Quy tắc 9
Sử dụng khóa chính là số nguyên trong mọi bảng. Nếu không có, hãy tạo một trường id để làm khóa chính.

## Quy tắc 10
Lựa chọn các cột có kiểu giá trị số nguyên để đánh index. Đánh index trường có kiểu dữ liệu ký tự có thể sẽ gây ra các vấn đề về hiệu năng.

## Quy tắc 11
Sử dụng các trường bit để lưu các giá trị boolean. Trường số nguyên hoặc ký tự là không cần thiết để lưu trữ trong trường hợp này. Với các trường này nên đặt tên với tiền tố “is_”.

## Quy tắc 12
Cung cấp cơ chế xác thực khi truy cập CSDL. Không gán quyền admin cho mọi người dùng.

## Quy tắc 13
Tránh sử dụng truy vấn “SELECT *” nếu không thực sự cần thiết. Sử dụng truy vấn “SELECT {tên cột cần lấy}” để đảm bảo hiệu năng tốt hơn.

## Quy tắc 14
Với các hệ thống CSDL lớn, nhạy cảm nên sử dụng các dịch vụ bảo mật và khôi phục sau thảm họa như failover clustering, sao lưu tự động, nhân rộng …

## Quy tắc 15
Sử dụng các ràng buộc (khóa ngoại, kiểm tra, not null…) để đảm bảo toàn vẹn dữ liệu. Không nên đưa toàn bộ các ràng buộc này kiểm soát trên mã ứng dụng.

## Quy tắc 16
Không được thiếu tài liệu CSDL. Tài liệu hóa thiết kế CSDL với lược đồ ER và hướng dẫn. Đồng thời viết các dòng ghi chú (comment lines) cho các triggers, procedure và các scripts khác

## Quy tắc 17
Sử dụng index cho các truy vấn được dùng thường xuyên với bảng dữ liệu lớn. Các công cụ phân tích có thể được dùng để xác định cần đặt index tại đâu. Với truy vấn cho kết quả là nhiều dòng thì sử dụng clustered index sẽ tốt hơn, với truy vấn cho kết quả là 1 dòng thì sử dụng non clustered sẽ tốt hơn.

## Quy tắc 18
Máy chủ CSDL và máy chủ web nên để riêng biệt trên 2 server vật lý. Việc này sẽ đảm bảo bảo mật hơn (kẻ tấn công không thể tấn công trực tiếp dữ liệu). Hiệu năng bộ nhớ và CPU của server sẽ tốt hơn do giảm tải số lượng yêu cầu và các tiến trình xử lý.

## Quy tắc 19
Các cột dữ liệu blob và image không nên định nghĩa trong các bảng thường xuyên truy vấn do vấn đề hiệu năng. Những dữ liệu này phải được đặt tại các bảng riêng và chúng sẽ được trỏ tới từ bảng được truy vấn.

## Quy tắc 20
Chuẩn hóa là cần thiết để tối ưu hiệu năng. Chuẩn hóa ở mức thấp sẽ gây ra vấn đề dư thừa dữ liệu, chuẩn hóa quá sâu sẽ gây ra vấn đề join ở quá nhiều bảng. Cả 2 loại chuẩn hóa trên đều gây ra các vấn đề về hiệu năng.

## Quy tắc 21
Dành thời gian nhiều nhất có thể cho việc thiết kế và mô hình hóa CSDL. Việc thiết kế sơ sài sẽ dẫn đến mất nhiều thời gian cho sửa đổi và bảo trì sau này.

## Quy tắc 22
Giữ khóa chính ít ký tự hơn hoặc số nguyên. Xử lý sẽ tốt hơn với khóa chính nhỏ.

## Quy tắc 23
Lưu trữ đường dẫn hình ảnh trong CSDL thay cho hình ảnh sẽ giúp giảm tải.

## Quy tắc 24
Dùng các kiểu dữ liệu hợp lý cho các trường. Ví dụ: Ngày sinh nên để datetime thay vì varchar

## Quy tắc 25
Sử dụng mệnh đề LIKE chính xác. Nếu bạn tìm kiếm chính xác thì sử dụng “=” thay thế.

## Quy tắc 26
Sử dụng JOIN sẽ tốt hơn cho hiệu năng so với sử dụng các truy vấn con hoặc truy vấn lồng nhau.

## Quy tắc 27
Sử dụng các stored procedure sẽ giúp nhanh hơn, bảo mật hơn và bảo trì tốt hơn.

## Quy tắc 28
Viết các ghi chú để hướng dẫn các cán bộ phát triển sau. Tài liệu hóa cũng là cách tốt để giúp đỡ họ.

## Quy tắc 29
Đánh index hợp lý sẽ giúp cải tiến tốc độ và hoạt động của CSDL.

## Quy tắc 30
Đảm bảo có thể test được toàn bộ các chương trình liên quan đến CSDL.

## Quy tắc 31
Viết từ khóa SQL bằng chữ in hoa để dễ đọc
