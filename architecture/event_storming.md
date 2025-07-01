### **EventStorming là gì?**
- **Định nghĩa**: EventStorming là một workshop tương tác, nơi các bên liên quan (developer, domain expert, stakeholder) sử dụng sticky notes để lập bản đồ các sự kiện miền (domain events), quy trình, và hành vi trong hệ thống.
- Là một phương pháp hợp tác trực quan, giúp domain expert (người hiểu nghiệp vụ) và developer cùng nhau khám phá hệ thống thông qua các sự kiện nghiệp vụ (domain events).

- **Mục đích**: 
  - Hiểu rõ quy trình nghiệp vụ.
  - Xác định các **Bounded Context**, **Aggregate**, và **Domain Event** trong DDD.
  - Tạo sự đồng thuận giữa các bên về cách hệ thống hoạt động.
- **Cách hoạt động**: 
  - Dùng sticky notes (hoặc bảng số) để ghi lại các **Domain Event** (sự kiện đã xảy ra, ví dụ: "Đơn hàng được đặt", "Thanh toán hoàn tất").
  - Sắp xếp các sự kiện theo dòng thời gian (timeline).
  - Bổ sung các yếu tố như **Command** (hành động kích hoạt sự kiện), **Actor** (người thực hiện), **Aggregate** (đối tượng miền), và **Policy** (quy tắc nghiệp vụ).

### **Các loại EventStorming**
1. **Big Picture EventStorming**: 
   - Khám phá toàn bộ quy trình nghiệp vụ, không đi sâu vào chi tiết.
   - Phù hợp để hiểu tổng quan hệ thống, xác định Bounded Context.
2. **Process Modeling EventStorming**: 
   - Tập trung vào một quy trình cụ thể, mô tả chi tiết các bước và tương tác.
   - Dùng để thiết kế quy trình hoặc cải thiện quy trình hiện tại.
3. **Software Design EventStorming**: 
   - Chi tiết hơn, dùng để thiết kế phần mềm, xác định Aggregate, Command, và mã hóa logic.
   - Thường áp dụng khi đã có Bounded Context.

### **Quy trình cơ bản**
1. **Chuẩn bị**: 
   - Mời các bên liên quan (developer, domain expert, PO).
   - Chuẩn bị bảng lớn, sticky notes nhiều màu, bút.
2. **Bắt đầu với Domain Events**:
   - Ghi các sự kiện (màu cam) theo thứ tự thời gian, ví dụ: "Khách hàng đăng ký", "Hóa đơn được tạo".
3. **Bổ sung chi tiết**:
   - Thêm **Command** (màu xanh): Hành động dẫn đến sự kiện, ví dụ: "Đăng ký tài khoản".
   - Thêm **Actor** (màu vàng): Ai thực hiện hành động, ví dụ: "Khách hàng", "Hệ thống".
   - Thêm **Aggregate** (màu trắng): Đối tượng miền, ví dụ: "Đơn hàng", "Khách hàng".
   - Thêm **Policy** (màu tím): Quy tắc hoặc điều kiện, ví dụ: "Nếu thanh toán thất bại, hủy đơn hàng".
4. **Phân tích và tinh chỉnh**:
   - Nhóm các sự kiện liên quan để xác định **Bounded Context**.
   - Tìm điểm nghẽn, mâu thuẫn, hoặc thiếu sót trong quy trình.
5. **Kết quả**: Tạo mô hình miền (domain model) hoặc tài liệu để phát triển phần mềm.

### **Ưu điểm**
- **Tăng cộng tác**: Tạo sự đồng thuận giữa kỹ thuật và nghiệp vụ.
- **Trực quan**: Dễ hiểu, không cần kỹ năng kỹ thuật cao.
- **Nhanh chóng**: Khám phá miền phức tạp trong thời gian ngắn (vài giờ đến vài ngày).
- **Linh hoạt**: Áp dụng cho dự án mới hoặc cải thiện hệ thống hiện tại.

### **Nhược điểm**
- **Phụ thuộc vào người tham gia**: Cần domain expert có kiến thức sâu về nghiệp vụ.
- **Khó quản lý với hệ thống lớn**: Có thể tạo ra quá nhiều sticky notes, gây rối.
- **Yêu cầu facilitator giỏi**: Cần người điều phối để giữ workshop hiệu quả.

### **Ứng dụng thực tế**
- **Thương mại điện tử**: Mô hình hóa quy trình đặt hàng (từ "Thêm vào giỏ hàng" đến "Giao hàng hoàn tất") để xác định Bounded Context như "Order Management", "Payment".
- **Ngân hàng**: Phân tích quy trình chuyển khoản, xác định sự kiện như "Tiền được rút", "Tiền được gửi", và các Aggregate như "Tài khoản".
- **Startup**: Khám phá quy trình nghiệp vụ mới để thiết kế hệ thống từ đầu, ví dụ: ứng dụng đặt xe như Grab.

### **Tóm lại**
EventStorming là công cụ mạnh mẽ trong DDD để mô hình hóa miền nghiệp vụ, giúp đội phát triển hiểu rõ hệ thống và thiết kế phần mềm hiệu quả. Nó phù hợp cho các dự án cần sự cộng tác chặt chẽ giữa kỹ thuật và nghiệp vụ, đặc biệt trong hệ thống phức tạp.

Nếu cần ví dụ chi tiết, hướng dẫn tổ chức workshop, hoặc file .md, hãy cho biết!