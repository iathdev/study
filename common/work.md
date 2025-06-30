# Kiến trúc dự án: Kết hợp N-layer và Hexagonal Architecture

## 🔧 Cấu trúc 4 tầng:

1. **User Interface**
   - Tầng giao diện, tương tác trực tiếp với người dùng (UI).

2. **Business Layer**
   - Xử lý nghiệp vụ, logic hệ thống (Service).
   - Ứng dụng nguyên lý **Dependency Inversion** thông qua interface.

3. **Repository Layer**
   - Tương tác với CSDL (Repository).
   - Ứng dụng **port-adapter (Hexagonal)** để cách ly service và persistence.

4. **Database Layer**
   - Tầng dữ liệu (Database, schema, SQL).

> Giao tiếp giữa các tầng thông qua Dependency Injection (DI).

---

## ✅ Các chức năng đã thực hiện:

### 1. Tạo Item

**Phức tạp vì:**
- Mỗi item chứa nhiều thông tin.
- Có nhiều loại item: vé thường, vé seat, vé gate.
- Vé thường có tới **21 case** khác nhau.

**Giải pháp:**
- Dùng **Factory Pattern** để tạo object theo loại vé.
- Dùng **Factory Pattern** để tạo object theo từng case vé thường.
- Dùng Factory ở cả: FE, Request và Service.
- Dùng **Builder Pattern** để khởi tạo và cập nhật từng phần item (thông tin cơ bản, bổ sung, bán hàng,...).

---

### 2. Tính tồn kho còn lại & Mua hàng đồng thời

**Vấn đề:**
- `remaining_stock_qty` tính bằng view nên chậm.
- Mua hàng đồng thời không chính xác do phụ thuộc vào DB & view.

#### 2.1 Cải thiện `v_stocks`

**Vấn đề:**
- View query chậm.
- Dữ liệu thiết kế dàn trải, phải join nhiều bảng: order, cart, temporary_cart,...

**Giải pháp:**
- Trải phẳng dữ liệu, giảm join → tăng tốc query.
- Dùng bảng thật thay vì view.
- Tạo bảng riêng lưu lịch sử `add_to_cart` và `order`.
- Tính `remaining_stock_qty` từ bảng này.

#### 2.2 Dùng Redis Cache

**Chiến lược Read-aside:**
- Không có cache → lấy từ DB và ghi vào cache.
- Có cache → dùng trực tiếp.

**Xử lý ghi đồng thời:**
- Dùng `SETNX` để khóa khi write.
- Nếu chưa có cache → lock (`cache::lock`) với TTL = 1s → lấy từ DB → ghi cache (TTL=30s).
- Các user khác retry tối đa 10 lần.
- DB đủ nhanh → không bị treo người dùng.

---

### 3. Tối ưu màn hình Admin (Order) & Download TSV

#### 3.1 Tối ưu màn hình thông tin order

**Vấn đề:**
- Join nhiều bảng.
- Index chưa được dùng tốt.
- Dữ liệu nhiều → quét lớn.

**Giải pháp:**
- Tạo bảng mới chứa dữ liệu đã trải phẳng (đánh đổi hiệu suất vs chuẩn).
- Đánh index hợp lý.
- Giảm dữ liệu cần quét để tận dụng index.

#### 3.2 Tối ưu Download TSV

**Vấn đề:**
- Các vấn đề như trên.
- Dữ liệu lớn → dễ leak memory.

**Giải pháp:**
- Tối ưu query như admin screen.
- Tối ưu PHP: giảm vòng lặp, dùng `chunk`.
- Dùng **streaming + chunk** để tránh leak.
- Bật **OPcache + JIT**.

**Cách khác:**
- Download ở background, hoàn tất thì thông báo.
- Upload file định kỳ lên S3 → người dùng download từ S3.

---

### 4. Crawler dữ liệu

Sử dụng:
- **Puppeteer + NodeJS + Lambda + SQS + OpenSearch**

---

## ⚠️ Khó khăn gặp phải

- Giai đoạn đầu phụ thuộc vào quyết định của khách hàng.
- Đề xuất thay đổi DB & API nhưng KH không chấp nhận.
- Không thể đập đi làm lại → phải vá bằng thêm bảng, sửa logic.

### Vấn đề về DB:
- Dữ liệu thiết kế không chuẩn, không tổng hợp, khó bảo trì/mở rộng.
- Logic về tiền, coin, kho bị dàn trải → tổng hợp phải join quá nhiều bảng.
- Thông tin đơn hàng có thể lưu trong bảng `order`, nhưng lại phải join để biết thanh toán thành công hay không.
- Có thể gom giỏ hàng & order vào 1 bảng để tính kho, nhưng lại dàn trải → join nhiều bảng.

### Vấn đề về API:
- Không theo chuẩn RESTful.
- 1 API dùng nhiều nơi → thay đổi chỗ này ảnh hưởng chỗ khác.
- Logic quá nhiều trong 1 API, thừa data, query dư thừa.

---

## ❌ Sai lầm đã mắc phải

- **Lạm dụng View**: tái sử dụng tốt nhưng khó debug, maintain.
- **Không thể ảnh hưởng đến quyết định thiết kế của KH** → bị động, phải xử lý hậu quả về sau.
