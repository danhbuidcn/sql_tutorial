# Transactions

Transactions trong SQL là một khái niệm quan trọng, cho phép nhóm một loạt các câu lệnh SQL lại với nhau để chúng hoạt động như một đơn vị duy nhất. Nếu một phần của transaction thất bại, toàn bộ transaction có thể được hủy bỏ (rollback), đảm bảo rằng cơ sở dữ liệu luôn ở trong trạng thái nhất quán.

## Tính chất của Transactions (ACID)

### Atomicity (Tính nguyên tử):

Một transaction là một đơn vị nguyên tử của công việc; hoặc là tất cả các thay đổi của nó được thực hiện, hoặc là không có thay đổi nào được thực hiện.

### Consistency (Tính nhất quán):

Một transaction biến cơ sở dữ liệu từ một trạng thái nhất quán này sang một trạng thái nhất quán khác.

### Isolation (Tính cô lập):

Các transaction xảy ra độc lập với nhau. Kết quả của một transaction không được nhìn thấy bởi các transaction khác cho đến khi nó được commit.

### Durability (Tính bền vững):

Một khi một transaction đã được commit, các thay đổi của nó là vĩnh viễn, ngay cả khi có sự cố hệ thống.

## Cách sử dụng Transactions trong SQL

Dưới đây là cách cơ bản để bắt đầu, commit và rollback một transaction trong SQL:

- BEGIN TRANSACTION: Bắt đầu một transaction.
- COMMIT: Ghi vĩnh viễn các thay đổi được thực hiện bởi transaction.
- ROLLBACK: Hủy bỏ tất cả các thay đổi được thực hiện bởi transaction.

Giả sử chúng ta có hai bảng: accounts và transactions. Chúng ta muốn chuyển 100 đơn vị tiền từ tài khoản A sang tài khoản B.

```sql
BEGIN TRANSACTION;

-- Trừ 100 đơn vị tiền từ tài khoản A
UPDATE accounts
SET balance = balance - 100
WHERE account_id = 'A';

-- Thêm 100 đơn vị tiền vào tài khoản B
UPDATE accounts
SET balance = balance + 100
WHERE account_id = 'B';

-- Lưu thông tin giao dịch vào bảng transactions
INSERT INTO transactions (account_from, account_to, amount)
VALUES ('A', 'B', 100);

-- Nếu mọi thứ đều thành công, commit các thay đổi
COMMIT;
```

Nếu có lỗi xảy ra trong bất kỳ câu lệnh nào, chúng ta có thể rollback transaction để hoàn tác các thay đổi
```sql
BEGIN TRANSACTION;

-- Trừ 100 đơn vị tiền từ tài khoản A
UPDATE accounts
SET balance = balance - 100
WHERE account_id = 'A';

-- Kiểm tra lỗi trước khi thực hiện các thao tác tiếp theo
IF @@ERROR <> 0
BEGIN
    ROLLBACK;
    RETURN;
END

-- Thêm 100 đơn vị tiền vào tài khoản B
UPDATE accounts
SET balance = balance + 100
WHERE account_id = 'B';

-- Kiểm tra lỗi trước khi tiếp tục
IF @@ERROR <> 0
BEGIN
    ROLLBACK;
    RETURN;
END

-- Lưu thông tin giao dịch vào bảng transactions
INSERT INTO transactions (account_from, account_to, amount)
VALUES ('A', 'B', 100);

-- Kiểm tra lỗi trước khi commit
IF @@ERROR <> 0
BEGIN
    ROLLBACK;
    RETURN;
END

-- Nếu mọi thứ đều thành công, commit các thay đổi
COMMIT;
```

## Isolation Levels

SQL cung cấp các mức độ cô lập khác nhau để kiểm soát cách thức mà các transaction tương tác với nhau:

- `READ UNCOMMITTED`: Cho phép đọc dữ liệu chưa được commit từ các transaction khác. Điều này có thể dẫn đến "dirty reads".
- `READ COMMITTED`: Chỉ cho phép đọc dữ liệu đã được commit bởi các transaction khác. Điều này ngăn chặn "dirty reads".
- `REPEATABLE READ`: Đảm bảo rằng nếu một hàng được đọc hai lần trong cùng một transaction, kết quả sẽ giống nhau. Điều này ngăn chặn "non-repeatable reads" (đọc dữ liệu không đồng nhất).
- `SERIALIZABLE`: Mức độ cô lập cao nhất, đảm bảo rằng các transaction xảy ra một cách tuần tự, như thể chúng được thực hiện lần lượt. Điều này ngăn chặn "phantom reads".

Bạn có thể đặt mức độ cô lập của transaction bằng câu lệnh sau:
```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
BEGIN TRANSACTION;

-- Your SQL commands here

COMMIT;
```

`Transactions là một công cụ mạnh mẽ để đảm bảo tính nhất quán và độ tin cậy của cơ sở dữ liệu. Việc hiểu và sử dụng chúng đúng cách là rất quan trọng trong việc phát triển các ứng dụng cơ sở dữ liệu.`

----

`Dirty Read` (đọc bẩn) là một tình huống xảy ra trong cơ sở dữ liệu khi một transaction có thể đọc dữ liệu mà một transaction khác đã thay đổi nhưng chưa commit. Điều này có thể dẫn đến dữ liệu không nhất quán nếu transaction thực hiện thay đổi đó bị rollback (hủy bỏ).

### Ví dụ về Dirty Read

Giả sử chúng ta có hai transaction, T1 và T2, và một bảng tài khoản với các cột account_id và balance.

- Transaction T1 bắt đầu và cập nhật số dư tài khoản:
```sql
BEGIN TRANSACTION T1;
UPDATE accounts
SET balance = balance + 100
WHERE account_id = 'A';
```

- Transaction T2 bắt đầu và đọc số dư tài khoản trước khi T1 commit hoặc rollback:
```sql
BEGIN TRANSACTION T2;
SELECT balance
FROM accounts
WHERE account_id = 'A';
```

- Nếu T2 đọc số dư tại thời điểm này, nó sẽ thấy số dư đã được cập nhật bởi T1.

- Transaction T1 sau đó bị rollback:
```sql
ROLLBACK TRANSACTION T1;
```

- Bây giờ, số dư tài khoản A trở về trạng thái ban đầu, nhưng T2 đã đọc dữ liệu không nhất quán.

### Kết quả của Dirty Read

Dirty read dẫn đến tình huống không nhất quán, vì T2 đã đọc giá trị số dư mà không thực sự tồn tại sau khi T1 bị rollback. Điều này có thể gây ra các vấn đề nghiêm trọng trong ứng dụng, đặc biệt khi quyết định dựa trên dữ liệu không nhất quán.

### Ngăn chặn Dirty Read

Để ngăn chặn dirty read, cơ sở dữ liệu cần phải sử dụng mức độ cô lập cao hơn. Mức độ cô lập `Read Committed` hoặc cao hơn sẽ ngăn chặn dirty read bằng cách đảm bảo rằng chỉ các dữ liệu đã được commit mới có thể được đọc bởi các transaction khác.

```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
BEGIN TRANSACTION;

-- Các câu lệnh SQL của bạn

COMMIT;
```
