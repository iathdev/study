# Monolithic vs Microservice

## Monolithic

- Kiến trúc nguyên khối  
- Tất cả module đều nằm trong một project lớn

### Ưu điểm:
+ Là kiến trúc đơn giản, dễ code  
+ Quá trình deploy cũng đơn giản hơn  
+ Phù hợp với dự án nhỏ và vừa  
+ Testing dễ dàng hơn

### Nhược điểm:
+ Cấu trúc code phức tạp theo thời gian  
+ Khó bảo trì, nâng cấp hay thêm tính năng mới  
+ Khó áp dụng agile  
+ Thời gian deploy dài, mỗi khi deploy phải build lại toàn bộ  
+ Khó sử dụng công nghệ mới  
+ Khi có lỗi có thể dẫn đến sập toàn bộ hệ thống  
+ Khó mở rộng (scale)

---

## Microservice

- Chia thành nhiều service nhỏ  
- Mỗi service đảm nhận một chức năng cụ thể  
- Giao tiếp qua HTTP/REST, gRPC hoặc message broker

### Ưu điểm:
+ Scale linh hoạt  
+ Linh hoạt công nghệ  
+ Dễ áp dụng agile  
+ Tăng tính chịu lỗi  
+ Service bị lỗi không ảnh hưởng toàn hệ thống  
+ Giảm coupling

### Nhược điểm:
+ Quản lý hệ thống phức tạp  
+ Giao tiếp mạng chậm hơn  
+ Cần đội ngũ DevOps mạnh  
+ Khó xử lý consistency, transaction  
+ Tăng chi phí vận hành

---

## Giao tiếp giữa các microservice

### 1. Giao tiếp đồng bộ

#### 1.1 HTTP (RESTful API)
- **Ưu:** dễ triển khai, phổ biến  
- **Nhược:** chậm nếu service chờ response, dễ nghẽn

#### 1.2 gRPC
- **Ưu:** nhanh, hỗ trợ streaming  
- **Nhược:** khó debug, config phức tạp

### 2. Giao tiếp không đồng bộ

#### 2.1 Message Queue
- Gửi nhận thông qua hàng đợi  
- **Ưu:** tách biệt service, chịu tải cao  
- **Nhược:** khó debug, theo dõi flow

#### 2.2 Event-Driven (Pub/Sub)
- **Ưu:** mở rộng tốt, giảm phụ thuộc  
- **Nhược:** kiểm soát trạng thái khó khăn

---

## Cơ chế transaction

### 1. Two-Phase Commit (2PC)
- **Ưu:** đảm bảo nhất quán  
- **Nhược:** hiệu suất thấp, dễ treo nếu coordinator lỗi

### 2. Saga Pattern

- **Chained:** từng service gọi tiếp nhau  
- **Orchestrated:** có orchestrator điều phối  
- Có action rollback riêng từng bước

**Ví dụ:**  
1. A tạo đơn hàng  
2. B trừ hàng  
3. C thanh toán  
→ Nếu C lỗi, rollback B và A

- **Ưu:** không cần khoá DB, linh hoạt  
- **Nhược:**
