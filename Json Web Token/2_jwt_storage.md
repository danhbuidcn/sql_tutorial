# Lưu trữ JSON Web Token

## 1. Local Storage

### Ưu điểm:

**Dễ sử dụng**: Local Storage đơn giản để lưu trữ và truy xuất dữ liệu từ JavaScript.

### Nhược điểm:

**Nguy cơ tấn công XSS**: Dữ liệu trong Local Storage có thể bị truy cập bởi các script độc hại, nếu trang web bị tấn công XSS (Cross-Site Scripting).

## 2. Session Storage

### Ưu điểm:

Phiên làm việc: Session Storage **chỉ tồn tại trong một phiên** làm việc của trình duyệt. 

Khi người dùng đóng tab hoặc cửa sổ, dữ liệu bị xóa. Điều này giúp giảm thời gian mà token có thể bị lộ.

### Nhược điểm:

**Nguy cơ tấn công XSS**: Như Local Storage, Session Storage cũng có nguy cơ bị truy cập bởi các script độc hại.

## 3. Cookies

### Ưu điểm:

HttpOnly Cookies: Nếu cookie được đánh dấu là HttpOnly, nó không thể được truy cập bởi JavaScript, giúp **bảo vệ khỏi tấn công XSS**.

**Secure Cookies**: Nếu cookie được đánh dấu là Secure, nó chỉ được gửi qua các kết nối HTTPS, tăng cường bảo mật.

Tự động gửi: Cookies được **gửi tự động** trong mỗi yêu cầu HTTP đến máy chủ cùng với các yêu cầu cùng miền.

### Nhược điểm:

**Nguy cơ tấn công CSRF**: Cookies có thể bị lợi dụng trong các cuộc tấn công Cross-Site Request Forgery (CSRF). 

Để bảo vệ, bạn có thể sử dụng các biện pháp phòng chống CSRF như thêm token xác thực vào yêu cầu hoặc sử dụng SameSite attribute cho cookie.

## So Sánh và Khuyến Nghị

`Local Storage `và `Session Storage`: Thích hợp cho các ứng dụng web yêu cầu truy cập dễ dàng và không cần gửi token tự động với mỗi yêu cầu. 
Tuy nhiên, bạn cần phải bảo vệ ứng dụng của mình khỏi các cuộc tấn công XSS.

`*Cookies*`: Thích hợp khi bạn muốn bảo mật hơn với việc bảo vệ token khỏi các cuộc tấn công XSS. 
Sử dụng HttpOnly và Secure attribute để giảm thiểu rủi ro. Đảm bảo thêm các biện pháp bảo vệ khỏi CSRF khi sử dụng cookies.

## Tóm Tắt

`Local Storage`: Phù hợp với những ứng dụng không quá nhạy cảm và khi bảo vệ chống XSS là khả thi.

`Session Storage`: Tốt cho các phiên làm việc tạm thời và khi không cần lưu trữ dữ liệu lâu dài.

`Cookies`: Đảm bảo bảo mật hơn nếu cấu hình chính xác (HttpOnly và Secure) và được dùng với các biện pháp chống CSRF.

Việc lựa chọn phương pháp lưu trữ JWT phụ thuộc vào mức độ bảo mật cần thiết cho ứng dụng của bạn và các nguy cơ bảo mật mà bạn có thể chấp nhận.
