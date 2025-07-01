# 📌 Change Data Capture (CDC)

## ✅ CDC là gì?
**CDC (Change Data Capture)** là kỹ thuật theo dõi và ghi nhận **mọi thay đổi** (INSERT, UPDATE, DELETE) trong **cơ sở dữ liệu nguồn** để đồng bộ hoặc xử lý ở hệ thống khác theo **thời gian thực hoặc gần thực**.

---

## 🎯 Mục tiêu của CDC

- Đồng bộ dữ liệu giữa các hệ thống
- Kích hoạt xử lý sự kiện khi dữ liệu thay đổi
- Gửi dữ liệu thay đổi vào hệ thống streaming như **Kafka**

---

## ✅ Các phương pháp CDC phổ biến

| Phương pháp | Mô tả | Ưu điểm | Nhược điểm |
|-------------|-------|---------|------------|
| **1. Log-based CDC** | Đọc trực tiếp từ **transaction log (binlog, WAL...)** của database | - Hiệu năng cao<br>- Ít ảnh hưởng DB | - Cần hiểu sâu log nội bộ<br>- Không phải DB nào cũng hỗ trợ |
| **2. Trigger-based CDC** | Tạo **trigger trong database** để ghi lại thay đổi vào bảng log riêng | - Linh hoạt, tùy biến dễ | - Ảnh hưởng hiệu năng<br>- Phức tạp khi scale |
| **3. Timestamp-based CDC (Polling)** | Định kỳ kiểm tra bảng với điều kiện `updated_at > last_time` | - Đơn giản, dễ hiểu | - Không real-time<br>- Dễ bỏ sót hoặc trùng lặp |
| **4. Diff-based CDC** | So sánh dữ liệu giữa 2 snapshot | - Không cần can thiệp DB | - Chậm, tốn tài nguyên |
| **5. Middleware-based CDC (Outbox Pattern)** | Ứng dụng ghi thay đổi vào bảng trung gian (outbox), rồi push đi | - Kiểm soát logic tại ứng dụng | - Tốn công implement, không tự động 100% |

---

## 🔄 Ví dụ phân biệt

### 1. Log-based (MySQL binlog)

- **Công cụ**: Debezium, Maxwell, Kafka Connect
- **Mô tả**: MySQL ghi `UPDATE user SET name='A'` → Ghi vào binlog → Kafka đọc được ngay

---

### 2. Trigger-based

```sql
CREATE TRIGGER after_update_user
AFTER UPDATE ON users
FOR EACH ROW
INSERT INTO audit_log (table, action, data)
VALUES ('users', 'UPDATE', NEW.data);
```

### 3. Timestamp-based

```sql
SELECT * FROM orders WHERE updated_at > '2024-07-01 10:00:00';
```
Poll mỗi 5 phút, không real-time và dễ duplicate

### Các công cụ hỗ trợ CDC phổ biến
| Công cụ                                 | Hỗ trợ                         | Ghi chú                                |
| --------------------------------------- | ------------------------------ | -------------------------------------- |
| **Debezium**                            | MySQL, PostgreSQL, MongoDB,... | Dựa trên log-based, tích hợp tốt Kafka |
| **Maxwell**                             | MySQL                          | Nhẹ, log-based                         |
| **Kafka Connect JDBC + Timestamp mode** | Tất cả DB qua JDBC             | Polling                                |
| **Oracle GoldenGate**                   | Oracle DB                      | Enterprise-grade                       |
| **AWS DMS**                             | AWS database                   | Có chế độ CDC                          |


### Khi nào dùng phương pháp nào?
| Trường hợp                            | Khuyến nghị                         |
| ------------------------------------- | ----------------------------------- |
| Cần real-time, dữ liệu lớn            | ✅ Log-based (Debezium, Maxwell)     |
| Dễ tích hợp, không can thiệp hệ thống | ✅ Kafka Connect polling             |
| Không có quyền truy cập binlog        | ✅ Trigger-based hoặc Outbox Pattern |
| Làm đơn giản POC                      | ✅ Timestamp-based                   |


