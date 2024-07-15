# Aggregate Queries (Truy vấn tổng hợp)

Truy vấn tính toán tổng hợp được sử dụng để thực hiện các phép tính trên một tập hợp giá trị và trả về một giá trị duy nhất.
Các truy vấn này thường bao gồm việc sử dụng các hàm tổng hợp, là các hàm tích hợp hoạt động trên nhiều hàng của một bảng để trả về một kết quả duy nhất.
Dưới đây là một số hàm tổng hợp phổ biến trong SQL:

## Các Hàm Tổng Hợp Phổ Biến

### 1. COUNT()

Đếm số lượng bản ghi trong một cột của bảng dữ liệu.

```sql
SELECT COUNT(*) AS tong_hang
FROM nhanvien;
```

### 2.SUM()

Được sử dụng để tính tổng các giá trị trong một cột số của bảng dữ liệu.

```sql
SELECT SUM(luong) AS tong_luong
FROM nhanvien;
```

### 3.AVG()

Trả về giá trị trung bình của các giá trị trong một cột số.

```sql
SELECT AVG(luong) AS luong_trung_binh
FROM nhanvien;
```

### 4.MIN()

Trả về giá trị nhỏ nhất trong một tập hợp

```sql
SELECT MIN(luong) AS luong_nho_nhat
FROM nhanvien;
```

### 4.MAX()

Trả về giá trị lớn nhất trong một tập hợp

```sql
SELECT MAX(luong) AS luong_nho_nhat
FROM nhanvien;
```

## Sử Dụng Hàm Tổng Hợp với GROUP BY

### Mệnh đề GROUP BY

Được sử dụng để sắp xếp dữ liệu giống nhau thành các nhóm, thường được sử dụng với các hàm tổng hợp để thực hiện các phép tính trên từng nhóm dữ liệu.

```sql
SELECT phongban_id, AVG(luong) AS luong_trung_binh
FROM nhanvien
GROUP BY phongban_id;
```

### Mệnh Đề HAVING

Mệnh đề `HAVING` được sử dụng để lọc các bản ghi dựa trên dữ liệu đã tổng hợp, giống như mệnh đề `WHERE` nhưng sử dụng với các hàm tổng hợp.

```sql
SELECT phongban_id, COUNT(*) AS tong_nhanvien
FROM nhanvien
GROUP BY phongban_id
HAVING COUNT(*) > 10;
```

## Kết Hợp Các Hàm Tổng Hợp

Bạn có thể kết hợp nhiều hàm tổng hợp trong một truy vấn để thực hiện các tính toán khác nhau trên cùng một tập dữ liệu.

```sql
SELECT phongban_id,
       COUNT(*) AS tong_nhanvien,
       AVG(luong) AS luong_trung_binh,
       SUM(luong) AS tong_luong
FROM nhanvien
GROUP BY phongban_id;
```

### Tính Toán Tổng Hợp với DISTINCT

Bạn có thể sử dụng từ khóa `DISTINCT` trong một hàm tổng hợp để chỉ xem xét các giá trị duy nhất trong phép tính.

```sql
SELECT COUNT(DISTINCT phongban_id) AS phongban_duc_dao
FROM nhanvien;
```

### Truy Vấn Tổng Hợp Nâng Cao

- Các Hàm Tổng Hợp Lồng Nhau

```sql
-- Tìm phòng ban có mức lương trung bình cao nhất
SELECT phongban_id, AVG(luong) AS luong_trung_binh
FROM nhanvien
GROUP BY phongban_id
ORDER BY luong_trung_binh DESC
LIMIT 1;
```

- Tính Toán Tổng Hợp với Các Lệnh Join

```sql
-- Tính tổng lương cho mỗi phòng ban bằng cách join hai bảng
SELECT p.tenphongban, SUM(n.luong) AS tong_luong
FROM nhanvien n
JOIN phongban p ON n.phongban_id = p.phongban_id
GROUP BY p.tenphongban;
```
