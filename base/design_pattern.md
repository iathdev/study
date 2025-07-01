# Design Pattern – Phân nhóm & Ví dụ

## 1. Nhóm khởi tạo (Creational Patterns)

**Mục tiêu**: Tách việc khởi tạo đối tượng ra khỏi phần sử dụng.

### 1.1 Factory Pattern

- Tạo đối tượng từ lớp cha nhưng để lớp con quyết định loại cụ thể.
- ✅ Giảm phụ thuộc vào class cụ thể
- ✅ Tăng tính mở rộng
- ✅ Dễ bảo trì

**Ví dụ**:

- Vé sử dụng nhiều cách: Button, QR...
- Item có nhiều loại: vé cổng vào, vé đặt chỗ...

---

### 1.2 Builder Pattern

- Xây dựng đối tượng phức tạp theo từng bước một.
- ✅ Chia nhỏ quá trình khởi tạo
- ✅ Dễ quản lý và bảo trì
- ✅ Không cần khởi tạo toàn bộ các thuộc tính

**Ví dụ**:

- Tạo class giống model để lấy dữ liệu từ OpenSearch
- Eloquent trong Laravel

---

### 1.3 Singleton Pattern

- Đảm bảo 1 class chỉ có duy nhất 1 instance trong suốt lifecycle.

**Ví dụ**:

- Kết nối database
- HTTP client gọi đến bên thứ 3

---

## 2. Nhóm cấu trúc (Structural Patterns)

**Mục tiêu**: Tổ chức các object để xây dựng cấu trúc phức tạp hơn.

### 2.1 Adapter Pattern

- Cho phép interface không tương thích làm việc cùng nhau.
- Dùng khi cần chuyển đổi / nâng cấp hệ thống.

**Ví dụ**:

- Hệ thống EmailService cũ → chuyển sang AraraMail mới.
- Tạo AWSMailAdapter implement EmailServiceInterface:
  - `sendMail()` → gọi `SendEmailAWS::send()`

---

### 2.2 Decorator Pattern

- Thêm hành vi (chức năng) mới vào đối tượng hiện có **mà không sửa đổi nó**.

**Ví dụ**:

- Hệ thống bán vé: thêm combo bỏng, nước...

---

## 3. Nhóm hành vi (Behavioral Patterns)

**Mục tiêu**: Tối ưu hóa việc giao tiếp và phân công trách nhiệm giữa các đối tượng.

### 3.1 Chain of Responsibility

- Cho phép dữ liệu đi qua chuỗi các bước xử lý (class riêng biệt).

**Lợi ích**:

- Tách biệt rõ logic
- Dễ mở rộng

**Ví dụ**:

- Middleware
- Pipeline tìm kiếm:
```php
  $criteria = $this->filterCriteria(conditions: $conditions);
  return app(Pipeline::class)
      ->send($query)
      ->through($criteria)
      ->thenReturn();
```

### 3.2 Command Pattern

- Biến một yêu cầu thành đối tượng chứa thông tin của yêu cầu đó.
- Đối tượng này được sử dụng làm đầu vào cho class xử lý.
- Mục tiêu: Biến hành vi thành object và truyền vào (`__construct()`) của class xử lý.

**Ưu điểm:**

- Phân chia rõ ràng các hành động cần xử lý
- Dễ dàng tái sử dụng, mở rộng hành vi

**Ví dụ:**

- Hành động tắt & bật đèn có thể được biểu diễn thành object (`TurnOnCommand`, `TurnOffCommand`) và truyền vào class `RemoteControl`.

---

### 3.3 Observer Pattern

- Cho phép nhiều đối tượng nhận thông báo về sự kiện mà chúng quan tâm.
- Hỗ trợ tách rời publisher (người phát sự kiện) và subscriber (người nhận sự kiện).

**Ưu điểm:**

- Tách biệt code
- Giảm sự phụ thuộc giữa bên phát và bên nhận

**Ví dụ:**

- Laravel Event – Listener
- Ứng dụng Chat: khi có tin nhắn mới thì mọi người trong phòng cùng nhận được

---

### 3.4 State Pattern

- Cho phép một đối tượng thay đổi hành vi khi trạng thái của nó thay đổi.

**Ví dụ:**

- Hệ thống giao hàng:
  - Trạng thái: `chưa giao` → shipper có thể thao tác
  - Trạng thái: `đã nhận` → shipper không thể thao tác

---

### 3.5 Strategy Pattern

- Xác định một tập hợp các hành vi tương tự nhau, mỗi hành vi là một class riêng biệt dùng chung interface.
- Các chiến lược có thể được hoán đổi **runtime**.

**Ưu điểm:**

- Thay đổi linh hoạt hành vi mà không ảnh hưởng tới logic chính
- Tăng khả năng mở rộng và bảo trì

**Ví dụ:**

- Các phương thức thanh toán: `COD`, `Momo`, `Paypal`, ...
- Laravel hỗ trợ nhiều driver Cache: `redis`, `file`, `memcache`, ...

---

### 3.6 Dependency Injection (DI)

**Bài toán thực tế:** Bóng đèn – đui đèn

- Đại diện cho nguyên lý **Composition over Inheritance**.
- Một đối tượng nên được tạo thành từ các thành phần bên ngoài thay vì khởi tạo bên trong.

**Ưu điểm:**

- Dễ viết unit test thông qua mocking
- Giảm ràng buộc, tăng khả năng mở rộng
- Dễ dàng thay thế các dependency (implementation)

**Ứng dụng:**

- Áp dụng rộng rãi trong framework hiện đại như Laravel, Spring Boot.

---

### Data Transfer Object (DTO)

**Ưu điểm:**

- Đảm bảo tính đúng đắn dữ liệu
- Type hint rõ ràng hơn
- Dễ dàng tái sử dụng code

---

### Repository Pattern

- Lớp trung gian giữa **business logic** và **infrastructure (DB, API,...)**.
- Tách biệt logic nghiệp vụ khỏi cách lưu trữ dữ liệu.

**Ưu điểm:**

- Code business rõ ràng, không phụ thuộc trực tiếp vào DB
- Linh hoạt trong việc thay đổi DB, caching, gọi API,...
- Dễ dàng test và mở rộng

**Ví dụ:**

- `ProductRepository` có thể ẩn sau nhiều bảng: `items`, `stocks`, `prices`
- Có thể implement nhiều phiên bản: đọc từ master/slave, gọi API, ...

---

### Các design pattern đang dùng trong dự án

1. **Dependency Injection**
2. **Factory Pattern**
   - Khởi tạo các loại vé: vé thường, vé năm, vé tháng, vé cổng, vé chỗ ngồi,...
3. **Builder Pattern**
   - Tránh khởi tạo object phức tạp
   - Dùng trong truy vấn OpenSearch (giống Eloquent)
4. **Observer Pattern**
   - Dùng Laravel Event – Listener
5. **Singleton Pattern**
   - Dùng cho kết nối API bên thứ 3
   - Kết hợp Builder để gọi các hàm cần thiết
6. **Command Pattern**
   - Đóng gói hành vi thành object để điều khiển


   

