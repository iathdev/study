1. Encapsulation (đóng gói) - private & public
Dấu bên trong (private) - người dùng chỉ cần quan tâm đến bên ngoài (public)

Tính chất:
- Dấu thông tin chỉ để lộ ra các phương thức public để tương tác
- Tránh người dùng can thiệp trực tiếp vào thuộc tính nội bộ

Liên quan: public - protected - private

2. Inheritance (kế thừa) - extends
Lớp con kế thừa đặc điểm từ lớp cha

Tính chất:
- Giúp tái sử dụng code
- Cho phép tạo mối quan hệ “is-a”

3. Polymorphism (đa hình) - interface
Một hành động, nhiều cách thực hiện

Tính chất:
- Một interface nhưnng có nhiều class triển khai theo cách riêng
- Giúp hệ thống mở rộng mà không sửa code cũ

| Mục tiêu                         | Vai trò của Đa hình                                      |
| -------------------------------- | -------------------------------------------------------- |
| **DI (Dependency Injection)**    | Cho phép inject nhiều `implementation` cho 1 interface   |
| **Port & Adapter** (Clean Arch)  | Port là interface, adapter là class implements (đa hình) |
| **Testing & mocking**            | Dễ mock interface trong test                             |
| **Mở rộng mà không sửa code cũ** | Vì không bị gắn chặt với 1 class cụ thể                  |


4. Abstraction (trừu tượng)
Ẩn chi tiết, chỉ lộ cái cần lộ

Tính chất:
- Chỉ mô tả hành vi quan trọng, ẩn chi tiết
- Giao tiếp thông qua interface/abstract thay vì cụ thể

