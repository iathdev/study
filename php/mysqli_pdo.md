# So sánh chi tiết: MySQLi vs PDO

| **Tiêu chí**                             | **MySQLi**                                                    | **PDO (PHP Data Objects)**                                       |
| ---------------------------------------- | ------------------------------------------------------------- | ---------------------------------------------------------------- |
| **Hỗ trợ CSDL**                          | Chỉ hỗ trợ **MySQL**                                          | Hỗ trợ **12+ CSDL**: MySQL, PostgreSQL, SQLite, Oracle, MSSQL... |
| **API**                                  | Hỗ trợ **2 kiểu**: Procedural & Object-Oriented               | Chỉ hỗ trợ **Object-Oriented**                                   |
| **Khả năng chuyển đổi DB dễ không?**     | **Khó**, vì phụ thuộc MySQL-specific functions                | **Dễ**, chỉ đổi chuỗi DSN                                        |
| **Named parameters trong query**         | ❌ Không hỗ trợ                                                | ✅ Có (`:name`, `:email`, ...)                                    |
| **Prepared statements**                  | ✅ Có – nhưng cú pháp khác nhau giữa Procedural/OOP            | ✅ Có – cú pháp đồng nhất và đơn giản hơn                         |
| **Hiệu suất (trên MySQL)**               | Gần như tương đương với PDO nếu chỉ dùng MySQL                | Gần tương đương – nhưng có thêm overhead do abstraction          |
| **Tính năng bind parameters**            | ✅ Có (`bind_param()`) – nhưng cần đúng thứ tự và kiểu dữ liệu | ✅ Có (`bindParam()` hoặc truyền mảng) – hỗ trợ **named params**  |
| **Hỗ trợ stored procedures**             | ✅ Có                                                          | ✅ Có                                                             |
| **Support Multi Queries (multi\_query)** | ✅ Có                                                          | ❌ Không hỗ trợ                                                   |
| **Cách xử lý lỗi**                       | Qua `mysqli_error()` hoặc `$conn->error`                      | Dùng `try-catch` & `PDOException`, tốt hơn cho logging           |
| **Hỗ trợ transactions**                  | ✅ Có (`begin_transaction`, `commit`, `rollback`)              | ✅ Có (`beginTransaction`, `commit`, `rollBack`)                  |
| **Tự động escaping dữ liệu**             | ❌ Không – cần dùng `mysqli_real_escape_string()`              | ❌ Không – cần dùng `bindParam()` hoặc `quote()`                  |
| **Fetch dữ liệu linh hoạt**              | Ít hơn – thường trả về dạng `mysqli_fetch_assoc()`            | Nhiều tùy chọn: `fetch()`, `fetchAll()`, `fetchObject()`         |
| **Documentation & Community**            | Rộng – vì phổ biến từ lâu                                     | Rộng – nhưng có thể ít người mới quen hơn                        |
