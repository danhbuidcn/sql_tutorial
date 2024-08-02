# Access Token và Refresh Token: Tổng Quan và Cơ Chế Hoạt Động

`Access Token và Refresh Token` là hai thành phần quan trọng trong cơ chế xác thực và ủy quyền, đặc biệt là trong các ứng dụng web sử dụng JSON Web Token (JWT).

## 1. Access Token

`Access Token` là một mã thông báo mà client (ứng dụng phía người dùng) sử dụng để truy cập tài nguyên được bảo vệ trên máy chủ. 

Thông thường, `Access Token` có thời hạn ngắn (vài phút đến vài giờ) để giảm thiểu rủi ro nếu bị đánh cắp.

Cơ chế hoạt động:

  - Xác thực ban đầu: Người dùng **đăng nhập** và cung cấp thông tin xác thực (như tên người dùng và mật khẩu).

  - Cấp phát Access Token: Nếu thông tin xác thực đúng, máy chủ **cấp một Access Token** cho client.

  - Sử dụng Access Token: **Client gửi Access Token** này trong mỗi yêu cầu để truy cập các tài nguyên được bảo vệ.

  - Xác minh Access Token: Máy chủ **xác minh Access Token** mỗi khi nhận được yêu cầu để đảm bảo tính hợp lệ và quyền truy cập của nó.

## 2. Refresh Token

`Refresh Token` là một mã thông báo mà client sử dụng để lấy một Access Token mới khi Access Token cũ hết hạn. 

`Refresh Token` có thời hạn dài hơn Access Token (có thể là vài ngày đến vài tháng).

Cơ chế hoạt động:

  - Cấp phát Refresh Token: Cùng với Access Token, máy chủ cũng **cấp một Refresh Token** cho client.
  
  - Lưu trữ Refresh Token: Client **lưu trữ Refresh Token** một cách an toàn (thường là trong bộ nhớ an toàn hoặc cookie).
  
  - Yêu cầu Access Token mới: Khi Access Token hết hạn, client sử dụng Refresh Token để **yêu cầu một Access Token** mới từ máy chủ.
  
  - Cấp phát Access Token mới: Nếu Refresh Token hợp lệ, máy chủ **cấp một Access Token mới** và có thể cấp một Refresh Token mới (nếu cần).
  
  - Hủy Refresh Token: Refresh Token có thể **bị hủy bất kỳ lúc nào** (ví dụ khi người dùng đăng xuất).

## 3. JWT (JSON Web Token)

JWT là một định dạng phổ biến cho `Access Token` và `Refresh Token`. 

Một JWT bao gồm ba phần: header, payload, và signature, được mã hóa thành chuỗi base64.

Header: Chứa thông tin về thuật toán mã hóa và loại token.
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```
Payload: Chứa các thông tin xác thực và các quyền hạn của người dùng.
```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true,
  "iat": 1516239022
}
```
Signature: Được tạo ra bằng cách mã hóa header và payload với một khóa bí mật.
```scss
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

## 4. Ưu điểm của Access Token và Refresh Token

- **Bảo mật cao**: Giảm thiểu rủi ro khi Access Token bị đánh cắp do thời hạn ngắn.

- **Hiệu quả**: Client không cần gửi thông tin xác thực liên tục, giảm tải cho máy chủ.

- **Trải nghiệm người dùng tốt hơn**: Người dùng không bị yêu cầu đăng nhập lại thường xuyên nhờ Refresh Token.

# Cơ Chế Xác Thực: Stateless và Stateful

## Stateless Authentication

`Stateless Authentication` không lưu trữ trạng thái phiên làm việc trên máy chủ. 

Thay vào đó, tất cả thông tin cần thiết để xác thực và ủy quyền được chứa trong token (thường là JWT).

### Ưu điểm:

- **Tính mở rộng cao**: Không cần lưu trữ trạng thái phiên làm việc trên máy chủ, dễ dàng mở rộng hệ thống bằng cách thêm máy chủ.

- **Giảm tải cho máy chủ**: Không cần duy trì phiên làm việc, giảm yêu cầu bộ nhớ và lưu trữ.

- **Độc lập máy chủ**: Yêu cầu có thể được xử lý bởi bất kỳ máy chủ nào trong cụm mà không cần chia sẻ trạng thái phiên.

### Nhược điểm:

- `Bảo mật`: Vì thông tin chứa trong token, nếu token bị đánh cắp, kẻ tấn công có thể sử dụng nó cho đến khi hết hạn.

- `Quản lý hạn sử dụng token`: Phải có cơ chế để làm mới hoặc hủy token khi cần thiết.

## Stateful Authentication

`Stateful Authentication` lưu trữ trạng thái phiên làm việc trên máy chủ. 

Máy chủ duy trì thông tin phiên làm việc của người dùng và sử dụng ID phiên để xác định và truy xuất thông tin này.

### Ưu điểm:

- `Bảo mật`: Thông tin phiên không chứa trong token, giảm rủi ro khi token bị đánh cắp.

- `Kiểm soát phiên tốt hơn`: Có thể hủy phiên làm việc bất kỳ lúc nào từ phía máy chủ.

### Nhược điểm:

- `Khó mở rộng`: Cần chia sẻ trạng thái phiên giữa các máy chủ, có thể phức tạp khi hệ thống mở rộng.

- `Yêu cầu lưu trữ`: Máy chủ cần duy trì và quản lý phiên làm việc, tăng yêu cầu về bộ nhớ và lưu trữ.

# Nơi Lưu Trữ Access Token và Refresh Token

## Access Token:

- `Bộ nhớ tạm thời (Session Storage)`: Phù hợp cho các ứng dụng web, Access Token chỉ tồn tại trong phiên làm việc của trình duyệt.

- `Local Storage`: Cũng là một tùy chọn, nhưng ít an toàn hơn do có thể bị tấn công XSS.

- `Memory`: Lưu trữ trong bộ nhớ của ứng dụng (đối với các ứng dụng single-page).

## Refresh Token:

- `HttpOnly Cookies`: An toàn hơn do không thể truy cập bằng JavaScript, giảm nguy cơ tấn công XSS.

- `Secure Cookies`: Chỉ được gửi qua các kết nối HTTPS, tăng tính bảo mật.

- `Server-side Storage`: Lưu trữ trên máy chủ, có thể yêu cầu một cơ chế quản lý phiên làm việc (cơ chế stateful).

# Khi Nào Sử Dụng Stateless và Stateful

## Stateless:

- Khi cần **tính mở rộng** cao và có nhiều máy chủ.

- Khi muốn giảm tải cho máy chủ và **không cần quản lý trạng thái phiên làm việc**.

## Stateful:

- Khi yêu cầu **bảo mật cao** và **kiểm soát phiên làm việc chặt chẽ**.

- Khi hệ thống không cần mở rộng quá lớn hoặc có cơ chế chia sẻ trạng thái phiên hiệu quả.

# Kết Luận

- `Stateless` sử dụng `Access Token` để xác thực mà không cần lưu trữ trạng thái phiên làm việc trên máy chủ.

- `Stateful` sử dụng `Refresh Token` lưu trữ trạng thái phiên làm việc trên máy chủ, yêu cầu quản lý phiên làm việc và bảo mật hơn.

Việc lựa chọn giữa `stateless` và `stateful` phụ thuộc vào yêu cầu cụ thể của hệ thống và mức độ ưu tiên về bảo mật, khả năng mở rộng và hiệu quả hoạt động.
