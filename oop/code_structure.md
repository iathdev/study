# Code Structure & Architectural Styles

## 1. Layer Architecture

**Nguyên tắc:**
- Mỗi lớp chỉ phụ thuộc vào lớp bên dưới.
- Không biết và không phụ thuộc vào các lớp bên trên sử dụng nó.

**Ưu điểm:**
- Đơn giản, dễ implement.
- Dễ test.

**Nhược điểm:**
- Khó mở rộng khi hệ thống lớn.
- Các tầng trên bị phụ thuộc vào tầng dưới (có thể gây tight coupling).

---

## 2. Hexagonal Architecture (Ports & Adapters)

**Khái niệm:**
- **Port**: Interface (application-facing).
- **Adapter**: Implementation (external-facing).
- Tách biệt phần lõi (core logic) với các thành phần bên ngoài như DB, Email, File, UI, v.v.

**Ưu điểm:**
- **Loose Coupling**: Các phần của ứng dụng độc lập hơn.
- Dễ kiểm tra (test) core logic độc lập.
- Dễ thay thế adapter mà không ảnh hưởng tới core logic (ví dụ thay MySQL bằng PostgreSQL).

**Nhược điểm:**
- Khó áp dụng nếu chưa quen.

> 📌 Lưu ý: Bất kỳ sự giao tiếp nào với bên ngoài nên tạo ra interface để phần application không phụ thuộc trực tiếp vào bên ngoài.

---

## 3. Onion Architecture

**Giải quyết nhược điểm của Layer Architecture:**
- Tránh các layer phụ thuộc lẫn nhau.
- Loại bỏ sự phụ thuộc vào Infrastructure.

**Đặc điểm:**
- Business Domain là trung tâm của hệ thống.
- Infrastructure (như DB) nằm ở ngoài cùng, không phải trung tâm.

**Tuân theo Dependency Inversion Principle:**
- Layer bên trong không biết gì về layer bên ngoài.
- Layer ngoài **import** code của layer bên trong.

**Ưu điểm:**
- Domain là trọng tâm → hệ thống linh hoạt, dễ thay đổi hạ tầng.
- Layer tách biệt → dễ test.
- **Loose Coupling**: dễ maintain và mở rộng.

---

## 4. Clean Architecture

**Nguyên tắc chính:**
- Đề cao **Dependency Inversion Principle**.
- Số lượng layer không cố định.

**Sơ đồ tầng (từ trong ra ngoài):**
Entities → Use Cases → Interface Adapters → Frameworks & Drivers


**Ưu điểm:**
- Không phụ thuộc framework.
- Dễ maintain.
- Dễ test.
- Linh hoạt & dễ mở rộng.

**Nhược điểm:**
- Tốn thời gian học và làm quen.
- Có thể gây over-engineering với hệ thống đơn giản.

---

## 5. Domain-Driven Design (DDD)

**Mục tiêu:**  
Thiết kế phần mềm tập trung vào mô hình hóa **business domain**.

**Đặc điểm:**
- Không quan tâm công nghệ/infrastructure.
- Class, method phải thể hiện rõ nghiệp vụ.
- Sử dụng **Ubiquitous Language**: ngôn ngữ chung giữa dev và domain expert, phản ánh vào code.

---

### 5.1. Bounded Context

- Nhóm các chức năng, thành phần & concept theo từng context cụ thể.
- Mỗi context có ngôn ngữ riêng biệt, chạy độc lập với các context khác.

---

### 5.2. Collaborative Modeling

- Dev và Domain Expert cùng nhau mô hình hóa domain.
- Sử dụng **Ubiquitous Language** giúp giao tiếp rõ ràng và đồng nhất giữa người và code.

**Ví dụ:**  
> Nếu gọi tài khoản nhận tiền là `CreditAccount`, thì trong code cũng phải đặt là `creditAccount`.

---

### 5.3. Tactical Design

#### a. Entity
- Có **ID** và **vòng đời** (lifecycle).
- Phản ánh sự thay đổi theo nghiệp vụ.
- Ví dụ: trạng thái đơn hàng qua các bước khác nhau.

#### b. Value Object
- Không có ID.
- **Bất biến** (Immutable).
- Mô tả đặc tính của Entity.

**Ví dụ:**
```text
Address: street, postal code
Money: currency, amount
```

#### c. Aggregate (tiếp)

- Là một nhóm các Entity và Value Object có quan hệ chặt chẽ với nhau.
- Có một Entity đóng vai trò là **Aggregate Root** — là điểm duy nhất để truy cập và thao tác các thành phần bên trong Aggregate.
- Tất cả các thay đổi và tương tác với các Entity con phải thông qua Aggregate Root.
- Đảm bảo tính **nhất quán dữ liệu** trong phạm vi Aggregate.

**Ví dụ:**
```text
Aggregate: Order
- Order (Aggregate Root)
- OrderItem (Entity con)
- ShippingAddress (Value Object)

→ Tất cả thay đổi đến OrderItem hay ShippingAddress đều phải thông qua Order.

