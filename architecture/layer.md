# N-Layer Architecture (Kiến trúc nhiều tầng)

## 1. Định nghĩa

**N-Layer Architecture** là một mô hình thiết kế phần mềm truyền thống, chia hệ thống thành các **tầng riêng biệt**, mỗi tầng đảm nhiệm một vai trò cụ thể.

Số tầng thường gặp: **3 hoặc 4 tầng**, nhưng có thể mở rộng thành nhiều hơn tùy hệ thống → gọi là **N-layer**.

---

## 2. Các tầng phổ biến

### 1. Presentation Layer (UI Layer)

- Giao tiếp với người dùng hoặc client
- Nhận input, hiển thị output
- Ví dụ: Web UI, REST API controller

### 2. Application Layer (Service Layer)

- Điều phối luồng xử lý
- Gọi các service, xử lý nghiệp vụ ở mức cao
- Không chứa logic domain sâu

### 3. Domain Layer (Business Layer)

- Chứa logic nghiệp vụ chính
- Các Entity, Aggregate, Service domain, Rule...

### 4. Data Access Layer (Infrastructure / Persistence Layer)

- Giao tiếp với database hoặc storage
- Repository, DAO, ORM, raw SQL

---

## 3. Sơ đồ tổng quan

```pgsql
+-------------------------+
| Presentation Layer | ← Controller, UI, API
+-------------------------+
| Application Layer | ← Services, orchestrators
+-------------------------+
| Domain Layer | ← Business rules, Entities
+-------------------------+
| Data Access Layer | ← Repository, DB access
+-------------------------+
```


---

## 4. Nguyên tắc hoạt động

- Tầng trên **phụ thuộc vào tầng dưới**
- Không được "đi tắt" từ UI xuống DB
- Mỗi tầng **chỉ giao tiếp với tầng liền kề**
- Dễ thay thế tầng dưới nếu dùng abstraction (interface)

---

## 5. Ưu điểm

- **Dễ hiểu** và phổ biến, phù hợp cho team mới
- **Tách biệt rõ vai trò** giữa các thành phần
- Dễ maintain, dễ chia nhỏ team theo tầng

---

## 6. Nhược điểm

- Dễ bị **"Anemic Domain Model"** (domain yếu, chỉ có DTO)
- Tầng Application thường trở thành **God Service**, chứa quá nhiều logic
- Khó test từng tầng nếu phụ thuộc nhiều (nếu không dùng DI)
- Logic domain bị tách rời khỏi Entity (vi phạm DDD)
- Độ phức tạp của dự án tăng theo thười gian
- Khó bảo trì, khó viết test

---

## 7. So sánh với Clean Architecture

| Tiêu chí                | N-Layer Architecture | Clean Architecture |
|-------------------------|----------------------|--------------------|
| Phụ thuộc chiều         | Tầng trên phụ tầng dưới | Tất cả phụ thuộc vào core |
| Test độc lập domain     | Khó                   | Dễ dàng           |
| Viết test Application   | Phức tạp nếu không DI | Dễ dàng           |
| Entity có chứa logic?   | Ít (anemic)           | Có (rich domain)  |
| Phù hợp với             | CRUD app, team mới    | Hệ thống logic phức tạp, DDD |

---

## 8. Khi nào nên dùng?

- Dự án nhỏ đến trung bình
- CRUD app, logic đơn giản
- Muốn code nhanh, chia tầng rõ ràng
- Dễ đào tạo team junior

---

## 9. Kết luận

- **N-Layer Architecture** là mô hình phổ biến, dễ học và triển khai.
- Tuy nhiên, khi nghiệp vụ phức tạp, cần xét đến kiến trúc như **Hexagonal** hoặc **Clean Architecture** để tránh tình trạng "service-fat" và "domain mỏng".

