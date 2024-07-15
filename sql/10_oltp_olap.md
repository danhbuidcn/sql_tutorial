# OLAP vs OLTP

## 1. Khái niệm

### OLAP (Online Analytical Processing)

- **Mục đích**: Hỗ trợ phân tích dữ liệu phức tạp, báo cáo và ra quyết định.
- **Tính chất**: Đọc nhiều, ghi ít, tập trung vào việc phân tích dữ liệu lịch sử.
- **Cấu trúc dữ liệu**: Thường sử dụng cấu trúc dữ liệu đa chiều, như bảng sự kiện (fact) và bảng thứ nguyên (dimension).
- **Ví dụ**: Hệ thống báo cáo doanh số bán hàng hàng tháng, phân tích hành vi khách hàng, dự báo tài chính.

### OLTP (Online Transaction Processing)

- **Mục đích**: Xử lý các giao dịch ngắn hạn, thời gian thực, đảm bảo tính toàn vẹn của dữ liệu.
- **Tính chất**: Ghi nhiều, đọc nhiều, tập trung vào việc xử lý giao dịch nhanh chóng và chính xác.
- **Cấu trúc dữ liệu**: Thường sử dụng cấu trúc dữ liệu quan hệ, các bảng được chuẩn hóa.
- **Ví dụ**: Hệ thống đặt hàng trực tuyến, hệ thống quản lý ngân hàng, hệ thống điểm bán hàng (POS).

## 2. So sánh chi tiết

| Tiêu chí                   | OLAP                                    | OLTP                                  |
|----------------------------|-----------------------------------------|---------------------------------------|
| Mục đích                   | Phân tích và báo cáo                    | Xử lý giao dịch                        |
| Dữ liệu                    | Lịch sử, dữ liệu tổng hợp               | Thời gian thực, dữ liệu chi tiết      |
| Hoạt động                  | Đọc nhiều, ghi ít                       | Đọc và ghi nhiều                      |
| Tốc độ phản hồi            | Chậm hơn (giây, phút)                   | Nhanh (mili giây, giây)               |
| Kích thước dữ liệu         | Lớn                                     | Nhỏ hơn                               |
| Độ phức tạp của truy vấn   | Phức tạp                                | Đơn giản                              |
| Thiết kế                   | Dữ liệu đa chiều (star, snowflake schema)| Dữ liệu quan hệ (3NF)                 |
| Khả năng mở rộng           | Khó mở rộng hơn                         | Dễ mở rộng                            |


## 3. Ví dụ Cụ Thể

### dụ về OLAP

Một công ty bán lẻ lớn muốn phân tích xu hướng mua sắm của khách hàng trong năm qua để lập kế hoạch cho các chiến dịch marketing trong tương lai. Họ sử dụng hệ thống OLAP để:
                                                                                                                                                                                                            - Tổng hợp doanh số bán hàng theo từng tháng, quý, và năm.
- Phân tích dữ liệu theo các chiều khác nhau như khu vực địa lý, loại sản phẩm, và kênh bán hàng.
- Tạo các báo cáo tổng hợp và biểu đồ để ra quyết định kinh doanh.

```sql
  -- Truy vấn OLAP ví dụ: Tổng hợp doanh số bán hàng theo tháng và khu vực
  SELECT
    region,
    MONTH(sale_date) AS sale_month,
    SUM(sales_amount) AS total_sales
  FROM
    sales_fact
  JOIN
    region_dimension ON sales_fact.region_id = region_dimension.region_id
  GROUP BY
    region, sale_month
  ORDER BY
    region, sale_month;
```

### Ví dụ về OLTP

Một cửa hàng trực tuyến xử lý hàng ngàn đơn đặt hàng mỗi ngày. Họ sử dụng hệ thống OLTP để:

- Ghi lại từng đơn hàng của khách hàng ngay khi được đặt.
- Cập nhật thông tin hàng tồn kho và xử lý thanh toán thời gian thực.
- Đảm bảo tính toàn vẹn dữ liệu và khả năng phục hồi trong trường hợp xảy ra sự cố.

```sql
-- Truy vấn OLTP ví dụ: Thêm một đơn đặt hàng mới
BEGIN TRANSACTION;

INSERT INTO orders (order_id, customer_id, order_date, status)
VALUES (12345, 67890, '2024-07-15', 'Pending');

INSERT INTO order_items (order_id, product_id, quantity, price)
VALUES (12345, 111, 2, 19.99);

UPDATE products
SET stock_quantity = stock_quantity - 2
WHERE product_id = 111;

COMMIT;
```
