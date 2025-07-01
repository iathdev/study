## Laravel Lifecycle

### Request Flow

1. `public/index.php`
2. Autoload (Composer)
3. `Kernel.php`
4. Register Service Providers
5. Bootstrap Service Providers
6. Router
7. Middleware
8. Controller
9. Response / View

---

## Service Container

Là nơi quản lý class dependency và thực hiện dependency injection.

### Các kiểu binding:

* **Singleton binding**: instance chỉ được resolve một lần duy nhất trong suốt vòng đời ứng dụng.
* **Instance binding**: bind một instance cụ thể vào container.
* **Interface binding**: bind interface với implement tương ứng.

---

## Service Provider

Là trung tâm của việc khởi tạo tất cả các phần của ứng dụng Laravel, bao gồm các thành phần cốt lõi.

Bao gồm việc register:

* Service container binding
* Event listener
* Middleware
* Route

---

## Cơ chế thực thi của PHP

PHP là một ngôn ngữ lập trình **thông dịch**, nghĩa là mã PHP không được biên dịch trực tiếp thành mã máy, mà được thực thi bởi một trình **thông dịch PHP**.

### Quá trình thực thi mã PHP:

1. **Phân tích cú pháp (Lexical Analysis)**:

   * Mã nguồn PHP được phân tích thành các token: từ khóa, biến, toán tử...

2. **Phân tích cú pháp (Parsing)**:

   * Các token được tổ chức thành cây cú pháp (syntax tree).

3. **Biên dịch thành opcode (Intermediate Code)**:

   * Cây cú pháp được chuyển thành opcode – mã trung gian dùng cho trình thông dịch.

4. **Thực thi (Execution)**:

   * Opcode được thực thi trực tiếp. Trong PHP 8, một phần được JIT compile thành mã máy để tăng hiệu suất.

> **Ghi chú**: PHP sử dụng kỹ thuật **JIT (Just-in-Time)** từ phiên bản PHP 8 trở đi.

---

## OPcache (Operation Code Cache)

OPcache là cơ chế tối ưu hóa giúp **cache lại opcode** đã được biên dịch từ mã PHP để tăng hiệu năng.

### Lợi ích:

* **Không cần biên dịch lại**: Lưu lại opcode của các file PHP để tránh parse lại.
* **Tiết kiệm tài nguyên**: Giảm tải CPU do tránh phải phân tích cú pháp nhiều lần.
* **Cải thiện hiệu năng**: Đặc biệt trong hệ thống có nhiều request.

### Cách hoạt động:

* Lần đầu thực thi file PHP → biên dịch và lưu vào OPcache.
* Lần sau nếu file không thay đổi → dùng opcode đã cache.
* Khi file thay đổi → OPcache cập nhật lại opcode mới.

### Cấu hình php.ini:

```ini
; Bật OPcache
opcache.enable=1
opcache.memory_consumption=128
opcache.interned_strings_buffer=8
opcache.max_accelerated_files=10000
opcache.revalidate_freq=2
opcache.validate_timestamps=1
```

### Tóm tắt lợi ích:

* Giảm thời gian thực thi.
* Giảm tải CPU.
* Cải thiện khả năng mở rộng của hệ thống PHP.

OPcache là công cụ quan trọng giúp nâng cao hiệu suất cho các hệ thống PHP lớn như API hoặc website có nhiều người truy cập.
