
# Design Patterns và Kiến trúc Sử dụng trong Dự Án

## 1. Dependency Injection (DI)
### Bài toán thực tế: Bóng đèn - đui đèn
- Đại diện cho **Composition over Inheritance**
- Một đối tượng nên được tạo thành từ các thành phần bên ngoài thay vì tự khởi tạo bên trong.

### Ưu điểm:
- Dễ viết unit test thông qua mocking
- Giảm sự phụ thuộc và ràng buộc chặt chẽ
- Dễ dàng thay đổi các dependencies (implement)

### Ứng dụng:
- Áp dụng nhiều trong các controller/service để inject service qua constructor.

---

## 2. Factory Design Pattern
Dự án có nhiều loại item:
- Vé bình thường, vé năm, vé tháng, vé cổng vào, vé chỗ ngồi
- Vé bình thường cũng có nhiều trường hợp khởi tạo khác nhau

### Ứng dụng:
- Sử dụng Factory để khởi tạo các đối tượng tương ứng với từng loại vé.

---

## 3. Builder Design Pattern
Tránh việc khởi tạo một đối tượng phức tạp, builder tạo ra từng phần cụ thể.

### Ứng dụng:
- Sử dụng cho OpenSearch
- Viết tương tự như Eloquent ORM
- Các hàm sử dụng: khởi tạo, query, where, get, pagination

---

## 4. Observer Design Pattern
### Ứng dụng:
- Sử dụng Event - Listener để lắng nghe và xử lý logic.

---

## 5. Singleton Design Pattern
### Ứng dụng:
- Kết nối API bên thứ 3
- Chỉ khởi tạo một class duy nhất chứa các cấu hình cần thiết để gọi API.
- Áp dụng thêm Builder để gọi các hàm cần thiết.

---

## 6. Command Design Pattern
- Áp dụng command để đóng gói hành động và tách logic xử lý.

---

## 7. Data Transfer Object (DTO)
### Ưu điểm:
- Đảm bảo tính đúng đắn của dữ liệu
- Type hint giúp code rõ ràng hơn
- Dễ dàng tái sử dụng code

---

## 8. Repositories (Interface vs Implement)
Là lớp trung gian giữa lớp business logic và lớp hạ tầng (Infrastructure)

### Ưu điểm:
- Nghiệp vụ rõ ràng, tách biệt với logic kỹ thuật
- Linh hoạt trong triển khai: gọi API, đọc DB khác, master/slave, ...
- Tái sử dụng code, linh hoạt thay đổi DB (ít khi dùng)

### Lưu ý:
- Nếu dự án quá đơn giản thì không nên áp dụng.

---

## 9. SOLID Principles

### 1. Single Responsibility Principle (SRP)
- Một class chỉ có một trách nhiệm duy nhất.

**VD**: Mỗi Action chỉ xử lý một logic cụ thể. Ví dụ: Action tính hoàn tiền khi huỷ vé.

### 2. Open/Closed Principle (OCP)
- Class nên mở rộng, không nên sửa đổi trực tiếp.

**VD**: 
- Framework: Model, Controller kế thừa từ core.
- Hệ thống quét vé có thể mở rộng thêm nhiều phương thức (QR, nút bấm) thông qua interface `ProductUsageInterface` với hàm `usage()`.

### 3. Liskov Substitution Principle (LSP)
- Class con có thể thay thế class cha mà không làm thay đổi tính đúng đắn của chương trình

**VD**: Class con không được thay đổi kiểu trả về — cha return `Collection` thì con cũng phải return `Collection`.

### 4. Interface Segregation Principle (ISP)
- Interface nên nhỏ, chuyên biệt.

**VD**: Không gom tất cả phương thức di chuyển vào 1 interface `Movable` mà nên chia nhỏ như: `Flyable`, `Runnable`, `Swimmable`

### 5. Dependency Inversion Principle (DIP)
- Module cấp cao không phụ thuộc module cấp thấp. Cả hai nên phụ thuộc abstraction (interface).


